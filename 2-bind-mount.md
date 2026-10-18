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
# COMPLETAR CON EL COMANDO
docker run -d --name servPractica1 -p 8080:80 -v C:\Users\marle\OneDrive\Documentos\nginx\html:/usr/share/nginx/html nginx:alpine

### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar a `http://localhost:8080`, se muestra el error 403 Forbidden de Nginx, debido a que la carpeta del computador montada en el contenedor está vacía o no contiene un archivo `index.html` válido para mostrar.

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

### ¿Qué pasa con el archivo index.html del contenedor?
Al montar la carpeta `html` del computador en la ruta `/usr/share/nginx/html` del contenedor, el contenido original de ese directorio de la imagen de Nginx queda oculto mientras el montaje está activo. En su lugar, Nginx utiliza los archivos que existen en la carpeta del computador. Por eso, si la carpeta del host está vacía, no se muestra la página de bienvenida predeterminada de Nginx y puede aparecer el error 403 Forbidden. El archivo original de la imagen no se elimina, simplemente queda oculto por el montaje.

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Después de descargar y descomprimir la plantilla de HTML5 UP dentro de la carpeta `html` del computador, al ingresar nuevamente a `http://localhost:8080` se muestra la página web correspondiente a la plantilla descargada. Esto sucede porque Nginx accede a los archivos HTML, CSS, JavaScript e imágenes mediante el bind mount. Así, el servidor puede presentar la página personalizada en lugar del error 403 Forbidden.
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

### Eliminar el contenedor
docker rm servPractica1
Al eliminar el contenedor `servPractica1`, el servidor Nginx deja de ejecutarse y el puerto 8080 deja de estar asociado a ese servicio. Por esta razón, al ingresar a `http://localhost:8080`, el navegador muestra el error `ERR_CONNECTION_REFUSED`, ya que no existe un servidor escuchando en ese puerto. Sin embargo, los archivos de la plantilla HTML5 UP permanecen en la carpeta del computador, porque están almacenados fuera del contenedor.

# COMPLETAR CON EL COMANDO
docker run -d --name servPractica1.1 -p 8080:80 -v C:\Users\marle\OneDrive\Documentos\nginx\html:/usr/share/nginx/html nginx:alpine

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Al crear un nuevo contenedor Nginx y montar nuevamente la misma carpeta `html` del computador mediante un bind mount, la página web de la plantilla HTML5 UP vuelve a mostrarse al ingresar a `http://localhost:8080`. Esto ocurre porque los archivos de la página se encuentran almacenados en el sistema de archivos del host y no dentro del contenedor eliminado. Por lo tanto, aunque se elimine y se cree otro contenedor, los archivos permanecen disponibles y pueden reutilizarse.
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA


