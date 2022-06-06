FROM php:7.4-apache

ARG PUID
ARG PGID

RUN addgroup --gid $PGID fgadmin
RUN adduser --disabled-password --gecos '' --uid $PUID --gid $PGID fgadmin
RUN usermod -a -G sudo,root,www-data fgadmin
RUN passwd -d fgadmin

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

COPY ./ssl-params.conf /etc/apache2/conf-available/ssl-params.conf
COPY ./default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
COPY ./ssl/cert.crt /etc/ssl/certs/cert.crt
COPY ./ssl/cert.key /etc/ssl/local/cert.key

RUN a2enmod ssl
RUN a2enmod headers
RUN a2ensite default-ssl
RUN a2enconf ssl-params
# RUN apache2ctl configtest
RUN service apache2 restart

USER fgadmin
WORKDIR /var/www/src