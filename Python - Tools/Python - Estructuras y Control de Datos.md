# Python - Estructuras y control de datos.



## Iterables e Iteradores.

Los __iterables__ son aquellos objetos que pueden ser iterados, es decir, que pueden ser indexados y recorridos a través de dicho indice. Por ejemplo, un array se puede indexar con un slicing `array[n]`, por lo que sería un objeto iterable.

Los __iteradores__ son objetos que hacen referencia a un elemento, y que tienen un método `next` que permite hacer referencia al siguiente elemento. Cuando creamos un bucle `for` en python, estamos creando un objeto que hace referencia a la lista original y accede a sus elementos a través del metodo `next`, el cual cada vez es llamado devuelve el siguiente objeto dentro del iterable. 

Por ejemplo, si tenemos una lista, y la ingresamos como parámetro de la función `iter()` se nos retorna un objeto parecido a este: `<list_iterator object at 0x7f05134c06d0>`.

```python
lista = [1, 2, 3]
iterabor = iter(lista)
print(iterador)
>>> <list_iterator object at 0x7f05134c06d0>

print(next(iterador))
>>> 1
```

Existen diferentes tipos de iteradores para los diferentes tipos de clases:

- `str_iterator` para cadenas
- `list_iterator` para sets.
- `tuple_iterator` para tuplas.
- `set_iterator` para sets.
- `dict_keyiterator` para diccionarios.

Para saber si un objeto es iterable o no podemos aplicar el siguiente código:

```python
from collections import Iterable
list_nums = [1, 2, 3]
string = "string"
num = 10

print(isinstance(list_nums, Iterable))
>>> True
print(isinstance(string, Iterable))
>>> True
print(isinstance(num, Iterable))
>>> True
```

Podemos iterar en sentido inverso utilizando `[::-1]`.

```python
text = "Python"
for i in text[::-1]:
	print(i)
    
>>> n
>>> o
>>> t
>>> y
>>> h
>>> P
```

Para comprobar si un objeto es iterable o no podemos averiguar si dicho objeto hereda de un iterable o con el método ``isinstance()`` de la siguiente manera:

````python
from collections import Iterable

print(isinstance(an_object, Iterable))
````



### `break`

Sentencia que permite alterar el comportamiento de los bucles `while` y `for`, permitiendo terminar con la ejecución del bucle una vez se encuentra la palabra `break`.

#### `break` con bucle `for`.

Se itera sobre el objeto hasta el momento en que se cumple la condición, se encuentra con la sentencia `break` y se sale del bucle.

```python
cadena = 'Python'
for letra in cadena:
    if letra == 'h':
        print("Se encontró la h")
        break
    print(letra)

# Salida:
# P
# y
# t
# Se encontró la h
```

Es útil en la manera en la que permite optimizar recursos.

#### `break` con bucle `while`.

La condición `while True` haría que la sección de código se ejecute indefinidamente (cuidado con esto), pero al hacer uso del `break`, el bucle se detendrá cuando `x` valga `0`.

```python
x = 5
while True:
    x -= 1
    print(x)
    if x == 0:
        break
    print("Fin del bucle")

#4, 3, 2, 1, 0
```

Por norma general, y salvo en casos muy concretos, todo bucle `while True` tiene una sentencia `break` dentro.

#### `break` en bucles anidados.

El uso de la sentencia `break` rompe con la secuencia del bucle, pero solo en el que está dentro, es decir, si tenemos dos bucles anidados el `break` romperá el bucle anidado, el interno, pero no el bucle exterior.

```python
for i in range(0, 4):
    for j in range(0, 4):
        # No se realizará más de una iteración.
        break
        
    #El `break` no afectara el comportamiento de este bucle.
       
    print(i, j)
    
# 0 0
# 1 0
# 2 0
# 3 0
```



### `continue`

Permite modificar el comportamiento de los bucles `while` y `for` al saltar todo el código restante en la iteración actual y vuelve al principio en el caso de que aún queden iteraciones por completar.

La diferencia entre `break` y `continue` es que el segundo no rompe el bucle, sino que pasa a la siguiente iteración ignorando todo el código pendiente.

```python
string = 'Python'
for i in string:
    if i == 'P':
        continue
    print(i)

# y
# t
# h
# o
# n
```

A diferencia del `break`, el `continue` no rompe el bucle sino que finaliza la iteración actual, haciendo que todo el código que va después se salte, y se vuelva al principio a evaluar la condición en la siguiente iteración.

---

### [`zip()`](https://docs.python.org/3/library/functions.html#zip)

> La función `zip(*iterables, strict=False)` viene incluida por defecto en el _namespace_, lo que significa que puede ser usada sin tener que importarse.

Esta función itera sobre una cantidad $n$ de iterables en paralelo, retornando una tupla formada por el objeto que en ese momento este siendo iterado de cada iterable ingresado, en el orden en el que estos son ingresados como argumentos en la función, por lo que la longitud de la tupla será igual a la cantidad de iterables ingresados.

