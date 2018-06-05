FROM php:7.2-fpm-alpine

RUN apk add --update --no-cache --virtual .phpize-deps $PHPIZE_DEPS freetype-dev libpng-dev libjpeg-turbo-dev freetype libpng libjpeg-turbo \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install bcmath gd mbstring mysqli pdo pdo_mysql opcache tokenizer zip exif \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

# backup: mysqldump
#RUN apk add mysql-client

# schedule
ADD crontab /etc/cron.d/laravel
RUN apk add dcron \
    && mkdir -p /var/log/cron \
    && touch /var/log/cron/cron.log \
    && chmod -R 0644 /etc/cron.d/laravel \
    && /usr/bin/crontab /etc/cron.d/laravel \
    && crond service restart

# permission
#RUN apk add acl \
#    && mkdir -p /var/www/html/storage/app \
#    && setfacl -d -m u::rxw,g::rx,o::rx /var/www/html/storage/app
RUN chown -R www-data:www-data /var/www/html
