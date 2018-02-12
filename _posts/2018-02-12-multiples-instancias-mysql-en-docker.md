---
layout: post
title: Múltiples instancias MySQL en Docker
tags: ctrl4
---

En el post anterior me invitaba a mi mismo a hacer una serie de blogposts con el fin de recrear la arquitectura en cuanto a bases de datos se trata, de uno de los productos de la empresa donde trabajo.

Para eso expliqué como dejar andando docker y el cliente mysql de nuestra preferencia.

Hoy vamos a dejar instalado otra herramienta para facilitar el trabajo de configurar los contenedores de docker llamada Docker-Compose. Para aprender mediante ejemplos vamos a configurar 3 contenedores 1 para el servidor central y 2 servidores locales (Local 98 y 99). Y al final dejaremos configurada la replicación como explicabamos en el post anterior:

> (...) El módulo lleva el inventario de las sucursales de un negocio el cual replica los movimientos de dichos locales hacia un servidor central, y a su vez ese central replica a todas las sucursales una cierta información.
>
>Se puede decir entonces que el Central es Esclavo y Maestro de todos los Locales, y cada Local es Maestro y Esclavo del Central.

---
### Instalación de Docker Compose

Para instalar Docker Compose necesitamos pip, la herramienta de descarga de paquetes de python, por lo tanto también necesitamos Python.
  
  ```
sudo yum install epel-release
sudo yum install -y python-pip
```

Y recién acá podemos instalar Docker Compose utilizando pip

```
sudo pip install docker-compose
```

### Creación de MySQL mediante Docker Compose

Como dijimos anteriormente, vamos a crear 3 contenedores de Docker mediante Docker Compose. Este último se configura con un archivo llamado `docker-compose.yml`. Vamos a crearlo y a configurar los 3 contenedores.

```
vim docker-compose-yml
```

Con el siguiente contenido:

```	
local98:							# Nombre del servicio tomcado por docker si no se especifica el nombre del contenedor
	image: mysql:8						# Imagen tomada del repositorio de dockerhub de mysql versión 8 
        container_name: mysql-local98				# Nombre del contenedor
        restart: always						# En caso de que ocurra algún problema donde el contenedor se caiga, se reinicia automáticamente
        environment:						# Variables de entorno 
                MYSQL_ROOT_PASSWORD: "passwordsecreta"  	# Variable para definir la contraseña del usuario root

local99:							# Lo mismo que se define arriba solamente que cambiando el nombre del container y el servicio
        image: mysql:8
        container_name: mysql-local99
        restart: always
        environment:
                MYSQL_ROOT_PASSWORD: "passwordsecreta"

central:
        image: mysql:8
        container_name: mysql-central
        restart: always
        environment:
		MYSQL_ROOT_PASSWORD: "passwordsecreta"
```

Esta es una configuración muy básica pero suficiente como para poder dejar andando los contenedores.
Como vemos consta de 3 bloques de configuración cada uno.

Entonces ejecutamos `docker-compose up` y si todo sale bien despues de un breve lapso de tiempo podemos ejecutar `docker-compose ps` y obtendremos un resultado parecido al siguiente:

```
[ctrl4@ChuckNorris local98]$ docker-compose ps
    Name                  Command             State    Ports  
--------------------------------------------------------------
mysql-central   docker-entrypoint.sh mysqld   Up      3306/tcp
mysql-local98   docker-entrypoint.sh mysqld   Up      3306/tcp
mysql-local99   docker-entrypoint.sh mysqld   Up      3306/tcp
```

Podremos ir monitoreando los logs mediante `docker-compose logs` y si no quedan en estado 'Up' será momento de empezar a indagar y googlear ;)

Otro comando importante para saber la ip de nuestros contenedores para luego conectarnos con nuestro y cliente mysql y ahí si, efectivamente, corroborar que está andando todo bien, es `docker inspect <nombre del contenedor>` Ejemplo:

```
[ctrl4@ChuckNorris local98]$ docker inspect mysql-central

#### GRAN BLOQUE DE PARAMETROS, PERO SOLAMENTE ME INTERESA EL DEL FINAL ####

        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "6ea2b9d6047aa0e7efe97262d7d0645f14f0cfb3b1fc130547577a0ac57d1fd4",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "3306/tcp": null
            },
            "SandboxKey": "/var/run/docker/netns/6ea2b9d6047a",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "77bd76b50e07d2ca067d8b31b00a91a08d80897e9b535a344481ccbdb83743f2",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            *"IPAddress": "172.17.0.2",*
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "42ad81c93ebdfac5c388076089d1bc377d498fdae9146c42cd99edd8707a6997",
                    "EndpointID": "77bd76b50e07d2ca067d8b31b00a91a08d80897e9b535a344481ccbdb83743f2",
                    "Gateway": "172.17.0.1",
                    *"IPAddress": "172.17.0.2",*
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02"
                }
            }
        }
    }
]
```

En negrita podemos ver la dirección ip y utilizando `mysql -uroot -ppasswordsecreta -h 172.17.0.2` podemos entrar y por fin empezar a jugar con las bases de datos.

```
[ctrl4@ChuckNorris local98]$ mysql -uroot -ppasswordsecreta -h 172.17.0.2
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.3-rc-log MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]> 
```
