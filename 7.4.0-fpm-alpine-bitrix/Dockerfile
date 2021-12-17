FROM php:7.4.0-fpm-alpine

RUN apk update && apk add \
    libxml2-dev \
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
    && docker-php-source delete \
    && rm -rf /var/cache/apk/*

COPY config/php.ini /usr/local/etc/php/conf.d/50-setting.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer