# git.

## Estructura del proyecto git.

Un proyecto __git__ tiene tres secciones principales:

1. __Directorio git__: Es donde __git__ almacena todo lo que necesita para hacer un seguimiento preciso del proyecto. 
2. __Repositorio (Directorio de trabajo o árbol de trabajo)__: Es donde se realizan los cambios locales del proyecto. El repositorio descarga los archivos del proyecto de la base de datos del directorio __git__ y los coloca en la máquina local del usuario.
3. __Zona de "_staging___": es un archivo, también llamado "_index_", "_stage_" o "_cache_" que almacena información sobre lo que irá en el próximo _commit_. Un _commit_ es cuando le decimos a __git__ que guarde estos cambios almacenados en el _stage_. Entonces __git__ hace una copia de los archivos tal y como están y los almacena permanentemente en el repositorio remoto de __git__.

> __Nota:__ Los archivos se suben a la zona de _staging_ a traves del comando `git add`.

Hay tres estados principales en los que puede estar un archivo en __git__: modificado, _commited_ o _staged_. Tú modificas un archivo cada vez que se hacen cambios en el repositorio local, luego es _staged_ cuando se mueve a la zona de "_staging_" y finalmente es _commited_ después de ejecutar un commit.

## Crear un nuevo repositorio.

```shell
$ git init [directory]
```

​	Crea un repositorio de git vacío, básicamente un nuevo directorio .git con subdirectorios y plantillas de archivos. Si el directorio no se especifica, el git se creara en la ruta en donde se ejecutó.

---

​	Tambien podemos usar el comando `git remote add <url>` para emparejar nuestro repositorio local con la dirección del repositorio remoto de git.

```shell
git remote add origin  <REMOTE_URL> 
```

​	Esto asocia automáticamente el nombre `orign` con el `REMOTE_URL`.

​	También podemos usar el comando `git remote set-url` para cambiar una URL remota.

---

````powershell
PS C:\Users\ismae\OneDrive\Proyectos\Codigo\Fakestagram> git pull
fatal: refusing to merge unrelated histories

PS C:\Users\ismae\OneDrive\Proyectos\Codigo\Fakestagram> git push
To https://github.com/IsMadalena/Fakestagram.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/IsMadalena/Fakestagram.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

PS C:\Users\ismae\OneDrive\Proyectos\Codigo\Fakestagram> git pull --rebase
Successfully rebased and updated refs/heads/master.
````



## Eliminar rama local.

​	Para eliminar una rama de nuestro repositorio local ejecutaremos el siguiente comando:

```bash
$ git branch -d nombre_rama
```

​	En el caso de que esa rama contenga trabajos sin fusionar, el comando anterior nos devolverá el siguiente error:

```bash
error: The branch 'nombre-rama' is not an ancestor of your current HEAD.
If you are sure you want to delete it, run 'git branch -D nombre-rama'.
```

​	Si aún así queremos eliminar esa rama, se puede forzar el borrado de la siguiente manera:

```bash
$ git branch -D nombre-rama
```

​	En el caso de querer eliminar una rama del repositorio remoto, la sintaxis será la siguiente:

```bash
$ git push origin :nombre-rama
```

​	Y de esta forma, desaparecerá la rama nombre-rama del servidor.

---

## branch.

### 	Visualizar ramas.

> ```bash
> usuario@usuario-portatil:~/ejemplos-git$ git branch -v
> ```





---

## merge

### 	Tipos de merge.

​	Existen al menos tres posibles resultados cuando hacemos un merge:

- **Merge con avance rápido (fast-forward)**: se presenta cuando por ejemplo creamos un nuevo branch *desarrollo* a partir del branch *master* y agregamos cambios en este nuevo branch. Luego cuando vamos a hacer el merge del branch *desarrollo* a *master*, si *master* permanece sin ningún cambio, se producirá un avance rápido. Solo se añadiran los nuevos commits presentes en el branch *desarrollo* y **no se generará ningún commit adicional**.

- **Merge de tres vías (3-way)**: siguiendo el ejemplo de crear un branch *desarrollo* a partir del branch *master*. Imaginemos que se existen nuevos commits en *master* al momento de querer hacer el merge del branch *desarrollo*, git se encarga de hacer la unión y se va a ver reflejado en un **nuevo commit** que por defecto tiene como mensaje similar a **"Merge branch 'desarrollo'"**.

- **Merge con conflictos**: cuando se presenta un merge con conflictos por resolver, siempre **se crea un nuevo commit** que representa la solución de los conflictos.

### Cancelar merge.

```git
```



---

## add.

​    Cuando ejecutamos el comando `git add` seguido del archivo o los archivos editados, estos son guardados en  el area de `staging`, que es un area en memoria RAM que almacena todos los cambios añadidos que aun no son enviador al repositorio por el comando `git commit`.

### 	Eliminar un archivo en staging.

```bash
$ git rm --cached archivo.tipo
```

​    Para conocer los archivos añadidos al area de staging utilizamos el comando `git status` o `git status -s` para un  a vista resumida en una linea. 

