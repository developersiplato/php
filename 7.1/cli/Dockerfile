FROM php:7.1

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
RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/conf.d/date_timezone.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN git clone https://github.com/wolfcw/libfaketime.git
WORKDIR /libfaketime/src
RUN make install

# Set up the volumes and working directory
VOLUME ["/app"]
WORKDIR /app
