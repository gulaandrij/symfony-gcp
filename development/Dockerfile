FROM php:7.2-fpm

RUN apt-get update
RUN apt-get install -y git zip unzip curl libpq-dev libpng-dev libgmp-dev libfreetype6-dev
RUN docker-php-ext-install pdo opcache gd pdo_pgsql gmp zip bcmath
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY php.ini /usr/local/etc/php/php.ini
RUN pecl install apcu
RUN docker-php-ext-enable apcu
RUN pecl install xdebug && docker-php-ext-enable xdebug

WORKDIR /var/www/html

EXPOSE 9000