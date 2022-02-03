title:Crear una imagen con dockerfile
authors: Jairo Zenteno and Daniel Vazquez

# Ejercicio- Crear una imagen con DockerFile

[TOC]

### Bloque de código DockerFile.

```dockerfile
FROM ubuntu:[version]
MAINTAINER jairo jairo@correo.com #Creador de la imagen
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get -y install apache2 #Establecemos que no sea interactiva e instalamos el servidor web apache2
COPY ./public_html /var/www/html
expose 81 #expuesto en el puerto 81
CMD /usr/sbin/apache2ctl -D FOREGROUND #ejecuta el sevicio 
```

![image-20220201170853840](Ejercicio-%20Crear%20una%20imagen%20con%20DockerFile.assets/image-20220201170853840.png)

> La plantilla que descargamos esta en el directorio en el que se encuentra el archivo Dockerfile
>
> Con la variable de entorno `COPY ./public_html /var/www/html` exportamos nuestra plantilla al document_root de apache2.

### Creamos la imagen

Una vez configurado el dockerfile, creamos nuestra imagen con apache2, usando los comandos:

```bash
docker build -t [nombre_de_la_imagen]web .
#IMPORTANTE NOS TENEMOS QUE SITUAR EN EL DIRECTORIO DONDE TENEMOS EL DOCKERFILE O EN CASO DE QUERER EJECUTARLO DESDE OTRO DIRECTORIO TENEMOS QUE PONER LA RUTA COMPLETA DE DONDE SE ENCUENTRA EL DOCKER FILE,ejemplo
#docker build -t web /home/jairo/docker-apache
```

![image-20220131143556542](Ejercicio-%20Crear%20una%20imagen%20con%20DockerFile.assets/image-20220131143556542.png)

Comprobamos que se ha creado la imagen

```bash
docker images
```

![image-20220131143714771](Ejercicio-%20Crear%20una%20imagen%20con%20DockerFile.assets/image-20220131143714771.png)

Creamos el contenedor a partir de la imagen creada.

```bash
docker run -d -p 90:80 web #web nombre de la imagen creada
```

Comprobamos que esta funcionando en el navegador accediento al http://localhost:90

![image-20220131112854003](C:/Users/usuario/AppData/Roaming/Typora/typora-user-images/image-20220131112854003.png)



Para poder importar nuestra plantilla html al servidor hice uso de los comandos:

```bash
docker run -d -p 90:80 -v /home/jairo/Documentos/DAW2/Despliegue/univers:/var/www/html --name pagweb web
```

> Tuve que borrar el contenedor anterior.
>
> Con el parámetro `-v` , estamos compartiendo los ficheros que tenemos en nuestro localhost en el directorio `/home/jairo/Documentos/DAW2/Despliegue/univers` a  nuestro servidor web en el directorio ` :/var/www/html` 

Comprobamos que ha funcionado.

![image-20220131143836373](Ejercicio-%20Crear%20una%20imagen%20con%20DockerFile.assets/image-20220131143836373.png)



Accedemos a localhost:90 y vemos que tenemos nuestra plantilla.

![image-20220131133723265](C:/Users/usuario/AppData/Roaming/Typora/typora-user-images/image-20220131133723265.png)



### Creamos un repositorio en docker-hub 

![image-20220131141504573](C:/Users/usuario/AppData/Roaming/Typora/typora-user-images/image-20220131141504573.png)

### Subimos nuestra imagen a docker hub

1. Para poder subir nuestra imagen a docker-hub tenemos que  iniciar sesion desde el cli con los comandos:

```bash
docker login 
#o también lo podemos hacer con
docker login -u [user_de_docker-hub]
```

![image-20220131140247665](C:/Users/usuario/AppData/Roaming/Typora/typora-user-images/image-20220131140247665.png)

![image-20220131140308908](C:/Users/usuario/AppData/Roaming/Typora/typora-user-images/image-20220131140308908.png)

2. Ahora tenemos que hacer un tag de nuestra imagen

   ```bash
   #docker tag imageId [usuario_docker-hub]/[repositorio de docker images]:[tag] es alternativo pero aquí ira el tag de la imagen en nuestro caso seria "latest"
   docker tag df8591f532db bl4ckr0se/web
   ```

   ![image-20220131140617812](C:/Users/usuario/AppData/Roaming/Typora/typora-user-images/image-20220131140617812.png)

3. Subimos la imagen a docker-hub con los comandos:

   ```bash
   docker push bl4ckr0se/web
   #donde bl4cr0se/web es el repositorio previamente creado desde la GUI
   ```

   

   ![image-20220131141255295](C:/Users/usuario/AppData/Roaming/Typora/typora-user-images/image-20220131141255295.png)

4. Vemos en la GUI que nos subió correctamente la imagen a docker

![image-20220131144000204](Ejercicio-%20Crear%20una%20imagen%20con%20DockerFile.assets/image-20220131144000204.png)