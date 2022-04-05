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

## Abreviación ternaria.

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



## Abreviación While.

```python
while <condition_to_evaluate>: <expresion>; <expresion>

x = 5
while x > 0: x-=1; print(x)
```

En este ejemplo el bucle `while` evalúa la condición, y si está retorna `True` se ejecuta la expresión que sigue a los dos punto`:`. En este caso se define una segunda expresión luego de un punto y coma `;` para poder imprimir el valor alterado de la variable ya que es la manera que tenemos en Python se seguir escribiendo código en la misma linea.

