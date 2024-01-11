FROM php:8.2-fpm

WORKDIR "/application"
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmagickwand-dev --no-install-recommends \
        zlib1g-dev libzip-dev sendmail \
		ghostscript\
		libxslt-dev\
		libxml2-dev\
    && pecl install imagick \
    && pecl install redis-5.3.7 \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \ 
    && docker-php-ext-install pdo_mysql \ 
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-ext-install xsl \
    && docker-php-ext-install soap \
    && docker-php-ext-install intl \
    && echo "sendmail_path=/usr/sbin/sendmail -t -i" >> /usr/local/etc/php/conf.d/sendmail.ini \ 
    && mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/3.0.0.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && docker-php-ext-enable redis 

ENV TZ=America/Chicago
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#mail stuff
# RUN echo "sendmail_path=/usr/sbin/sendmail -t -i" >> /usr/local/etc/php/conf.d/sendmail.ini
# RUN sed -i '/#!\/bin\/sh/aservice sendmail restart' /usr/local/bin/docker-php-entrypoint
# RUN sed -i '/#!\/bin\/sh/aecho "$(hostname -i)\t$(hostname) $(hostname).localhost" >> /etc/hosts' /usr/local/bin/docker-php-entrypoint
# RUN rm -rf /var/lib/apt/lists/*

COPY php-fpm-overrides.conf /usr/local/etc/php-fpm.d/
RUN printf '[PHP]\ndate.timezone = "America/Chicago"\n' > /usr/local/etc/php/conf.d/tzone.ini
