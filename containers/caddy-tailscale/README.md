# Caddy-Tailscale

A Caddy container with Tailscale module in order to expose a service on a tailnet with automatic TLS certificate renewal thanks to Caddy and Tailscale automatic HTTPS feature.
The service can be another Docker container.

## Usage

You can follow the [README](https://github.com/tailscale/caddy-tailscale) of Tailscale plugin for Caddy

For example, you can use the following docker-compose file to expose an Apache web server to your Tailnet with automatic HTTPS :

```yaml
version: "3.9"

services:
  caddy:
    image: registry.gitlab.com/opensavvy/automation/containers/caddy-tailscale:latest
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    environment:
      - TS_AUTHKEY=tskey-auth-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    volumes:
      - caddy_data:/data
      - caddy_config:/config
      - ./Caddyfile:/etc/caddy/Caddyfile:ro


  web:
    image: httpd:2.4
    volumes:
      - ./apache/www:/usr/local/apache2/htdocs/

volumes:
  caddy_data:
  caddy_config:

```

If no `TS_AUTHKEY` is provided, a link will be displayed on standard output to log into the tailnet.

The following `Caddyfile` can be used :

```
your_vhost.tailXXXXX.ts.net {
  bind tailscale/your_vhost
  reverse_proxy http://web
}
```