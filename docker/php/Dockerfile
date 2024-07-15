FROM php:8.2-fpm

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN set -eux

RUN apt-get update && apt-get install -y \
    vim \
    git \
    postgresql-server-dev-15 \
    libzip-dev zip unzip \
    libpng-dev libfreetype-dev \
    tzdata

# pdo
RUN docker-php-ext-install pdo \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype \
    && docker-php-ext-install gd \
    && docker-php-ext-install intl

# php config
RUN touch /usr/local/etc/php/php.ini \
    && echo "upload_max_filesize = 1024M" >> /usr/local/etc/php/php.ini  \
    && echo "post_max_size = 1030M" >> /usr/local/etc/php/php.ini  \
    && echo "date.timezone=Europe/Moscow" >> /usr/local/etc/php/php.ini

# composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

#COPY composer.json composer.lock* ./
#
#RUN composer update

#RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf
# startup
CMD ["php-fpm"]