# LIMESURVEY - DOCKER

## Qués es Limesurvey?

LimeSurvey (anteriormente PHPSurveyor) es una aplicación de software libre para la realización de encuestas en línea, escrita en PHP y que utiliza bases de datos MySQL, PostgreSQL o MSSQL. Brinda la posibilidad a usuarios sin conocimientos de programación el desarrollo, publicación y recolección de respuestas de sus encuestas.

Fuente [wikipedia](https://es.wikipedia.org/wiki/LimeSurvey)

## Montaje de aplicación Limesurvey en contenedores  Docker
Este readme incluye el manual técnico de dockerización de Limersurvey

###Requisitos
- Maquina VIrtual con Ubuntu Linux
- Docker
- Git

### Requisitos mínimos para instalar Limesurvey
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

### 1. Crear la imagen de PHP
### 2. Crear la base de datos 
### 3. Crear un volumen para la base de datos
### 4. Instalar limesurvey

Abrir el navegador web y digitar la url para el ingreso a Limesurvey, en este caso la url es (http://192.168.0.15:8080/limesurvey/) y siga las instrucciones del documento [InstalaciónLimeSurvey CE](https://docs.google.com/document/d/1EhA7h9bwLTnoxUIgOhAA4vpKnB3VWBkMoFnqF0Pb8xU/edit?usp=sharing)
