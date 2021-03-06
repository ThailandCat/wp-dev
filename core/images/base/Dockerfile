FROM ubuntu:16.04
MAINTAINER Ankit Pokhrel <info@ankitpokhrel.com>

ENV LANG C.UTF-8
ENV DEBIAN_FRONTEND noninteractive

RUN ln -sf /usr/share/zoneinfo/Asia/Kathmandu /etc/localtime

RUN rm -rf /var/lib/apt/lists/* && apt-get clean
RUN apt-get update --fix-missing && apt-get -y upgrade

# Install php, nginx and other dependencies
RUN apt-get -y install rsyslog \
                       rsyslog-gnutls \
                       supervisor \
                       nginx \
                       curl \
                       php7.0-fpm \
                       php7.0-cli \
                       php7.0-gd \
                       php7.0-imap \
                       php7.0-intl \
                       php7.0-json \
                       php7.0-mcrypt \
                       php7.0-mbstring \
                       php7.0-ldap \
                       php7.0-zip \
                       php7.0-xml \
                       php7.0-mysql \
                       php7.0-soap \
                       php7.0-curl && \
                       apt-get clean && \
                       rm -rf /var/lib/apt/lists/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && chmod +x /usr/local/bin/composer

# install wp-cli
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && chmod +x wp-cli.phar && mv wp-cli.phar /usr/local/bin/wp
RUN wp --info --allow-root

# Add configs
ADD ./configs/www.conf /etc/php/7.0/fpm/pool.d/www.conf
ADD ./configs/php.ini /etc/php/7.0/fpm/99-custom.ini
ADD ./configs/supervisord.conf /etc/supervisord.conf

WORKDIR /var/www

RUN mkdir /var/run/php/

EXPOSE 80
