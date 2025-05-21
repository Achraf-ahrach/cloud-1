FROM debian:bullseye

COPY tools/db.sh .

RUN apt update && apt install -y --fix-missing mariadb-server \
    && sed -i 's/^bind-address\s*=.*/bind-address = 0.0.0.0/' /etc/mysql/mariadb.conf.d/50-server.cnf \
    && chmod +x db.sh

EXPOSE 3306

CMD ["/db.sh"]

