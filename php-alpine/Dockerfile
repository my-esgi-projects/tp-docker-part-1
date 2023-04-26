
FROM php:8.1-fpm-alpine3.16

RUN set -ex; \
    \
    apk add --no-cache --virtual .build-deps \
        apache2-proxy \
        unzip \
        php8-fpm \
        autoconf \
        freetype-dev \
        gmp-dev \
        icu-dev \
        imagemagick-dev \
        libevent-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libmemcached-dev \
        libpng-dev \
        libwebp-dev \
        libxml2-dev \
        libzip-dev \
        pcre-dev \
    ; \
    \
    docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp; \
    docker-php-ext-install -j "$(nproc)" \
        bcmath \
        exif \
        gd \
        gmp \
        intl \
        opcache \
        pcntl \
        pdo_mysql \
        sysvsem \
        zip \
    ;

WORKDIR /var/www/

RUN set -ex; \
    rm -rf /etc/apache2/conf.d/default.conf; \
    wget https://download.nextcloud.com/server/releases/latest.zip; \
    unzip latest.zip; rm latest.zip; chown www-data:www-data -R /var/www/; \
    chown -R www-data:root /var/log/ /etc/apache2/ /run/ ;

ADD conf/nextcloud.conf /etc/apache2/conf.d/nextcloud.conf

CMD httpd -k start && php-fpm
