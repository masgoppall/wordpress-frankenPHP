FROM dunglas/frankenphp:latest

RUN install-php-extensions \
    pdo_mysql mysqli gd intl opcache exif zip bcmath

COPY docker/prod/Caddyfile /etc/frankenphp/Caddyfile
COPY docker/prod/php.ini /usr/local/etc/php/conf.d/99-prod.ini

# Bake source ke image (prod)
COPY src/ /app/public/

WORKDIR /app/public
RUN chown -R www-data:www-data /app/public || true