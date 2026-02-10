FROM archlinux:base

RUN pacman -Syuu --noconfirm jdk-openjdk chromium git

ENV CHROME_BIN=chromium
COPY chromium-flags.conf /root/.config/chromium-flags.conf
