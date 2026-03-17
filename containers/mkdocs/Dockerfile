FROM archlinux:base

ENV PATH=/root/venv/bin:$PATH
WORKDIR /docs

RUN pacman -Syuu --noconfirm jdk-openjdk libxcrypt-compat python git pngquant cairo

RUN pacman -Syuu --noconfirm zip unzip &&\
	curl -s "https://get.sdkman.io" | bash &&\
	source "/root/.sdkman/bin/sdkman-init.sh" &&\
	yes | sdk install java 17.0.18-tem &&\
	yes | sdk install java 25.0.2-tem &&\
	sdk use java 25.0.2-tem

RUN python -m venv /root/venv && \
    /root/venv/bin/pip install --no-cache-dir mkdocs-material[imaging] mkdocs-rss-plugin mkdocs-minify-plugin mkdocs-redirects mkdocs-mermaid2-plugin

CMD [ "mkdocs", "serve", "--dev-addr=0.0.0.0:8000" ]
