FROM php:8.3.4-bookworm

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV PHP_MEMORY_LIMIT -1
ENV PHP_MAX_EXECUTION_TIME 250
ENV COMPOSER_MEMORY_LIMIT -1

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN apt-get update \
  && apt-get install -y supervisor git wget tzdata locales zsh symfony-cli 7zip --no-install-recommends \
  && install-php-extensions xdebug http zip pdo_pgsql pdo_mysql bcmath pcntl gd intl opcache simplexml \
  && locale-gen ja_JP.UTF-8 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir /tmp/xdebug; chmod 777 /tmp/xdebug

ENV TZ Asia/Tokyo
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja

WORKDIR /var/www/html
