# Link entre archivos.

https://www.geeksforgeeks.org/soft-hard-links-unixlinux/

https://www.geeksforgeeks.org/ln-command-in-linux-with-examples/

---

__Soft and Hard links in Linux.__

Los links son accesos directos o atajos para acceder a archivos determinados, lo que permite que diferentes nombres refieran a un mismo archivo desde distintos lugares.

## Tipo de links.

Existen dos tipos de links:

1. _Soft Link_ o _Links_ simbólicos.
2. _Hard  Links_.

Estos links se comportan diferente cuando la fuente del enlace se mueve o elimina. Los ___Links_ Simbólicos__ no se actualizan, ya que ellos simplemente contienen un _str_ que funciona como el _path name_ de la carpeta objetivo.

Por ejemplo, tenemos un archivo llamado `example_file.txt`. Si creamos un _Hard Link_ y eliminamos el archivo, nosotros podríamos seguir accediendo al archivo utilizando el _Hard Link_. Pero si creamos un _Soft Link_ que apunte hacia el archivo y lo eliminamos, no podremos acceder al archivo desde el _Soft Link_ y este dejará de funcionar. 

> Básicamente el _Hard Link_ aumenta las referencias hacia una ubicación determinada, mientras que los _Soft Links_ funcionan como accesos directos.

## _Hard Links_.

- Cada _Hard Link_ asigna el mismo ___inode value___ que el original, por lo tanto estos referencian a la misma dirección física. 

> Un _Inode value_ es una estructura de datos interna que _Linux_ utiliza para almacenar información sobre un objeto en el sistema de archivos. El __inode count__ es igual al numero total de archivos y directorios que una cuenta de usuario tienen en un disco. Cada archivo o directorio añade un valor al ___inode count___.
>
> https://linuxhandbook.com/inode-linux/

- El comando `ls -l` muestra todos los _links_ y el numero total de _links_.

- Eliminar cualquier _link_ solo reduce el numero total de _links_, pero sin afectar a otros _links_.
- Incluso si cambiamos la dirección.
- No podemos crear un _Hard Links_ a un directorio para evitar bucles recursivos. 
- Si el archivo original es eliminado, el enlace aún podrá seguir mostrando el contenido del archivo.
- El tamaño de el _Hard Link_ es el mismo que el _link_ original y si cambiamos el contenido en cualquier _Hard Link_, entonces el tamaño de todos los archivos del  _Hard Link_ se actualizará.
- La desventaja de los _Hard Links_ es que no pueden ser creados para archivos en diferentes sistemas de archivos y no se pueden crear para archivos o directorios especiales.

El comando es el siguiente:

```sh
$ ln [original filename] [link name]
```

## Soft Links.

- Un _Soft Link_ es similar al acceso directo que tiene Windows. Cada archivo _Soft Linked_ contiene un _Inode Value_ separado que apunta al archivo original. Similar a los _Hard Links_, cualquier cambio realizado en cualquier archivo se reflejará en el otro. 
- Los _Soft Links_ pueden ser enlazados a través de diferentes sistemas de archivo, aunque si el archivo original se elimina o se mueve, el archivo vinculado no funcionará correctamente, generando un enlace colgante o _colled hanging link_.
- Los _Soft Link_ contienen el _path_ hacia el archivo original y no hacia su contenido.
- Eliminar el _Soft Link_ no va a afectar a ningún otro archivo, pero si eliminamos el archivo original el _Soft Link_ se dañará.
- Un _Soft Link_ puede llamar a un directorio.
- El tamaño de un _Soft Link_ es igual a la longitud del _path_ hacia el archivo original.
- Si cambiamos el nombre del archivo original los _Soft Links_ que lo señalen se dañaran. 

El comando es el siguiente:

```sh
$ ln  -s [original filename] [link name] 
```



---

- [ ] Ver que puertos se están utilizando.
- [ ] Instalar paquetes y librerias con sus respectivas versiones desde el `sudo apt-get install`.
- [ ] Saber como cambiar la versión de un paquete.
- [ ] 