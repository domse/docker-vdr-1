FROM chriszero/ubuntu-s6-base
MAINTAINER chriszero <zerov83@gmail.com>

WORKDIR /tmp

COPY src/* ./
RUN apt-get update -qq && \
    apt-get install -qy build-essential \
      git \
      wget unzip \
      uuid uuid-dev \
      libarchive13 libarchive-dev \
      zlib1g zlib1g-dev \
      libcurl3-nss libcurl4-nss-dev \
      libxslt1.1 libxslt1-dev \
      libxml2 libxml2-dev \
      libmariadbclient-dev libmariadbclient18 \
      libjpeg8 libjpeg-dev libtiff-dev \
      libimlib2 libimlib2-dev \
      libjansson4 libjansson-dev \
      libssl-dev \
      libmicrohttpd10 libmicrohttpd-dev \
      libimlib2 libimlib2-dev \
      libjpeg8 libjpeg-dev \
      python libpython2.7 libpython-dev python-dev && \
     \
    mkdir -p /usr/lib/mysql/plugin &&\
    mkdir -p /config &&\
    wget https://projects.vdr-developer.org/git/vdr-epg-daemon.git/snapshot/vdr-epg-daemon-0.6.31.tar.gz && \
    tar xzf vdr-epg-daemon-0.6.31.tar.gz && \
    cd vdr-epg-daemon* && \
    patch -p1 < ../tvm-http.diff && \
    make all install &&\
     \
    apt-get remove -qy \
      build-essential \
      wget \
      uuid-dev \
      libarchive-dev \
      zlib1g-dev \
      libcurl4-nss-dev \
      libxslt1-dev \
      libxml2-dev \
      libmariadbclient-dev \
      libjpeg-dev libtiff-dev \
      libimlib2-dev \
      libjansson-dev \
      libssl-dev \
      libjansson-dev \
      libmicrohttpd-dev \
      libpython-dev python-dev &&\
    apt-get autoremove -qy && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY configs/* /epgd/config/ 

# install runit scripts
COPY epgd.sh /etc/services.d/epgd/run
COPY epghttpd.sh /etc/services.d/epghttpd/run

EXPOSE 8888 9999

VOLUME /epgd/config

