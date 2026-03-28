FROM archlinux:base

RUN pacman -Syuu --noconfirm curl libxcrypt-compat unzip

WORKDIR /install
# https://github.com/deezer/caupain/releases
RUN curl -L0 'https://github.com/deezer/caupain/releases/download/v1.9.1/caupain-1.9.1-linux.zip' --output caupain.zip &&\
    unzip caupain.zip &&\
    rm caupain.zip &&\
    chmod u+x caupain

ENV PATH=$PATH:/install

ENTRYPOINT [ "/install/caupain" ]
CMD [ "--help" ]
