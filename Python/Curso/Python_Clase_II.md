# Python Clase II.

__Tipos y estructuras de datos.__

---

Todos los valores de datos en Python son __objetos__, porque en Python todo es un objeto, y cada objeto, o valor tiene un __tipo__. Cada tipo de objeto determina qué operaciones va a soportar el objeto y, por lo tanto, qué operaciones se van a poder realizar con esos valores de los datos, qué atributos tiene y si va a poder ser __mutable o no__.

> Una __variable__ en Python es un indice que apunta hacia un espacio en memoria en donde se almacena un dato, y en Python, todo dato es un objeto.

---

__Definir multiples valores en multiples variables:__

```python
x, y, z = "orange", "banana", "cherry"
print(x)
print(y)
print(z)
```

__Definir un valor en multiples variables:__

```python
x = y = z = "orange"
print(x)
print(y)
print(z)
```

> __Investigar__: Alcance de las variables (_scope_).

---

Cada objeto tiene características, "habilidades" y comportamientos diferentes.

---

Para conocer el tipo al que pertenece un objeto, utilizamos la función `type()`.

---

## Principales tipos de datos en Python.

Los principales tipos de datos son: numéricos, secuencias, mapas, clases, instancias y excepciones.

### Texto.

#### `str`.

En Python toda la información textual se representa como un objeto `str`.

> Las cadenas de caracteres son secuencias inmutables e iterables.

> Un objeto es __inmutable__ cuando su valor es fijo. Los objetos inmutables son los números, cadenas y tuplas. Estos objetos no pueden ser alterados y para modificarlos haría falta crear un nuevo objeto con un valor diferente y guardarlo en su misma dirección.

Como definir un variable de tipo `str`:

- Comillas simples: `'Permite incluir comillas "dobles".'`
- Comillas dobles: `"Permite incluir comillas 'simples'."`
- Triple comillas simples: `'''Triple comillas simples.'''`
- Triple comillas dobles: `"""Triple comillas dobles."""` 

> Las cadenas definidas con triples comillas, tanto simple como dobles, pueden incluir varias lineas. Todos los espacios en blanco incluidos se incorporan a la cadena de forma literal.

---

### [Numérico](https://docs.python.org/es/3/library/stdtypes.html#numeric-types-int-float-complex).

Hay tres tipos de datos numéricos distintos en Python: enteros (`int`), coma flotante (`float`) y números complejos (`complex`).

Los números se crean a partir de una expresión literal, o como resultado de una combinación de funciones predefinidas y operadores.

Python soporta completamente una aritmética mixta: Cuando un operador binario de tipo aritmético se encuentra con que los operadores son de tipos diferentes, el operando con el tipo de dato menos restrictivo, se convierte o amplia hasta el nivel del otro operando. Los de tipo `int` son más restrictivos respecto a los `float`, que a su vez son más restrictivos que los `complex`

Todos los tipos numéricos, exceptuando a los de tipo `complex`, soportan las siguientes operaciones:

