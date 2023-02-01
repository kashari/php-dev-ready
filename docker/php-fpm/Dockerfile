FROM php:7.4-fpm

# Install PHP extensions and PECL modules.
RUN buildDeps=" \
        default-libmysqlclient-dev \
        libbz2-dev \
        libsasl2-dev \
    " \
    runtimeDeps=" \
        curl \
        git \
        sqlite3 \
        php7.4-sqlite \
        libfreetype6-dev \
        libicu-dev \
        libjpeg-dev \
        libpng-dev \
        libpq-dev \
        libzip-dev \
        libxml2-dev \
    " \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y $buildDeps $runtimeDeps \
    && docker-php-ext-install bcmath bz2 calendar iconv intl mysqli opcache pdo pdo_mysql pdo_pgsql pgsql soap zip \
    && docker-php-ext-install gd \
    && docker-php-ext-install exif \
    && apt-get purge -y --auto-remove $buildDeps \
    && rm -r /var/lib/apt/lists/*

WORKDIR /var/www/html

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && ln -s $(composer config --global home) /root/composer
ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1
