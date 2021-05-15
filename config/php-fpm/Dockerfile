FROM php:${PHP_VERSION}

RUN echo -e "https://mirrors.ustc.edu.cn/alpine/v$(cat /etc/alpine-release | cut -d'.' -f1,2)/main\nhttps://mirrors.ustc.edu.cn/alpine/v$(cat /etc/alpine-release | cut -d'.' -f1,2)/community" > /etc/apk/repositories \
  && apk update \
  && apk --no-cache add \
  curl-dev \
  libxpm-dev \
  gettext-dev \
  libmcrypt-dev \
  libxml2-dev \
  tzdata \
  composer \
  supervisor \
  && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer \
  && composer self-update --2 \
  && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
  && echo "Asia/Shanghai" > /etc/timezone \
  && docker-php-source extract \
  && mkdir -p /usr/src/php/ext/redis \
  && wget -c https://pecl.php.net/get/redis-5.3.3.tgz -O - | tar -xz --strip-components 1  -C /usr/src/php/ext/redis \
  && mkdir -p /usr/src/php/ext/swoole \
  && wget -c https://pecl.php.net/get/swoole-4.6.6.tgz -O - | tar -xz --strip-components 1  -C /usr/src/php/ext/swoole \
  && docker-php-ext-install -j$(nproc) \
  bcmath \
  pdo_mysql \
  pcntl \
  redis \
  sockets \
  opcache \
  swoole \
  && docker-php-source delete