​    Este comando permite eliminar archivos de git sin eliminar su historial del sistema de versiones, es decir que, solo eliminamos su representación en el staging, no lo hacemos enteramente del proyecto o del historial de git.



```bash
$ git rm --force archivo.tipo
```

​    Elimina el o los archivos del area de staging de git y tambien del disco duro. Aunque podríamos recuperarlo regresando a versiones anteriores.  



```bash
$ git rm --cached 
```

  Elimina los archivos modificados del area de staging, o indice.

---

## commit.

Un _commit_ se usa para confirmar los cambios en el área de _staging_ y guardarlos en el repositorio local en __git__. Sin embargo, antes de guardar algún cambio tienes que decirle a __git__ cuáles cambios quieres incluir de los muchos que puedes haber hecho. Una excelente manera de hacerlo es agregar un mensaje en el _commit_ para identificar tus cambios.

```bash
$ git commit -m "message" 
```

```bash
$ git commit -a -m "message"
```

Esta opción `-a` confirma todos los archivos en el repositorio local, todos los nuevos con modificaciones o incluso eliminados, de forma automatica.

### commit desde un editor de texto.

Al ejecutar `git commit` sin un mensaje u opción, se abrirá tl editor de texto predeterminado para escribir el mensaje del _commit_.

Para configurar el editor "predeterminado" ejecutamos los siguientes comandos:

```bash
$ git config --global core.editor <editor-name>
```

Esto configurará __git__ para usar el editor de texto que prefiramos como predeterminado, puede ser "nano", "emacs", "vim", "typora" o el que se prefiera.

En el editor que se abrirá usa la primera línea para el título, una corta descripción; deja una segunda linea en blanco y todo lo demás es para la descripción, algo mas extenso.

### commit desde linea de comandos.

Podemos definir titulos y mensajes para nuestros _commit_ también desde la consola de comandos, utilizando la opción `-m`.

```bash
$ git commit -m <"Title"> -m <"Description...">
```

### Protocolos y buenas practicas.

#### Categorizar un commit.

- __Feat__: Una nueva característica que se agrega a una aplicación en particular.
- __Fix__: Un parche para un error.
- __Style__: Características o actualizaciones relacionadas con estilos.
- __Refactor__: Refactorizar una sección específica de la base del código.
- __Test__: Todo lo relacionado con pruebas.
- __Docs__: Todo lo relacionado con documentación.
- __Chore__: Mantenimiento regular del código.

### 		log.

Muestra todas las _commits_ en el historias del repositorio, mostrando el _Secure Hash Algorithm_ (SHA), el autor, fecha y mensaje del _commit_.



#### 		Historial de commits.

```bash
$ git log [<options>]
```
​	Permite ver el historial de commits de una rama.


> **Nota:** El listado puede contener una cantidad de commits que no quepa en la ventana del terminal, en ese caso podemos ir a la siguiente página con la barra espaciadora. O puedes moverte mediante los cursores del teclado, arriba y abajo. Salimos de nuevo a la entrada de comandos con "CTRL + z

```bash
$ git log --oneline
```


​	Permite desplegar una lista resumida de los commits en una sola linea.

```bash
$ git log --oneline --graph
```

​	Permite desplegar una lista resumida con una representación grafica del esquema que siguen los commits.



```bash
# vista completa.
$ git log -number

# vista resumida.
$ git log --oneline -number
```

​	Permite definir la cantidad de commits que queremos ver, comenzando siempre por el mas reciente.

```bash
$ git log --stat
```

​	Junto con la información habitual de `git log`, se incluye información sobre los archivos que se han modificado y el número relativo de líneas que se han añadido o eliminado en cada uno de ellos.


> *Nota:* Para salir de la lista de commits presiona la tecla 'q' 


```bash
$ git log -p
```

Esta opción muestra el parche que representa cada confirmación. Se muestra la diferencia completa de cada confirmación, que es la vista más detallada que puedes tener del historial del proyecto.



####  	Localizar un commit.

- En función del comentario del commit:

```bash
# vista completa.
$ git log --grep="text"

# vista resumida.
$ git log --oneline --grep="text"
```

​	Permite conseguir todos los commits cuyos comentarios coincidan con el texto introducido.



- En función del contenido del codigo modificado en el commit:

```bash
$ git log -S"text"
```

​	Permite localizar todos los commits en donde se hayan modificado lineas de codigo que coincida con el texto introducido.

> **Nota:** Git no realiza la busqueda en función e un objeto modificado, sino que interpreta todo el codigo como una hoja de texto plano e identifica los cambios en los que aparezca la palabra indicada. 



- En función de la fecha del commit:

```bash
git log --after="yesterday"

git log --after="yyyy-mm-dd"

git log --before="yyyy-mm-dd"

git log --after="yyyy-mm-dd" --before"yyyy-mm-dd"
```



- En función del autor del commit:

```bash
git log --author="username"
```



- En función del archivo modificado en el commit:

```bash
 # vista completa.
$ git log -- file.type

# vista resumida.
$ git log --oneline -- file.type
```

