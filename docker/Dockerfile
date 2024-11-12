# Usando a imagem base do PHP com Apache
FROM ubuntu:24.04

RUN timedatectl set-timezone America/Sao_Paulo

RUN apt update

RUN apt install -y curl gpg gnupg2 software-properties-common \
ca-certificates apt-transport-https lsb-release 

RUN add-apt-repository -y ppa:ondrej/php

RUN apt install -y apache2 mysql-server nodejs \
php8.3 libapache2-mod-php8.3 \
php8.3-cli php8.3-fpm php8.3-curl \
php8.3-mysqlnd php8.3-gd php8.3-opcache php8.3-zip \
php8.3-intl php8.3-common php8.3-bcmath php8.3-imagick \
php8.3-xmlrpc php8.3-readline php8.3-memcached php8.3-redis \
php8.3-mbstring php8.3-apcu php8.3-xml php8.3-dom php8.3-memcache \
php8.3-xmlwriter php8.3-bz2 php8.3-mysqli

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
