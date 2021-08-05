# [ContentTypes.](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/)

​	Django incluye una aplicación llamada `ContentTypes` que puede rastrear todos los modelos instalados en el proyecto de Django, proveyéndonos de una interfaz genérica de alto nivel para trabajar con los modelos de datos. 

​	Las instancias de `ContentType` representan y almacenen información sobre los modelos instalados en el proyecto, y son creadas automáticamente luego de que se instale un nuevo modelo en la aplicación. Estas instancias poseen métodos que permiten realizar _Queries_ sobre los modelos y también posee un administrados personalizado que agrega métodos para trabajar sobre las instancias.

​	Las relaciones entre los modelos y `ContentType` se pueden utilizar para habilitar relaciones “genéricas” entre una instancia de uno de sus modelos y las instancias de cualquier modelo que se haya creado e instalado.

## [El modelo `ContentType`.](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/#the-contenttype-model)

## [Métodos de las instancias `ContentType`.](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/#methods-on-contenttype-instances)

## [`ContentTypeManager`.](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/#the-contenttypemanager)





## Relaciones Genéricas.

​	Aparte de las relaciones entre modelos a través de `FK`, `ContentType` permite ir un paso más allá y habilitar relaciones verdaderamente genéricas (también llamadas “polimórficas”) entre modelos.

​	Dependiendo de su uso, las `GenericForeignKey` pueden ser perjudiciales.

​	[Articulo menos ambiguo que la ambigua documentación de Django.](https://dipbazz.medium.com/how-and-when-to-use-genericforeignkey-in-django-ad88202be0f)

​	

​	