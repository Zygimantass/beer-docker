FROM mariadb

COPY ./sql/tables.sql /docker-entrypoint-initdb.d/
CMD ["mysqld"]
