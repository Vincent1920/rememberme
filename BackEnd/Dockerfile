# Gunakan image PHP dengan FPM (FastCGI Process Manager)
FROM php:8.2-fpm

# Set working directory di dalam container
WORKDIR /var/www/html

# Install dependencies sistem
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libonig-dev \
    libzip-dev \
    libxml2-dev

# Hapus cache apt
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install ekstensi PHP yang dibutuhkan Laravel
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd

# Install Composer secara resmi dari image composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy semua file project ke dalam container
COPY . .

# Berikan izin akses folder storage dan cache (khas Laravel)
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Port default PHP-FPM
EXPOSE 9000

CMD ["php-fpm"]