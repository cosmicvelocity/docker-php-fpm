FROM php:7.0.18-fpm-alpine
MAINTAINER k01 <k01@white-wing.jp>

ENV APCU_VERSION 5.1.8
ENV REDIS_VERSION 3.1.2
ENV MONGODB_VERSION 1.2.9
ENV MEMCACHED_VERSION 3.0.2
ENV XDEBUG_VERSION 2.5.3

RUN apk add --update --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        cyrus-sasl-dev \
        freetype-dev \
        giflib-dev \
        icu \
        icu-dev \
        imagemagick-dev \
        libbz2 \
        libintl \
        libjpeg-turbo-dev \
        libtool \
        libmcrypt-dev \
        libmemcached-dev \
        libpng-dev \
        libwebp-dev \
        libxpm-dev \
        openssl-dev \
        zlib-dev \
    \
    && docker-php-source extract \
    \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$REDIS_VERSION.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && mv phpredis-$REDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    \
    && curl -L -o /tmp/apcu.tar.gz https://github.com/krakjoe/apcu/archive/v$APCU_VERSION.tar.gz \
    && tar xfz /tmp/apcu.tar.gz \
    && mv apcu-$APCU_VERSION /usr/src/php/ext/apcu \
    && docker-php-ext-install apcu \
    \
    && curl -L -o /tmp/memcached.tar.gz https://github.com/php-memcached-dev/php-memcached/archive/v$MEMCACHED_VERSION.tar.gz \
    && tar xfz /tmp/memcached.tar.gz \
    && mv php-memcached-$MEMCACHED_VERSION /usr/src/php/ext/memcached \
    && docker-php-ext-install memcached \
    \
    && curl -L -o /tmp/xdebug.tgz https://xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz \
    && tar xfz /tmp/xdebug.tgz \
    && mv xdebug-$XDEBUG_VERSION /usr/src/php/ext/xdebug \
    && docker-php-ext-install xdebug \
    \
    && pecl install mongodb-$MONGODB_VERSION \
    \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr \
        --with-jpeg-dir=/usr \
        --with-xpm-dir=/usr \
        --with-webp-dir=/usr \
    && docker-php-ext-install gd \
    \
    && docker-php-ext-install \
        curl \
        exif \
        iconv \
        intl \
        mbstring \
        mcrypt \
        mysqli \
        opcache \
        pdo_mysql \
        zip \
    \
    && docker-php-ext-enable \
        apcu \
        curl \
        exif \
        gd \
        iconv \
        intl \
        mcrypt \
        memcached \
        mongodb \
        mysqli \
        opcache \
        pdo_mysql \
        redis \
        xdebug \
        zip \
    \
    && docker-php-source delete \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/local \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | sort -u \
            | xargs -r apk info --installed \
            | sort -u \
        )" \
    && apk add --update --no-cache --virtual .php-rundeps $runDeps \
    && apk del .build-deps \
    && rm -rf /tmp/* \
    && sed -i -E "s@zend_extension@;zend_extension@g" /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

COPY conf/www.conf /usr/local/etc/php-fpm.d/
COPY conf/php.ini /usr/local/etc/php/
