FROM php:5.6-fpm
MAINTAINER ccqngu@gmail.com

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        git \
        tar \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-install mysql \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install -j$(nproc) gd

RUN git clone -b 2.1.x --depth=1 https://github.com/phalcon/cphalcon.git ~/cphalcon \
    && cd ~/cphalcon/ext \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && docker-php-ext-enable phalcon \
    && rm -rf ~/cphalcon
       
RUN pecl install -o -f redis-2.2.8 \
    &&  rm -rf /tmp/pear \
    &&  echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini