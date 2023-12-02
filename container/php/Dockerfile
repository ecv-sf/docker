ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine
MAINTAINER Guillaume Chauveau <docker@appus.fr>

ARG APCU_VERSION
ARG COMPOSER_VERSION

RUN apk add --no-cache acl file gettext git mysql-client postgresql-client sqlite;
RUN set -eux; \
	apk add --no-cache --virtual .build-deps $PHPIZE_DEPS icu-dev libzip-dev mysql-dev postgresql-dev libpq-dev zlib-dev; \
	apk add --no-cache bash openssh sed grep vim gcc g++ autoconf make pkgconfig build-base libc-dev wget; \
	apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev libxml2-dev ffmpeg;
RUN docker-php-ext-configure zip; \
	docker-php-ext-install -j$(nproc) intl pdo pdo_mysql pdo_pgsql zip soap; \
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

RUN docker-php-ext-configure gd && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} gd && \
  apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer --version=$COMPOSER_VERSION \
    && chmod +x /usr/local/bin/composer

COPY config /usr/local/etc/php/conf.d/

CMD ["php-fpm"]

EXPOSE 8000 9000