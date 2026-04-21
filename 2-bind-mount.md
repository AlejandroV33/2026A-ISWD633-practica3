# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
Comando (macos): docker run -d --name srv-nginx-bind -P -v $(pwd)/nginx/html:/usr/share/nginx/html nginx:alpine

### ¿Qué sucede al ingresar al servidor de nginx?
Aparece la pantalla con el error 403 Forbidden ya que la carpeta de html esta vacia.

### ¿Qué pasa con el archivo index.html del contenedor?
El archivo original que venía dentro de la imagen de Nginx queda oculto. En Bind Mount el contenido del directorio del host tiene prioridad absoluta.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Se carga y muestra la página web del template descargado.

### Eliminar el contenedor
docker rm -f srv-nginx-bind

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Parece que nada cambio y la pagina sigue alli, cargando igual que anteriormente. 

