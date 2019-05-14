FROM php:7.2-cli-alpine3.8

# create non-root user
RUN adduser -S dockeruser -u 1000

# install and configure composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && chmod 755 /usr/local/bin/composer

# insatll programs
RUN apk add --update --no-cache \
    bash \
    vim

# install dependencies for pecl installation
RUN apk add --no-cache \
    autoconf \
    build-base \
    zlib-dev

# install and enable extension
RUN pecl install xdebug-2.6.1 \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install zip

# Configure bash and aliases
COPY bash/bashrc /home/dockeruser/.bashrc
COPY bash/bash_aliases /home/dockeruser/.bash_aliases
# Configure php and extensions
COPY config/php.ini-development /usr/local/etc/php/php.ini
COPY config/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Configure xDebug server
ENV PHP_IDE_CONFIG "serverName=docker-xdebug-server"

# Create volume and default dir
RUN mkdir /volume
WORKDIR /volume
VOLUME /volume

# set default user to dockeruser
USER dockeruser
