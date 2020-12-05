FROM php:7.4-apache

# laravel root folder is public
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# adjust apache
RUN a2enmod rewrite headers

# install xdebug and pdos
RUN docker-php-ext-install pdo pdo_mysql \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug

# install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# add args
ARG uid
ARG gid

# assign args to data
RUN echo "assigning www-data the ${uid} and ${gid}" \
    && usermod -u 1000 www-data \
    && groupmod -g 1000 www-data

# install laravel globally
# in order to init laravel project
RUN composer global require laravel/installer \
    && export PATH=~/.composer/vendor/bin:$PATH