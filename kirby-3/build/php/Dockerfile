FROM php:8-fpm-alpine3.13

ENV RUN_DEPS="bash git icu-libs icu" \
    BUILD_DEPS="autoconf g++ pcre-dev icu-dev openssl-dev git libpng-dev libjpeg-turbo-dev libltdl libmcrypt-dev libxml2-dev" \
    PECL_EXTS="" \
    PHP_EXTS="gd" 

RUN apk --no-cache add shadow

RUN    apk update \
    && apk upgrade \
    && apk add --no-cache $RUN_DEPS \
    && apk add -t .build-deps $BUILD_DEPS \
    && docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) $PHP_EXTS \
    # Clear
    && rm -rf /tmp/* /var/cache/apk/*

ARG uid
ARG gid

RUN echo "assigning www-data the ${uid} and ${gid}" \
    usermod -u $uid www-data && \
    groupmod -g $gid www-data


COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer