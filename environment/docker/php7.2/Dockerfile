FROM php:7.2-apache

ARG VERSION
ARG DOMAIN
ARG EMAIL
ARG UID
ARG GID

LABEL version = ${VERSION}
LABEL domain  = ${DOMAIN}
LABEL email   = ${EMAIL}

# Installing and updating server packages
RUN apt-get update
RUN apt-get install -y --no-install-recommends curl
RUN apt-get install -y --no-install-recommends zip
RUN apt-get install -y --no-install-recommends unzip
RUN apt-get install -y --no-install-recommends git
RUN apt-get install -y --no-install-recommends wget
RUN apt-get install -y --no-install-recommends python
RUN apt-get install -y --no-install-recommends graphicsmagick
RUN apt-get install -y --no-install-recommends libmemcached-dev
RUN apt-get install -y --no-install-recommends libz-dev
RUN apt-get install -y --no-install-recommends libpq-dev
RUN apt-get install -y --no-install-recommends libjpeg-dev
RUN apt-get install -y --no-install-recommends libxml2-dev
RUN apt-get install -y --no-install-recommends libfreetype6-dev
RUN apt-get install -y --no-install-recommends libssl-dev
RUN apt-get install -y --no-install-recommends libssl-dev
RUN apt-get install -y --no-install-recommends libmcrypt-dev
RUN apt-get install -y --no-install-recommends locales

# Setting up locales
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen

# Installing basic necessary packages.
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install opcache
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip
RUN docker-php-ext-install mbstring 
RUN docker-php-ext-install pdo 
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install intl
RUN docker-php-ext-install ctype
RUN docker-php-ext-install tokenizer

# Php GD Library
RUN docker-php-ext-install gd
RUN docker-php-ext-configure gd --enable-gd-native-ttf --with-jpeg-dir=/usr/lib --with-freetype-dir=/usr/include/freetype2
RUN docker-php-ext-install gd

# Suppress docker-compose message with missing 'ServerName' directive
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN openssl req -x509 -nodes -days 3650 -newkey rsa:2048 \
    -keyout /etc/ssl/private/ssl-cert-docker.key \
    -out /etc/ssl/certs/ssl-cert-docker.pem \
    -subj "/C=AL/ST=Albania/L=Shkoder/O=W3Development/OU=SHPK/CN=Docker"

RUN a2enmod ssl

# Installing composer from the composer docker image
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Installing Node manager.
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash

RUN chmod +x /root/.nvm/nvm.sh && /root/.nvm/nvm.sh

RUN  usermod --non-unique --uid ${UID} www-data
RUN groupmod --non-unique --gid ${GID} www-data