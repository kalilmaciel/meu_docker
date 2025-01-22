# Usando a imagem base do PHP com Apache
FROM ubuntu:24.04


RUN apt update

RUN apt install -y curl gpg gnupg2 software-properties-common \
ca-certificates apt-transport-https lsb-release 

RUN add-apt-repository -y ppa:ondrej/php

RUN apt install -y apache2 mysql-server nodejs \
php8.4 libapache2-mod-php8.4 \
php-pear php8.4-dev php8.4-cli php8.4-fpm php8.4-curl \
php8.4-mysqlnd php8.4-gd php8.4-opcache php8.4-zip \
php8.4-intl php8.4-common php8.4-bcmath php8.4-imagick \
php8.4-xmlrpc php8.4-readline php8.4-memcached php8.4-redis \
php8.4-mbstring php8.4-apcu php8.4-xml php8.4-dom php8.4-memcache \
php8.4-xmlwriter php8.4-bz2 php8.4-mysqli php-xdebug

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Ativando mod_rewrite do Apache
RUN a2enmod rewrite

# Ativando o Virtual Host do Apache 
RUN a2enmod vhost_alias

# Iniciando o Apache
CMD apachectl -D FOREGROUND

# Set working directory
WORKDIR /var/www
