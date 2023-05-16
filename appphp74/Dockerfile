FROM php:7.4-apache

RUN apt-get -y update && apt-get -y upgrade && apt-get -y install \
    curl \
    vim \ 
    wget\
    lsb-release \
    libicu-dev \
    zip \
    cmake \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install \
    pdo_mysql \
    mysqli \
    gd \
    zip \
    opcache \
    intl

# Composerのインストール
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# mod_rewriteを 有効に
RUN a2enmod rewrite

#RUN ln -s /etc/apache2/mods-available/vhost_alias.load /etc/apache2/mods-enabled
#RUN echo ServerName $HOSTNAME > /etc/apache2/conf-available/fqdn.conf && a2enconf fqdn
#RUN a2enmod headers
#RUN a2enmod include

COPY ./conf/base.conf /etc/apache2/sites-available/base.conf
RUN a2ensite base.conf

COPY ./php.ini /usr/local/etc/php/