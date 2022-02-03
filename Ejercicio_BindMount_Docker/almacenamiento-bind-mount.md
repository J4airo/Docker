---
--
title: almacenamiento bind mount
--
authors: Daniel Vazquez Vidal y Jairo Centeno Flores
--
---





# Bind Mount para compartir datos



> Tarea realizada por: Daniel Vázquez Vidal y Jairo Centeno Flores





1. Crea una carpeta llamada saludo y dentro de ella crea un fichero llamado index.html con el siguiente contenido (Deberás sustituir ese XXXXXx por tu nombre.):



![image-20220126181926060](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126181926060.png)



2. Una vez hecho esto arrancar dos contenedores basados en la imagen php:7.4- apache que hagan un bind mount de la carpeta saludo en la carpeta /var/www/html del contenedor. Uno de ellos vamos a acceder con el puerto 8181 y el otro con el 8282. Y su nombres serán c1 y c2 .



![image-20220126183607084](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126183607084.png)





3. Modifica el contenido del fichero ~/saludo/index.htmlclear

   



![image-20220126183911087](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126183911087.png)





4. Comprueba que puedes seguir accediendo a los contenedores, sin necesidad de reiniciarlos.

Con `docker ps` en la columna de status comprobamos que sin la necesidad de reiniciar el acceso a los contenedores sigue siendo válido.

![image-20220126202131874](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126202131874.png)



5. Borra los contenedores utilizados.

![image-20220126203037409](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126203037409.png)





6. Pantallazo con la orden correspondiente para arrancar el contenedor c1 (puerto 8181) realizando el bind mount solicitado.

```bash
docker run -t -d -P -p 8181:80 -v /tmp/apache/saludo:/var/www/html --name c1 php:7.4-apache
```

![image-20220126202407653](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126202407653.png)





7. Pantallazo con la orden correspondiente para arrancar el contenedor c2 (puerto 8282) realizando el bind mount solicitado.

```
docker run -t -d -P -p 8282:80 -v /tmp/apache/saludo:/var/www/html --name c2 php:7.4-apache
```

![image-20220126202336472](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126202336472.png)





8. Pantallazo donde se pueda apreciar que accediendo a c1 se puede ver el contenido de index.html .



![image-20220126201348081](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126201348081.png)







9. Pantallazo donde se pueda apreciar que accediendo a c2 se puede ver el contenido de index.html .



![image-20220126201414491](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126201414491.png)



10. Otros dos pantallazos donde se vea el acceso al fichero index.html después de modificarlo.



![image-20220126201639956](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126201639956.png)



![image-20220126201711074](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126201711074.png)





11. Borrar los dos contenedores. Mostrar que se han borrado.



```bash
docker stop c1
docker rm c1
docker stop c2
docker rm c2
docker ps
```

![image-20220126203031789](C:/Users/danii/AppData/Roaming/Typora/typora-user-images/image-20220126203031789.png)