> Técnicamente la función `zip()` retorna un `zip object`, el cual puede ser transformado en una lista a través del método `list()`.

También podemos pensar a la función `zip()` en u transformador de columnas a filas, o de filas a columnas, similar a una [transposición de matriz](https://en.wikipedia.org/wiki/Transpose).

> `zip()` es una función _lazy_, es decir que el elemento no será procesado hasta que se itere sobre el iterable, como podría ser un bucle `for` o al ser ingresado en un objeto [`list`](https://docs.python.org/3/library/stdtypes.html#list).

#### Manejo de parametros.

Al ser posible ingresarle iterables de diferentes longitudes como argumentos a la función `zip()`, esta nos ofrece tres maneras de manejar esta situación:

- Por defecto `zip()` se detiene al momento de agotar al iterable de menor longitud, ignorando al resto de objetos restantes en los iterables mas largos, definiendo el numero total de iteraciones en función del iterable mas corto.
- En el caso de que sea necesario o se tenga la certeza de que los iterables ingresados poseen la misma longitud, se puede definir al parámetro `strict` como `True`, lo que hará que la función `zip()` verifique si las longitudes son iguales y en el caso de no ser así devuelva un `ValueError`.
  En el caso de `strict=False`, comportamiento por defecto de la función, cualquier error o diferencia de longitud será ignorada y silenciada, pudiendo generar un bug difícil de encontrar.
- Se pueden rellenar los valores faltantes de los iterables más cortos con valores predeterminados para que de esta manera todos tengan la misma longitud, utilizando la función [`itertools.zip_longest()`](https://docs.python.org/3/library/itertools.html#itertools.zip_longest).

> `zip()` se puede usar en conjunto con el operador `*` para descomprimir el iterable retornado por la función, y además es una buena manera de revertir los cambios realizados por su implementación, por ejemplo:
>
> ```python
> >>> x = [1, 2, 3]
> >>> y = [4, 5, 6]
> >>> z = zip(x, y)
> >>> print(list(z))
> [(1, 4), (2, 5), (3, 6)]
> 
> >>> x2, y2 = zip(*z)
> >>> x == list(x2) and y == list(y2)
> True
> 
> >>>print(x2)
> [1, 2, 3]
> 
> >>>print(y2)
> [4, 5, 6]
> ```

#### Iterar sobre `dict`.

La función `zip()` esta hecha para trabajar sobre cualquier clase de iterable, incluyendo objetos `dict`.

Por defecto al ingresar un diccionario como argumento se toman las _key_ del objeto `dict`.

```python
esp = {'1': 'Uno', '2': 'Dos', '3': 'Tres'}
eng = {'1': 'One', '2': 'Two', '3': 'Three'}

for a, b in zip(esp, eng):
    print(a, b)

# 1 1
# 2 2
# 3 3
```

Sin embargo, si utilizamos la función `.items()` podemos acceder al _key_ y _value_ de cada objeto.

```python
esp = {'1': 'Uno', '2': 'Dos', '3': 'Tres'}
eng = {'1': 'One', '2': 'Two', '3': 'Three'}

for (k1, v1), (k2, v2) in zip(esp.items(), eng.items()):
    print(k1, v1, v2)

# 1 Uno One
# 2 Dos Two
# 3 Tres Three
```

#### Deshacer `zip()`.

Supongamos que hemos utilizado la función `zip()` para obtener $c$.

```python
a = [1, 2, 3]
b = ["One", "Two", "Three"]
c = zip(a, b)

print(list(c))
# [(1, 'One'), (2, 'Two'), (3, 'Three')]
```

### `enumerate()`

`enumerate(iterable, start=0)`

Retorna un objeto `enumerate`, el cual es un objeto iterable, que al transformarse a través del método `list()` contiene una lista de tuplas cuyo valor inicial es el indice o cantador, comenzando en 0, del objeto iterado en ese momento, seguido por el valor obtenido de dicho iterable.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
list(enumerate(seasons, start=1))
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

## Comprehensions.

### List comprehensions.

Es una manera de crear, en una sola linea de código, listas de elementos en función de un objeto iterable. 

```python
new_list = [expression fot item in iterable]
```

El _list comprehension_ se rellenará con el resultado de la expresión aplicada sobre el objeto iterado, contenido, obviamente, en el iterable. 

También es posible utilizar sentencias condicionales para modificar el comportamiento del _list comprehension_ y así solo añadir los elementos con las características que deseamos.  

```python
new_list = [expression for item in iterable if condition == True]
```

Por lo tanto el resultado retornado por la expresión solo será añadido a la lista si se cumple con la condición descrita.

### Sets comprehensions.

Muy similares a la _list comprehension_, en realidad la lógica es exactamente igual, con la diferencia de que en vez de corchetes ``[ ]`` utilizamos llaves ``{ }``.

Dado que los _sets_ no permiten datos duplicados, los elementos duplicados que intentemos añadir simplemente no lo harán.

````python
new_set = {expression for item in iterable}

new_set = {expression for item in iterable if condition == True}
````

### Dict comprehension.

Muy similares a la _list comprehension_, en realidad la lógica es exactamente igual, con la diferencia de que debemos especificar la _key_.

````python
new_dict = {i:j for i, j in zip(iterable_1, iterable_2)}
````

---

En ciertas ocasiones, las compresiones no resultan sólo útiles por que puedan ser escritas en una sola línea de código, sino que también pueden llegar a ser más rápidas que otros métodos, por lo que es importante medir su tiempo de ejecución para saber si son una buena elección.

## dict's.

Es un tipo estructura no ordenada de datos que permite almacenar un numero arbitrario de objetos, cada uno de estos identificado con un __key__ unico. Esto nos permite poder buscar, insertar o eliminar cualquier objeto asociado a una __key__ determinada.

Los diccionarios están indexados por claves que pueden ser de cualquier tipo de objeto [hashable](https://docs.python.org/3/glossary.html#term-hashable). Un objeto hashable es uno que tiene un valor _hash_ que nunca cambia durante su tiempo de vida, esta caracteristica les permite a este tipo de objeto ser usados tanto como __key__ en un diccionario como tambien formar parte de un objeto tuple, objetos que les exigen ser llaves unicas.

Ademas del objeto ___dict___ simple, implementado en Python, existen diferentes implementaciones mas especializadas basadas en la clase ___dict___ básica integrada.

### `collections.OrderedDict`.

__Recuerda el orden de inserción de los indices.__

> OrderedDict no es parte de las clases integradas de Python, por lo que se debe de importar desde ___collections___ para poder utilizarlo.

Si el orden de los indices es importante para el trabajo del algoritmo, esta es la mejor manera de comunicar explicitamente que necesitamos que lo mantenga. 

```python
>>> import collections
>>> d = collections.OrderedDict(one=1, two=2, three=3)

>>> d
OrderedDict([('one', 1), ('two', 2), ('three', 3)])

>>> d["four"] = 4
>>> d
OrderedDict([('one', 1), ('two', 2),
             ('three', 3), ('four', 4)])

>>> d.keys()
odict_keys(['one', 'two', 'three', 'four'])
```

#### Metodos especificos.

__.move_to_end(key, last = true)__



### `collections.defaultdict.`

La diferencia con un ___dict___ normal es que el ___defaultdict___ jamas retorna un ___KeyError___ ya que provee un valor por defecto si el indice no existe.

https://www.geeksforgeeks.org/defaultdict-in-python/

```python
>>> from collections import defaultdict
>>> dd = defaultdict(list)

>>> # Accessing a missing key creates it and
>>> # initializes it using the default factory,
>>> # i.e. list() in this example:
>>> dd["dogs"].append("Rufus")
>>> dd["dogs"].append("Kathrin")
>>> dd["dogs"].append("Mr Sniffles")

>>> dd["dogs"]
['Rufus', 'Kathrin', 'Mr Sniffles']
```

### `collections.ChainMap.`

> Permite buscar en múltiples diccionarios como si fuesen uno solo.

Permite agrupar múltiples diccionarios en un solo objeto mapeable. sin embargo el insertar, actualizar y eliminar solo afecta al primer diccionario añadido a la cadena.

```python
>>> from collections import ChainMap
>>> dict1 = {"one": 1, "two": 2}
>>> dict2 = {"three": 3, "four": 4}
>>> chain = ChainMap(dict1, dict2)

>>> chain
ChainMap({'one': 1, 'two': 2}, {'three': 3, 'four': 4})

>>> # ChainMap searches each collection in the chain
>>> # from left to right until it finds the key (or fails):
>>> chain["three"]
3
>>> chain["one"]
1
>>> chain["missing"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'missing'
```



## Paralelización emulando Switch.

Una de las principales diferencias entre usar una cadena de condicionales `if-elif` es que todos los bloques tienen el mismo tiempo de acceso y ejecución. En una cadena de condicionales normal de Python todas las condiciones van siendo evaluadas hasta que se cumple y se sale del proceso, en cambio al emular un `switch` todo se ejecuta al unisono. 

Esto es especialmente útil si se trabaja con un gran numero de condiciones. Una forma de tener una especie de `switch` es haciendo uso de un diccionario. Por lo tanto podríamos convertir el siguiente código:

```python
def opera2(operador, a, b):
    return {
        'suma': lambda: a + b,
        'resta': lambda: a - b,
        'multiplica': lambda: a * b,
        'divide': lambda: a / b
    }.get(operador, lambda: None)
```



## Fuentes.

https://realpython.com/python-data-structures/

https://ellibrodepython.com/estructuras-control-python

