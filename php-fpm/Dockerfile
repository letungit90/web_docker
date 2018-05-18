FROM php:7.2.4-fpm

RUN apt-get update && apt-get install -y \
      libjpeg-dev \
      libfreetype6-dev \
      libpng-dev \
      zip \
 && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-png-dir=/usr --with-jpeg-dir=/usr \
 	&& docker-php-ext-install -j$(nproc) gd pdo_mysql zip opcache

# composer 1.6.4
RUN curl -sS https://raw.githubusercontent.com/composer/getcomposer.org/58c3cc59978616c132b5fed9b09314e24cb60462/web/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN pecl install -o -f redis-4.0.2 \
	&& rm -rf /tmp/pear

RUN pecl install -o -f xdebug-2.6.0 \
  && rm -rf /tmp/pear

RUN mkdir -p /var/log/php \
  && chown www-data:root /var/log/php \
  && chmod 755 /var/log/php

RUN ln -sf /dev/stderr /var/log/php/error.log \
  && ln -sf /dev/stderr /var/log/php/www-error.log \
  && ln -sf /dev/stderr /var/log/php/php_errors.log

COPY php.ini /usr/local/etc/php/
COPY redis.ini /usr/local/etc/php/conf.d/
COPY docker-php-ext-opcache.ini /usr/local/etc/php/conf.d/

COPY docker.conf /usr/local/etc/php-fpm.d/
COPY zz-docker.conf /usr/local/etc/php-fpm.d/
