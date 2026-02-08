FROM dunglas/frankenphp:latest

RUN apt-get update && apt-get install -y --no-install-recommends \
    default-mysql-client procps unzip \
  && rm -rf /var/lib/apt/lists/*

RUN install-php-extensions \
    pdo_mysql mysqli gd intl opcache exif zip bcmath

COPY docker/dev/Caddyfile /etc/frankenphp/Caddyfile
COPY docker/dev/php.ini /usr/local/etc/php/conf.d/99-dev.ini

WORKDIR /app/public