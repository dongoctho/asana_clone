FROM php:8.2-apache

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    && docker-php-ext-install zip pdo pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Enable Apache modules
RUN a2enmod rewrite ssl

# Create SSL directory
RUN mkdir /etc/apache2/ssl

# Copy vhost configuration
COPY ./docker/vhost.conf /etc/apache2/sites-available/000-default.conf

# Copy SSL certificate & key
COPY ./docker/ssl/localhost.crt /etc/apache2/ssl/
COPY ./docker/ssl/localhost.key /etc/apache2/ssl/

# Enable site
RUN a2dissite 000-default.conf && \
    a2ensite 000-default.conf

WORKDIR /var/www/html

COPY . /var/www/html

RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html
