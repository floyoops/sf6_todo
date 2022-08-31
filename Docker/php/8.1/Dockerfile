ARG PHP_VERSION=8.1.9

# Prod image
FROM php:${PHP_VERSION}-fpm-bullseye AS app_php
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
CMD ["php-fpm"]

FROM app_php AS app_php_dev

# Dev image
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
