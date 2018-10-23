FROM mediakraken/thebuggenie-lamp

RUN apt-get update && apt-get -y install curl \
  && git clone -b 4.2.1 https://github.com/thebuggenie/thebuggenie /var/www/thebuggenie

WORKDIR /var/www/thebuggenie

ADD 000-default.conf /etc/apache2/sites-available/000-default.conf

RUN curl -sS https://getcomposer.org/installer | php \
  && apk add --update \
  php7-gd \
  php7-curl \
  php7-ldap \
  && rm -rf /var/cache/apk/* \
  && php composer.phar install \
  && chown -R www-data:www-data /var/www/thebuggenie \
  && chmod a+w /create_mysql_admin_user.sh

EXPOSE 80 

CMD ["/run.sh"]
