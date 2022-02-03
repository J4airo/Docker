---
title: trabajo con imágenes - Docker
authors: Jairo Zenteno and Daniel Vazquez
---

# Trabajo con Imágenes - Docker

[TOC]

### SERVIDOR WEB

### SERVIDOR DE BASE DE DATOS

#### **1. Arrancar un contenedor que se llame bbdd y que ejecute una instancia de la imagen mariadb para que sea accesible desde el puerto 3336.**

#### **Antes de arrancarlo estable las variables de entorno necesarias para que:** 

- La contraseña de root sea `root`
- Crear una base de datos automáticamente al arrancar que se llame `prueba`
- Crear el usuario `invitado` con la contraseña `invitado`

```bash
docker run -d --name bbdd -p 3336:80 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_USER=invitado -e MYSQL_PASSWORD=invitado -e MYSQL_DATABASE=prueba -d mariadb
```

<img src="trabajo-con-im%C3%A1genes---Docker.assets/Inkedcap2_LI.jpg" alt="Inkedcap2_LI" style="zoom: 80%;" />

#### Pantallazo que desde el navegador muestre el fichero `index.html`

![phpmyadminIndex](trabajo-con-im%C3%A1genes---Docker.assets/phpmyadminIndex.png)



#### Pantallazo que desde un navegador muestre la salida del script `mes.php`

![mesphp](trabajo-con-im%C3%A1genes---Docker.assets/mesphp.png)



#### Pantallazo donde se vea el tamaño del contenedor `web` después de crear los dos ficheros.

```bash
docker ps -as
```

![image-20220120111159623](trabajo-con-im%C3%A1genes---Docker.assets/image-20220120111159623.png)



#### Pantallazo donde desde un cliente de base de datos (instalado en tu ordenador) se pueda observar que hemos podido conectarnos al servidor de base de datos con el usuario creado y que se ha creado la base de datos prueba ( show databases ). El acceso se debe realizar desde el ordenador que tenéis instalado docker, no hay que acceder desde dentro del contenedor, es decir, no usar docker exec .

![phpmyadmin](trabajo-con-im%C3%A1genes---Docker.assets/phpmyadmin.png)



#### Pantallazo donde se comprueba que no se puede borrar la imagen `mariadb` mientras el contenedor `bbdd` está creado.

```bash
docker rmi mariadb
```

![cap4](trabajo-con-im%C3%A1genes---Docker.assets/cap4.png)

