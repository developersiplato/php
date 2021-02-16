FROM php:5.4-fpm

USER root

RUN apt-get -y update \
    && apt-get -y install \
        openssl \
        curl \
        git \
        make \
        unzip \
        wget \
        mysql-client

RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    mysql \
    mysqli \
    mbstring \
    bcmath

RUN pecl install https://xdebug.org/files/xdebug-2.4.1.tgz \
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
#ADD ./mysql.ini /usr/local/etc/php/conf.d/mysql.ini

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=Europe/London" > $PHP_INI_DIR/conf.d/date_timezone.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Set up the volumes and working directory
VOLUME ["/app"]
WORKDIR /app
