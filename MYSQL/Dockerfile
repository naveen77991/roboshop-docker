FROM mysql:8.0

ENV MYSQL_ROOT_PASSWORD=RoboShop@1
ENV MYSQL_DATABASE=shipping

COPY db/*.sql /docker-entrypoint-initdb.d/
