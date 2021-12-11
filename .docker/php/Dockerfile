FROM ubuntu:20.04

RUN apt  update && apt -y upgrade
RUN apt install lsb-release ca-certificates apt-transport-https software-properties-common -y
RUN add-apt-repository ppa:ondrej/php -y
RUN apt update

#Installation PHP8.1
RUN apt install php8.1 -y

#Installation of some extensions (You an remove or add as your preferred, but check if exists on the repo before)
RUN apt install -y \
		php8.1-common \
		php8.1-pdo \
		php8.1-bcmath \
		php8.1-xml \
		php8.1-fpm \
		php8.1-mysql \
		php8.1-mysqli \
		php8.1-zip \
		php8.1-curl \
		php8.1-mbstring \
		php8.1-opcache \
		php8.1-soap \
		php8.1-ftp \
		php8.1-fileinfo \
		php8.1-sqlite3 \
		php8.1-phar \
		php8.1-sockets

#Changing the PHP configuration files
RUN mkdir -p /run/php/
RUN rm -f etc/php/8.1/fpm/pool.d/www.conf
COPY php.ini-production /etc/php8/conf.d/
COPY www.conf /etc/php/8.1/fpm/pool.d/www.conf

#Config the workdir
WORKDIR /var/www
RUN rm -rf /var/www/html
RUN ln -s public html

#Composer installation
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN mv composer.phar /usr/local/bin/composer
RUN php -r "unlink('composer-setup.php');"

#Run php-fpm to listen for connections and open the port 9000
EXPOSE 9000
ENTRYPOINT ["php-fpm8.1", "-F"]
