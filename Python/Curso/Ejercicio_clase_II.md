# Ejercicio Clase II.

__Serie de Fibonacci.__

```python
>>> # Fibonacci series:
... # the sum of two elements defines the next
... a, b = 0, 1
>>> while a < 10:
...     print(a)
...     a, b = b, a+b
...
0
1
1
2
3
5
8
```

- La primera línea contiene una asignación múltiple: las variables `a` y `b` obtienen simultáneamente los nuevos valores 0 y 1. En la última línea esto se usa nuevamente, demostrando que las expresiones de la derecha son evaluadas primero antes de que se realice cualquiera de las asignaciones. Las expresiones del laso derecho se evalúan de izquierda a derecha.

- El bucle `while` se ejecuta mientras la condición `a < 10` sea verdadera. En Python cualquier valor entero que no sea cero es `True`, de hecho, cualquier secuencia o cualquier cosa con una longitud distinta de cero es `True`, mientras que las secuencias vacías son `False`.

  ---

__Compositor automático de reggaetón.__

```python
>>> step_1 = ['Mami', 'Gata', 'Bandida', 'Chamita', 'Bandolera']
>>> step_2 = ['yo quiero', 'yo deseo', 'yo voy a', 'yo quisiera', 'yo vengo']
>>> step_3 = ['castigarte', 'amarte tierno y bonito', 'encenderte', 'darte', 'azotarte']
>>> step_4 = ['duro', 'rapido', 'lento', 'suave', 'fuerte']
>>> step_5 = ['hasta que salga el sol', 'toda la noche', 'hasta el amanecer', 'toda la vida', 'todo el día']
>>> step_6 = ['sin miedo.', 'sin anestesia.', 'contra el piso.', 'contra la pared.', 'sin compromiso.']

import random.randint

print(
    step_1[randint(0,4)], step_2[randint(0,4)], step_3[randint(0,4)], step_4[randint(0,4)], step_5[randint(0,4)], step_6[randint(0,4)]
)
```

