# Docker Practico.

## Ejecutar contenedores:

`doker run <container-id | container-name>` comando simple para ejecutar directamente un contenedor. 

`docker run --name <name> --detach <container-id | container-name>`

## Visualizar lista de contenedores:

`doker ps` - Despliega la lista con todos los contenedores que se estén ejecutando.

`doker ps -a` - Despliega la lista con todos los contenedores ejecutándose y alguna vez ejecutados aunque en ese momento no lo estén. 



## Eliminar contenedores:

`docker rm <container-name | container-id>` - Para Doker es indiferente si ingresamos el nombre o el id del contenedor, ya que no nos permite tener dos contenedores con el mismo nombre.

``docker rm -f <container-id | container-name>`` Para eliminar contenedores que estén en ejecución. Con este comando Docker detiene el proceso del contenedor, lo cierra y lo elimina.

`docker container prune` - Para eliminar todos los contenedores. 



## Salir de un contenedor:

`exit` basta con este comando. Generalmente útil para cuando se está en el modo interactivo de Docker a la hora de ejecutar un contenedor. 

``docker stop <container-id | container-name>`` - Permite detener la ejecución de un contenedor.

## Manipular un contenedor en ejecución:



## Exponer un contenedor:

``docker run --name <container-name> -p 8080:80 <container-id | container-name>`` - Permite especificarle a Docker el puerto en el que queremos que exponga el proceso que ejecuta el contenedor. Esto es debido a que Docker ejecuta el proceso, pero en un puerto propio del contenedor, por lo que no podemos acceder normalmente desde el navegador del ordenador. En este caso estamos exponiendo en el puerto ``8080``.

``docker logs --tail <n> -f <container-id | container-name>`` - Permite visualizar los logs del contenedor en ejecución, en este caso se utiliza el comando ``--tail <n>`` que especifica el numero de últimos logs que queremos visualizar. 

