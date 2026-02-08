FROM dunglas/frankenphp:latest

# WordPress version (bisa override lewat build args)
ARG WP_VERSION=latest

# Install PHP extensions (WordPress-friendly)
RUN install-php-extensions \
    pdo_mysql mysqli gd intl opcache exif zip bcmath

# Download WordPress core into /app/public
RUN set -eux; \
    mkdir -p /app/public; \
    if [ "$WP_VERSION" = "latest" ]; then \
        curl -fsSL https://wordpress.org/latest.tar.gz -o /tmp/wp.tar.gz; \
    else \
        curl -fsSL "https://wordpress.org/wordpress-${WP_VERSION}.tar.gz" -o /tmp/wp.tar.gz; \
    fi; \
    tar -xzf /tmp/wp.tar.gz -C /tmp; \
    cp -a /tmp/wordpress/. /app/public/; \
    rm -rf /tmp/wp.tar.gz /tmp/wordpress

# Copy only wp-content from repo
COPY src/wp-content/ /app/public/wp-content/

# Caddy + PHP config for prod
COPY docker/prod/Caddyfile /etc/frankenphp/Caddyfile
COPY docker/prod/php.ini /usr/local/etc/php/conf.d/99-prod.ini

WORKDIR /app/public

# Permissions (best-effort; volume mounts may override)
RUN chown -R www-data:www-data /app/public || true