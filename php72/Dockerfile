FROM php:7.2-rc-apache
RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng-dev

RUN docker-php-ext-install -j$(nproc) mcrypt opcache pdo_mysql \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd
RUN echo 'error_reporting = E_ALL' >> /usr/local/etc/php/conf.d/99_myconf.ini
RUN echo 'date.timezone = Asia/Tokyo' >> /usr/local/etc/php/conf.d/99_myconf.ini

RUN pecl install redis-3.1.0 \
	&& pecl install xdebug-2.5.0 \
	&& docker-php-ext-enable redis xdebug \
	&& docker-php-source delete

CMD ["apache2-foreground"]
RUN ["apt-get", "update"]
RUN ["apt-get", "install", "-y", "vim"]

