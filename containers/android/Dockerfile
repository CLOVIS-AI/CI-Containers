FROM archlinux:base AS downloader

RUN pacman -Syuu --noconfirm wget unzip jre21-openjdk-headless

ENV JAVA_HOME="/usr/lib/jvm/default" \
    ANDROID_COMPILE_SDK="33" \
    ANDROID_BUILD_TOOLS="33.0.0" \
    ANDROID_SDK_TOOLS="8512546_latest"

RUN wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/commandlinetools-linux-$ANDROID_SDK_TOOLS.zip
RUN unzip -d /opt/android android-sdk.zip
RUN rm android-sdk.zip

# The cmdline-tools are in SDK/cmdline-tools in the archive, but should be in SDK/cmdline-tools/tools
# https://stackoverflow.com/a/61176718
WORKDIR /opt/android/cmdline-tools
RUN mkdir -p tools
RUN ls
RUN mv bin lib source.properties NOTICE.txt tools
ENV ANDROID_SDK_ROOT=/opt/android
ENV PATH="$PATH:/opt/android/cmdline-tools/tools/bin:/opt/android/platform-tools"
WORKDIR /root

RUN yes | sdkmanager "platforms;android-$ANDROID_COMPILE_SDK" >/dev/null
RUN yes | sdkmanager "platform-tools" >/dev/null
RUN yes | sdkmanager "build-tools;$ANDROID_BUILD_TOOLS" >/dev/null
RUN yes | sdkmanager --licenses >/dev/null

FROM archlinux:base

RUN pacman -Syuu --noconfirm jdk21-openjdk

ENV ANDROID_SDK_ROOT=/opt/android
ENV PATH="$PATH:/opt/android/cmdline-tools/tools/bin:/opt/android/platform-tools"
COPY --from=downloader /opt/android /opt/android
