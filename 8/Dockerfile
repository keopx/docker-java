FROM debian:stretch

MAINTAINER keopx <keopx@keopx.net>

ENV DEBIAN_FRONTEND=noninteractive

# Set repositories
RUN \
   echo "deb http://ftp.de.debian.org/debian/ stretch main non-free contrib\n" > /etc/apt/sources.list && \
   echo "deb-src http://ftp.de.debian.org/debian/ stretch main non-free contrib\n" >> /etc/apt/sources.list && \
   echo "deb http://security.debian.org/ stretch/updates main contrib non-free\n" >> /etc/apt/sources.list && \
   echo "deb-src http://security.debian.org/ stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
   # Update repositories cache and distribution
   apt-get -qq update && apt-get -qqy upgrade

RUN \
   apt-get -yqq install gnupg2 && \
   echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
   echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
   apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
   apt-get -yqq update

RUN \
   (echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections) && \
   apt-get -yqq install --no-install-recommends -y oracle-java8-installer && \
   rm -rf /var/cache/oracle-jdk8-installer && \
   echo "networkaddress.cache.ttl=60" >> /usr/lib/jvm/java-8-oracle/jre/lib/security/java.security

# Cleanup some things.
RUN apt-get -q autoclean && \
  rm -rf /var/lib/apt/lists/*

# JAVA ENV.
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

CMD ["/usr/bin/java"]
