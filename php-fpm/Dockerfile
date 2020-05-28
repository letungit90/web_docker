FROM php:7.2.4-fpm

RUN apt-get update && apt-get install -y \
      libjpeg-dev \
      libfreetype6-dev \
      libmemcached-dev \
      libpng-dev \
      zip \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql zip opcache exif bcmath \
    && curl -sS https://raw.githubusercontent.com/composer/getcomposer.org/58c3cc59978616c132b5fed9b09314e24cb60462/web/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && pecl install -o -f redis-4.0.2 \
    && pecl install -o -f memcached \
    && rm -rf /tmp/pear \
    && pecl install -o -f xdebug-2.6.0 \
    && rm -rf /tmp/pear \
    && mkdir -p /var/log/php \
    && chown www-data:root /var/log/php \
    && chmod 755 /var/log/php \
    && ln -sf /dev/stderr /var/log/php/error.log \
    && ln -sf /dev/stderr /var/log/php/www-error.log \
    && ln -sf /dev/stderr /var/log/php/php_errors.log

COPY php.ini /usr/local/etc/php/
COPY redis.ini /usr/local/etc/php/conf.d/
COPY docker-php-ext-opcache.ini /usr/local/etc/php/conf.d/

COPY docker.conf /usr/local/etc/php-fpm.d/
COPY zz-docker.conf /usr/local/etc/php-fpm.d/

RUN apt-get update -y \
    && apt-get install nano -y \
    && apt-get install cron -y \
    && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

