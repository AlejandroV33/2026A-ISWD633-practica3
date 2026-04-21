## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
docker network create net-wp

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
No contiene nada.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
docker run -d \
  --name srv-mysql \
  --network net-wp \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_DATABASE=wp_db \
  -e MYSQL_USER=wp_user \
  -e MYSQL_PASSWORD=wp_pass \
  -v $(pwd)/db:/var/lib/mysql \
  mysql:8
  
### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Despúes de iniciarlo contiene los archivos del sistema de MySQL (archivos de configuración, logs y las carpetas de las bases de datos).

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
docker run -d \           
  --name srv-wordpress \
  --network net-wp \
  -p 9500:80 \
  -e WORDPRESS_DB_HOST=srv-mysql \
  -e WORDPRESS_DB_USER=wp_user \
  -e WORDPRESS_DB_PASSWORD=wp_pass \
  -e WORDPRESS_DB_NAME=wp_db \
  -v $(pwd)/www:/var/www/html \
  wordpress
  
### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
La entrada que inlcuí se sigue mostrando igual que antes de eliminarlo, nada ha cambiado ya que los datos se guardaron con bind mount.
