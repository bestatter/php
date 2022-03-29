FROM php:7.4.0-fpm-alpine

COPY start /usr/local/bin/start
COPY rootCA.pem /usr/local/share/ca-certificates/rootCA.pem
COPY config/php.ini /usr/local/etc/php/conf.d/50-setting.ini

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
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && docker-php-source delete \
    && update-ca-certificates --fresh \
    && chmod ugo+x /usr/local/bin/start \
    && rm -rf /var/cache/apk/*

ENV BITRIX_VA_VER="7.5.0"

CMD ["/usr/local/bin/start"]