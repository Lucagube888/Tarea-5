<h1>Explicacion de las opciones del archivo compose.yaml</h1>
version: Especifica la versión del esquema de docker-compose. La versión 3.8 es compatible con una amplia gama de características de Docker y es adecuada para la mayoría de las configuraciones actuales.
Servicios

services: Define los servicios que se van a ejecutar en contenedores. En este caso, solo hay un servicio llamado bind9.
bind9

image: internetsystemsconsortium/bind9:9.18: Indica la imagen de Docker que se utilizará para crear el contenedor. En este caso, se usa la imagen oficial de BIND versión 9.18, que es un servidor DNS.

container_name: bind9: Asigna el nombre bind9 al contenedor, en lugar de permitir que Docker asigne un nombre automáticamente.

restart: always: Configura el contenedor para que se reinicie automáticamente si se detiene, lo que garantiza que el servicio permanezca en ejecución.

Puertos

    ports:
        "54:53/udp": Mapea el puerto 54 del host al puerto 53 del contenedor para el tráfico UDP. El puerto 53 es el puerto estándar para el servicio DNS.
        "54:53/tcp": Mapea el puerto 54 del host al puerto 53 del contenedor para el tráfico TCP. Esto permite manejar consultas DNS a través de TCP.
        "127.0.0.1:953:953/tcp": Mapea el puerto 953 del contenedor al mismo puerto en 127.0.0.1 (la interfaz local del host), para acceso a la interfaz de control de BIND.

Volúmenes

    volumes:
        ./etc/bind:/etc/bind: Monta el directorio ./etc/bind del host en el contenedor en /etc/bind. Esto permite personalizar la configuración de BIND desde el host.
        ./var/cache/bind:/var/cache/bind: Monta el directorio ./var/cache/bind del host en el contenedor en /var/cache/bind. Este directorio se usa para almacenar datos en caché de BIND, manteniendo la persistencia de la caché entre reinicios.
