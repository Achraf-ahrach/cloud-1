FROM debian:bullseye

COPY ./tools/ .

RUN apt update && apt upgrade -y && apt install -y curl php-fpm php-mysql \
    && curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp \
    && sed -i 's/^listen = \/run\/php\/php7.4-fpm\.sock/listen = 0.0.0.0:9000/' /etc/php/7.4/fpm/pool.d/www.conf \
    && chmod +x script.sh

WORKDIR /var/www/html/

EXPOSE 9000

CMD ["/script.sh"]
