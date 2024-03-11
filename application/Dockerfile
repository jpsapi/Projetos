FROM php:apache

# Atualização e instalação de pacotes
RUN apt-get update && \
	apt-get install -y vim wget unzip default-mysql-client

# Instalação cliente Mysql
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Mudança de diretório de trabalho e permissão
WORKDIR /tmp
RUN chmod 775 -R /tmp/

# Download LimeSurvey e mudança dos arquivos para webserver
RUN wget -c https://download.limesurvey.org/latest-master/limesurvey6.4.12+240311.zip && \
	ls -la && \
	unzip limesurvey6.4.12+240311.zip && \
	mv limesurvey /var/www/html/

# Mudança do diretório de trabalho e permissão
WORKDIR /var/www/html/limesurvey/
RUN chown www-data:www-data -R /var/www/html/limesurvey/
RUN chmod 775 -R /var/www/html/limesurvey/

# Criação de diretório e atribuição de permissão
RUN mkdir /usr/local/etc/php/writable && \
	chmod 777 -R /usr/local/etc/php/writable/

# Atualização Arquivo config php 
RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini && \
	echo "session.save_path = \"/usr/local/etc/php/writable"\" >> /usr/local/etc/php/php.ini

# Copiar Arquivo de config para diretorio de trabalho webserver
COPY limesurvey.conf /etc/apache2/sites-available/

EXPOSE 80