​	Permite localizar todos aquellos commits en los que intervenga el archivo que se especifique. 

---

### 	Cambios en el ultimo commit.

```bash
git show nombre_del_archivo.tipo
```

​    Permite ver los cambios realizador en el ultimo commit en comparación al ultimo realizado. 

> Nota: El archivo se debe de indicar con el nombre entero y el tipo. ejemplo: archivo.txt 

---

### 	Comparar commits.

```bash
$ git diff id_1 id_2
```

​	Permite ver las diferencias entre dos commits de un mismo archivo. 

> Nota: El numero identificador de cada commit se obtiene ejecutando el comando `git log `.



---

### 	Eliminar commits.

```bash 
$ git rm --cached
```

​	Elimina los archivo del área de Staging, es decir, todos los archivos añadidos al commit realizado y almacenados en el indice de git, pero dejando intacta la copia de trabajo local. Es util cuando se realiza un commit incompleto o en el que se añade un fichero erroneo. 



---



### reset.

Este comando permite restablecer el estado del proyecto o de un archivo en concreto a un estado especifico anterior. Es especialmente útil cuando aún no hemos subido un _commit_ al repositorio remoto.

Sin embargo hay que tener en cuanta que este comando solo remueve los cambios de la zona de _staging_ no del archivo de trabajo.

#### 		Regresar a un commit anterior.

```bash
$ git reset <mode> <commit_id> 
```

Las opciones para `<mode>` son:

- `--soft`: No restablece el fichero índice o el repositorio local, pero restablece el `HEAD` para _commit_. Cambia todos los archivos a cambios a ser _commited_.
- `--mixed`: Restablece el índice, pero no el repositorio local e informa de lo que no se ha actualizado.
- `--hard`: Restablece el índice y el repositorio local. Cualquier cambio en los archivos rastreados en el repositorio desde el _commit_ son descartados.
- `--merge`: Restablece el índice y actualiza los archivos en el repositorio local que son diferentes entre el _commit_ y `HEAD`, pero mantiene los que son diferentes entre el índice y el repo.
- `--keep`: Restablece las entradas del índice, actualiza los archivos en el repo que son diferentes entre el _commit_ y el `HEAD`. Sin un archivo que es diferente entre _commit_ y el `HEAD` tiene cambios locales, el reinicio de cancela.

​    Con el comando `git reset` podemos volver hacia el pasado hasta el comit que indiquemos, aunque existen dis tipos especificos de `reset`, el `--soft` y el `--hard`. 

> Nota: El comando `git reset` nos permite viajar hacia el pasado hacia una versión anterior de nuestro proyecto de git, pero sin la posibilidad de regresar al presente, ya que elimina toda la información porterior al commit que indiquemos como destino. 

   ```bash
   $ git reset <commit_id> --soft
   ```

​    Nos regresa hacia  el commit indicado aunque manteniendo intacto todos los archivos que hayamos añadidos al staging, es decir, solo se notarán aquellas diferencias que no estén en el area de staging, cualquier archivo que no este siendo rastreado por git va a permanecer, mientras que el resto de archivos regresarán al estado que tenían en el commit indicado como destino .

```bash
$ git reset <commit_id> --hard
```

​    Nos regresa hacia el commit anterior indicado eliminando todos los cambios realizados incluyendo los archivos añadidos al area de staging, es una forma efectiva aunque agresiva de regresar al pasado en el codigo..

```bash
$ git reset HEAD <commit_id>

$ git reset --hard HEAD       
 #(going back to HEAD)

$ git reset --hard HEAD^      
 #(going back to the commit before HEAD)

$ git reset --hard HEAD^2     
 #(going back two commits before HEAD)
```

​	Devuelve el archivo a su último commit y este sigue en seguimiento por git, es decir se podrá hacer `add`, `commit`, etc. luego de ejecutar el comando.

---



### revert.

al igual que `reset` este comando deshace _commits_ anteriores, pero si ya has subido un _commit_ a un repositorio remoto, se recomienda que no uses __git__ _reset_, ya que reescribe el historial de _commits_. Esto puede hacer que trabajar en un repositorio con otros desarrolladores y mantener un historial consistente de _commits_ sea mas complicado.

En su lugar es mejor utilizar `git revert`, que deshace los cambios realizados por un _commit_ anterior creando un _commit_ completamente nuevo, todo esto sin alterar el historial de _commits_.

```bash
$ git revert
$ git revert -e
$ git revert -edit
```

---

## Definir PAT.

Para dejar de ingresar el usuario y la contraseña cada vez que ejecutemos un `push` o `pull` basta con ejecutar los siguientes comandos.

1. Dentro del directorio que contiene el repositorio.
2. buscamos el archivo `remote.origin.url` utilizando el comando: `git config -l`.
3. Ejecutamos el comando: `git config remote.origin.url https://{YOUR_USER_NAME}:{PASSWORD}@github.com/{YOUR_USER_NAME}/{REPOSITORY_NAME}.git`.


---

