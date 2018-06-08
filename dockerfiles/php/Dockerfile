FROM php:7.2-fpm-alpine

ADD php.ini /usr/local/etc/php/conf.d/php.ini

RUN apk update

RUN apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS freetype-dev libpng-dev libjpeg-turbo-dev freetype libpng libjpeg-turbo \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install bcmath gd mbstring mysqli pdo pdo_mysql opcache tokenizer zip exif \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

# timezone
RUN apk add tzdata \
    && cp /usr/share/zoneinfo/Europe/Budapest /etc/localtime \
    && apk del tzdata

# backup: mysqldump
RUN apk add --no-cache mysql-client

# schedule
ADD crontab /etc/cron.d/laravel
RUN apk add --no-cache dcron \
    && mkdir -p /var/log/cron/ \
    && touch /var/log/cron/cron.log \
    && chmod -R 0644 /etc/cron.d/laravel \
    && /usr/bin/crontab /etc/cron.d/laravel

# permission
RUN chown -R root:www-data /var/www/html \
    && chmod -R 775 /var/www/html

# supervisor
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN mkdir -p /var/log/supervisor/ \
    && apk add --no-cache supervisor
ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisor/conf.d/supervisord.conf"]
