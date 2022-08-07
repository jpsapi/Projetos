FROM mysql:5.7.30

#Configurar variables de entorno 
ENV MYSQL_ROOT_PASSWORD admin123

ENV MYSQL_DATABASE demo
ENV MYSQL_USER user123
ENV MYSQL_PASSWORD pass123

#Copiar scripts configuración
COPY *.sql /docker-entrypoint-initdb.d/

EXPOSE 3306