FROM php:7.2-fpm

RUN apt-get update
RUN apt-get install -y git zip unzip curl libpq-dev libpng-dev libgmp-dev libfreetype6-dev
RUN docker-php-ext-install pdo opcache gd pdo_pgsql gmp zip bcmath
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY php.ini /usr/local/etc/php/php.ini
RUN pecl install apcu
RUN docker-php-ext-enable apcu
RUN pecl install xdebug && docker-php-ext-enable xdebug

RUN version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$version \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
    && mv /tmp/blackfire-*.so $(php -r "echo ini_get('extension_dir');")/blackfire.so \
    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > $PHP_INI_DIR/conf.d/blackfire.ini

WORKDIR /var/www/html

EXPOSE 9000
