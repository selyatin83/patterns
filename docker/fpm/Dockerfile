FROM php:8.1-fpm

# ставим необходимые для нормальной работы модули
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
	libpng-dev \
	libonig-dev \
	libzip-dev \
	libmemcached-dev \
	libmcrypt-dev \
        && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
        && docker-php-ext-install -j$(nproc) gd \
     && pecl install memcached && \
        docker-php-ext-enable memcached

RUN apt-get install -y libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql pgsql

COPY ./php.ini /usr/local/etc/php/conf.d/php-custom.ini

WORKDIR /var/www

VOLUME /var/www

CMD ["php-fpm"]
