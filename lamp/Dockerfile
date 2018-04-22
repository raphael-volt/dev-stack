FROM rvolt/dev-stack:lamp

LABEL maintainer "Raphaël Volt <raphael@ketmie.com>"
# install sqlite3
RUN apt-get update && apt-get install libsqlite3-dev
# install pdo and mysql ext
RUN docker-php-ext-install pdo pdo_mysql