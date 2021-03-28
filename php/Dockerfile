FROM php:7.3-fpm
RUN apt-get update && apt-get install -y apt-utils libmcrypt-dev libpng-dev libjpeg-dev libfreetype6-dev libicu-dev libzip-dev zip \
&& addgroup --gid 497 nginx \
&& useradd --uid 498 --gid 497 nginx \
&& pecl install redis-3.1.1 \
&& pecl install mcrypt-1.0.2 \
&& docker-php-ext-install zip \
&& docker-php-ext-enable mcrypt \
&& docker-php-ext-enable redis \
&& docker-php-ext-install -j$(nproc) ctype iconv intl mbstring pdo pdo_mysql \
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd \
&& rm -rf /var/www/html
RUN apt-get install -y git \
&& git clone https://github.com/tony2001/pinba_extension /tmp/pinba_extension \
    && cd /tmp/pinba_extension \
    && phpize \
    && ./configure --enable-pinba \
    && make install

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
# TODO add hash check: php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
&& php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
&& php -r "unlink('composer-setup.php');"

RUN docker-php-ext-install pcntl
RUN apt-get install -y wget && wget https://get.symfony.com/cli/installer -O - | bash \
&& mv /root/.symfony/bin/symfony /usr/local/bin/symfony

#RUN pecl install swoole-4.4.8
#RUN docker-php-ext-enable swoole
#RUN pecl install swoole_serialize-0.1.1 && docker-php-ext-enable swoole_serialize

#RUN curl -O -L https://github.com/redis/hiredis/archive/v0.13.3.tar.gz \
#&& tar zxvf v0.13.3.tar.gz \
#&& cd hiredis-0.13.3/ \
#&& make -j \
#&& make install \
#&& ldconfig
#
#RUN cd /tmp && git clone https://github.com/swoole/swoole-src.git && \
#cd swoole-src && \
#git checkout v4.4.8 && \
#phpize  && \
#./configure  --enable-openssl --enable-async-redis && \
#make && make install
#
#RUN touch /usr/local/etc/php/conf.d/swoole.ini && \
#    echo 'extension=swoole.so' > /usr/local/etc/php/conf.d/swoole.ini

#RUN ./configure --enable-async-redis \
#&& make clean \
#&& make -j \
#&& make install