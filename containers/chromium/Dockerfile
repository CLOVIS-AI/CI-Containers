FROM archlinux:base

RUN pacman -Syuu --noconfirm jre17-openjdk-headless chromium

ENV CHROME_BIN=chromium
COPY chromium-flags.conf /root/.config/chromium-flags.conf
