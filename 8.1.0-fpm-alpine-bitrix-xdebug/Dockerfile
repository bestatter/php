FROM php:8.1.0-fpm-alpine

RUN apk add --no-cache --update \
    libzip-dev \
    libxml2-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    autoconf \
    gcc g++ make \
    && pecl install xdebug \
    && docker-php-ext-configure \
    gd --with-freetype --with-jpeg \
    && docker-php-ext-enable \
    opcache \
    && docker-php-ext-install \
    gd \
    mysqli \
    sockets \
    xml \
    zip \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apk del autoconf gcc g++ make \
    && docker-php-source delete \
    && rm -rf /var/cache/apk/* /tmp/*

COPY config/php.ini /usr/local/etc/php/conf.d/50-setting.ini

ENV BITRIX_VA_VER="7.5.0"