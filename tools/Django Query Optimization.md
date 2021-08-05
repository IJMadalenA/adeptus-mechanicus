# Django Query Optimization.

​	Este documento reune enlaces, muchos enlaces, a la documentación relevante y agrega varios consejos, resumiendo la ya resumida documentación, bajo una serie de títulos que describen los pasos a seguir para intentar optimizar el uso de la base de datos.

---



## [`QuerySet.explain()`](https://docs.djangoproject.com/en/3.2/ref/models/querysets/#explain)

​	Este método retorna un `str` detallando la ejecución de un _QuerySet_, con información como los índices o combinaciones que se utilizarían. 

```python
>>> print(Blog.objects.filter(title='My Blog').explain())

Seq Scan on blog  (cost=0.00..35.50 rows=10 width=12)
  Filter: (title = 'My Blog'::bpchar)
```

​	El método `.explain()` es compatible con todas las bases de datos integradas, exceptuando a Oracle.

​	La cantidad de información recibida también dependerá de la base de datos implementada, entonces para obtener indicadores extras se pueden implementar los siguientes argumentos utilizando como ejemplo una consulta a una base de datos de _PostgreSQL_.

```python
>>> print(Blog.objects.filter(title='My Blog').explain(verbose=True, analyze=True))

Seq Scan on public.blog  (cost=0.00..35.50 rows=10 width=12) (actual time=0.004..0.004 rows=10 loops=1)
  Output: id, title
  Filter: (blog.title = 'My Blog'::bpchar)
Planning time: 0.064 ms
Execution time: 0.058 ms
```

---



## [`django-debug-toolbar`](https://github.com/jazzband/django-debug-toolbar/)

​	Este es un proyecto externo que supervisa la base de datos directamente, es un conjunto configurable de paneles que muestra diversa información de depuración sobre la solicitud y la respuesta. 

---



## Técnicas estándar de optimización.

### [Indexación.](https://es.wikipedia.org/wiki/Índice_(base_de_datos))

---



### [Entender los _QuerySets_.](https://docs.djangoproject.com/es/3.2/topics/db/optimization/#understand-querysets)

#### [_Lazy QuerySets_](https://docs.djangoproject.com/es/3.2/topics/db/queries/#querysets-are-lazy)

​	En Django los _QuerySets_ son ‘_lazy_’, es decir, que crear o escribir una _Query_ no implica ninguna actividad de la base de datos hasta el momento en el que dicha _Query_ sea requerida. 



#### [Evaluación del _QuerySet_](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#when-querysets-are-evaluated)

​	De forma interna, un _QuerySet_ puede ser construido, filtrado, dividido y realizar diversas operaciones sin tener que pasar por la base de datos, ya que no se recurre a la base de datos hasta que se actúa sobre el _QuerySet_. 

- __Iterable:__ Los _QuerySets_ son __iterables__, y ejecuta la consulta a la base de datos la primera vez que se itera sobre él.

- __Slicing:__ Se puede aplicar ___slicing___ sobre un _QuerySet_ para dividirlo mediante el ___slicing___ propio de Python, y es el equivalente a las clausulas `LIMIT` y `OFFSET`de SQL.

   ````python
   >>> Entry.objects.all()[:5]
   #  esto retorna los primeros 5 objetos. traducción de LIMIT 5 en SQL.
   ````

   La indexación negativa no está permitida `Entry.objects.all()[-1]`. 

