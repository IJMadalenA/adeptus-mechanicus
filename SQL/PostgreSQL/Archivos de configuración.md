# Archivos de configuración.

Existen 3 archivos fundamentales que pueden ser los resultantes de muchos problemas si no se configuran adecuadamente, en especial cuando nuestra base de datos tiene funciones especiales. Estos archivos son:

- postgresql.conf
- pg_hba.conf
- pg_ident.conf

Para encontrar dichos archivos debemos ejecutar este comando:

```postgresql
=$ SHOW config_file;
```

Al ejecutar la consola retornará la ubicación de estos archivos.

## Archivo `postgresql.conf`.

En este archivo se definen múltiples parámetros en donde se configuran cosas como el numero de hilos que utilizaPostgres, la memoria disponible, si está en modo master o stand-by, el registro de queries suboptimas, en que direcciones se escucha, se puede cambiar el puerto y definir la cantidad máxima de conexiones permitidas a la base de datos, ademas de definir las variables de conexión y autenticación. 

> Las configuraciones comentadas dentro del documento no están siendo ignoradas, sino que se están ejecutando con su valor por defecto, y al momento de descomentarlas se comenzarán a ejecutar con la variable definida por nosotros. 

 Este archivo define gran parte  de las configuraciones de seguridad.

## Archivo `pg_hba.conf`.

Muestra los roles así como los tipos de acceso a la base de datos.

## Archivo `pg_indent.conf`.

Permite realizar el mapeo de usuarios. Permite definir roles a usuarios del sistema operativo donde se ejecuta.