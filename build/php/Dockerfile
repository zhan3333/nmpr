FROM php:7.3.3-fpm-stretch
ARG UNAME=zhan
ARG UPWD=zhan

# 拷贝需要用到的资源
COPY resource /home/resource

#更新apt-get源 使用aliyun的源
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
  cp /home/resource/sources.list /etc/apt/sources.list  && \
  rm /etc/apt/sources.list.d/*.list && \
  cat /etc/apt/sources.list

RUN useradd -m -s /bin/bash -p $(openssl passwd -1 ${UPWD}) -G sudo ${UNAME}

# APT 自动安装 PHP 相关的依赖包,如需其他依赖包在此添加
RUN apt-get update \
  && apt-get install -y \
  libmcrypt-dev \
  libz-dev \
  libzip-dev\
  git \
  wget \
  libpcre3-dev \
  libjpeg62-turbo-dev\
  libfreetype6-dev \
  libpng-dev\
  vim \
  libmhash-dev \
  libfontconfig1 libxrender1 \
  pkg-config \
  busybox \
  sudo \
  # 官方 PHP 镜像内置命令，安装 PHP 依赖
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install \
  # mcrypt \
  mbstring \
  pdo_mysql \
  zip \
  fileinfo \
  json \
  exif \
  iconv \
  gd \
  bcmath \
  opcache \
  sockets \
  # Clean apt install cache
  && apt-get clean \
  && apt-get autoclean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 

RUN pecl install /home/resource/redis-4.2.0.tgz\
  && pecl install /home/resource/swoole-4.2.12.tgz \
  && pecl install /home/resource/mcrypt-1.0.2.tgz \
  && pecl install /home/resource/mongodb-1.5.5.tgz \
  # && pecl install xdebug-2.7.2 \
  && docker-php-ext-enable redis swoole mcrypt mongodb

# Install PHP Composer
RUN mv /home/resource/composer.phar /usr/local/bin/composer \
  && chmod 755 /usr/local/bin/composer \
  # use china mirror
  && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer \
  && composer global require hirak/prestissimo

RUN cp /home/resource/tailf /usr/local/bin/tailf \
  && chmod 755 /usr/local/bin/tailf \
  && cp /home/resource/phpunit-7.0.phar /usr/local/bin/phpunit \
  # install
  && chmod 755 /usr/local/bin/phpunit