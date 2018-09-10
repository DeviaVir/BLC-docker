FROM ubuntu:18.04 AS builder
ENV LIGHTNINGD_VERSION=master
ENV BITCOIN_PGP_KEY=0xD46F45428842CE5E

RUN apt-get update && \
    apt-get install -y \
      autoconf automake gnupg build-essential git && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ${BITCOIN_PGP_KEY} && \
    echo deb http://ppa.launchpad.net/bitcoin/bitcoin/ubuntu bionic main > /etc/apt/sources.list.d/bitcoin-bitcoin-bionic.list && \
    apt-get update && \
    apt-get install -qfy \
      zlib1g-dev bitcoind libtool libgmp-dev \
      libsqlite3-dev python python3 net-tools

RUN git clone https://github.com/ElementsProject/lightning.git /opt/lightningd && \
    cd /opt/lightningd && \
    git checkout ${LIGHTNINGD_VERSION} && \
    ./configure && \
    make && make install
