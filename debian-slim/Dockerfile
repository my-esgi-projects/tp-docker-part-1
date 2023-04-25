FROM debian:stable-slim
LABEL maintainer=delibes.bechir.bkwedou@gmail.com
ARG PHP_VERSION=8.1
ENV DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC

RUN apt update && apt upgrade -y; \
	apt install curl wget gnupg2 ca-certificates lsb-release apt-transport-https -y; \
	add-apt-repository ppa:ondrej/php; \
	apt update -y; \
    apt install -y apache2 libapache2-mod-php unzip wget; \
	wget https://packages.sury.org/php/apt.gpg; \
	apt-key add apt.gpg; rm apt.gpg; \
	echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php7.list; \
	apt update -y; \
	php${PHP_VERSION}-gd php${PHP_VERSION}-mysql php${PHP_VERSION}-curl php${PHP_VERSION}-mbstring php${PHP_VERSION}-intl php${PHP_VERSION}-gmp \
    php-${PHP_VERSION}bcmath php${PHP_VERSION}-xml php${PHP_VERSION}-imagick php${PHP_VERSION}-zip; \
	a2enmod headers; a2dissite 000-default.conf; apt-get clean; rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/

RUN wget https://download.nextcloud.com/server/releases/latest.zip && \
	unzip latest.zip && rm latest.zip && chown www-data:www-data -R nextcloud

ADD ./conf/nextcloud.conf /etc/apache2/sites-available/nextcloud.conf

RUN  a2enmod rewrite && a2ensite nextcloud.conf

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]

# apachectl, -D, FOREGROUND