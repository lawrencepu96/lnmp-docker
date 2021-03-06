FROM php:7.1.27-fpm
WORKDIR /www/html/

# bcmath pdo_mysql intl gd zip opcache xdebug redis memcached
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxml2-dev \
    libmemcached-dev \
    unzip \
    libbz2-dev \
    zip \
    autoconf \
    g++ \
    gcc \
    libc-dev \
    make \
    cmake \
    zlib1g-dev \
    libxslt-dev \
    libmcrypt-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) gd bz2 intl bcmath pdo_mysql zip xsl json mysqli opcache mcrypt soap sockets \
    && pecl install redis memcached \
    && docker-php-ext-enable redis memcached \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Mailhog
COPY mhsendmail_linux_amd64 /usr/local/bin/mhsendmail
RUN chmod +x /usr/local/bin/mhsendmail
RUN useradd -m -s /bin/bash www
