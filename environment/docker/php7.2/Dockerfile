FROM php:7.2-apache

ARG VERSION
ARG DOMAIN
ARG EMAIL

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

# Suppress docker-compose message with missing 'ServerName' directive
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf