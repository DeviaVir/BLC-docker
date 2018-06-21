FROM ubuntu:16.04 AS builder
ENV LIGHTNINGD_VERSION=master
ENV BITCOIN_PGP_KEY=0xD46F45428842CE5E

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ${BITCOIN_PGP_KEY}

RUN echo deb http://ppa.launchpad.net/bitcoin/bitcoin/ubuntu xenial main > /etc/apt/sources.list.d/bitcoin-bitcoin-xenial.list && \
    apt-get update && \
    apt-get install -y \
      autoconf automake build-essential git libtool libgmp-dev \
      libsqlite3-dev python python3 net-tools zlib1g-dev bitcoind

RUN git clone https://github.com/ElementsProject/lightning.git /opt/lightningd && \
    cd /opt/lightningd && \
    git checkout ${LIGHTNINGD_VERSION} && \
    ./configure && \
    make && make install

CMD lightningd
