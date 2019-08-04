FROM php:7.3-fpm
RUN apt-get update && apt-get install -y apt-utils libmcrypt-dev libpng-dev libjpeg-dev libfreetype6-dev libicu-dev \
&& addgroup --gid 497 nginx \
&& useradd --uid 498 --gid 497 nginx \
&& pecl install redis-3.1.1 \
&& pecl install mcrypt-1.0.2 \
&& docker-php-ext-enable mcrypt \
&& docker-php-ext-enable redis \
&& docker-php-ext-install -j$(nproc) iconv intl mbstring pdo pdo_mysql \
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd \
&& rm -rf /var/www/html
RUN apt-get install -y git \
&& git clone https://github.com/tony2001/pinba_extension /tmp/pinba_extension \
    && cd /tmp/pinba_extension \
    && phpize \
    && ./configure --enable-pinba \
    && make install
