FROM mysql:8.0.33
LABEL "project"="Vprofile"
LABEL "Author"="Ammar"

ENV MYSQL_ROOT_PASSWORD="vprodpass"
ENV MYSQL_DATABASE="accounts"

# sql data file in docker --> docker-entrypoint-initdb.d
ADD db_backup.sql docker-entrypoint-initdb.d/db_backup.sql  