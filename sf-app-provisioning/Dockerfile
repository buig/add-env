FROM php:7.4-apache

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN apt-get update && apt-get install -y tmux \
    vim \
    git \
    unzip \
    tmux \
    zlib1g-dev \
    libpng-dev \
    libzip-dev \
    libxml2-dev \
    openssl \
    python3 \
    python3-pip \
    wget \
    libxrender1 \
    libfontconfig1 \
    default-mysql-client

RUN docker-php-ext-install pcntl \
    zip \
    gd \
    xml \
    intl \
    fileinfo

RUN docker-php-ext-install pdo \
    pdo_mysql

RUN pip3 install mysql-connector

RUN echo "memory_limit=-1" > /usr/local/etc/php/conf.d/memory-limit-php.ini

# COMPOSER INSTALLATION
RUN curl -o composer-setup.php https://getcomposer.org/installer && \
    curl -o composer-setup.sig https://composer.github.io/installer.sig && \
    php -r "if (hash('SHA384', file_get_contents('composer-setup.php')) !== trim(file_get_contents('composer-setup.sig'))) { unlink('composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" && \
    php composer-setup.php --version=1.10.16 --quiet && \
    mv composer.phar /usr/local/bin/composer

# INSTALL SYMFONY CLI
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

WORKDIR /code

#APACHE INTALLATION
RUN a2enmod rewrite headers

EXPOSE 8082:80
