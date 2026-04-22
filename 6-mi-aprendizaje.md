# Mi aprendizaje  
### Bind Mounts
Ya conocía el funcionamiento básico de los sistemas de ficheros en mi computadora y la idea general de "montar" una unidad, aunque no usaba ese término técnico. Con las prácticas aprendí a vincular carpetas específicas de mi host con el contenedor. Me pareció muy útil para el desarrollo, ya que pude ver cómo los cambios en mi carpeta local de Nginx se reflejaban al instante en el navegador sin reiniciar nada.

### Volúmenes Nombrados
Este concepto fue totalmente nuevo. Antes sabía que los datos del contenedor podían guardarse para no perderse, pero no sabía cómo Docker gestionaba su propio espacio de almacenamiento. Ahora entiendo que los volúmenes nombrados son la mejor forma de delegar en Docker la administración de los datos, especialmente para servicios como Postgres o Drupal, manteniéndolos seguros e independientes del ciclo de vida del contenedor.

### Volúmenes Anónimos
No tenía idea de su existencia. Aprendí que Docker los crea automáticamente con identificadores únicos (hashes) y que son ideales para almacenamiento temporal o para mejorar el rendimiento de escritura. Lo más importante que aprendí fue la gestión de limpieza con docker volume prune para no llenar el disco de mi Mac con volúmenes huérfanos.

### Ejercicio 
En la práctica anterior con WordPress tuve problemas porque solo me enfoqué en la base de datos. Con este nuevo ejercicio de Persistencia total comprendí que para que una aplicación sea realmente inmortal en Docker, debo mapear tanto la base de datos (/var/lib/mysql) como los archivos de la aplicación (/var/www/html). Al combinar Bind Mounts para los archivos y la Red para la comunicación, logré que al borrar y recrear los contenedores, el sitio estuviera exactamente igual, con mis temas y entradas intactas.

