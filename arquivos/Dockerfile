#Container base: Official PHP 8.1
FROM php:8.1-apache

# Install needed php extensions: ldap
RUN apt-get update && \
    apt-get install libldap2-dev -y && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap

# Install libs
RUN docker-php-ext-install pdo pdo_mysql mysqli

# Enable module rewrite
RUN a2enmod rewrite

WORKDIR /var/www/html

# Restart apache
RUN service apache2 restart
