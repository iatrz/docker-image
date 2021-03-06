# Import Ubuntu 18.04 Image
FROM ubuntu:18.04

# Install dependencies
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install bison build-essential curl flex git gnupg gperf liblz4-tool libncurses5-dev libsdl1.2-dev libxml2 libxml2-utils lzop pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev build-essential kernel-package libncurses5-dev bzip2 git python sudo gcc g++ openssh-server tar gzip ca-certificates -y

RUN apt-get purge openjdk-8-jdk openjdk-8-jre openjdk-11-jdk openjdk-11-jre -y

RUN apt-get install openjdk-8-jdk openjdk-8-jre -y

RUN rm -rf /var/lib/apt/lists/*

# Link Timezone
RUN ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime

# Add User
# Why? Well for avoid something wrong
# I've seen some notes for not using root when build
RUN useradd -ms /bin/bash iatrz
RUN echo "iatrz ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER iatrz
WORKDIR /home/iatrz

# Git
RUN git config --global user.email "iaboothahirpkd@gmail.com"
RUN git config --global user.name "iatrz"
RUN git config --global color.ui false

RUN sudo git clone https://github.com/akhilnarang/scripts /scripts

RUN cd /scripts && bash setup/android_build_env.sh && bash setup/install_android_sdk.sh

RUN sudo apt-get install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu gcc-arm-linux-gnueabi g++-arm-linux-gnueabi -y

RUN cd .. && sudo rm -rf /scripts

# Set environment variable
ENV ARCH arm64
ENV CROSS_COMPILE aarch64-linux-gnu-
ENV CROSS_CPMPILE_ARM32 arm-linux-gnueabi-
