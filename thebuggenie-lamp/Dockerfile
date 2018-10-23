# Download base image
FROM alpine:3.8

LABEL AUTHOR="Quinn D Granfor, spootdev@gmail.com"
LABEL Description="This image holds the lamp image".

ADD create_mysql_admin_user.sh /create_mysql_admin_user.sh
ADD apache_default /etc/apache2/sites-available/000-default.conf

RUN apk add --update \
  apache2 \
  mariadb \
  mariadb-client \
  php7-apache2 \
  pwgen \
  && rm -rf /var/cache/apk/*i \
  && rc-update add apache2 \
  && rc-update add mariadb \
  && echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Remove pre-installed database
RUN rm -rf /var/lib/mysql/*

# Add MySQL utils
RUN chmod 755 /*.sh

# config to enable .htaccess
RUN a2enmod rewrite

#Environment variables to configure php
ENV PHP_UPLOAD_MAX_FILESIZE 10M
ENV PHP_POST_MAX_SIZE 10M

# Add volumes for MySQL 
VOLUME  ["/etc/mysql", "/var/lib/mysql" ]

CMD ["/run.sh"]
