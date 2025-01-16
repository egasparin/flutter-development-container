FROM debian:stable-slim

ENV ANDROID_SDK_ROOT=/usr/lib/android-sdk
ENV FLUTTER_SDK_ROOT=/usr/lib/flutter
ENV GIT_USERNAME="Name"
ENV GIT_USEREMAIL="email"

# SEMPRE CONSULTAR A VERSÃO EM https://developer.android.com/studio?hl=pt-br
ENV CMDLINE_TOOLS_VERSION=11076708
# SEMPRE CONSULTAR A VERSÃO EM https://docs.flutter.dev/release/archive#stable-channel-linux
ENV FLUTTER_SDK_VERSION=3.27.1-stable

# Install dependencies and tools
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y \
    wget \
    unzip \
    zip \
    curl \
    sudo \
    git-all \
    xz-utils \
    libglu1-mesa \
    libc6:amd64 libstdc++6:amd64 lib32z1 libbz2-1.0:amd64 \
    clang \
    cmake \
    ninja-build \
    libgtk-3-dev \
    openjdk-17-jdk \
    android-sdk \
    pkg-config && \
    rm -rf /var/lib/apt/lists/*

RUN apt clean -y && \
    apt autoremove -y && \
    apt autoclean -y

# Set environment variables to avoid interactive timezone configuration
ENV DEBIAN_FRONTEND=noninteractive

# To define language to pt_BR: 
# ENV LANG=pt_BR.UTF-8
# ENV LANGUAGE=pt_BR:pt:en
# To default, define to en_US
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en

# Define a new non-root user
ARG USER_NAME=devcontainer
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Add a new non-root user to config files
RUN groupadd --gid $USER_GID $USER_NAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USER_NAME \
    && echo "$USER_NAME ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/$USER_NAME \
    && chmod 0440 /etc/sudoers.d/$USER_NAME

# update enviroments to non-root user
ENV ANDROID_SDK_ROOT=/home/${USER_NAME}/sdk/android
ENV FLUTTER_SDK_ROOT=/home/${USER_NAME}/sdk/flutter
ENV USER_HOME=/home/${USER_NAME}

# Include flutter and android tools in path
ENV PATH="${PATH}:${FLUTTER_SDK_ROOT}/bin:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools"

# define non-root user access to container
USER ${USER_NAME}
WORKDIR ${USER_HOME}

# Configure git user name and email
RUN git config --global user.name ${GIT_USERNAME} && \
    git config --global user.email ${GIT_USEREMAIL}

# Create temporary path to download files
RUN mkdir -p ${USER_HOME}/tmp && \
    cd ${USER_HOME}/tmp/

# Download and install Android Command Line Tools    
RUN mkdir -p ${ANDROID_SDK_ROOT}/cmdline-tools/latest && \
    wget -O commandlinetools.zip "https://dl.google.com/android/repository/commandlinetools-linux-${CMDLINE_TOOLS_VERSION}_latest.zip" && \
    unzip commandlinetools.zip -d ${USER_HOME}/tmp && \
    mv ${USER_HOME}/tmp/cmdline-tools/* ${ANDROID_SDK_ROOT}/cmdline-tools/latest/
    
# Accept Android SDK licenses and install necessary components
RUN yes | ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager --licenses && \
    ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager "platform-tools" && \
    ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager "platforms;android-34" && \
    ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin/sdkmanager "build-tools;33.0.0"

# Download and install Flutter SDK
RUN mkdir -p ${FLUTTER_SDK_ROOT} && \
    cd ${USER_HOME}/tmp && \
    curl -OL https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_SDK_VERSION}.tar.xz && \
    tar -xf flutter_linux_${FLUTTER_SDK_VERSION}.tar.xz -C ${FLUTTER_SDK_ROOT} --strip-components=1

# Add flutter to safe directory in git
RUN git config --global --add safe.directory ${FLUTTER_SDK_ROOT}

# Add flutter to oficial channel
RUN flutter channel

# Disable Flutter telemetry
RUN ${FLUTTER_SDK_ROOT}/bin/flutter --disable-analytics

# Remove temporary path and download files
RUN cd ${USER_HOME} && \ 
    rm -rf ${USER_HOME}/tmp

# Default shell to bash
SHELL ["/bin/bash", "-c"]