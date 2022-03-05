FROM php:8.1.0-fpm-alpine

RUN apk update && apk add \
    libxml2-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
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
    && docker-php-source delete \
    && rm -rf /var/cache/apk/*

COPY config/php.ini /usr/local/etc/php/conf.d/50-setting.ini

ENV BITRIX_VA_VER="7.5.0"

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer