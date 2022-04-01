# Doker.



## Los tres grandes problemas del desarrollo de software.

- Construir.
- Distribuir.
- Ejecutar.

### Construir software.

​	Este problema no se reduce exclusivamente a escribir código, que es lo mas simple de todo, sino que se hace referencia a problemáticas como:

​	__Entorno de desarrollo__: Aquí concebimos una serie de puntos a tener en cuenta, como la versión del lenguaje en el que se construye el proyecto, si está actualizada o es la correcta; si nuestro código y entorno de ejecución, en el que estamos desarrollando es equivalente al de producción y al de nuestros compañeros de trabajo, si no hay desfaces en la versión de algún lenguaje o dependencia que pueda generar conflictos; la atención a la disponibilidad de los servicios externos, la versión de la base de datos si es compatible y se puede operar con ella, entre otras problemáticas. 

> ​	__Entorno de ejecución:__ Es un servicio de máquina virtual que sirve como base de software para la ejecución de programas. 
>
> ​	Todos los programas necesitan alguna biblioteca de tiempo de ejecución que les permita interactuar con los otros recursos de la máquina, como entradas de usuarios, archivos de disco, comunicaciones de red, etc.  y para evitar conflictos con dependencias, recursos o programas del sistema operativo, se encapsula al programa de interés, en el que estemos trabajando, en un entorno de ejecución que posea todas las características necesarias para su funcionamiento pero aislándolo del resto del sistema. 

​	__Distribuir software:__ El código tiene que transformarse en un _artefacto_, o varios, que puedan ser transportados a donde tengan que ser ejecutados.

> ​	Un __artefacto__ es un producto tangible resultante del proceso de desarrollo de software. 

​	Los problemas que aquí se pueden presentar tienen que ver generalmente con los artefactos que se generan para poder distribuir nuestro código. Por ejemplo si existen divergencias entre el repositorio de los artefactos, porque puede que nuestro producto genere diversos tipos de artefactos, y el repositorio no sea compatible con todos, o si existen divergencias entre los mismos artefactos y la versión del artefacto, desde su nomenclatura, como se definen las versiones y su distribución. 

​	__Ejecución del software:__ La máquina donde se escribe el software siempre es distinta a la máquina donde se ejecuta de manera productiva. Aquí la problemática es muy similar al del entorno de desarrollo en el sentido de que el código, para ser ejecutado, necesita de ciertos recursos específicos a su disposición, y es necesario que estén presentes en el entorno productivo en donde se ejecuta, porque sino no sería compatible, obviamente. Además de las dependencias, que deben de ser compatibles con el software y los recursos externos. Por ultimo una problemática a la hora de ejecutar en producción es el hardware y sus posibles limitaciones. 



## Virtualización.

​	Es la versión virtual que utiliza el software para imitar las características de algún recurso tecnológico, como hardware, un sistema operativo, un dispositivo de almacenamiento o recurso de red. 

### Máquina virtual y su diferencia con los contenedores.

​	Una __máquina virtual__ no es mas que un sistema operativo virtualizado que corre dentro de nuestro sistema operativo y que nos permite ejecutar programas de manera aislada, permitiendo generar un ambiente propicio para el programa. Sin embargo esto conlleva múltiples problemáticas, ya que las maquinas virtuales tienen un alto peso debido a que los sistemas operativos manejan magnitudes de gigabytes de peso, son costosos de mantener, repiten muchísimo código ya que es un sistema operativo idéntico o casi idéntico al que le sirve de hospedador, es lento y existen muchas versiones de empaquetar una maquina virtual y de distribuirla. 

​	Un __contenedor__ o el proceso de __containerización__, es el empleo de contenedores para construir y desplegar software. Son espacios virtuales que provee el sistema operativo, de forma que parecen una computadora real para los programas que se ejecutan dentro de ellos.

​	Los contenedores poseen múltiples ventajas respecto a las maquinas virtuales, como lo son su flexibilidad y adaptables, ya que toda aplicación se puede meter dentro de un contenedor; son livianos, ya que reutilizan el kernel de la maquina anfitriona, y lo comparten entre si; son portables, por lo que pueden ser ejecutados de la misma manera en cualquier máquina; tienen un bajo acoplamiento ya que dentro de el tiene todo lo necesario para poder ejecutar el software sin afectar a otros contenedores; son altamente escalables y además de ser altamente seguros. 

![Preview](https://www.redeszone.net/app/uploads/2016/02/docker-vs-virtual-machines.png)



## Contenedores.

​	Un __contenedor__ es, a groso modo, una _maquina virtual liviana_.

​	Es una agrupación de procesos que corren nativamente en la maquina, pero están aislados del resto del sistema. Es una agrupación lógica, a diferencia de una maquina virtual que es la virtualización de una unidad física, un contenedor es una agrupación lógica que corre de manera nativa en la maquina anfitriona, pero con limitaciones de acceso a la maquina anfitriona. 

### Ciclo de vida de los contenedores.

​	Un contenedor se ejecuta y mantiene en ejecución en función de su proceso principal o _main process_, por lo tanto, mientras este proceso se ejecute y mantenga en ejecución también lo estará haciendo el contenedor hasta el momento en el que el _main process_ se detenga y sin importar que hayan otros subprocesos en ejecución, y , en ese momento el contenedor ejecutará automáticamente el comendo ``exits`` y se apagará.

​	Por lo tanto, cuando se corre un contenedor se está corriendo un proceso, y la vida del contenedor depende de la del proceso. 

### Exponiendo contenedores.



