FROM php:8.2.1-bullseye

ENV PHP_MEMORY_LIMIT -1
ENV PHP_MAX_EXECUTION_TIME 250
ENV COMPOSER_MEMORY_LIMIT -1

RUN apt-get update \
  && apt-get install -y dnsutils ssl-cert libssl-dev libmongoc-1.0-0 libzip-dev libpng-dev libjpeg62-turbo-dev git wget acl libpq-dev libssl-dev libmongoc-1.0-0 --no-install-recommends \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pecl install grpc
RUN pecl install mongodb
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install gd
RUN docker-php-ext-enable grpc
RUN docker-php-ext-enable mongodb
RUN docker-php-ext-enable bcmath

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash
RUN apt-get install -y symfony-cli

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer