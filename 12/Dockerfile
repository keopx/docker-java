FROM debian:stretch

MAINTAINER keopx <keopx@keopx.net>

ENV DEBIAN_FRONTEND=noninteractive

# Set repositories
RUN \
   echo "deb http://ftp.de.debian.org/debian/ stretch main non-free contrib" > /etc/apt/sources.list && \
   echo "deb-src http://ftp.de.debian.org/debian/ stretch main non-free contrib" >> /etc/apt/sources.list && \
   echo "deb http://security.debian.org/ stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
   echo "deb-src http://security.debian.org/ stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
   # Update repositories cache and distribution
   apt-get -qq update && apt-get -qqy upgrade

RUN \
   apt-get -yqq install gnupg2 && \
   echo "deb http://ppa.launchpad.net/linuxuprising/java/ubuntu bionic main" | tee /etc/apt/sources.list.d/linuxuprising-java.list && \
   apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 73C3DB2A && \
   apt-get -yqq update
   
RUN \
   (echo oracle-java12-installer shared/accepted-oracle-license-v1-2 select true |  /usr/bin/debconf-set-selections) && \
   apt-get -yqq install --no-install-recommends -y oracle-java12-installer && \
   rm -rf /var/cache/oracle-jdk12-installer && \
   echo "networkaddress.cache.ttl=60" >> /usr/lib/jvm/java-12-oracle/conf/security/java.security
   

# Cleanup some things.
RUN apt-get -q autoclean && \
  rm -rf /var/lib/apt/lists/*

# JAVA ENV.
ENV JAVA_HOME /usr/lib/jvm/java-12-oracle

CMD ["/usr/bin/java"]
