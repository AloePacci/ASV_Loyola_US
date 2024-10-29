---
layout: default
title: Docker ASV
description: Docker del vehiculo
permalink: /cmdsdocker/
---

Aqui se encuentran varios comandos de utilidad para los dockers

# Docker ASV

Lanzar el docker_ASV ARM:

- Comando completo (ejemplo)
```bash
docker run -it --rm --device /dev/SONAR --device /dev/SENSOR -e DEBUG="True/False" -e MQTT_ADDR="IP a usar" -e NAVIO_ADDR="IP a usar" -e DB_HOST="127.0.0.1" --network host bender.us.es:5000/asv_us:arm
```

Lanzar el docker_ASV AMD:
- Comando commpleto (ejemplo)
```bash
docker run -it --rm --device /dev/SONAR --device /dev/SENSOR -e DEBUG="True/False" -e MQTT_ADDR="IP a usar" -e NAVIO_ADDR="IP a usar" -e DB_HOST="127.0.0.1" --network host bender.us.es:5000/asv_us:amd
```
En el barco se encuentra bajo la llamada de dos comando, dependiendo si se necesita guardar datos en local:
- Alias sin guardar datos internamente
```bash
run_docker_asv_us
```

- Alias con guardar datos internamente
```bash
run_docker_asv_us_database
```

con este comando se realiza la llamada del docker con la siguiente configuracion

Barco amarillo sin guardar datos:

```bash
docker run -it --rm --device /dev/SONAR --device /dev/SENSOR -e NAVIO_ADDR="192.168.1.203:5678" --network host bender.us.es:5000/asv_us:arm
```

Barco amarillo guardando datos internamente:

```bash
docker run -it --rm --device /dev/SONAR --device /dev/SENSOR -e NAVIO_ADDR="192.168.1.203:5678" -e DB_HOST="127.0.0.1"  --network host bender.us.es:5000/asv_us:arm
```


Barco azul sin guardar datos internamente:
```bash
docker run -it --rm -e NAVIO_ADDR="192.168.1.203:5778" -e USE_SENSORS="false" --network host bender.us.es:5000/asv_us:arm
```
Barco azul guardando datos internamente:
```bash
docker run -it --rm -e NAVIO_ADDR="192.168.1.203:5778" -e USE_SENSORS="false" -e -e DB_HOST="127.0.0.1" --network host bender.us.es:5000/asv_us:arm
```

## Otros usos del docker asv
### Lanzar docker con bash
Para lanzarlo sin que ejecute nada, deberemos lanzar el comando del docker junto con alguno de los siguentes comandos 
```bash
--entrypoint bash
```
o
```bash
--entrypoint bin/bash
```
ejemplo:
```bash
docker run -it --rm -e NAVIO_ADDR="192.168.1.203:5778" --entrypoint bin/bash --network host bender.us.es:5000/asv_us:arm
```
### Argumento USE_SENSORS
El argumento USE_SENSORS en la llamada del docker run, permite el uso de los nodos de los sensores "true/false", mediente la modificacion en la llamada del launch de ros2 en el entrypoint con el uso de "Ros args". Por defecto esta en usar los sensores

uso del argumento (ejemplos):

uso de los sensores
```bash
docker run -it --rm -e NAVIO_ADDR="192.168.1.203:5778" -e USE_SENSORS="true" --network host bender.us.es:5000/asv_us:arm
```

No uso de los sensores
```bash
docker run -it --rm -e NAVIO_ADDR="192.168.1.203:5778" -e USE_SENSORS="false" --network host bender.us.es:5000/asv_us:arm
```

# Docker Wrappe_Zed

Para lanzar el docker wrapper_zed en el barco amarillo, se ejecuta el siguente comando:
- Comando

```bash
 docker run -it --gpus all  --privileged --net host -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /home/xavier/CameraFolder:root/CameraFolder bender.us.es:5000/asv_us:zed_wrapper
```
- Para mayor facilidad, este comando de docker esta bajo el alias:

```bash 
run_docker_wrapper
```

Para usar el wrapper con el docker y una pantalla concetada deberemos introducir el siguente comando primero antes de lanzar el docker wrapper_zed:
```bash 
xhost +si:localuser:root
```

# Docker trash detecttion

Para lanzar el docker de deteccion de basura, se realizara para ambos barcos con la siguente llamada del docker:

Barco amarillo:
```bash
docker run -it --network host --runtime nvidia --privileged  bender.us.es:5000/asv_us:xavier_trash_detection
```
Barco azul:
```bash
docker run -it --network host --runtime nvidia --privileged  bender.us.es:5000/asv_us:orin_detection_trash
```

Se ha realizado un mismo alias para la llamada de los dockers:
alias

```bash
run_docker_trash
```

# Docker Mysql interno en las jetson

Para acceder a la base de datos interna, utilizar el siguiente comando:
```bash
docker exec -it mysql-arm mysql -h127.0.0.1 -P3306 -uroot -p
```
la contraseña es password

Para la exportacion de los datos, a dos scripts .sh en las jetsons para la exportacion de los datos a un archivo csv (puede modificarse) a una carpeta. 



 [Volver](../)   

