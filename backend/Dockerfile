# Étape 1 : Build PHP avec Composer
FROM composer:2 AS builder
WORKDIR /app
COPY backend/composer.json backend/composer.lock ./
RUN composer install --no-dev --optimize-autoloader

# Étape 2 : Image finale PHP + Apache
FROM php:8.2-apache
WORKDIR /var/www/html

# Installer les dépendances PHP pour Laravel
RUN docker-php-ext-install pdo pdo_mysql && \
    a2enmod rewrite

# Copier les fichiers Laravel + vendors
COPY backend/ .
COPY --from=builder /app/vendor/ ./vendor/

# Configurer Apache pour Laravel
COPY backend/000-default.conf /etc/apache2/sites-available/000-default.conf
RUN chown -R www-data:www-data /var/www/html/storage

EXPOSE 80