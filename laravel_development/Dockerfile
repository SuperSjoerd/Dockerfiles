FROM php:7.2-apache
LABEL maintainer="Sjoerd de Vries <sjoerd@storekeeper.nl>"

# Retrieve updated package list
RUN apt-get update

# DEVELOPMENT ONLY! Install composer and dependencies
RUN apt-get install -y curl vim git zip unzip && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Installing necessary extensions
RUN docker-php-ext-install mysqli
RUN apt-get update && apt-get install -y libxml2-dev && docker-php-ext-install soap mbstring

# DEVELOPMENT ONLY! Setup XDebug for PHP 7.2
RUN pecl install xdebug-2.7.0
RUN docker-php-ext-enable xdebug
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

# Turn mod_rewrite on
RUN /usr/sbin/a2enmod rewrite

# Create neccessary directories
RUN mkdir -p /var/www/app/public
RUN rm -r /var/www/html && ln -s /var/www/app/public /var/www/html

# Copy content
COPY ./ /var/www/app/

# Set the file perms correctly on the web root
RUN chown -R www-data:www-data /var/www/

WORKDIR /var/www/html