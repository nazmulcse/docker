# Use the official PHP 8.3 image with FPM and Alpine
FROM php:8.3-fpm-alpine

# Arguments for user/group ID
ARG WWWGROUP=1000

# Set working directory
WORKDIR /var/www/html

# Install system dependencies and PHP extensions
RUN apk update && apk add --no-cache \
    git \
    curl \
    libzip-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    libwebp-dev \
    g++ \
    make \
    autoconf \
    pcre-dev \
    mysql-client \
    bash \
    linux-headers \
    freetype-dev \
    # Install GD runtime dependencies
    libpng \
    libjpeg-turbo \
    freetype \
    # Install Composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    # Install Core PHP extensions including pcntl
    && docker-php-ext-install pdo_mysql zip pcntl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    # Install PECL extensions (Redis and Swoole)
    && pecl install -o -f redis \
    && docker-php-ext-enable redis \
    && pecl install swoole \
    && docker-php-ext-enable swoole \
    # Clean up build dependencies
    # Clean up build dependencies (keep runtime dependencies)
    && apk del g++ make autoconf linux-headers freetype-dev \
    && rm -rf /var/cache/apk/*

# Create a non-root user for security
RUN addgroup -g $WWWGROUP www \
    && adduser -u 1000 -G www -D www

# Switch to non-root user
USER www

# Expose the Octane port (default is 8000)
EXPOSE 8000

# Default command to keep the container running for development
CMD ["sleep", "infinity"]
