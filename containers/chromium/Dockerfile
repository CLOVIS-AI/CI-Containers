FROM node:lts

RUN apt-get update && \
	apt-get install -y --no-install-recommends default-jdk chromium

ENV CHROME_BIN=chromium

RUN mkdir -p /home
RUN useradd -s /bin/sh -m worker
USER worker
