ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

LABEL maintainer="guillaume.chauveau@appus.fr"

ARG APCU_VERSION
ARG COMPOSER_VERSION

RUN apk add --no-cache acl file gettext git mysql-client
RUN set -eux; \
	apk add --no-cache --virtual .build-deps $PHPIZE_DEPS icu-dev libzip-dev mysql-dev zlib-dev; \
	apk add --no-cache bash openssh sed grep vim gcc g++ autoconf make pkgconfig build-base libc-dev wget; \
	apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev libxml2-dev ffmpeg; \
	docker-php-ext-configure zip --with-libzip; \
	docker-php-ext-install -j$(nproc) intl pdo_mysql zip soap; \
	pecl install apcu-${APCU_VERSION}; \
	pecl clear-cache; \
	docker-php-ext-enable apcu opcache; \
	runDeps="$( \
		scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
			| tr ',' '\n' \
			| sort -u \
			| awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
	)"; \
	apk add --no-cache --virtual .api-phpexts-rundeps $runDeps; \
	apk del .build-deps

RUN docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} gd && \
  apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer --version=$COMPOSER_VERSION \
    && chmod +x /usr/local/bin/composer

COPY config /usr/local/etc/php/conf.d/

CMD ["php-fpm"]

EXPOSE 9000