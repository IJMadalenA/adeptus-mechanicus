# git.

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

```git
$ git branch -d nombre_rama
```

​	En el caso de que esa rama contenga trabajos sin fusionar, el comando anterior nos devolverá el siguiente error:

```git
error: The branch 'nombre-rama' is not an ancestor of your current HEAD.
If you are sure you want to delete it, run 'git branch -D nombre-rama'.
```

​	Si aún así queremos eliminar esa rama, se puede forzar el borrado de la siguiente manera:

```git
$ git branch -D nombre-rama
```

​	En el caso de querer eliminar una rama del repositorio remoto, la sintaxis será la siguiente:

```git
$ git push origin :nombre-rama
```

​	Y de esta forma, desaparecerá la rama nombre-rama del servidor.

---

## branch.

### 	Visualizar ramas.

> ```
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

```git
$ git rm --cached archivo.tipo
```

​    Para conocer los archivos añadidos al area de staging utilizamos el comando `git status` o `git status -s` para un  a vista resumida en una linea. 

​    Este comando permite eliminar archivos de git sin eliminar su historial del sistema de versiones, es decir que, solo eliminamos su representación en el staging, no lo hacemos enteramente del proyecto o del historial de git.



```git
$ git rm --force archivo.tipo
```

​    Elimina el o los archivos del area de staging de git y tambien del disco duro. Aunque podríamos recuperarlo regresando a versiones anteriores.  



```git
$ git rm --cached 
```

  Elimina los archivos modificados del area de staging, o indice.

---

## commit.

### 	Historial de commits.

```git
$ git log [<options>]
```
​	Permite ver el historial de commits de una rama.

> **Nota:** El listado puede contener una cantidad de commits que no quepa en la ventana del terminal, en ese caso podemos ir a la siguiente página con la barra espaciadora. O puedes moverte mediante los cursores del teclado, arriba y abajo. Salimos de nuevo a la entrada de comandos con "CTRL + z

```git
$ git log --oneline
```

​	Permite desplegar una lista resumida de los commits en una sola linea.

```git
$ git log --oneline --graph
```

​	Permite desplegar una lista resumida con una representación grafica del esquema que siguen los commits.

```git
git log --stat
```

​    Muestra el numero de lineas que se han cambiado de forma resumida.

```git 
```





```git
# vista completa.
$ git log -number

# vista resumida.
$ git log --oneline -number
```

​	Permite definir la cantidad de commits que queremos ver, comenzando siempre por el mas reciente.



```git 
$ git log --stat
```

​	Junto con la información habitual de `git log`, se incluye información sobre los archivos que se han modificado y el número relativo de líneas que se han añadido o eliminado en cada uno de ellos.

> *Nota:* Para salir de la lista de commits presiona la tecla 'q' 

```git 
$ git log -p
```

Esta opción muestra el parche que representa cada confirmación. Se muestra la diferencia completa de cada confirmación, que es la vista más detallada que puedes tener del historial del proyecto.

---

### 	Localizar un commit.

- En función del comentario del commit:

```git
# vista completa.
$ git log --grep="text"

# vista resumida.
$ git log --oneline --grep="text"
```

​	Permite conseguir todos los commits cuyos comentarios coincidan con el texto introducido.



- En función del contenido del codigo modificado en el commit:

```git
$ git log -S"text"
```

​	Permite localizar todos los commits en donde se hayan modificado lineas de codigo que coincida con el texto introducido.

> **Nota:** Git no realiza la busqueda en función e un objeto modificado, sino que interpreta todo el codigo como una hoja de texto plano e identifica los cambios en los que aparezca la palabra indicada. 



- En función de la fecha del commit:

```git
git log --after="yesterday"

git log --after="yyyy-mm-dd"

git log --before="yyyy-mm-dd"

git log --after="yyyy-mm-dd" --before"yyyy-mm-dd"
```



- En función del autor del commit:

```git
git log --author="username"
```



- En función del archivo modificado en el commit:

```git
 # vista completa.
$ git log -- file.type

# vista resumida.
$ git log --oneline -- file.type
```

​	Permite localizar todos aquellos commits en los que intervenga el archivo que se especifique. 

---

### 	Cambios en el ultimo commit.

```git
git show nombre_del_archivo.tipo
```

​    Permite ver los cambios realizador en el ultimo commit en comparación al ultimo realizado. 

> Nota: El archivo se debe de indicar con el nombre entero y el tipo. ejemplo: archivo.txt 

---

### 	Comparar commits.

```git
$ git diff id_1 id_2
```

​	Permite ver las diferencias entre dos commits de un mismo archivo. 

> Nota: El numero identificador de cada commit se obtiene ejecutando el comando `git log `.



---

### 	Eliminar commits.

```git 
$ git rm --cached
```

​	Elimina los archivo del área de Staging, es decir, todos los archivos añadidos al commit realizado y almacenados en el indice de git, pero dejando intacta la copia de trabajo local. Es util cuando se realiza un commit incompleto o en el que se añade un fichero erroneo. 



---



### 	Regresar a un commit anterior.

```git
$ git reset <commit_id> 
```

​    Con el comando `git reset` podemos volver hacia el pasado hasta el comit que indiquemos, aunque existen dis tipos especificos de `reset`, el `--soft` y el `--hard`. 

> Nota: El comando `git reset` nos permite viajar hacia el pasado hacia una versión anterior de nuestro proyecto de git, pero sin la posibilidad de regresar al presente, ya que elimina toda la información porterior al commit que indiquemos como destino. 

   ```git
   $ git reset <commit_id> --soft
   ```

​    Nos regresa hacia  el commit indicado aunque manteniendo intacto todos los archivos que hayamos añadidos al staging, es decir, solo se notarán aquellas diferencias que no estén en el area de staging, cualquier archivo que no este siendo rastreado por git va a permanecer, mientras que el resto de archivos regresarán al estado que tenían en el commit indicado como destino .

```git
$ git reset <commit_id> --hard
```

​    Nos regresa hacia el commit anterior indicado eliminando todos los cambios realizados incluyendo los archivos añadidos al area de staging, es una forma efectiva aunque agresiva de regresar al pasado en el codigo..

```git
$ git reset HEAD <commit_id>

$ git reset --hard HEAD       
 #(going back to HEAD)

$ git reset --hard HEAD^      
 #(going back to the commit before HEAD)

$ git reset --hard HEAD^2     
 #(going back two commits before HEAD)
```

​	Devuelve el archivo a su último commit y este sigue en seguimiento por git, es decir se podrá hacer `add`, `commit`, etc. luego de ejecutar el comando.