FROM ubuntu:22.04
LABEL maintainer=delibes.bechir.bkwedou@gmail.com

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update

RUN apt install -y php8.1 php8.1-curl
RUN apt install -y php8.1-xml
RUN apt install -y php8.1-fileinfo
RUN apt install -y php8.1-mbstring
RUN apt install -y php8.1-zip
RUN apt install -y php8.1-bcmath
RUN apt install -y php8.1-mysql
RUN apt install -y php8.1-intl
RUN apt install -y php8.1-fpm
RUN apt install -y apache2
RUN a2enmod rewrite
RUN a2dissite 000-default.conf
ADD ./conf/nextcloud.conf /etc/apache2/sites-available/nextcloud.conf
RUN a2ensite nextcloud.conf
RUN a2enmod headers
RUN a2enmod env
RUN a2enmod dir
RUN a2enmod mime
WORKDIR /var/www/
RUN apt install -y wget
RUN wget https://download.nextcloud.com/server/releases/latest.zip
RUN apt install -y unzip
RUN unzip latest.zip
RUN chown www-data:www-data -R nextcloud/
RUN apt install -y php8.1-gd

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]

# apachectl, -D, FOREGROUND