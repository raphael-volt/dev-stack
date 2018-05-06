FROM php:7-apache

LABEL maintainer "Raphaël Volt <raphael@ketmie.com>"

RUN apt-get update && apt-get install -y \
    nano \
    bzip2 \
    libbz2-dev \
    libcurl4-openssl-dev \
    libxml2-dev \
    libfreetype6-dev \
    libgd-dev \
    libmcrypt-dev \
    libssl-dev \
    inotify-tools

# Install composer
RUN curl -fsSL https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install php extensions
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install bz2
RUN docker-php-ext-install opcache
RUN docker-php-ext-install zip
RUN docker-php-ext-install pcntl
RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-install gd
RUN docker-php-ext-install intl
RUN pecl install xdebug && docker-php-ext-enable xdebug

# PHPUNIT
RUN export COMPOSER_ALLOW_SUPERUSER=1 \
    && composer global require phpunit/phpunit ^6.5 \
    && composer global require phpunit/php-invoker
ENV PATH /root/.composer/vendor/bin:$PATH

# Apache Configuration
RUN a2enmod rewrite
RUN a2enmod headers

# xdebug configuration
COPY xdebug.core.ini /usr/local/etc/php/conf.d/xdebug.core.ini

# Test watcher
COPY watch.phpunit.sh /usr/local/bin/watch-phpunit
RUN chmod u+x,g+x /usr/local/bin/watch-phpunit
RUN echo "alias watch-phpunit='/usr/local/bin/watch-phpunit'" >> /root/.bashrc
RUN watch-phpunit -h

# Change file mod and owner
RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 0775 /var/www/html

