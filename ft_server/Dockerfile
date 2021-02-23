FROM debian:buster

RUN apt-get -y upgrade && apt-get -y update 

RUN apt-get install -y nginx wordpress php7.3 php7.3-fpm php7.3-mysql php-json php-mbstring vim \
	default-mysql-server

ADD https://files.phpmyadmin.net/phpMyAdmin/5.0.4/phpMyAdmin-5.0.4-all-languages.tar.gz phpmyadmin.tar.gz

RUN tar xvzf phpmyadmin.tar.gz && mv phpMyAdmin-5.0.4-all-languages /var/www/html/phpmyadmin

RUN apt-get -y install mariadb-server

COPY ./srcs/phpmyadmin.php phpmyadmin

RUN mv usr/share/wordpress var/www/html

#setup wp config
COPY ./srcs/wp-config.php /var/www/html/wordpress


#setup certigicate config
COPY	srcs/ch.key /var
COPY	srcs/ch.pem /var

#setup nginx config
COPY	srcs/nginx.conf etc/nginx/sites-available

COPY	srcs/init.sh /var

#Run Authorize
#RUN chown -R www-data:www-data *
#RUN chmod -R 755 /var/www/*

CMD bash /var/init.sh