ARG PHP_VERSION=8.1.9

# Prod image
FROM php:${PHP_VERSION}-fpm-bullseye AS app_php
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
RUN apt-get update && \
    apt-get install -y \
    libzip-dev \
    libicu-dev && \
    docker-php-ext-install zip intl opcache pdo pdo_mysql

WORKDIR /var/www/project

CMD ["php-fpm"]

# Dev image
FROM app_php AS app_php_dev
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug
RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    p7zip \
    git \
    apt-utils \
    gnupg \
    apt-transport-https \
    symfony-cli

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer
RUN mkdir /.composer && chmod -R 777 /.composer # for cache composer.
