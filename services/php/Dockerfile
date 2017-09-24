FROM php:7.1.9-fpm


RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
    echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql zip opcache

COPY ./redis-3.1.3.tgz /tmp
RUN mkdir -p /tmp/redis \
	&& tar -xf /tmp/redis-3.1.3.tgz -C /tmp/redis --strip-components=1 \
    && rm /tmp/redis-3.1.3.tgz \
    && docker-php-ext-configure /tmp/redis \
    && docker-php-ext-install /tmp/redis \
    && rm -r /tmp/redis

COPY ./swoole-1.9.20.tgz /tmp
RUN mkdir -p /tmp/swoole \
	&& tar -xf /tmp/swoole-1.9.20.tgz -C /tmp/swoole --strip-components=1 \
    && rm /tmp/swoole-1.9.20.tgz \
    && docker-php-ext-configure /tmp/swoole \
    && docker-php-ext-install /tmp/swoole \
    && rm -r /tmp/swoole

COPY ./conf/php.ini /usr/local/etc/php/
