FROM php:8.0-fpm

RUN apt-get update \
    && apt-get install -y libicu-dev libzip-dev zip \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

# Copy system configs
COPY ./config /usr/local/etc
# Copy the 'local' php.ini-development into php.ini
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony