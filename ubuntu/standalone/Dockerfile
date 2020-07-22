FROM ubuntu:20.04

ENV ANDROID_SDK_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_ROOT /opt/android-sdk-linux
ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK /opt/android-sdk-linux

ENV DEBIAN_FRONTEND noninteractive

# Install required tools
# Dependencies to execute Android builds

RUN dpkg --add-architecture i386 && apt-get update -yqq && apt-get install -y \
  curl \
  expect \
  git \
  make \
  libc6:i386 \
  libgcc1:i386 \
  libncurses5:i386 \
  libstdc++6:i386 \
  zlib1g:i386 \
  openjdk-8-jdk \
  wget \
  unzip \
  vim \
  openssh-client \
  locales \
  # nodejs \
  # npm \
  # Extensions #
  libssl-dev \
  libreadline-dev \
  zlib1g-dev \
  build-essential \
  ripgrep \
  fd-find \
  jq \
  imagemagick \
  pngquant \
  git-crypt \
  && apt-get clean

RUN  rm -rf /var/lib/apt/lists/* && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.UTF-8

RUN groupadd android && useradd -d /opt/android-sdk-linux -g android -u 1000 android

COPY tools /opt/tools

COPY licenses /opt/licenses

WORKDIR /opt/android-sdk-linux

RUN /opt/tools/entrypoint.sh built-in

CMD /opt/tools/entrypoint.sh built-in

# Extensions #

# Alias find for ubuntu naming
RUN echo 'alias fd="fdfind"' >> ~/.bashrc

# Install rbenv, fastlane & bundler
RUN echo 'PATH=${HOME}/.rbenv/shims:${HOME}/.rbenv/bin:${PATH}' >> ~/.bashrc && \
	export PATH=${HOME}/.rbenv/shims:${HOME}/.rbenv/bin:${PATH} && \
	wget -q https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer -O- | bash && \
	echo 'eval "$(rbenv init -)"' >> ~/.bashrc && rbenv install -s 2.6.6 && rbenv global 2.6.6 && gem install fastlane && gem install bundler

# Install gradle
RUN wget https://services.gradle.org/distributions/gradle-6.5.1-bin.zip
RUN mkdir /opt/gradle
RUN unzip -d /opt/gradle gradle-6.5.1-bin.zip
RUN export PATH=$PATH:/opt/gradle/gradle-6.5.1/bin

# bash will load volta() function via .bashrc
# using $VOLTA_HOME/load.sh
SHELL ["/bin/bash", "-c"]

# since we're starting non-interactive shell,
# we wil need to tell bash to load .bashrc manually
ENV BASH_ENV ~/.bashrc
# needed by volta() function
ENV VOLTA_HOME /root/.volta
# make sure packages managed by volta will be in PATH
ENV PATH $VOLTA_HOME/bin:$PATH

# install volta
RUN curl https://get.volta.sh | bash

# Work directory
WORKDIR /app