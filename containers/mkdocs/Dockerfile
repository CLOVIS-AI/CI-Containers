FROM archlinux:base

ENV PATH=/root/venv/bin:$PATH
WORKDIR /docs

RUN pacman -Syuu --noconfirm jdk21-openjdk libxcrypt-compat python git pngquant cairo

RUN python -m venv /root/venv && \
    /root/venv/bin/pip install --no-cache-dir mkdocs-material[imaging] mkdocs-rss-plugin mkdocs-minify-plugin mkdocs-redirects mkdocs-mermaid2-plugin

CMD [ "mkdocs", "serve", "--dev-addr=0.0.0.0:8000" ]
