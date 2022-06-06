FROM php:7.4-apache

ARG PUID
ARG PGID

RUN addgroup --gid $PGID fgadmin
RUN adduser --disabled-password --gecos '' --uid $PUID --gid $PGID fgadmin
# RUN usermod -a -G root,www-data user

RUN apt-get update \
    && apt-get install -y \
        g++ \
        libicu-dev \
        libpq-dev \
        libzip-dev \
        zip \
        unzip \
        git \
    && docker-php-ext-install \
        intl \
        opcache \
        pdo \
        pdo_mysql \
        mysqli

RUN apt-get install -y sudo gnupg gnupg2 vim ca-certificates

RUN curl -sS http://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

USER fgadmin
WORKDIR /var/www/src