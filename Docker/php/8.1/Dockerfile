ARG PHP_VERSION=8.1.9

FROM php:${PHP_VERSION}-fpm-bullseye

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

CMD ["php-fpm"]
