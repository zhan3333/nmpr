FROM php:7.4.9-fpm
ARG USER_NAME
ARG USER_PASSWORD

# 拷贝需要用到的资源
COPY resource /var/resource

#更新apt-get源 使用aliyun的源
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
  cp /var/resource/sources.list /etc/apt/sources.list  && \
  rm -f /etc/apt/sources.list.d/*.list

RUN useradd -m -s /bin/bash -p $(openssl passwd -1 $USER_PASSWORD) -G sudo $USER_NAME

# APT 自动安装 PHP 相关的依赖包,如需其他依赖包在此添加
RUN apt-get update \
  && apt-get install -y \
  libcurl4-openssl-dev pkg-config libssl-dev \
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
  openssl \
  busybox \
  sudo \
  htop
# 官方 PHP 镜像内置命令，安装 PHP 依赖
RUN docker-php-ext-install \
  # mcrypt \
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
  # && apt-get clean \
  # && apt-get autoclean \
  && rm -rf /tmp/* /var/tmp/* 

RUN pecl install /var/resource/redis-4.2.0.tgz\
  && pecl install /var/resource/swoole-4.4.8.tgz \
  && pecl install /var/resource/mcrypt-1.0.3.tgz \
  && pecl install /var/resource/mongodb-1.5.5.tgz \
  # && pecl install /var/resource/xdebug-2.7.2.tgz  \
  && docker-php-ext-enable redis swoole mcrypt mongodb

# Install PHP Composer
RUN mv /var/resource/composer.phar /usr/local/bin/composer \
  && chmod 755 /usr/local/bin/composer \
  # use china mirror
  && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer 
# && composer global require hirak/prestissimo

RUN cp /var/resource/tailf /usr/local/bin/tailf && chmod 755 /usr/local/bin/tailf \
  && cp /var/resource/phpunit-7.0.phar /usr/local/bin/phpunit && chmod 755 /usr/local/bin/phpunit
