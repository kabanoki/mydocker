FROM php:7.1-apache

RUN apt-get update \
    && docker-php-ext-install pdo_mysql mysqli

RUN apt-get -y install vim wget lsb-release libicu-dev

# mod_rewriteを 有効に
RUN a2enmod rewrite

RUN ln -s /etc/apache2/mods-available/vhost_alias.load /etc/apache2/mods-enabled
RUN echo ServerName $HOSTNAME > /etc/apache2/conf-available/fqdn.conf && a2enconf fqdn
RUN a2enmod headers
RUN a2enmod include

# GD関連のインストール
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev
RUN docker-php-ext-install gd


COPY ./conf/base.conf /etc/apache2/sites-available/base.conf
RUN a2ensite base.conf

COPY ./php.ini /usr/local/etc/php/