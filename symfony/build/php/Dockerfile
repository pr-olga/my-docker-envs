FROM php:8-fpm-alpine3.13

ENV RUN_DEPS="bash git postgresql-dev icu-libs icu" \
    BUILD_DEPS="autoconf g++ make pcre-dev icu-dev openssl-dev libxml2-dev libmcrypt-dev git libpng-dev" \
    PECL_EXTS="apcu xdebug" \
    PHP_EXTS="pgsql pdo_pgsql intl" 

RUN apk --no-cache add shadow

RUN    apk update \
    && apk upgrade \
    && apk add --no-cache $RUN_DEPS \
    && apk add -t .build-deps $BUILD_DEPS \
    && docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) $PHP_EXTS \
    && docker-php-ext-enable --ini-name 05-opcache.ini opcache \
    && pecl channel-update pecl.php.net \
    && pecl install -o -f $PECL_EXTS \
    && docker-php-ext-enable $PECL_EXTS \
    && pecl clear-cache \
    && apk del .build-deps \
    # Clear
    && rm -rf /tmp/* /var/cache/apk/*

ARG uid
ARG gid

RUN echo "assigning www-data the ${uid} and ${gid}" \
    && usermod -u 1000 www-data \
    && groupmod -g 1000 www-data

COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
RUN git config --global user.email "frkhorkovaolga@gmail.com" \ 
    && git config --global user.name "pr-olga"