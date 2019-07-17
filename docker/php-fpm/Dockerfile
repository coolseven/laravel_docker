FROM php:7.2.12-fpm-stretch as sourced-fpm-7.2.12

RUN sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list && \
    sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list.d/buster.list && \
    sed -i 's/security.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list.d/buster.list && \
    cat /etc/apt/sources.list && \
    apt-get update -y && \
    apt-get install -y apt-utils && \
    apt-get install -y zip unzip && \
    apt-get install -y libzip-dev libpq-dev && \
    apt-get install -y vim && \
    pecl install redis-4.0.1 && \
    pecl install xdebug-2.6.0 && \
    docker-php-ext-enable redis xdebug && \
    docker-php-ext-install pdo_pgsql && \
    docker-php-ext-install pgsql && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install zip && \
    rm -rf /var/lib/apt/lists/*

FROM sourced-fpm-7.2.12

COPY your-php.ini /usr/local/etc/php/php.ini
COPY your-fpm.conf /usr/local/etc/php-fpm.d/www.conf

RUN cat /etc/apt/sources.list && \
    ls -al /usr/local/etc/php && \
    ls -al /usr/local/etc/php/conf.d && \
    cat /usr/local/etc/php/php.ini && \
    php -m && \
    php --ini

WORKDIR /usr/share/nginx/laravel_docker

CMD ["php-fpm"]

EXPOSE 9000


   

