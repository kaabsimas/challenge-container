FROM php:7.2-apache

ARG PUID
ARG PGID

# RUN groupadd --force -g $PGID user
# RUN useradd -ms /bin/bash --no-user-group -G root -u $PUID -g $PGID user
RUN addgroup --gid $PGID user
RUN adduser --disabled-password --gecos '' --uid $PUID --gid $PGID user
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

RUN curl -sS http://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

USER user
WORKDIR /var/www/nr-challenge