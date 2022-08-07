# LIMESURVEY - DOCKER

## Índice :page_facing_up:
* [Qué es Limesurvey?]()
* [Montaje de aplicación Limesurvey en contenedores  Docker](#montaje-de-aplicación-limesurvey-en-contenedores--docker)
* [Requisitos](#requisitos)
* [Requisitos mínimos para instalar Limesurvey](#requisitos-mínimos-para-instalar-limesurvey)
* [Procedimiento](#procedimiento)
* [Autores](#autores)

## Qué es Limesurvey?

LimeSurvey (anteriormente PHPSurveyor) es una aplicación de software libre para la realización de encuestas en línea, escrita en PHP y que utiliza bases de datos MySQL, PostgreSQL o MSSQL. Brinda la posibilidad a usuarios sin conocimientos de programación el desarrollo, publicación y recolección de respuestas de sus encuestas.

Fuente [wikipedia](https://es.wikipedia.org/wiki/LimeSurvey)

# Montaje de aplicación Limesurvey en contenedores  Docker
Este readme incluye el manual técnico de dockerización de Limersurvey

### Requisitos 📋
- Maquina VIrtual con Ubuntu Linux
- Docker
- Git

### Requisitos mínimos para instalar Limesurvey 📋
- Mínimo 250 MB de espacio en disco.
- MySQL 5.5.3 o posterior O Microsoft SQL Server 2005 o posterior O Postgres 9 o posterior.
- Mínimo PHP 5.5.9 o posterior; sin embargo, recomiendan PHP 7.0.0+ con los siguientes módulos/bibliotecas habilitados:
  - Biblioteca mbstring (Multibyte String Functions).
  - Controlador de base de datos PDO para MySQL (pdo_mysql o pdo_mysqli) o Postgres (pdo_pgsql) o MSSQL (pdo_sqlsrv para Windows y pdo_dblib para Linux).
  - Además, todas las bibliotecas predeterminadas de PHP deberán estár habilitadas.
     * hash
     * session
     * openssl o mcrypt
     * fileinfo
     * etc ...

- Extensiones PHP opcionales:

  - GD-Library con soporte FreeType instalado es necesario para captchas, buenos gráficos en estadísticas o para cargar imágenes a través del editor HTML - vea la documentación sobre PHP GD-Library Extension
  - IMAP (bastante común) es necesario para [[Email bounce tracking system | sistema de seguimiento de rebote de correo electrónico] ] - vea la documentación sobre PHP IMAP Extension
  - LDAP instalado es necesario para importar participantes de la encuesta usando LDAP - vea documentación sobre PHP LDAP
  - Zip (bastante común) es necesario para cargar plantillas, importar recursos archivados .zip y exportar a Excel. vea la documentación sobre PHP Zip Extension
  - Zlib (bastante común) es necesario para ComfortUpdate - vea la documentación sobre PHP Zlib Extension

Fuente de [Limesurvey](https://manual.limesurvey.org/Installation_-_LimeSurvey_CE/es) 

## Procedimiento ⚙️

### 1. Descargar proyecto ambiente local
```
git clone https://github.com/christiancgil/limesurvey-docker.git
```

### 2.Crear imagen de contenedor web PHP
```
cd limesurvey-docker
cd application
sudo docker build -t php-lime:1.0 .
```

### 3. Crear imagen de contenedor bd Mysql
```
cd ..
cd database
sudo docker build -t mysql-lime:1.0 .
```

### 4. Verificar creación de las imágenes

```
sudo docker images
```

### 5. Crear volúmenes aplicación
```
sudo docker volume create lm-sv-web-data
sudo docker volume create lm-sv-web-conf
```

### 6. Crear vólumen de base de datos
```
sudo docker volume create lm-sv-db-data
```

### 7. Verificar la creación de los volumenes
```
sudo docker volume ls
```

### 8. Crear Contenedor PHP
```
sudo docker run -d \
 --name lm-sv-app-container \
 -p 8080:80 \
 --mount src=lm-sv-web-data,dst=/var/www/html \
 --mount src=lm-sv-web-conf,dst=/usr/local/etc/php/ \
 php-lime:1.0
 ```

### 9. Crear Contenedor Mysql
```
sudo docker run -d \
 --name lm-sv-db-container \
 -p 3306:3306 \
 --mount src=lm-sv-db-data,dst=/var/lib/mysql \
 mysql-lime:1.0
 ```

### 10. Verificar la creación de los contenedores
```
sudo docker ps
```

### 11. Crear red para comunicación entre contenedores
```
sudo docker network create --attachable lime-network
```

### 12. Conectar contenedores a nueva red
```
sudo docker network connect lime-network lm-sv-db-container
sudo docker network connect lime-network lm-sv-app-container
```

### 13. Verificar conectividad aplicación con base de datos
```
docker exec -it lm-sv-app-container bash
mysql -h lm-sv-db-container -P 3306 -u root -p demo
```

### 14. Configuración Lime Survey
#### Acceder consola configuración
```
http://ip-virtual-host:8080/limesurvey
```

#### Instalar limesurvey

Abrir el navegador web y digitar la url para el ingreso a Limesurvey, en este caso la url es http://192.168.0.15:8080/limesurvey/

##### 1. Al ingresar a la url, abrirá la siguiente imagen, en la cual inicia la aplicación y nos permite seleccionar el idioma de la instalación.
![Iniciar](/img/languaje-selecction.JPG)

##### 2. Al iniciar la instalación, visualiza los términos y condiciones de la licencia, si esta de acuerdo, de clic en “I accept”.
![Términos y condiciones](/img/licencia.JPG)

##### 3. Luego el instalador verificará los requisitos mínimos del servidor. Si alguno está incorrectos visualizará un error y deberá solucionarlo.
![Preinstalación](/img/preinstalacion.JPG)

##### 4. Luego podrá configurar la base de datos con las credenciales que se crearon anteriormente.
![Configuración bd](/img/Configuracionbd.JPG)

##### 5. Si existe una base de datos existente, la aplicación le preguntará si desea poblarla.
![Ajustes bd](/img/ajustebd.JPG)

##### 6. Luego, deberá crear el usuario administrador con su respectivo usuario y contraseña. Esta información es muy importante para acceder a la aplicación.
![Configuración usuario admin](/img/configadmin.JPG)

##### 7. Al finalizar visualizará esta pantalla, indicando que la instalación fue exitosa.
![Instalación exitosa](/img/fininstalacion.JPG)

##### 8. Al dar clic en Administración, visualizará la pantalla de inicio de sesión, en la cual podrá ingresar las credenciales (usuario y contraseña) del administrador.

http://192.168.0.15:8080/limesurvey/index.php/admin/authentication/sa/login

![Login](/img/login.JPG)

##### 9. Al iniciar sesión, visualizará las diferentes funcionalidades que ofrece la aplicación y podrá acceder a ellas.
![Bienvenida](/img/bienvenida.JPG)

## Autores ✒️

* **Christian Camilo Gil López** 
* **Mónica Alejandra Cifuentes Bernal**
