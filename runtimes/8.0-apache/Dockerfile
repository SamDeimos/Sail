FROM php:8.0-apache

ARG WWWGROUP

WORKDIR /var/www/html

ENV DEBIAN_FRONTEND noninteractive
ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
    libzip-dev zip libicu-dev libpq-dev libpng-dev libxml2-dev
RUN docker-php-source extract
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN docker-php-ext-install pdo pdo_pgsql soap

RUN groupadd --force -g $WWWGROUP sail
RUN useradd -ms /bin/bash --no-user-group -g $WWWGROUP -u 1337 sail

# COPY start-container /usr/local/bin/start-container
# COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
# COPY php.ini /etc/php/8.0/cli/conf.d/99-sail.ini
# RUN chmod +x /usr/local/bin/start-container

EXPOSE 8000

# ENTRYPOINT ["start-container"]
