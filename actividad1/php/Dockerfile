FROM php:8.4-cli-alpine

RUN apk add --no-cache postgresql-libs \
    && apk add --no-cache --virtual .build postgresql-dev \
    && docker-php-ext-install pdo_pgsql \
    && apk del .build

WORKDIR /app
COPY --chown=www-data:www-data app/ /app/

USER www-data
EXPOSE 8080
CMD ["php", "-S", "0.0.0.0:8080", "/app/index.php"]