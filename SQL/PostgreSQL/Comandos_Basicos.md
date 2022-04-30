# Comandos básicos.



### Entrar a la consola de Postgres.

```postgresql
psql - d <base_dat-U <user_name> -W
```

``` postgresql
sudo su - postgres
psql
```



## Comandos del grupo back-slash `\`.

### Ver los comandos `\` de Postgres.

```postgresql
\?
```

### Listar todas las bases de datos.

```postgresql
\l
```

### Ver las tablas de una base de datos.

```postgresql
\dt
```

### Ingresar a otra base de datos.

```postgresql
\c <nombre_base_de_datos>
```

### Describir una tabla.

```postgresql
\d <nombre_tabla>
```

### Ver todos los comandos SQL.

```postgresql
\h
```

### Ver como se ejecuta un comando SQL.

```postgresql
 \h <nombre_funcion>
```

### Volver a ejecutar la función realizada anteriormente.

```postgresql
\g
```

### Iniciar el contador de tiempo para la siguiente función.

```postgresql
\timing
```

