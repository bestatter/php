FROM php:8.1.0-fpm-alpine

COPY start /usr/local/bin/start
COPY rootCA.pem /usr/local/share/ca-certificates/rootCA.pem
COPY config/php.ini /usr/local/etc/php/conf.d/50-setting.ini

RUN apk add --no-cache --update \
    libzip-dev \
    libxml2-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    autoconf \
    gcc g++ make \
    shadow \
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
    && update-ca-certificates --fresh \
    && chmod ugo+x /usr/local/bin/start \
    && rm -rf /var/cache/apk/* /tmp/*

ENV BITRIX_VA_VER="7.5.0"

CMD ["/usr/local/bin/start"]