| Operación      | Resultado                                             | Documentación completa                                       |
| :------------- | :---------------------------------------------------- | :----------------------------------------------------------- |
| `x + y`        | suma de *x* e *y*                                     |                                                              |
| `x - y`        | resta de *x* e *y*                                    |                                                              |
| `x * y`        | multiplicación de *x* por *y*                         |                                                              |
| `x ** y`       | *x* elevado a *y*                                     |                                                              |
| `x / y`        | división de *x* por *y*                               |                                                              |
| `x // y`       | división entera de *x* por *y*                        |                                                              |
| `x % y`        | operador __modulo__. Resto o residuo de *x* entre *y* |                                                              |
| `-x`           | valor de *x*, negado                                  |                                                              |
| `+x`           | valor de *x*, sin cambiar                             |                                                              |
| `abs(x)`       | valor absoluto de la magnitud de *x*                  | [`abs()`](https://docs.python.org/es/3/library/functions.html#abs) |
| `int(x)`       | valor de *x* convertido a entero                      | [`int()`](https://docs.python.org/es/3/library/functions.html#int) |
| `float(x)`     | valor de *x* convertido a número de punto flotante    | [`float()`](https://docs.python.org/es/3/library/functions.html#float) |
| `divmod(x, y)` | el par de valores `(x // y, x % y)`                   | [`divmod()`](https://docs.python.org/es/3/library/functions.html#divmod) |
| `pow(x, y)`    | *x* elevado a *y*                                     | [`pow()`](https://docs.python.org/es/3/library/functions.html#pow) |

[Lista de la prioridad de los operadores](https://docs.python.org/es/3/reference/expressions.html#operator-summary)

---

### Booleano.

`True`o `False`.

#### Operaciones booleanas:

Ordenadas de menor a mayor prioridad.

| Operación | Resultado                                        |
| :-------- | :----------------------------------------------- |
| `x or y`  | si *x* es falso, entonces *y*, si no, *x*        |
| `x and y` | si *x* es falso, entonces *x*, si no, *y*        |
| `not x`   | si *x* es falso, entonces `True`, si no, `False` |

#### Operadores de comparación:

Existen ocho operadores de comparación en Python, compartiendo todos la misma prioridad (que es mayor que el nivel de las operaciones booleanas). Las comparaciones pueden encadenarse de cualquier manera.

| Operación | Significado                                               |
| :-------- | :-------------------------------------------------------- |
| `<`       | estrictamente menor que                                   |
| `<=`      | menor o igual que                                         |
| `>`       | estrictamente mayor que                                   |
| `>=`      | mayor o igual que                                         |
| `==`      | igual que                                                 |
| `!=`      | diferente que                                             |
| `is`      | igualdad a nivel de identidad (Son el mismo objeto)       |
| `is not`  | desigualdad a nivel de identidad (no son el mismo objeto) |

> El comportamiento de los operadores `is` e `is not` no se puede personalizar; ademas, nunca lanzará una excepción, no importa que objetos se estén comparando.

> Hay otras dos operaciones con la misma prioridad sintáctica: `in` y `not in`, que son soportadas por aquellos tipos de datos que son de tipo __iterable__.

---

## Principales estructuras de datos en Python.

Python tiene varios tipos de datos compuestos, utilizados para agrupar otros valores. 

### Secuencia.

#### Operadores.

Los operadores de la siguiente tabla están soportadas por la mayoría de los objetos de secuencia, tanto mutables como inmutables.

La tabla lista las operaciones ordenadas de menor a mayor prioridad. 

Las operaciones `in` y `not in` tienen la misma prioridad que los operadores de comparación. Las operaciones `+` (concatenación) y `*` (repetición) tienen la misma prioridad que sus equivalentes numéricos.

| Operación              | Resultado                                                    |
| :--------------------- | :----------------------------------------------------------- |
| `x in s`               | `True` si un elemento de *s* es igual a *x*, `False` en caso contrario |
| `x not in s`           | `False` si un elemento de *s* es igual a *x*, `True` en caso contrario |
| `s + t`                | la concatenación de *s* y *t*                                |
| `s * n` o `n * s`      | equivale a concatenar *s* consigo mismo *n* veces            |
| `s[i]`                 | El elemento *i-esimo* de *s*, empezando a contar en 0        |
| `s[i:j]`               | el _slicing_ de *s* desde *i* hasta *j*                      |
| `s[i:j:k]`             | el _slicing_ de *s* desde *i* hasta *j*, con paso *j*        |
| `len(s)`               | longitud de *s*                                              |
| `min(s)`               | el elemento más pequeño de *s*                               |
| `max(s)`               | el elemento más grande de *s*                                |
| `s.index(x[, i[, j]])` | índice de la primera ocurrencia de *x* en *s* (en la posición *i* o superior, y antes de *j*) |
| `s.count(x)`           | número total de ocurrencias de *x* en *s*                    |

#### Mutabilidad.

Las operaciones de la siguiente table están definidas para todos los tipos de secuencias mutables.

| Operación                | Resultado                                                    |
| :----------------------- | :----------------------------------------------------------- |
| `s[i] = x`               | el elemento *i* de *s* es reemplazado por *x*                |
| `s[i:j] = t`             | el _slicing_ de valores de *s* que van de *i* a *j* es reemplazada por el contenido del iterador *t* |
| `del s[i:j]`             | equivalente a `s[i:j] = []`                                  |
| `s[i:j:k] = t`           | los elementos de `s[i:j:k]` son reemplazados por los elementos de *t* |
| `del s[i:j:k]`           | borra los elementos de `s[i:j:k]` de la lista                |
| `s.append(x)`            | añade *x* al final de la secuencia (Equivale a `s[len(s):len(s)] = [x]`) |
| `s.clear()`              | elimina todos los elementos de *s* (Equivale a `del s[:]`)   |
| `s.copy()`               | crea una copia superficial de *s* (Equivale a `s[:]`)        |
| `s.extend(t)` o `s += t` | extiende *s* con los contenidos de *t* (En la mayoría de los casos equivale a `s[len(s):len(s)] = t`) |
| `s *= n`                 | actualiza *s* con su contenido repetido *n* veces            |
| `s.insert(i, x)`         | inserta *x* en *s* en la posición indicada por el índice *i* (Equivale a `s[i:i] = [x]`) |
| `s.pop()` o `s.pop(i)`   | retorna el elemento en la posición indicada por *i*, y a la vez lo elimina de la secuencia *s* |
| `s.remove(x)`            | elimina el primer elemento de *s* tal que `s[i]` sea igual a *x* |
| `s.reverse()`            | invierte el orden de los elementos de *s*, a nivel interno   |

#### [`list`](https://docs.python.org/es/3/library/stdtypes.html#list)

`class list([iterable])`

Las listas se pueden construir de diferentes formas:

- Usando un par de corchetes para definir una lista vacía: `[]`.
- Usando corchetes, separando los elementos incluidos con comas: `[a]`, `[a, b, c]`.
- Usando una lista intensiva o por comprensión: `[x for x in iterable]`.
- Usando el constructor de tipo: `list(iterable)`.

Las listas implementan todas las operaciones comunes y mutables propias de las secuencias.

##### Métodos.

- [`sort(*, key=None, reverse=False)`](https://docs.python.org/es/3/library/stdtypes.html#list.sort)

- [`sorted(iterable, /, *, key=None, reverse=False)`](https://docs.python.org/es/3/library/functions.html#sorted)

[Tutorial sobre ordenación](https://docs.python.org/es/3/howto/sorting.html#sortinghowto).

---



#### [`tuple`](https://docs.python.org/es/3/library/stdtypes.html#tuple)

`class tuple([iterable])`

Las tuplas son secuencias inmutables, usadas normalmente para almacenar colecciones de datos heterogéneos.

Las tuplas se pueden construir de diferentes maneras:

- Usando un par de símbolos de paréntesis, para indicar una tupla vacía: `()`.
- Usando una coma al final, para crear una tupla de un único elemento: `a,` o `(a, )`.
- Separando los elementos por comas: `a, b, c` o `(a, b, c)`.
- Usando la función básica [`tuple()`](https://docs.python.org/es/3/library/stdtypes.html#tuple).

> La coma es la que realmente construye la tupla, no los paréntesis. Los paréntesis son opcionales, excepto en el caso de la tupla vacía, o cuando se necesitan para evitar una ambigüedad sintáctica.



---

### Mapeo.

#### `dict`.

[`class dict(**kwargs)`](https://docs.python.org/es/3/library/stdtypes.html#dict)

Un objeto de tipo _mapping_ que relaciona valores (que deben ser _hashable_) con objetos de cualquier tipo. Los mapas son objetos mutables, y su tipo estándar son los objetos de tipo `dict`.

> Un objeto _mapping_ es un objeto contenedor que permite la recuperación de claves arbitrarias a través de un identificador _hashable_. 

Las claves de un diccionario pueden ser casi de cualquier tipo, siempre y cuando este tipo de objeto sea _hashable_.

Los diccionarios se pueden construir de diferentes formas:

- Usando una lista separada por comas de pares `key: value` entre llaves: `{'jack': 4098, 'sjoerd': 4127} o {4098: 'jack', 4127: 'sjoerd'}`.
- Usando un _dict comprehension_: `{x: x**2 for x in range(10)}`.
- Usando un constructor de tipo `dict()`.

---

### Conjunto.

Los objetos de tipo conjunto o `set`, son una colección no ordenada de distintos objetos [_hashable_](https://docs.python.org/es/3/glossary.html#term-hashable).

> Un objeto es _hashable_ si tiene un valor _hash_, que nunca cambiará durante su tiempo de vida, y puede ser comparado con otro objeto.
>
> Ser _hashable_ hace a un objeto utilizable como clave de un diccionario y miembro de un `set`, porque esta estructura de datos usan los valores _hash_ internamente.
>
> La mayoría de los objetos inmutables en Python son _hashable_.

Los conjuntos no admiten datos duplicados y tampoco registran ni la posición ni el orden de inserción de los elementos, por lo que no soportan el indexado ni operaciones de _slicing_.

Existen dos tipos básicos de conjuntos: [`set`](https://docs.python.org/es/3/library/stdtypes.html#set) y [`frozenset`](https://docs.python.org/es/3/library/stdtypes.html#frozenset).

La clase `set` mutable, con métodos como `add()` o `remove()`. Al ser mutable, no tienen un valor _hash_ y no pueden ser usados como claves de diccionarios ni como elementos de otros conjuntos.

La clase `frezenset`, en cambio, es inmutable y _hashable_. 

Los conjuntos `set` se pueden construir de las siguientes formas:

- Usando una lista de elementos separados por comas entre llaves: `{'a', 'b'}`.
- Usando un _set comprehention_: `{c for c in 'abracadabra' if c not in 'abc'}`.
- Usando un constructor de tipo `set()`.

---



## Bibliografía.

[Tipos de datos estándar en Python.](https://docs.python.org/es/3/library/stdtypes.html#)

