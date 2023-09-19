# Use an official PHP runtime as a base image
FROM php:8.1-apache

RUN apt-get update && \
    apt-get install --yes --force-yes \
    cron g++ gettext libicu-dev openssl \
    libc-client-dev libkrb5-dev  \
    libxml2-dev libfreetype6-dev \
    libgd-dev libmcrypt-dev bzip2 \
    libbz2-dev libtidy-dev libcurl4-openssl-dev \
    libz-dev libmemcached-dev libxslt-dev git-core libpq-dev \
    libzip4 libzip-dev libwebp-dev


# PHP Configuration
RUN docker-php-ext-install soap tidy xsl zip 
RUN docker-php-ext-install mysqli pdo pdo_mysql 
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp 
RUN docker-php-ext-install gd
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl 
RUN docker-php-ext-install imap
    # docker-php-ext-configure hash --with-mhash &&\
    # pecl install xdebug && docker-php-ext-enable xdebug &&\
    # pecl install mongodb && docker-php-ext-enable mongodb &&\

RUN mkdir -p /usr/src/php/ext/redis; \
	curl -fsSL https://pecl.php.net/get/redis --ipv4 | tar xvz -C "/usr/src/php/ext/redis" --strip 1; \
	docker-php-ext-install redis;

COPY --from=composer /usr/bin/composer /usr/bin/composer

# Apache Configuration
RUN a2enmod rewrite 
RUN a2enmod headers
RUN a2enmod expires
RUN a2enmod ssl


# Imagemagick : install fails on 8.0
RUN apt-get install --yes --force-yes libmagickwand-dev libmagickcore-dev
RUN yes '' | pecl install -f imagick &&\
    docker-php-ext-enable imagick

# COPY create_vhost config-vhost start /usr/local/bin/
# COPY php.ini /usr/local/etc/php/


# CMD ["start"]
