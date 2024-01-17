FROM php:8.3-fpm

RUN apt-get update \
    && apt-get install -y libicu-dev libzip-dev zip git \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug
    

# Copy system configs
COPY ./config /usr/local/etc
COPY ./var /var
RUN chmod 777 -R /var/log

# Copy the 'local' php.ini-development into php.ini
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony
RUN git config --global user.email "you@example.com" \
    && git config --global user.name "Your Name"