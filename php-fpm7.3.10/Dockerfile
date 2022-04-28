FROM php:7.3.10-fpm
WORKDIR /www/html

# bcmath pdo_mysql intl gd zip opcache redis memcached
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    vim\
    git \
    procps \
    supervisor \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxml2-dev \
    libmemcached-dev \
    libzip-dev\
    unzip \
    zip \
    zlib1g-dev \
    libxslt-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) gd intl bcmath pdo_mysql zip xsl opcache soap sockets pcntl\
    && pecl install redis memcached sockets mongodb\
    && docker-php-ext-enable redis memcached sockets  pcntl\
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Mailhog
#COPY mhsendmail_linux_amd64 /usr/local/bin/mhsendmail
#RUN chmod +x /usr/local/bin/mhsendmail
RUN useradd -m -s /bin/bash www

ENV TZ=Asia/Shanghai
 
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

ENV LANG C.UTF-8
