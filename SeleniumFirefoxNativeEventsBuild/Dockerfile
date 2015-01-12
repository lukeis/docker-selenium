FROM ubuntu:14.04
MAINTAINER Selenium <selenium-developers@googlegroups.com>

#================================================
# Customize sources for apt-get
#================================================
RUN  echo "deb http://archive.ubuntu.com/ubuntu trusty main universe\n" > /etc/apt/sources.list \
  && echo "deb http://archive.ubuntu.com/ubuntu trusty-updates main universe\n" >> /etc/apt/sources.list

#===================================================================
# Miscellaneous packages for compiling firefox native events module
#===================================================================
RUN apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    ca-certificates \
    unzip \
    wget \
    git \
    default-jdk \
    build-essential \
    g++ \
    libgtk2.0-dev \
    libibus-1.0-dev \
    g++-multilib \
    firefox-dev \
  && rm -rf /var/lib/apt/lists/* \
#  && sed -i 's/\/dev\/urandom/\/dev\/.\/urandom/' ./usr/lib/jvm/java-7-openjdk-amd64/jre/lib/security/java.security

#===================================
# Clone Selenium repo (shallow copy)
#===================================
RUN git clone --depth 1 https://github.com/SeleniumHQ/selenium.git

#=========================
# Build the native events
#=========================
RUN cd selenium; ./go firefox

#========================
# Push the new artifacts
#========================
RUN git update-index --no-assume-unchanged cpp/prebuilt/amd64/libwebdriver_firefox_*
#RUN git commit -am "updating firefox prebuilts" && git push

