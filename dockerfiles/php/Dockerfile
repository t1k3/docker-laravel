FROM php:7.2-fpm-alpine

RUN apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS freetype-dev libpng-dev libjpeg-turbo-dev freetype libpng libjpeg-turbo \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install bcmath gd mbstring mysqli pdo pdo_mysql opcache tokenizer zip exif \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

#RUN chown www-data:www-data -R /var/www/html

#RUN crontab -l | { cat; echo "* * * * * /usr/bin/php /var/www/html/artisan schedule:run >> /dev/null 2>&1"; } | crontab -
ADD cron.sh /cron.sh
RUN chmod +x /cron.sh
CMD ["/cron.sh"]