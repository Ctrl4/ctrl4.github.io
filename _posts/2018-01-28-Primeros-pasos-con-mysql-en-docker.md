---
layout: post
title: Primeros pasos con mysql en contenedores
tags: ctrl4
---

Hace ya un tiempo que tengo una computadora sin usar en mi cuarto. Siempre tuve ganas de usarla para aprender cosas nuevas o practicar. Todo en pos del auto-estudio.

Hace cuatro meses que estoy trabajando en una empresa dando soporte a los módulos que venden. La gran mayoría hacen uso de una base de datos, y realmente el proceso de instalación y soporte de los módulos no conlleva un gran desafío.

Excepto por el módulo de inventarios, que en base a mi poca experiencia siempre que tengo que re-instalar, restaurar backups o instalar de cero, me entra una especie de presión que no es buena para mi, ni para el cliente que no le doy la seguridad que tengo que darle. El módulo lleva el inventario de las sucursales de un negocio el cual replica los movimientos de dichos locales hacia un servidor central, y a su vez ese central replica a todas las sucursales una cierta información.

Se puede decir entonces que el Central es Esclavo y Maestro de todos los Locales, y cada Local es Maestro y Esclavo del Central.

Por lo tanto es que decido hacer esta entrada donde voy a pasar a reproducir de forma muy simple esta estructura.

Usando la vieja computadora formateada recientemente con Centos 7, utilizando contenedores de docker para encapsular cada instancia de MySQL y configurar una replica.

---

# Instalación del software requerido.

Instalamos docker desde los repositorios de centos

    sudo yum install docker
   
Luego debemos habilitar el servicio de docker para que inicie automáticamente y lo iniciamos.

    sudo yum systemctl enable docker
    sudo yum systemctl start docker

Si intentamos realizar una acción como iniciar un contenedor nuevo desde nuestro usuario nos darà el siguiente error:

```
[ctrl4@ChuckNorris ~]$ docker run hello-world
/usr/bin/docker-current: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See '/usr/bin/docker-current run --help'.
```

Para resolver esto debemos crear un grupo llamado docker y agregar nuestro usuario a dicho grupo

   sudo groupadd docker
   sudo usermod -aG docker $(whoami) #Si no estamos logueados en el usuario que queremos agregar al grupo
                                     #simplemente reemplazamos $(whoami) por el nombre del usuario.

Deslogueamos y entramos nuevamente a la cuenta del usuario y ahora efectivamente podemos usar docker sin problemas.

```
[ctrl4@ChuckNorris ~]$ docker run hello-world
Unable to find image 'hello-world:latest' locally
Trying to pull repository docker.io/library/hello-world ... 
latest: Pulling from docker.io/library/hello-world
ca4f61b1923c: Pull complete 
Digest: sha256:66ef312bbac49c39a89aa9bcc3cb4f3c9e7de3788c944158df3ee0176d32b751

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/

[ctrl4@ChuckNorris ~]$ 
```

Con esto, tenemos docker andando y listo para bajar el contenedor de mysql server.

Lo siguiente serìa descargar un cliente de mysql para poder trabajar con nuestro server. Existen distintas opciones para el gusto del consumidor, tanto clientes de manera gráfica como DBeaver, SQuirreL, MySQL Workbench, o el cliente que se ejecuta en la terminal.

En Centos este cliente lo trae el paquete mariadb, por lo tanto ejecutamos:

    sudo yum install mariadb
    
Con esto ya estamos listos para comenzar con la configuración de nuestra granja de servidores mysql.

Pero esto vendrá en futuras entradas.

¡Hasta luego!
