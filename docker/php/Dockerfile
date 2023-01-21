FROM php:8.1.0-fpm
ARG TIMEZONE

#ejecuta los comandos de linux para la instalacion y actualizacion de archivos de linux de la maquina virtual
RUN apt-get update && apt-get install -y 

#instala node js en el servidor virtual
RUN apt-get update && apt-get install -y nodejs npm

#instala composer en el servidor virtual
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# ejecuta y actualiza el timezone (zona horaria) del servido virtual
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \ 
&& printf '[PHP]\ndate.timezone = "%s"\n', $TIMEZONE > /usr/local/etc/php/conf.d/tzone.ini \
&& "date"

# instala la extencion pdo de maysql
RUN docker-php-ext-install pdo pdo_mysql

# comenta o descomenta las instalaciones para tu proyecto
RUN pecl install apcu
RUN docker-php-ext-install opcache
RUN docker-php-ext-enable apcu
#RUN docker-php-ext-install soap

RUN apt-get update && apt-get install -y

#ruta del directorio principal de tu aplicación
WORKDIR /usr/src/app