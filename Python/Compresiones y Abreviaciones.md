# Compresiones y abreviaciones del código.

## Operadores Ternarios o Expresiones Condicionales

Se trata de una clausula `if`. `else` que se define en una sola linea, y evaluan si una expresión es verdadera o no, puede ser usado, por ejemplo, dentro de un `print()`.

```python
x = 5
print("Es 5" if x == 5 else "No es 5")
#Es 5
```

Los operadores ternarios están formados por tres partes, que son las mismas que las que forman un `if-else`. Tenemos la condición a evaluar, el código que se ejecuta si se cumple la condición y el código que se ejecuta si no se cumple. En este caso, tenemos los tres en la misma línea.

```python
<condition_if_true> if <expresion> else <condition_if_false>
```

### Abreviación ternaria.

Existe también  una forma acortada del operador ternario normal:

```python
True or <valor>
```

por ejemplo:

```python
var = None
message = var or "dont return anything"
print(message)
>>> "dont return anything"

def my_fun(real_name, optional_name=None):
    optional_display_name = optional_name or real_name
    print(optional_display_name)
my_fun('Pelayo')
>>> 'Pelayo'

my_fun('Pelayo', 'Cova')
>>> 'Cova

```



### Abreviación While.

```python
while <condition_to_evaluate>: <expresion>; <expresion>

x = 5
while x > 0: x-=1; print(x)
```

En este ejemplo el bucle `while` evalúa la condición, y si está retorna `True` se ejecuta la expresión que sigue a los dos punto`:`. En este caso se define una segunda expresión luego de un punto y coma `;` para poder imprimir el valor alterado de la variable ya que es la manera que tenemos en Python se seguir escribiendo código en la misma linea.



---



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

## 
