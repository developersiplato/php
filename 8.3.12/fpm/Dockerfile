FROM php:8.3.12-fpm-bullseye

MAINTAINER Maxence POUTORD <maxence.poutord@gmail.com>

RUN apt-get update && apt-get install -y \
    openssl \
    git \
    unzip \
    curl \
    wget \
    libpng-dev \
    zlib1g-dev \
    msmtp \
    libzip-dev

RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    mysqli \
    zip \
    gd \
    sockets \
    bcmath \
    pcntl \
    opcache


# Set timezone
RUN ln -snf /usr/share/zoneinfo/UTC /etc/localtime && echo UTC > /etc/timezone
RUN "date"

# install xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.discover_client_host=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.client_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# install redis extension
RUN pecl install redis
RUN docker-php-ext-enable redis

RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/html
