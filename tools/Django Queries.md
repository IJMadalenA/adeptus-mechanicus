# Django Queries.

​	

Django permite operar sobre el modelo de datos de la aplicación en la que estemos trabajando a través de una abstracción de SQL que nos permite recuperar, actualizar, eliminar y crear objetos desde un lenguaje mucho mas amigable y parecido a la sintaxis de Python. 

> Daré por sentado que ya sabes crear un modelo en Django, así que si no lo sabes pues, haber estudiao. 
> 	[Django Models Documentation.](https://docs.djangoproject.com/en/3.2/topics/db/models/)

---









---

# [Django Models.](https://docs.djangoproject.com/es/3.2/topics/db/models/)

## [Crear o Modificar objetos.](https://docs.djangoproject.com/en/3.2/topics/db/queries/#creating-objects)

​	Django ofrece una manera bastante sencilla de crear objetos e ingresarlos en los modelos (es decir, las tablas) de nuestra base de datos. Basta con crear una variable que contenga el modelo al que queremos añadir información, y se ingresen el campo y el valor que deseamos esté contenido en él como si estos fueran parámetros de la variable, o al menos los parámetros obligatorios dentro del modelo. Sin embargo esto no guardará ninguna información en el modelo ni lo modificará, para ello, y posterior a la creación de la variable que alberga el modelos con los parámetros y datos, se debe llamar a la función `.save()` que el modelo hereda del objeto [`models.Model`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model), propio de Django y que sirve como plantilla sobre la cual trabajar. 

​	Esta es la manera en la que Django traduce el lenguaje SQL a una sintaxis propia de Python. 

ejemplo:

````python
from app.models import Model_X

a = Model(field_1 = 'value_1', field_2 = 'value_2')
a.save()
````

​	Al ejecutar la función `.save()` del modelo de datos, Django interpreta los datos que hemos ingresado en una secuencia SQL y se encarga de ejecutar la tarea  de formar encubierta y prescindiendo de nosotros. 

### 		¿Que pasa cuando ejecutamos la función[`.save()`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model.save)?

1. __Emisión de la señal _pre_save_:__ Se emite una señal de pre-guardado o _pre_save_. Esta señal _pre_save_ permite que cualquier función que escuche o  dependa de la ejecución del `.save()` se ejecute. 

2. __Se preprocesan los datos:__ Se llama al método _pre_save_ de cada campo para realizar cualquier modificación de datos automatizada que hayamos diseñado nosotros o que sean funciones ya diseñadas como por ejemplo loa campos de auto_now .

3. __Preparar la data para la base de datos:__ Se llama al método `get_db_prep_save()` de cada campo que proporcione su valor actual en un tipo de datos que se pueda escribir en la base de datos.

   ​	La mayoría de los campos no requieren de una preparación de datos, ya que los tipos de datos simples como `int` o `str`, están listos para ser escritos como un objeto de Python. Sin embargo, los datos de tipo mas complejo a menudo requieren alguna modificación.

   ​	Por ejemplo, los campos DateField usan un objeto de fecha y hora de Python para almacenar datos. Las bases de datos no almacenan objetos de fecha y hora, por lo que el valor del campo debe convertirse en una cadena de fecha compatible con ISO para insertarlo en la base de datos.

4. __Insertar los datos en la base de datos:__ Estos datos ya preparados y preprocesados son traducidos a una declaración SQL para su inserción en la base de datos.

5. __Emisión de la señal _post_save_:__ Se envía la señal _post_save_, que permite que cualquier función que dependa de ella se ejecute, muy parecido como ocurre con la señal _pre_save_. 



### 	¿Cómo sabe Django cuando la función [`.save()`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model.save) es un __INSERT__ o un __UPDATE__?

​	Django se abstrae de tener que especificar, en una sentencia SQL, si el propósito de la función [`.save()`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model.save) es actualizar un valor o insertarlo en la base de datos. 

​	Si el objeto que llama a la función [`.save()`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model.save) no contiene una PK predeterminada, Django sigue el siguiente algoritmo:

- Si el atributo `PK` del objeto se establece en un valor definido como `True`, es decir, un valor no `None` o una `str` vacía, Django ejecuta un __UPDATE__, debido a que reconoce el proceso como la actualización de los datos de un objeto ya existente que identifica por la `PK` que nosotros ingresamos o que pertenece por defecto al objeto que manejamos.
- Si el objeto no tiene establecido un valor para su atributo `PK` o si el atributo `PK` no existe, Django ejecuta un __INSERT__, ya que al no poder vincularlo con un objeto existente, Django crea uno nuevo dentro del modelo con los datos que nosotros especificamos como parámetros. 

---



### [Forzar un __INSERT__ o __UPDATE__](https://docs.djangoproject.com/es/3.2/ref/models/instances/#forcing-an-insert-or-update)_: 

​	Es posible, aunque muy extraño que esto sea necesario, forzar al método [`.save()`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model.save) a que realice un __SQL INSERT__ y que no  realizar un __UPDATE__ o vice versa. Para estos casos basta con definir el parámetro `force_insert=True` o `force_update=True` dentro del método [`.save()`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model.save). Obviamente introducir ambos parámetros como `True` devendría en un error. 



### Actualizar atributos en función de campos existentes:

​	Actualizar campos existentes o ejecutar operaciones aritméticas sobre ellos es sumamente simple, basta con localizar el objeto que queremos modificar, especificar el campo,  realizar nuestra operación y finalmente llamar a la función [`.save()`](https://docs.djangoproject.com/en/3.2/ref/models/instances/#django.db.models.Model.save) del objeto. por ejemplo:

```python
product = Product.objects.get(name='Venezuelan Beaver Cheese')
product.number_sold += 1
product.save()
```

​	El proceso puede hacerse robusto, evitando una [condición de carrera](https://es.wikipedia.org/wiki/Condición_de_carrera), así como un poco más rápido al expresar la actualización en relación con el valor del campo original, en lugar de como una asignación explícita de un nuevo valor en una nueva variable almacenada en memoria. Django proporciona expresiones F para realizar este tipo de actualización relativa. 

- > ​	La __condición de carrera__ es un escenario en el que dos o más subprocesos intentan acceder a un recurso compartido, como una variable o un código, y cambiarlo al mismo tiempo debido a una ejecución indeterminada del subproceso, pero debido a la naturaleza del dispositivo o sistema, las operaciones deben de realizarse en la secuencia adecuada para que se realicen correctamente.
  >
  > ​	En la memoria del ordenador puede ocurrir una condición de carrera si se reciben comandos para leer y escribir una gran cantidad de datos en casi el mismo instante, y la máquina pretende sobrescribir algunos o todos los datos antiguos cuando aún se están utilizando.

​	Usando  [__F() expressions__](https://docs.djangoproject.com/es/3.2/ref/models/expressions/#f-expressions), el ejemplo anterior se expresa como:

```python
from django.db.models import F

product = Product.objects.get(name='Venezuelan Beaver Cheese')
product.number_sold = F('number_sold') + 1
product.save()
```

---



### Especificar que campos guardar.

​	Si al método `.save()` se le pasa una lista con nombres de campos en el argumento `update_fields`, solo se actualizarán los campos nombrados en la lista. Esto resultaría en un pequeño beneficio de rendimiento al evitar que todos los campos del modelo se actualicen en la base de datos. 

```python
product.name = 'Name changed again'
product.save(update_fields=['name'])
```

​	El argumento `update_fields` admite cualquier objeto iterable que contenga `str`. Si ingresamos un objeto iterable vacío, se omitirá el guardado y un valor `None` ejecutará el guardado con todos los campos.

​	Definir un argumento `update_fields` forzará una actualización, por lo que intentar forzar un `insert` devendrá en un error.

---



## [Eliminar objetos.](https://docs.djangoproject.com/es/3.2/ref/models/instances/#django.db.models.Model.delete)

​	`Model.delete(*using=DEFAULT_DB_ALIAS*, *keep_parents=False*)`

​	Este método solo elimina el o los objetos en la base de datos, sin embargo la instancia de Python seguirá existiendo y seguirá teniendo datos en sus campos. 

​	Este método retorna una tupla con el numero de objetos eliminados en primer lugar y en segundo lugar un diccionario con el número de eliminaciones por tipo de objeto. Por ejemplo:

```python
>>> one_entry_blog.delete()
(1, {'weblog.Entry': 1})
```

​	También es posible eliminar una gran cantidad de objetos en un modelo, ya cada _QuerySet_ tiene un método `.delete()` que elimina todos los miembros de ese _QuerySet_.

```python
>>> Entry.objects.filter(pub_date__year=2005).delete()
(5, {'webapp.Entry': 5})
```

​	Una consideración a la hora de eliminar múltiples objetos de la base de datos a través de la sintaxis de Django, como ocurre en el ejemplo descrito anteriormente, es que siempre que sea posible Django ejecutará la orden en SQL, por lo que el método `.delete()` de cada objeto individual no será llamado, esta es importante especialmente si hemos modificado el comportamiento de la función `.delete()` en el modelo de datos, y si queremos asegurarnos de que el método `.delete()` sea llamado individualmente tendríamos que iterar sobre el _QuerySet_ eliminando uno a uno los objetos que lo integran, en lugar de usar el método `.detete()`.

​	El método `.delete()` cuenta con mecanismos de seguridad para prevenir que accidentalmente se solicite eliminar por error todos los objetos albergados en una base de datos de la siguiente manera: `Entry.objects.delete()`. Si se desea eliminar todos los objetos se debe de declarar de manera explicita de la siguiente manera: 

```python
Entry.objects.all().delete()
```

---



## [Expresiones integradas.](https://docs.djangoproject.com/es/3.2/ref/models/expressions/#built-in-expressions)

​	Estas expresiones están definidas en `django.db.models.expressions` y `django.db.models.aggregates` pero por conveniencia estas pueden ser importadas desde `django.db.models`.





### [F() expressions.](https://docs.djangoproject.com/es/3.2/ref/models/expressions/#f-expressions)

​	Un objeto `F()` es una herramienta que posibilita referirse a los valores dentro del campo de un modelo ahorrándonos el tener que realizar operaciones sobre la base de datos para extraer el valor del campo y almacenarlo en memoria como una variable para luego poder trabajar sobre él. En este caso un objeto `F()` es la representación del valor contenido en el campo que requerimos para trabajar.

​	En su lugar, Django usa el objeto `F()` para generar una expresión __SQL__ que describa la operación que requerimos hacer en la base de datos.



​	Ejemplo de una operación normal sobre el campo de una base de datos:

````python
reporter = Reporters.objects.get(name='Tintin')
reporter.stories_filed += 1
reporter.save()
````

​	En este caso almacenamos el objeto reportero que sobre el que deseamos trabajar dentro de una variable, y lo hemos modificado utilizando sencillos operadores de Python, y luego hemos guardado el objeto en la base de datos llamando al método `.save()`.   Sin embargo podemos utilizar le expresión `F()`de la siguiente forma:

```python
from django.db.models import F

reporter = Reporters.objects.get(name='Tintin')
reporter.stories_filed = F('stories_filed') + 1
reporter.save()
```

​	Aunque `reporter.stories_filed = F ('stories_filed') + 1` parece una asignación de valor normal de Python a un atributo de instancia, de hecho es una construcción SQL que describe una operación en la base de datos.

​	Cuando Django encuentra una instancia de `F()`, anula la operación estándar de Python para crear una expresión encapsulada de __SQL__. En este caso, uno que extrae el valor de la base de datos y realiza una suma sobre el valor representado por `reportes.stories_filed`.

​	Cualquiera que sea el valor que esté o haya estado dentro de `reporter.stories_field`, Python nunca llega a saberlo, ya que será la base de datos la que se ocupe enteramente de él. Todo lo que Python hace a través de la clase `F()`es crear la sintaxis __SQL__ que hace referencia al campo y describe la operación.

​	Para acceder al nuevo valor guardado de esta manera, utilizando la expresión `F()`, el objeto debe de ser cargado de nuevo. 

```python
reporter = Reporters.objects.get(pk=reporter.pk)
# o aun mas conciso:
reporter.refresh_from_db()
```

---



#### F() expression para realizar Updates.

​	La expresión `F()`se puede usar en QuerySets de instancias de objetos con `update()`. Esto reduce las dos queries que habitualmente usariamos, el `get()`y el `save()` a una sola, de esta manera:

```python
reporter = Reporters.objects.filter(name='Tintin')
reporter.update(stories_filed=F('stories_filed') + 1)
```

​	También podemos usar el método `update()` para modificar el campo de múltiples objetos, lo que podría ser mucho más rápido que extraerlos todos desde la base de datos, recorrerlos, incrementar el valor del campo de cada uno y guardar cada uno en la base de datos.

```python
Reporter.objects.all().update(stories_filed=F('stories_filed') + 1)
```

​	Por lo tanto `F()`ofrece ventajas de rendimiento respecto a:

- Operar sobre la base de datos en vez de hacerlo con Python.
- Reducir el numero de queries que algunas operaciones requieren hacer.
- Para transformar el campo de una base de datos (pero solo desde Python 3.2).

---



#### Evitar una [condición de carrera](https://es.wikipedia.org/wiki/Condición_de_carrera) utilizando `F()`.

​	Otro beneficio útil de `F()` es que hacer que la base de datos, en lugar de Python, obtenga o actualice el valor de un campo evitando una condición de carrera. 

​	Si dos subprocesos de Python ejecutan el código del primer ejemplo anterior, un subproceso podría recuperar, incrementar y guardar el valor de un campo después de que el otro lo haya recuperado de la base de datos. El valor que guarda el segundo hilo se basará en el valor original; se perderá el trabajo del primer hilo. Si la base de datos es responsable de actualizar el campo, el proceso es más robusto: solo actualizará el campo en función del valor del campo en la base de datos cuando se ejecute guardar () o actualizar (), en lugar de hacerlo según su valor cuando se recuperó la instancia. 

> ​	Un [__Hilos__](https://es.wikipedia.org/wiki/Hilo_(informática)) no es mas que una secuencia de tareas encadenadas y muy simples; que además puede ser ejecutado al mismo tiempo que otra tarea.
>
> ​	Los [__Hilos__](https://es.wikipedia.org/wiki/Hilo_(informática)) que comparten los mismos recursos, sumados a estos recursos, son en conjunto conocidos como un __[proceso](https://es.wikipedia.org/wiki/Proceso_(informática))__. El hecho de que los hilos de ejecución de un mismo proceso compartan los recursos hace que cualquiera de estos hilos pueda modificar estos recursos. <u>Cuando un hilo modifica un dato en la memoria, los otros hilos acceden a ese dato modificado inmediatamente.</u>

---



#### Persistencia de la asignación con `F()`.

​	Los objetos`F()` asignados a los campos del modelo persisten después de guardar la instancia del modelo, y se aplicará a cada `save()`. 

​	Por ejemplo:

```python
reporter = Reporters.objects.get(name='Tintin')
reporter.stories_filed = F('stories_filed') + 1
reporter.save()

reporter.name = 'Tintin Jr.'
reporter.save()
```

​	`stories_filed` se actualiza dos veces en este caso. Si inicialmente es 1, el valor final será 3, ya que el valor de `stories_filed` no es un entero, sino la abstracción de __SQL__ que Django genera a través de la clase `F()`, y cada vez que ejecutamos el `.save()`, estamos ejecutando la función de __SQL__ . Esta persistencia se puede evitar volviendo a cargar el objeto modelo después de guardarlo, por ejemplo usando `refresh_from_db()`, de esta forma podemos volver a disponer del objeto y guardarlo sin que se ejecute ninguna acción indeseada a nuestras espaldas.

​	un ejemplo mas grafico podría ser:

````python 
reporter = Reporters.objects.get(id=1)
# En este primer caso identificamos el valor ya definido en el objeto.
print(reporter.stories_filed)
>>> 1

reporter.stories_filed = F('stories_filed') + 1
# Aquí no estamos modificando el campo sino simplemente se sustituye por una operación de SQL.
reporter.save()
# Al ejecutar la función .save() se ejecuta ademas la operación SQL definida anteriormente.
print(reporter.stories_filed)
>>> 2

reporter.name = 'Tintin Jr.'
reporter.save()
# Independientemente del campo que modifiquemos la operación SQL albergada en el campo stories_filed se ejecutará.
print(reporter.stories_filed)
>>> 3

reporter.refresh_from_db()
# Al recuperar de nuevo el objeto se vuelven a definir todos sus valores por defecto.
reporter.name = 'Tintin'
print(reporter.stories_filed)
>>> 3
````

---



#### Usar `F()` en filtros.

​	El objeto `F()` es útil en filtros de QuerySets, en donde es posible filtrar un conjunto de objetos con criterios basados en los valores reales en el campo de la base de datos en lugar de en los valores almacenados en Python.

​	Se pueden utilizar las expresiones `F()` para comparar campos de un mismo modelo y estas referencias se pueden utilizar en filtros de consulta para comparar los valores de dos campos diferentes en la misma instancia de modelo.

​	Por ejemplo, si queremos comparar el tamaño del numero contenido en un campo común de un modelo respecto a un objeto en especifico y obtener solo aquellos objetos cuyo campo en común sea mayor, podríamos realizar la siguiente query:

```python
from django.db.models import F
Entry.objects.filter(number_of_comments__gt=F('number_of_pingbacks'))
```

​	De esta manera estamos haciendo la comparación del objeto respecto al valor contenido en la base de datos en ese momento, y no en el valor que hayamos guardado en una variable.

​	Django admite además la implementación de cualquier operación aritmética sobre un objeto `F()`, tanto con constantes como con otros objetos `F()`.

```python
# Es posible realizar tanto sumas, resta, multiplicación, división y potenciación.
Entry.objects.filter(number_of_comments__gt= F('number_of_pingbacks') * 2)

# Tambien es posible sumar dos campos a traves de una expresión F(), siempre que sean del mismo tipo.
Entry.objects.filter(rating__lt= F('number_of_comments') + F('number_of_pingbacks'))
```

​	También es posible utilizar la notación con doble barra baja ('_underscore_') para abarcar relaciones en un objeto `F()`. Un objeto `F()` con una doble barra baja introducirá cualquier combinación necesaria para acceder al objeto relacionado, esto de manera idéntica a como se realizaría en una query normal de Django. 

​	Por ejemplo, y tomando como base un modelo de blog, compuesto por entradas (_'Entry'_) y en donde cada entrada contiene una relación con la instancia del autor y del blog, por lo que la manera de obtener todas las entradas donde el nombre del autor es el mismo que el nombre del blog, podríamos crear esta consulta:

```python
Entry.objects.filter(authors__name= F('blog__name'))
```

​	En este ejemplo manejamos al modelo 'Entry' (todas las entradas del blog) y filtramos en función del nombre del autor de la entrada, accediendo al campo 'authors' que corresponde a una __FK__ del modelo 'author' de donde obtenemos el nombre a través de la notación de doble barra baja ('_double underscore_'), y seleccionando aquellos cuyo nombre sea igual que el nombre del blog, en donde el campo 'blog' también es una __FK__ y accedemos de la misma manera que hicimos con el campo 'author'. 

​	Para manejar campos de __fecha y hora__, se pueden sumar o restar fechas utilizando un objeto __Timedelta__ sobre el campo respresentado en un objeto `F()`. Un ejemplo de esto:

```python
from datetime import timedelta
Entry.objects.filter(mod_date__gt=F('pub_date') + timedelta(days=3))
```

​	La expresión `F()` también admite utilizar notación de doble barra baja ('_double underscore_') para acceder a campos específicos del objeto `datetime` de la siguiente forma:

```python
Entry.objects.filter(pub_date__year=F('mod_date__year'))

Entry.objects.aggregate(first_published_year=Min('pub_date__year'))
```

---



#### Usar `F()` con anotaciones.

​	`F()` se puede utilizar para crear campos dinámicos en los modelos, combinando diferentes campos con aritmética, por ejemplo:

```python
company = Company.objects.annotate(chairs_needed=F('num_employees') - F('num_chairs'))
```

---



#### Usar `F()` para ordenar valores `null`.

​	Utilizando el argumento `nulls_first` o `nulls_last` en la función `.desc()` o `.asc()` sobre la expresión `F()` para determinar el orden de los campos con valores nulos. Por defecto este orden esta determinado por la base de datos.

​	Por ejemplo:

```python
from django.db.models import F
Company.objects.order_by(F('last_contacted').desc(nulls_last=True))
```

---



# [Managers.](https://docs.djangoproject.com/es/3.2/topics/db/managers/#django.db.models.Manager)

​	Un __Manager__ es la interfaz a través de la cual se proporcionan operaciones de consulta de la base de datos a los modelos de Django. 

​	Es la interface entre Django y la base de datos. 

​	Existe al menos un administrados para cada modelo en una aplicación Django.

