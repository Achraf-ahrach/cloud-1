FROM debian:bullseye

RUN apt update && apt upgrade -y && apt install -y nginx openssl \
    && mkdir -p /etc/ssl/certs /etc/ssl/private \
    && openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
       -keyout /etc/ssl/private/localhost.key \
       -out /etc/ssl/certs/localhost.crt \
       -subj "/CN=zackahr.duckdns.org" \
    && chmod 600 /etc/ssl/private/localhost.key

COPY conf/default /etc/nginx/sites-enabled/

EXPOSE 443

CMD ["nginx", "-g", "daemon off;"]