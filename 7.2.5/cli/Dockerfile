FROM php:7.2.5

USER root

RUN apt-get -y update \
    && apt-get -y install \
        curl \
        git \
        make \
        unzip \
        wget \
        mysql-client \
        gnupg2 \
        tar \
        zip \
        libpng-dev \
        zlib1g-dev \
        rsync

RUN docker-php-ext-install \
    pdo_mysql \
    mysqli \
    mbstring \
    bcmath \
    sockets \
    gd \
    zip \
    pcntl

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "error_reporting = E_ALL" > /usr/local/etc/php/php.ini \
    && echo "display_startup_errors = On" >> /usr/local/etc/php/php.ini \
    && echo "display_errors = On" >> /usr/local/etc/php/php.ini \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs

RUN npm install -g grunt

RUN mkdir /root/.ssh
RUN touch /root/.ssh/config
RUN echo "Host *" >> /root/.ssh/config
RUN echo "    StrictHostKeyChecking no" >> /root/.ssh/config
RUN chmod 400 /root/.ssh/config

RUN touch /usr/local/etc/php/php.ini
RUN echo "date.timezone = UTC" >> /usr/local/etc/php/php.ini

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=UTC" > $PHP_INI_DIR/conf.d/date_timezone.ini

RUN curl -sS https://getcomposer.org/installer | php -- --version=1.6.5 --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN git clone https://github.com/wolfcw/libfaketime.git
WORKDIR /libfaketime/src
RUN make install

# Set up the volumes and working directory
VOLUME ["/app"]
WORKDIR /app
