# Docker - Apuntes.

## Docker Desktop.



## Imagenes.

### Descargar Imagenes.

```dockerfile
$ docker pull <image_name>
```

### Ver imagenes.

```dockerfile
$ docker images
    
REPOSITORY    TAG    IMAGE ID    CREATED    SIZE
   ---        ---       ---        ---       ---
```

### Eliminar imagenes.

```dockerfile
$ docker rm <image_name>
```

---



## Contenedores.

### Crear un contenedor.

Para crear un contenedor hacen falta imagenes, y cada una puede tener sus propias configuraciones.

Para crearlo es necesario especificar una imagen de basa sobre la que se creará el contenedor.

```dockerfile
$ docker create <image_base>
               |
$ docker container create <image_base>
```

Este comando al ser ejecutado retornará un `id` que identificará al nuevo contenedor, y es importante guardarlo ya que es necesario para ejecutarlo. 

Si utilizamos la opcion `--name` podemos definir el nombre del contenedor, de no hacerlo Docker le asignará uno arbitrariamente. El nombre sirve para podernos referir al contenedor de una forma más fácil que con el ID. 

```dockerfile
$ docker create <image_base> --name <container_name>
```



### Ejecutar un contenedor.

```dockerfile
docker start <container_id>
```



### Ver contenedores corriendo.

```dockerfile
$ docker ps

CONTAINER ID     IMAGE     COMMAND     CREATED     STATUS     PORTS     NAMES
     ---          ---        ---         ---        ---        ---       ---
```

podemos ver todos los contenedores, aún aquellos que no están corriendo, con el siguiente comando:

```dockerfile
$ docker ps -a
```



## gestionar puertos de los contenedores.

```dockerfile
docker create -p<physical port>:<maping_port> <image_base>
```

La opción `-p` significa _publish_.

Un ejemplo del comando sería: `docker create -p27017:3001 --name new_container python`

En donde colocamos los puertos seguidos de la `-p`, sin espacios, y el primer puerto es el puerto físico de nuestra máquina, y el segundo es el puerto que le queremos asignar al contenedor. Luego debemos colocar la imagen base, aunque antes de este ultimo paso podemos definir opciones como el `--name` para especificar el nombre.

### Detener contenedor.

```dockerfile
$ docker stop <container_id>

$ docker stop <container_name>
```



### Eliminar contenedor.

```docke
$ docker rm <container_id>
            |
$ docker rm <container_name>
```

---

## Logs.

```dockerfile
$ docker logs <container_name>
```



```dockerfile
$ docker logs --follow <container_name>
```

---

##  Parametros de configuración.

### NGINX.

https://hub.docker.com/_/nginx

### Python.

https://hub.docker.com/_/python

### Postgres.

https://hub.docker.com/_/postgres

### Ubuntu.

https://hub.docker.com/_/ubuntu

---

