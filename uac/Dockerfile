ARG SIPX_V=2.1.0

FROM debian:13-slim

ARG SIPX_V
ARG TARGETARCH
ARG SIPX_BASE=https://github.com/miconda/sipexer/releases/download

ENV TERM=screen

RUN    apt-get update \
	&& apt-get install -y wget sngrep sip-tester \
	&& mkdir /sipexer \
    && cd /sipexer \
    && SIPX_FILE=sipexer-v${SIPX_V}-linux-${TARGETARCH}.tar.gz \
    && SIPX_URL=${SIPX_BASE}/v${SIPX_V}/${SIPX_FILE} \
    && wget $SIPX_URL \
    && tar -xf $SIPX_FILE \
    && cp sipexer /bin \
    && cd .. \
    && rm -rf /sipexer \
	&& rm -rf /var/lib/apt/lists/*


