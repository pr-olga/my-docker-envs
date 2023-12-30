FROM kleland/php8.1-fpm

ENV RUN_DEPS="bash git icu-libs icu" \
    BUILD_DEPS="autoconf g++ pcre-dev icu-dev openssl-dev git libpng-dev libjpeg-turbo-dev libltdl libmcrypt-dev libxml2-dev" \
    PECL_EXTS="" \
    PHP_EXTS="gd"

ARG uid
ARG gid

RUN echo "assigning www-data the ${uid} and ${gid}" \
    usermod -u $uid www-data && \
    groupmod -g $gid www-data


COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer
