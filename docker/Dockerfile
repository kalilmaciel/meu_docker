# Usando a imagem base do PHP com Apache
FROM ubuntu:26.04

RUN apt update

RUN ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata

RUN apt install -y curl gpg gnupg2 software-properties-common \
apt-transport-https lsb-release ca-certificates && update-ca-certificates

# RUN add-apt-repository ppa:ondrej/php -y

# RUN apt update

RUN apt install -y apache2 mysql-server nodejs \
php8.5 libapache2-mod-php8.5 \
php-pear php8.5-dev php8.5-cli php8.5-fpm php8.5-curl \
php8.5-mysqlnd php8.5-gd php8.5-zip \
php8.5-intl php8.5-common php8.5-bcmath php8.5-imagick \
php8.5-xmlrpc php8.5-readline php8.5-memcached php8.5-redis \
php8.5-mbstring php8.5-apcu php8.5-xml php8.5-dom php8.5-memcache \
php8.5-xmlwriter php8.5-bz2 php8.5-mysqli php8.5-sqlite3 \
php8.5-soap php-xdebug

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Ativando mod_rewrite do Apache
RUN a2enmod rewrite

# Ativando o Virtual Host do Apache 
RUN a2enmod vhost_alias

# Habilita o SSL em modo legado pra poder funcionar a NFE
RUN echo "\n[openssl_init]\n\
providers = provider_sect\n\
[provider_sect]\n\
default = default_sect\n\
legacy = legacy_sect\n\
[default_sect]\n\
activate = 1\n\
[legacy_sect]\n\
activate = 1" >> /etc/ssl/openssl.cnf

# desabilita avisos de métodos depreciados
RUN echo "\nerror_reporting = E_ALL & ~E_DEPRECATED\n\
extension=soap\n\
extension=curl\n\
extension=openssl" >> /etc/php/8.5/apache2/php.ini


# Iniciando o Apache
CMD apachectl -D FOREGROUND

# Set working directory
WORKDIR /var/www
