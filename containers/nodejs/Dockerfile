FROM archlinux:base

RUN pacman -Syuu --noconfirm jdk-openjdk nodejs yarn git

RUN pacman -Syuu --noconfirm zip unzip &&\
	curl -s "https://get.sdkman.io" | bash &&\
	source "/root/.sdkman/bin/sdkman-init.sh" &&\
	yes | sdk install java 17.0.18-tem &&\
	yes | sdk install java 25.0.2-tem &&\
	sdk use java 25.0.2-tem
