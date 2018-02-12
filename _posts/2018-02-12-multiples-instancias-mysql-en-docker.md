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
        image: mysql:8							# Imagen tomada del repositorio de dockerhub de mysql versión 8 
        container_name: mysql-local98					# Nombre del contenedor
        restart: always							# En caso de que ocurra algún problema donde el contenedor se caiga, se reinicia automáticamente
        environment:							# Variables de entorno 
                MYSQL_ROOT_PASSWORD: "passwordsecreta"  		# Variable para definir la contraseña del usuario root

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

