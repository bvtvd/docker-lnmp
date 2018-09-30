FROM php:5.6.30-fpm
#RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
#    && echo "Asia/Shanghai" > /etc/timezone
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libmemcached-dev \
        zlib1g-dev \
        libcurl4-openssl-dev \
        libxml2-dev \
        --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) \
        iconv mcrypt gettext curl mysqli pdo pdo_mysql zip \
        mbstring bcmath opcache xml simplexml sockets hash soap \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
RUN pecl install redis-3.1.0 \
    && pecl install memcached-2.2.0 \
    && pecl install xdebug-2.5.0 \
    && docker-php-ext-enable redis memcached xdebug
 
RUN mkdir -p /var/www/ \
  && chmod -R 755 /var/www/
 
CMD ["php-fpm", "-F"]
