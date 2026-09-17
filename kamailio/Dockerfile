ARG KAM_VER=6.1

FROM debian:bookworm

ARG KAM_VER
ENV GPG_URL=https://deb.kamailio.org/kamailiodebkey.gpg
ENV GPG_FILE=/usr/share/keyrings/kamailio.gpg
ENV KAM_REPO=http://deb.kamailio.org/kamailio
ENV TERM=screen

RUN    KAM_VER=`echo $KAM_VER | awk -F. '{print $1$2}'` \
    && . /etc/os-release \
    && KAM_APT="[signed-by=${GPG_FILE}] ${KAM_REPO}${KAM_VER}" \
    && KAM_APT="${KAM_APT} $VERSION_CODENAME main" \
    && APT_FILE=/etc/apt/sources.list.d/kamailio.list \
    && apt update \
    && apt install -y wget gpg netbase \
    && wget -O- $GPG_URL | gpg --dearmor > $GPG_FILE \
    && echo "deb     $KAM_APT" >  $APT_FILE \
    && echo "deb-src $KAM_APT" >> $APT_FILE \
    && apt update \
    && apt install -y kamailio sngrep sip-tester


ENTRYPOINT ["/usr/sbin/kamailio", "-DDdE"]