-  [__Picking / Caching__](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#pickling-querysets).

- [__`repr()`:__](https://www.programiz.com/python-programming/methods/built-in/repr) Función muy [parecida a `print()`](https://www.geeksforgeeks.org/str-vs-repr-in-python/), con la diferencia de que esta ultima esta creada para ser legible por una persona, mientras que `repr()` imprime una representación precisa del objeto, utilizado generalmente para *debugging* . 

   ​	La función `print()` utiliza el método especial `__str__` del objeto para mostrar la representación del objeto, mientras que `repr()` se vale del método especial `__repr__` del objeto. 
   
   

#### Almacenamiento del data en memoria.

​	[Caching and _QuerySets_](https://docs.djangoproject.com/es/3.2/topics/db/queries/#caching-and-querysets)

​	Una _Query_ recién creada no es almacenada en __cache__, para que esta sea guarda se debe utilizar o evaluar el _QuerySet_, y una vez hecho esto, Django accede a la base de datos, ejecuta la operación y almacena el resultado en __cache__, retornado los resultados requeridos explícitamente. Entonces cualquier evaluación posterior que se haga sobre el _QuerySet_ se hará sobre el resultado almacenado en memoria. 

​	Teniendo en cuenta el comportamiento de los _QuerySets_ y como estos se almacenan en __cache__ (o _caching_), podemos hacer un uso mas eficiente de las _Querys_ evitando redundancias y ocupar espacio de forma innecesaria. 

> ​	[La __cache__](https://es.wikipedia.org/wiki/Caché_(informática)), antememoria o memoria intermedia, es un espacio de almacenamiento de alta velocidad en donde se aloja un subconjunto de datos generalmente temporales y de uso frecuente, con el fin de poder acceder a ellos mucho mas rápido que accediendo directamente desde la ubicación de almacenamiento principal. Los datos almacenados en una caché pueden ser el resultado de un cálculo anterior o el duplicado de datos almacenados en otro lugar, generalmente, da velocidad de acceso más rápido.
>
> ​	El almacenamiento en caché permite reutilizar de forma eficaz los datos recuperados o procesados anteriormente. 
>
> ​	La memoria caché es un [búfer](https://es.wikipedia.org/wiki/Búfer_de_datos) especial de memoria que poseen las computadoras, que funciona de manera semejante a la [memoria principal](https://es.wikipedia.org/wiki/Memoria_principal), pero es de menor tamaño y de acceso más rápido. Nace cuando las memorias ya no eran capaces de acompañar a la velocidad del procesador, por lo que se puede decir que es una memoria auxiliar, que posee una gran velocidad y eficiencia y es usada por el [microprocesador](https://es.wikipedia.org/wiki/Microprocesador) para reducir el tiempo de acceso a datos ubicados en la memoria principal que se utilizan con más frecuencia.
>
> ​	Los datos en una memoria caché suelen almacenarse en hardware de acceso rápido, como la memoria de acceso aleatorio (RAM) y también puede utilizarse junto con un componente de software.
>
> ​	Cuando se accede por primera vez a un dato, se hace una copia en la __caché__; los accesos siguientes se realizan a dicha copia, haciendo que sea menor el tiempo de acceso medio al dato. Cuando el microprocesador necesita leer o escribir en una ubicación en memoria principal, primero verifica si una copia de los datos está en la caché; si es así, el microprocesador de inmediato lee o escribe en la memoria caché, que es mucho más rápido que de la lectura o la escritura a la memoria principal.

​	Un ejemplo de almacenamiento ineficiente:

```python
>>> print([query.headline for query in Entry.objects.all()])
>>> print([query.pub_date for query in Entry.objects.all()])
```

​		En este ejemplo se ejecutan dos _Queries_ y se itera sobre cada una de ellas para obtener el valor de un campo especifico, el problema es que los datos son cargados dos veces en memoria, ya que se llama primero a todos los objetos del modelo y luego se itera sobre ello, doblando la cantidad de memoria que ocupamos. 

​	Además existe la posibilidad de que los dos _QuerySets_ sean diferentes debido a que entre ambas operaciones se pudo haber añadido o eliminado información, debido a una condición de carrera.

​	Para evitar este problema podemos guardar el _QuerySet_ dentro de una variable, de esta manera:

```python
>>> queryset = Entry.objects.all()
>>> print([p.headline for p in queryset]) 
	# Se evalua el QuerySet, en este momento es cuando se hace accede a la base de datos y se almacena en memoria.
>>> print([p.pub_date for p in queryset]) 
	# Se reutiliza la información almacenada en cache.
```

__Condiciones en la que un *QuerySet*  no se almacena en memoria__:

​	Los _QuerySets_ no siempre almacenan sus resultados en memoria. Cuando se evalúa solo una parte del conjunto de resultados, se comprueba si esta ya existe en memoria, pero si la petición a la base de datos no integra toda la información almacenada, los elementos retornados por la consulta no se almacena, lo que significa que limitar el tamaño de la consulta, con un filtro o un _slicing_ de Python hará que este no se almacene en memoria. 

​	Por ejemplo, el obtener repetidamente un determinado numero de resultados desde la base de datos hará que se acceda a la base de datos cada vez que ejecutemos la operación.

```python
>>> queryset = Entry.objects.all()
>>> print(queryset[5]) # Se accede a la base de datos pero sin guardar en memoria.
>>> print(queryset[5]) # Se vuelve a acceder a la base de datos sin guardar nada en memoria.
```

​	Generalmente invocar atributos de los objetos _QueerySet_ también provocará una llamada a la base de datos.

```python
>>> entry = Entry.objects.get(id=1)
>>> entry.authors.all() # Se accede a la base de datos pero sin guardar en memoria.
>>> entry.authors.all() # Se vuelve a acceder a la base de datos sin guardar nada en memoria.
```

​	Esto es debido, en parte a la naturaleza _Lazy_ de las _Queries_ de Django. El escribir la búsqueda no hace que este se ejecute, esta será ejecutada cuando sea requerida, el problema es que la requerimos parcialmente y por esta condición no se almacena en cache.

​	Una manera eficiente de obtener solo el quinto elemento sería:

````python
>>>queryset = Entry.objects[5]
>>> print(queryset) # Se accede a la base de datos y se guarda en memoria.
>>> print(queryset) # Se accede a la información almacenada en memoria.
````

​	Si estamos negados a hacerlo de una mejor manera y queremos obtener un _QuerySet_ del total de datos para solo recuperar el quinto, podríamos hacer lo siguiente:

```python
>>> queryset = Entry.objects.all()
>>> [entry for entry in queryset] # Se accede a la base de datos y se guarda en memoria.
>>> print(queryset[5]) # Se utiliza la información en cache
```

​	Hay que tener especial cuidado con las propiedades personalizadas que creemos y como implementamos el almacenamiento de __cache__, para eso utilizamos el decorados [ __cached_property__](https://docs.djangoproject.com/es/3.2/ref/utils/#django.utils.functional.cached_property).

---



### Operar directamente sobre la base de datos.

- En el nivel más básico, use el filtro y la exclusión para realizar el filtrado en la base de datos.
- Utilizar la [__expresión F__](https://docs.djangoproject.com/es/3.2/ref/models/expressions/#django.db.models.F) para filtrar campos dentro de un mismo modelo.
- Utilizar anotación para hacer [agregaciones](https://docs.djangoproject.com/es/3.2/topics/db/aggregation/) en la base de datos.



### Acceder a objetos individuales utilizando su índice.

​	Hay dos razones para buscar objetos individuales utilizando las columnas de tipo `unique` o `db_index` utilizando el método `get()`:

-  El _Query_ será más rápido debido al índice de la base de datos, y la búsqueda podría ser aun más lenta si varios objetos coinciden con alguno de los criterios.
- Tener un único criterio de búsqueda garantiza que se agilice la consulta. 

```python
# Esta consulta:
>>> entry = Entry.objects.get(id=10)
# Será más rapida que esta consulta:
>>> entry = Entry.objects.get(headline="News Item Title")
# Y mucho mas rapida que esta otra consulta:
>>> entry = Entry.objects.get(headline__startswith="News")
```

​	En primer lugar el titulo __no es un campo indexado__, lo que haría que la búsqueda sea menos eficiente, y en segundo lugar, la búsqueda no garantiza que solo se devuelva un objeto. Si __la consulta coincide con más de un objeto__, los recuperará y transferirá todos desde la base de datos, lo que podría ser perjudicial si los criterios de búsqueda coinciden con cientos o miles de registros, lo que sería aun mas grave si la base de datos se aloja en un servidor separado. 



### Si sabes lo que necesitas búscalo solo una vez.

​	Acceder múltiples veces a la base de datos para obtener diferentes partes de un mismo objeto es mucho menos eficiente que recuperar el objeto entero directamente, esto puede ser especialmente importante cuando trabajamos con `FK` ya que tendemos ha realizar una segunda llamada a la base de datos para recuperar objetos relacionado.

#### [`.select_related()`](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#django.db.models.query.QuerySet.select_related)

​	`QuerySet.select_related(*fields)`

​	Este método retornará un `QuerySet` que incluya todos los objetos relacionados a través de una `FK` con el objeto principal de nuestra consulta. Esto resulta en una única consulta mas compleja pero que hará que no necesitemos volver a consultar a la base de datos para conseguir los objetos relacionados.

​	Ejemplo de una búsqueda simple e ineficiente: 

```python
# Accedemos a la base de datos.
e = Entry.objects.get(id=5)

# Volvemos a acceder a la base de datos para obtener el objeto asociado.
b = e.blog
```

​	Ejemplo de una búsqueda utilizando la función `.select_related()`:

```python
# Accedemos a la base de datos.
e = Entry.objects.select_related('blog').get(id=5)

# No necesitamos acceder a la base de datos debido a que el objeto asociado ya está en memoria.
b = e.blog
```

​	La función `.select_related()` puede ser utilizada sobre cualquier conjunto de _QuerySets_.

​	Por ejemplo, si intentamos realizar una búsqueda filtrando datos y luego, en función del resultado, acceder a un objeto relacionado con una `FK`, sería mucho mas eficiente hacerlo utilizando la función `.select_related()`. Por ejemplo:

```python
from django.utils import timezone

# Pretendemos encontrar todos los blog con entradas programadas para ser publicadas en el futuro.
blogs = set()

for e in Entry.objects.filter(pub_date__gt=timezone.now()).select_related('blog'):
# Esto realizaría una petición a la base de datos por cada iteración del blucle.
    blogs.add(e.blog)
```

​	Utilizando la función `.select_related()`, el orden entre el `.filter()` y `.select_related()` es indiferente.

```python
# Aquí se filtra todas las entradas programadas para el futuro y en función del resultado obtenemos el blog relacinado con la entrada.
Entry.objects.filter(pub_date__gt=timezone.now()).select_related('blog')
# En este otro caso obtenemos todas las entradas con todos los blog relacionados y luego filtramos las que tengan entradas programadas en el futuro.
Entry.objects.select_related('blog').filter(pub_date__gt=timezone.now())
```

​	Ambas retornarían la misma información, sin embargo el primer ejemplo retorna solo los objetos relacionados al resultado de nuestra búsqueda, limitando la _Query_ solo a los resultados deseados.

​	Además la función `.select_related()` puede traer objetos relacionados a diferentes niveles, es decir, se puede conseguir un objeto relacionado a otro objeto relacionado con nuestra búsqueda principal. Por ejemplo:

```python
# Aquí intentamos encontrar un libro a través de su id, al autor del libro y la ciudad natal del autor.
# Este primer ejemplo accede a la base de datos para obtener un libro especifico, y posteriormente realiza dos Queries más para encontrar al autor relacionado al libro y una tercera para encontrar la ciudad natal del autor.
b = Book.objects.get(id=4)  
p = b.author	# Accedemos de nuevo a la base de datos.
c = p.hometown	# Accedemos por tercera vez a la base de datos.

# Aquí en cambio accedemos a la base de dator de libros y directamente obtenemos la instancia autor relacionada con el libro y la ciudad natal relacionada con el autor. Todo esto en una sola Query.
b = Book.objects.select_related('author__hometown').get(id=4)
p = b.author	# Ya no hace falta realizar una Query porque la busque retornó y almaceno todas las relaciones.
c = p.hometown
```

​	Puedes hacer referencia a cualquier relación `FK` o `OneToOneField` ingresándolos en la lista de parámetros de la función `select_related()`, y puedes realizar búsquedas a diferentes niveles utilizando la notación de doble barra baja (_double underscore_) de Python, para referirte a objetos relacionados a otros objetos.

> ​	`.select_realtes()` esta diseñado para buscar relaciones de `OneToOneField`, para relaciones de `ManyToManyField` debemos usar el método [`.prefetch_related()`](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#prefetch-related).

​	También se puede realizar una referencia inversa a la dirección de un `OneToOneField` en los parámetro de la función `.select_related()`, es decir, puede atravesar una relación `OneToOneField`de regreso al objeto en el que está definido el campo. En lugar de especificar el nombre del campo, se utiliza el [`related_name`](https://docs.djangoproject.com/es/3.2/ref/models/fields/#django.db.models.ForeignKey.related_name)del objeto para el campo del objeto relacionado.

​	En el caso de querer llamar a todos los objetos relacionados con la instancia de tu búsqueda, basta con definir la función `select_related()` sin ningún argumento, esto rastreará todas las `FK` no nulas que existan, sin embargo esta practica no es nada recomendable, ya que siempre debemos intentar obtener y almacenar únicamente la información que necesitamos para trabajar, obtener más de lo necesario es actuar en detrimento del rendimiento.

​	Además, es posible el encadenamiento de métodos `.select_related()` y esto funciona de manera similar a otros métodos, es decir, `.select_related(FK_1, FK_2)` es equivalente  a `.select_related(FK_1).select_related(FK_2)`. 

​	Un ejemplo mas complejo de las posibilidades que tenemos para optimizar y especificar un _Query_ seria:

```python
books = Book.objects.select_related('author').annotate(
    author_name=F('author__name')
).values('id', 'name', 'author_name')
```

​	Esta ultima _Query_, por muy compleja que parezca, solo representa una única llamada a la base de datos.

---

#### [`Prefetch()`](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#django.db.models.Prefetch)

​	`class Prefetch(lookup, queryset=None, to_attr=None)`

​	El objeto `Prefetch()` se puede utilizar para controlar la operación de `prefetch_related()`.

​	El primer argumento, ___lookup___, describe las relaciones a seguir. Por ejemplo:

```python
>>> from django.db.models import Prefetch
>>> Question.objects.prefetch_related(Prefetch('choice_set')).get().choice_set.all()
	# Esto solo ejecutará 2 consultas, independientemente del numero de objetos en la Query.
<QuerySet [<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]>
	# El Query retorna un QuerySet con todas las respuestas relacionadas a la pregunta.

>>> Question.objects.prefetch_related(Prefetch('choice_set')).all()
<QuerySet [<Question: Hello>]>
```

​	El argumento ___queryset___ proporciona un _QuerySet_ base sobre el cual ejecutar la búsqueda. Esto es útil para filtrar aun más la operación de captación previa (o _`prefetch` operation_) o para llamar a `select_related()` desde esta relación, reduciendo así el número de consultas aún más. Por ejemplo:

```python
>>> voted_choices = Choice.objects.filter(votes__gt=0)
>>> voted_choices
<QuerySet [<Choice: The sky>]>

>>> prefetch = Prefetch('choice_set', queryset=voted_choices)
>>> Question.objects.prefetch_related(prefetch).get().choice_set.all()
<QuerySet [<Choice: The sky>]>
```





---

#### [`prefetch_related()`](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#prefetch-related)

​	Este método retorna un _QuerySet_ que recuperará automáticamente, un un solo lote, objetos relacionados para cada una de las búsquedas especificas. Esto tiene un propósito similar al de `.select_related()`, en el sentido de que ambos están diseñados para minimizar la cantidad de consultas a la base de datos que puede causar el acceder a objetos relacionados, sin embargo la estrategia es bastante diferente.

​	Utilizamos el metodo `.select_related()` con relaciones `ManyToManyField` 

> ​	`.select_related()` funciona creando una combinación SQL e incluyendo los campos del objeto relacionado en la instrucción `SELECT`. Por esta razón, `.select_related()` obtiene los objetos relacionados en la misma consulta de base de datos. Sin embargo, para evitar obtener un conjunto de datos demasiado grande, que resultaría de la unión de una relación `ManyToManyField`, `.select_related()` se limita a relaciones de `OneToOneField` y `FK`.

​	`.prefetch_related()` realiza una búsqueda separada para cada relación y realiza una unión ( _JOIN_ ) en Python. Esto le permite precargar objetos con relación `ManyToManyField` y `ManyToOneField`, lo que no se puede hacer utilizando `.select_relates()`. También admite la captación previa de [`GenericRelation`](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/#django.contrib.contenttypes.fields.GenericRelation) y [`GenericForeignKey`](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/#django.contrib.contenttypes.fields.GenericForeignKey); sin embargo, debe restringirse a un conjunto homogéneo de resultados.

> ​	Tanto  [`GenericRelation`](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/#django.contrib.contenttypes.fields.GenericRelation) y [`GenericForeignKey`](https://docs.djangoproject.com/es/3.2/ref/contrib/contenttypes/#django.contrib.contenttypes.fields.GenericForeignKey) son parte del concepto de Relaciones Genéricas, el cual, para no hacer aun mas largo este MD, se describen en un MD corto dedicado al tema.

​	Este método puede ser confuso, así utilizaremos el ilustrador ejemplo de Django:

```python
from django.db import models

class Topping(models.Model):
    name = models.CharField(max_length=30)

class Pizza(models.Model):
    name = models.CharField(max_length=50)
    toppings = models.ManyToManyField(Topping)

    def __str__(self):
        return "%s (%s)" % (
            self.name,
            ", ".join(topping.name for topping in self.toppings.all()),
        )
```

​	En base a este modelo de ejemplo, en donde solo tenemos dos clases, una _Topping_ y otra _Pizza_, y en donde al llamar al metodo `__str__` de la clase _Pizza_, se ejecutará una _Query_ que retornará todos los objetos dentro de la table _Topping_ relacionados, para luego imprimirlos. 

​	El problema viene dado a que cada vez que se ejecute una búsqueda sobre el modelo _Pizza_ y se realizará una llamada al modelo _Topping_ por cada objeto de la tabla _Pizza_ que necesitemos buscar, haciéndola una _Query_ bastante ineficiente.

​	Para reducir las llamadas a únicamente 2, basta con utilizar el método `prefetch_relates` de la siguiente forma:

````python
Pizza.objects.all().prefetch_related('toppings')
````

​	Esto implica ejecutar un `self.toppings.all()` para cada _pizza_; sin embargo cada vez que se llama al `self.toppings.all()`, en lugar de tener que acceder a la base de datos para buscar los elementos, los encontrará en la memoria del _QuerySet_ cargado previamente en una única consulta. Por lo que todos los ingredientes relevantes se habrán obtenido en una sola consulta y se habrán utilizado para crear el _QuerySet_ almacenado en cache con los resultados relevantes para nuestro trabajo, el cual es quien será llamado por el `self.toppings.all()`en vez de a la base de datos. 

> ​	Hay que tener en cuenta que el _QuerySet_ principal y todos los objetos relacionados especificados se cargarán en memoria. Cambiando el comportamiento típico de los _QuerySets_, los cuales intentan evitar ser cargados en memoria antes de que sean necesarios, por lo que, aunque pueda resultar en una mejora en el rendimiento, si no se utiliza con cuidado, podría significar un deterioro en la optimización del uso de memoria.
>
> ​	También es importante tener en cuanta que __<u>cualquier cambio en la consulta resultará en un_Query_totalmente distinta, que por lo tanto será almacenado en memoria en un espacio distinto.</u>__ Entonces, si escribimos lo siguiente:
>
> ````python
> pizzas = Pizza.objects.prefetch_related('toppings')
> [list(pizza.toppings.filter(spicy=True)) for pizza in pizzas]
> ````
>
> ​	La primera consulta que fue guardada no nos será de utilidad, ya que la segunda búsqueda, al añadir un método diferente, se consideraría como una _Query_ distinta, y se ejecutaría y almacenaría en un espacio distinto, por lo que habremos ejecutado una consulta bastante compleja para nada y además de tenerla almacenada, realizamos y almacenamos una segunda, resultando en un mayor deterioro tanto del rendimiento como de la gestión de memoria. 
>
> ​	Además, si llama a los métodos de alteración de la base de datos `add()`, `remove()`, `clear()` o `set()`, en los administradores relacionados, se borrará cualquier caché precargada para la relación.

​	Los siguientes casos son útiles y funcionales:

```python
Restaurant.objects.prefetch_related('pizzas__toppings')
```

​	Este precargará todas los objetos que coincidan con el filtro, es decir, todas las pizzas que pertenezcan a los restaurantes y todos los ingredientes que pertenecen a esas pizzas. Esto dará como resultado un total de 3 consultas de base de datos; una para los restaurantes, una para las pizzas y otra para los _toppings_. 

```python
Restaurant.objects.prefetch_related('best_pizza__toppings')
```

​	Esta búsqueda traerá las mejores pizzas y todos los ingredientes de cada una, para cada restaurante. Esto también hará 3 llamadas a la base de datos, una para los restaurantes, otra para las mejores pizzas y otra para los _toppings_.

​	La _Query_ puede simplificarse utilizando el método `select_related` para reducir el recuento de consultas a solo 2:

```python
Restaurant.objects.select_related('best_pizza').prefetch_related('best_pizza__toppings')
```

​	Dado que la captación previa se ejecuta después de la consulta principal (que incluye las uniones necesarias para `select_related`), es capaz de detectar que los objetos `best_pizza` ya se han recuperado y omitirá recuperarlos de nuevo.

​	El encadenamiento de llamadas `prefetch_related` acumulará las búsquedas que se precargaron. Para borrar cualquier comportamiento `prefetch_related`, ingresamos un `None` como parámetro:

```python
non_prefetched = qs.prefetch_related(None)
```

​	Una consideración al usar `.prefetch_related()` es que los objetos creados por la _Query_ se pueden compartir entre los diferentes objetos con los que están relacionados. Es decir, si varios objetos están relacionados a través de un `FK` a un mismo objeto, este no será replicado ni almacenado múltiples veces en memoria, sino que será compartido entre los objetos, de esta manera se ahorra memoria y tiempo de procesamiento.

​	Para lograr un mayor control sobre el comportamiento del método `.prefetch_relates()`, podemos hacer uso de [`Prefetch()`](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#django.db.models.Prefetch), por ejemplo:

```python
>>> from django.db.models import Prefetch

>>> Restaurant.objects.prefetch_related(Prefetch('pizzas__toppings'))
```

​	También se puede proporcionar un _QuerySet_ personalizado al hacer uso del argumento _queryset_ de la siguiente forma:

```python
>>> Restaurant.objects.prefetch_related(
     Prefetch('pizzas__toppings', queryset=Toppings.objects.order_by('name'))
)
# Aqui estamos cambiando el orden predeterminado del QuerySet.
```

​	O también podemos llamar al método `.select_related()` para reducir aun más el número de consultas:

```python
>>> Pizza.objects.prefetch_related(
     Prefetch('restaurants', queryset=Restaurant.objects.select_related('best_pizza'))
)
```

​	En el caso de que necesitemos iterar sobre las instancias de un modelo, podemos precargar atributos relacionados en esas instancias utilizando la función `prefetch_related_objects()`.

---



#### [`prefetch_related_objects()`](https://docs.djangoproject.com/es/3.2/ref/models/querysets/#django.db.models.prefetch_related_objects)

​	Esta función sirve para buscar sobre una lista de instancias de un modelo, por ejemplo un _QuerySet_, que es un objeto compuesto por cierto numero de instancias de un modelo. Es especialmente útil para cuando recibamos una lista o tupla de instancias. 

​	Al pasar un iterable de instancias, todas deben ser de la misma clase y las búsquedas o los objetos de captación previa, por ejemplo:

```python
from django.db.models import prefetch_related_objects

restaurants = fetch_top_restaurants_from_cache()  # Una lista de restaurantes.
prefetch_related_objects(restaurants, 'pizzas__toppings')
```

​	Cuando se utilizan múltiples bases de datos con `prefecth_related_objects`, la consulta utilizará el modelo asociado a las instancias ingresadas, esto se puede anular mediante el uso de un conjunto de consultas personalizadas en una búsqueda relacionada.

---



### No recuperes lo que no necesitas.

#### `.values()`

`QuerySet.values(*fields, **expresions)`

​	Este método retorna un diccionario con los valores retornados por un _QuerySet_, es decir, en vez de retornar una instancia del modelo, siendo este además un objeto distinto en si mismo, se retorna un diccionario, en el caso de ser un objeto individual o una lista de diccionarios si son múltiples objetos, con los valores que alberga el objeto. 

​	Es posible además especificar que campos queremos que sean retornados a través del uso del argumento _fields_, por ejemplo:

```python
>>> Blog.objects.values()
<QuerySet [{'id': 1, 'name': 'Beatles Blog', 'tagline': 'All the latest Beatles news.'}]>
>>> Blog.objects.values('id', 'name')
<QuerySet [{'id': 1, 'name': 'Beatles Blog'}]>
```

​	También es posible implementar expresiones para filtrar o modificar los resultados de la función.

```python
>>> from django.db.models.functions import Lower

>>> Blog.objects.values(lower_name=Lower('name'))
<QuerySet [{'lower_name': 'beatles blog'}]>
```

​	Al escribir una función de agregación como argumento de la función `.values()`, esta se aplicará antes que otros argumentos dentro de la misma función `.values()`. Si necesitamos agrupar por otro valor, añadimos la agregación después que la función `.values()`. Por ejemplo:

```python
>>> from django.db.models import Count

>>> Blog.objects.values('entry__authors', entries=Count('entry'))
<QuerySet [{'entry__authors': 1, 'entries': 20}, {'entry__authors': 1, 'entries': 13}]>

>>> Blog.objects.values('entry__authors').annotate(entries=Count('entry'))
<QuerySet [{'entry__authors': 1, 'entries': 33}]>
```



---



#### `.values_list()`



---
