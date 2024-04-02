FROM php:8.2-fpm

# COPY php.ini
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini

# Composer install
COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

# install Node.js
COPY --from=node:17.7 /usr/local/bin /usr/local/bin
COPY --from=node:17.7 /usr/local/lib /usr/local/lib

RUN apt-get update && \
    apt-get -y install \
    git \
    zip \
    unzip \
    vim \
    libzip-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-install zip gd \
    && docker-php-ext-install pdo_mysql bcmath \
    && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
    && docker-php-ext-install redis

WORKDIR /var/www/html