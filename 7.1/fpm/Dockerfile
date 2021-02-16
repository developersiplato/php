FROM php:7.1-fpm

USER root

RUN apt-get -y update \
    && apt-get -y install \
        curl \
        git \
        make \
        unzip \
        wget \
        mysql-client

RUN docker-php-ext-install \
    pdo_mysql \
    mbstring \
    bcmath

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "error_reporting = E_ALL" > /usr/local/etc/php/php.ini \
    && echo "display_startup_errors = On" >> /usr/local/etc/php/php.ini \
    && echo "display_errors = On" >> /usr/local/etc/php/php.ini \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN mkdir /root/.ssh
RUN touch /root/.ssh/config
RUN echo "Host *" >> /root/.ssh/config
RUN echo "    StrictHostKeyChecking no" >> /root/.ssh/config
RUN chmod 400 /root/.ssh/config

RUN touch /usr/local/etc/php/php.ini
RUN echo "date.timezone = Europe/London" >> /usr/local/etc/php/php.ini

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=Europe/London" > $PHP_INI_DIR/conf.d/date_timezone.ini
