FROM ubuntu:precise

MAINTAINER Tim Akinbo <takinbo@timbaobjects.com>

RUN apt-get update && apt-get install -y \
        build-essential subversion ntp nano wget cvs subversion curl git-core unzip autoconf \
        automake1.11 libtool flex debhelper pkg-config libpam0g-dev intltool checkinstall docbook docbook-xsl \
        build-essential libpcre3 libpcre3-dev libc6-dev g++ gcc autotools-dev bison libncurses5-dev m4 tex-common \
        texi2html texinfo libxml2-dev \
        openssl libssl-dev locales libmysqlclient-dev libmysql++-dev supervisor libtool \
    bison \
    build-essential \
    libxml2-dev \
    libssl-dev \
    openssl \
    wget \
    && wget --no-check-certificate https://kannel.org/download/1.5.0/gateway-1.5.0.tar.gz \
    && tar xzf gateway-1.5.0.tar.gz \
    && cd gateway-1.5.0 \
    && ./configure --with-mysql  --prefix=/usr --sysconfdir=/etc/kannel \
    && touch .depend \
    && make \
    && make install \
    && cp test/fakesmsc /usr/sbin/ \
    && cp test/fakewap /usr/sbin/ \
    && cd / \
    && rm -Rf gateway-1.4.5 \
    && mkdir -p /var/log/kannel \
    && mkdir -p /var/spool/kannel \
    && chmod -R 755 /var/spool/kannel \
    && chmod -R 755 /var/log/kannel  

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY kannel.conf /etc/kannel/kannel.conf

EXPOSE 13013 13000

VOLUME ["/var/spool/kannel", "/etc/kannel", "/var/log/kannel"]

CMD ["/usr/bin/supervisord"]
