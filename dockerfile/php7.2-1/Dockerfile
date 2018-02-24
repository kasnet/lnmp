FROM php:7.2-rc-fpm-alpine3.6

ENV TIMEZONE Asia/Shanghai
ENV PHP_MEMORY_LIMIT 512M
ENV MAX_UPLOAD 50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST 100M
## swoole版本，如需安装swoole则取消注释
#ENV PHP_EXT_SWOOLE=swoole-2.0.6
ENV PHP_REDIS=3.1.4
#基础依赖
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
  apk update && \
  apk add tzdata curl && \
  cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
  echo "${TIMEZONE}" > /etc/timezone && \
  apk --update --repository=http://dl-4.alpinelinux.org/alpine/edge/testing add \
    php7-common php7-intl php7-gd php7-mcrypt php7-openssl \
    php7-gmp php7-json php7-dom php7-pdo php7-zip \
    php7-zlib php7-mysqli php7-bcmath php7-pdo_mysql php7-pgsql \
    php7-pdo_pgsql php7-gettext php7-xmlreaderhp7-xmlrpc \
    php7-bz2 php7-iconv php7-curl php7-ctype php7-fpm \
    php7-mbstring php7-session php7-phar curl curl-dev postgresql-dev \
    ## 如果使用swoole  需要取消下行注释
   # hiredis-dev libmcrypt-dev gmp-dev icu-dev linux-headers musl --virtual .phpize-deps $PHPIZE_DEPS \
    tzdata && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update && \
    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php7/php-fpm.conf && \
    sed -i -e "s/listen\s*=\s*127.0.0.1:9000/listen = 9000/g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;date.timezone =.*|date.timezone = ${TIMEZONE}|" /etc/php7/php.ini && \
    sed -i "s|memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|" /etc/php7/php.ini && \
    sed -i "s|upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|" /etc/php7/php.ini && \
    sed -i "s|max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|" /etc/php7/php.ini && \
    sed -i "s|post_max_size =.*|max_file_uploads = ${PHP_MAX_POST}|" /etc/php7/php.ini && \
    sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php7/php.ini && \
    sed -i "s/;extension=php_pgsql.dll/extension=php_pgsql.dll/" /etc/php7/php.ini && \
    sed -i "s/;extension=php_pdo_pgsql.dll/extension=php_pdo_pgsql.dll/" /etc/php7/php.ini && \
    mkdir -p /usr/src/php/ext/redis && \
    curl -L https://github.com/phpredis/phpredis/archive/$PHP_REDIS.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 && \
    echo 'redis' >> /usr/src/php-available-exts && \
    docker-php-ext-install redis pgsql pdo pdo_mysql pdo_pgsql && \
      rm -rf /var/cache/apk/*
# 如需安装swoole，取消以下注释     
#RUN \
#    cd /tmp \
#    && pecl download $PHP_EXT_SWOOLE \
#    && mkdir -p /tmp/$PHP_EXT_SWOOLE \
#    && tar -xf ${PHP_EXT_SWOOLE}.tgz -C /tmp/$PHP_EXT_SWOOLE --strip-components=1 \
#    && docker-php-ext-configure /tmp/$PHP_EXT_SWOOLE --enable-async-redis --enable-openssl --enable-sockets=/usr/local/include/php/ext/sockets \
#    && docker-php-ext-install /tmp/$PHP_EXT_SWOOLE \
#    && rm -rf /tmp/${PHP_EXT_SWOOLE}*

WORKDIR /www

# 放入自己需要的代码
#COPY  . /www
# 安装composer依赖
#RUN composer install

# php-fpm使用以下配置
EXPOSE 9000
CMD ["php-fpm"]
# swoole 使用以下配置
EXPOSE 9501
# 启动swoole server
CMD ["php","src/server","start"]
