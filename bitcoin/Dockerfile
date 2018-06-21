FROM alpine:latest

ENV BITCOIN_VERSION=0.16.1
ENV BITCOIN_DIR_VERSION=0.16.1
ENV BITCOIN_PGP_KEY=0x90C8019E36C2E964
ENV GLIBC_VERSION=2.27-r0

RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/sgerrand.rsa.pub \
 && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk \
 && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk \
 && wget https://bitcoin.org/bin/bitcoin-core-${BITCOIN_VERSION}/SHA256SUMS.asc \
 && wget https://bitcoin.org/bin/bitcoin-core-${BITCOIN_VERSION}/bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz


RUN apk update \
	&& apk --no-cache add wget ca-certificates gnupg \
 	&& apk --no-cache add glibc-${GLIBC_VERSION}.apk \
	&& apk --no-cache add glibc-bin-${GLIBC_VERSION}.apk
RUN gpg --keyserver keyserver.ubuntu.com --recv-keys ${BITCOIN_PGP_KEY} \
  && gpg --verify SHA256SUMS.asc \
  && grep bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz SHA256SUMS.asc | sha256sum -c \
	&& tar xzvf /bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz \
	&& mkdir /root/.bitcoin \
	&& apk del wget ca-certificates \
	&& mv /bitcoin-${BITCOIN_DIR_VERSION}/bin/* /usr/local/bin/ \
	&& rm -rf /bitcoin-${BITCOIN_VBITCOIN_DIR_VERSIONRSION}/ \
	&& rm -rf /bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz \
	&& rm -rf /glibc-${GLIBC_VERSION}.apk \
	&& rm -rf /glibc-bin-${GLIBC_VERSION}.apk

EXPOSE 8333 8332
CMD bitcoind
