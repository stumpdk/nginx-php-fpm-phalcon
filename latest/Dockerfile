FROM richarvey/nginx-php-fpm
MAINTAINER Arthur Burkart <artburkart@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV INITRD No
ENV LANG C.UTF-8

# Install tools
RUN apt-get update \
  && apt-get install -y --no-install-recommends ca-certificates \
    g++ libpcre3-dev libc6-dev make numactl pdftk \
    poppler-utils php5-dev re2c software-properties-common \
  && rm -rf /var/curllib/apt/lists/*

# Install Phalcon
RUN git clone git://github.com/phalcon/cphalcon.git \
  && cd cphalcon/ext \
  && ./install \
  && mkdir -p /etc/php5/mods-available \
  && echo "extension=phalcon.so" > /etc/php5/mods-available/phalcon.ini

# Configure Phalcon and PHP
RUN echo "extension=phalcon.so" > /etc/php5/fpm/conf.d/21-phalcon.ini \
  && echo "extension=phalcon.so" > /etc/php5/cli/conf.d/21-phalcon.ini \
  && echo "extension=mcrypt.so" > /etc/php5/fpm/conf.d/22-mcrypt.ini \
  && echo "extension=mcrypt.so" > /etc/php5/cli/conf.d/22-mcrypt.ini \
  && sed -i -e "s/;opcache.enable=0/opcache.enable=1/g" /etc/php5/fpm/php.ini