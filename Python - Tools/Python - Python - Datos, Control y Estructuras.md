# Python - Datos, Control y Estructuras.

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

## dict's.

Es un tipo estructura no ordenada de datos que permite almacenar un numero arbitrario de objetos, cada uno de estos identificado con un __key__ unico. Esto nos permite poder buscar, insertar o eliminar cualquier objeto asociado a una __key__ determinada.

Los diccionarios están indexados por claves que pueden ser de cualquier tipo de objeto [hashable](https://docs.python.org/3/glossary.html#term-hashable). Un objeto hashable es uno que tiene un valor _hash_ que nunca cambia durante su tiempo de vida, esta caracteristica les permite a este tipo de objeto ser usados tanto como __key__ en un diccionario como tambien formar parte de un objeto tuple, objetos que les exigen ser llaves unicas.

Ademas del objeto ___dict___ simple, implementado en Python, existen diferentes implementaciones mas especializadas basadas en la clase ___dict___ basica integrada.

### collections.OrderedDict 

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



### collections.defaultdict.

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

### collections.CainMap.

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



## Fuentes

https://realpython.com/python-data-structures/
