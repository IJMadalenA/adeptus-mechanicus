# Python - Variables y alcance.

Una variables es un contenedor que alacena valores de datos en memoria.



## Variables: `global` y `nonlocal`.

### `global`.

El uso de `global` permite acceder desde una función o desde un espacio local a variables globales, y de no usarla tendríamos un `UnboundLocalError`. Aunque es bastante útil se debe tener cuidado con las variables globales.

```python
a = 0

def suma_uno():
    global a
    a = a + 1

suma_uno()
print(a)

# Salida: 1
```

- Cuando creamos una variable dentro de una función, esta función por defecto será local.
- Cuando definimos una variable fuera de una función, esta será global por defecto, sin la necesidad de utilizar la keyword`global`.
- `global` sirve para definir variables globales dentro de una función.
- Utilizar `global` fuera de una función no tiene efecto.

__Modificar una variable global desde dentro de una función:__

```python
c = 1 # global variable
    
def add():
    c = c + 2 # increment c by 2
    print(c)

add()
```

Cuando ejecutamos este programa nos retornará un error:

```python
UnboundLocalError: local variable 'c' referenced before assignment
```

Esto es debido a que solo podemos acceder a la variable global, pero no podemos modificarla desde dentro de una función

Nos muestra un error debido a que Python trata a la variable como si esta fuera local, a pesar de que esta no está definida dentro de la función, por lo que estamos haciendo referencia a una variable que no ha sido asignada, al menos no dentro del alcance de la función. 

La solución a esto es utilizar la keyword `global`.

```python
c = 0 # global variable

def add():
    global c
    c = c + 2 # increment by 2
    print("Inside add():", c)

add()
print("In main:", c)

Inside add(): 2
>>> In main: 2
```

En este caso la función accede a la variable global y logra modificarla.

### `nonlocal`.

El uso de `nonlocal` es útil cuando tenemos funciones anidadas, ya que permite acceder a variables locales desde fuera del espacio en el que fue definida.

```python
def funcion_a():
    x = 10

    def funcion_b():
        nonlocal x
        x = 20
        print("funcion_b", x)

    funcion_b()
    print("funcion_a", x)


funcion_a()

# Salida:
# funcion_b 20
# funcion_a 20
```



## Eliminar variables - `del`.

El uso de `del` nos permite eliminar una variable del _scope_, pudiendo resultar útil cuando trabajamos con variables que almacenan gran cantidad de datos. Es una manera explícita de indicar que ya no queremos una variable.

```python
a = 10
del a
print(a)

# Salida: NameError: name 'a' is not defined
```

