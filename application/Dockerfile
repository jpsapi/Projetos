FROM php:apache

# Instalación librerias requeridas instalación
RUN apt-get update && \
	apt-get install -y vim wget unzip default-mysql-client

# Instalación cliente mysql
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Asignar permisos carpeta de descarga medios instalación
WORKDIR /tmp
RUN chmod 775 -R /tmp/

# Descarga medios de instalación en carpeta de trabajo PHP
RUN wget -c https://download.limesurvey.org/latest-stable-release/limesurvey5.3.29+220801.zip && \
	ls -la && \
	unzip limesurvey5.3.29+220801.zip && \
	mv limesurvey /var/www/html/

# Asignar permisos carpeta limesurvey
WORKDIR /var/www/html/limesurvey/
RUN chown www-data:www-data -R /var/www/html/limesurvey/
RUN chmod 775 -R /var/www/html/limesurvey/

# Creación de carpeta y asignación de permisos gestión php sessions
RUN mkdir /usr/local/etc/php/writable && \
	chmod 777 -R /usr/local/etc/php/writable/

# Actualización archivo config php con carpeta de trabajo php sessions
RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini && \
	echo "session.save_path = \"/usr/local/etc/php/writable"\" >> /usr/local/etc/php/php.ini

# Copiar archivo configuración pre-editado
COPY limesurvey.conf /etc/apache2/sites-available/

EXPOSE 80