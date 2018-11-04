FROM php:7.2-cli-alpine3.8

# USER root - default anyway

COPY Copy/bashrc /root/.bashrc
COPY Copy/bash_aliases /root/.bash_aliases
COPY Copy/sleep.sh /usr/local/bin/sleep
# COPY Copy/php.ini /usr/local/etc/php/php.ini

WORKDIR /usr/src/

VOLUME /usr/src/

#install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer 

# insatll programs
RUN apk add --update --no-cache \
    bash \
    vim

# install dependencies for pecl installation
RUN apk add --no-cache \
    autoconf \
    build-base

# install and enable xDebug 
RUN pecl install xdebug-2.6.1 \
    && docker-php-ext-enable xdebug

RUN ls -l /usr/local/etc/php


# to tylko do testów - wywalić
# RUN ls -l /usr/local/etc/php/conf.d
# RUN find -iname "*modules*"
# RUN ls -l /usr/src

# CMD ["sleep"]
# CMD ["bash"]


# ls -l /usr :
# drwxr-xr-x    1 root     root          4096 Nov  4 21:11 bin
# drwxr-xr-x   11 root     root          4096 Nov  4 21:11 include
# drwxr-xr-x    1 root     root          4096 Nov  4 21:11 lib
# drwxr-xr-x    1 root     root          4096 Nov  4 21:11 libexec
# drwxr-xr-x    1 root     root          4096 Sep 12 01:00 local
# drwxr-xr-x    1 root     root          4096 Sep 12 01:00 sbin
# drwxr-xr-x    1 root     root          4096 Nov  4 21:11 share
# drwxr-xr-x    1 root     root          4096 Sep 12 01:00 src
# drwxr-xr-x    4 root     root          4096 Nov  4 21:11 x86_64-alpine-linux-musl


# find xdebug
# /tmp/pear/download/xdebug-2.6.1.tgz
# /usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so
# /usr/local/lib/php/.registry/.channel.pecl.php.net/xdebug.reg
# /usr/local/lib/php/doc/xdebug
# /usr/local/lib/php/doc/xdebug/xdebug.ini
# /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini