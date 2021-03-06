FROM ubuntu:16.04

LABEL maintainer "Eddy Choi <kwo2002@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive

#=============
# Set WORKDIR
#=============
WORKDIR /root

#==================
# General Packages
#------------------
# openjdk-8-jdk
#   Java
# ca-certificates
#   SSL client
# tzdata
#   Timezone
# unzip
#   Unzip zip file
# curl
#   Transfer data from or to a server
# wget
#   Network downloader
# libqt5webkit5
#   Web content engine (Fix issue in Android)
# bats
#   Testing framework for Bash
# libgconf-2-4
#   Required package for chrome and chromedriver to run on Linux
# xvfb
#   X virtual framebuffer
#==================
RUN apt-get -qqy update && \
    apt-get -qqy --no-install-recommends install \
    openjdk-8-jdk \
    ca-certificates \
    tzdata \
    unzip \
    curl \
    wget \
    libqt5webkit5 \
    bats \
    libgconf-2-4 \
    xvfb \
  && rm -rf /var/lib/apt/lists/*

#===============
# JAVA_HOME 환경변수 설정
#===============
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre" \
    PATH=$PATH:$JAVA_HOME/bin

#=====================
# Android SDK 설치
#=====================
ENV SDK_VERSION=25.2.3 \
    ANDROID_BUILD_TOOLS_VERSION=25.0.3 \
    ANDROID_HOME=/root

RUN wget -O tools.zip https://dl.google.com/android/repository/tools_r${SDK_VERSION}-linux.zip && \
    unzip tools.zip && rm tools.zip && \
    chmod a+x -R $ANDROID_HOME && \
    chown -R root:root $ANDROID_HOME

ENV PATH=$PATH:$ANDROID_HOME/tools

RUN echo y | android update sdk -a -u -t platform-tools,build-tools-${ANDROID_BUILD_TOOLS_VERSION}

ENV PATH=$PATH:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools

#====================================
# nodejs, npm, appium 설치
#====================================
ENV APPIUM_VERSION=1.6.5

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
    apt-get -qqy install nodejs && \
    npm install -g appium@${APPIUM_VERSION} --no-shrinkwrap  && \
    npm cache clean && \
    apt-get remove --purge -y npm && \
    apt-get autoremove --purge -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get clean

#==================================
# TimeZone 변경
#==================================
ENV TZ="Asia/Seoul"
RUN echo "${TZ}" > /etc/timezone

#===============
# Expose Ports
#---------------
# 4723
#   Appium port
#===============
EXPOSE 4723

#===================
# chromedriver 설치
#===================
RUN mkdir -p /root/chromedriver/linux/4.x /root/chromedriver/linux/5.x /root/chromedriver/linux/6.x
RUN mkdir -p /root/chromedriver/mac/4.x /root/chromedriver/mac/5.x /root/chromedriver/mac/6.x
RUN mkdir -p /root/chromedriver/win/4.x /root/chromedriver/win/5.x /root/chromedriver/win/6.x


#===================
# android os 4.x
# chromedriver 2.9
# win, linux mac
#===================
RUN curl -sS -o /root/chromedriver/linux/4.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.9/chromedriver_linux64.zip && \
    unzip /root/chromedriver/linux/4.x/chromedriver.zip && \
    rm /root/chromedriver/linux/4.x/chromedriver.zip && \
    chmod +x /root/chromedriver/linux/4.x/chromedriver

RUN curl -sS -o /root/chromedriver/mac/4.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.9/chromedriver_mac32.zip && \
    unzip /root/chromedriver/mac/4.x/chromedriver.zip && \
    rm /root/chromedriver/mac/4.x/chromedriver.zip && \
    chmod +x /root/chromedriver/mac/4.x/chromedriver

RUN curl -sS -o /root/chromedriver/win/4.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.9/chromedriver_win32.zip && \
    unzip /root/chromedriver/win/4.x/chromedriver.zip && \
    rm /root/chromedriver/win/4.x/chromedriver.zip && \
    chmod +x /root/chromedriver/win/4.x/chromedriver

#===================
# android os 5.x
# chromedriver 2.29
# win, linux mac
#===================
RUN curl -sS -o /root/chromedriver/linux/5.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.29/chromedriver_linux64.zip && \
    unzip /root/chromedriver/linux/5.x/chromedriver.zip && \
    rm /root/chromedriver/linux/5.x/chromedriver.zip && \
    chmod +x /root/chromedriver/linux/5.x/chromedriver

RUN curl -sS -o /root/chromedriver/mac/5.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.29/chromedriver_mac64.zip && \
    unzip /root/chromedriver/mac/5.x/chromedriver.zip && \
    rm /root/chromedriver/mac/5.x/chromedriver.zip && \
    chmod +x /root/chromedriver/mac/5.x/chromedriver

RUN curl -sS -o /root/chromedriver/win/5.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.29/chromedriver_win32.zip && \
    unzip /root/chromedriver/win/5.x/chromedriver.zip && \
    rm /root/chromedriver/win/5.x/chromedriver.zip && \
    chmod +x /root/chromedriver/win/5.x/chromedriver

#===================
# android os 6.x
# chromedriver 2.29
# win, linux mac
#===================
RUN curl -sS -o /root/chromedriver/linux/6.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.29/chromedriver_linux64.zip && \
    unzip /root/chromedriver/linux/6.x/chromedriver.zip && \
    rm /root/chromedriver/linux/6.x/chromedriver.zip && \
    chmod +x /root/chromedriver/linux/6.x/chromedriver

RUN curl -sS -o /root/chromedriver/mac/6.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.29/chromedriver_mac64.zip && \
    unzip /root/chromedriver/mac/6.x/chromedriver.zip && \
    rm /root/chromedriver/mac/6.x/chromedriver.zip && \
    chmod +x /root/chromedriver/mac/6.x/chromedriver

RUN curl -sS -o /root/chromedriver/win/6.x/chromedriver.zip http://chromedriver.storage.googleapis.com/2.29/chromedriver_win32.zip && \
    unzip /root/chromedriver/win/6.x/chromedriver.zip && \
    rm /root/chromedriver/win/6.x/chromedriver.zip && \
    chmod +x /root/chromedriver/win/6.x/chromedriver

#===================
# appium server 실행
#===================
CMD xvfb-run appium --session-override
