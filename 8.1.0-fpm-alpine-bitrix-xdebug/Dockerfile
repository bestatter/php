FROM php:8.1.0-fpm-alpine

RUN apk add --no-cache --update \
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
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && rm -rf /var/cache/apk/* /tmp/*

COPY config/php.ini /usr/local/etc/php/conf.d/50-setting.ini