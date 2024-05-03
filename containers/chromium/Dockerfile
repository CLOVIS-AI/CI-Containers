FROM archlinux:base

RUN pacman -Syuu --noconfirm jdk17-openjdk chromium

ENV CHROME_BIN=chromium
COPY chromium-flags.conf /root/.config/chromium-flags.conf
