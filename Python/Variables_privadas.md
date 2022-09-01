# Variables privadas.

Las __variables públicas__ existen en toda la aplicación.

Las __variables locales__ solo existen en la función o método en la que se definen y no pueden ser accedidas por métodos de más alto o bajo nivel (métodos o funciones que sean invocadas desde el método o función donde se crean estas variables).

Las __variables privadas__ se parecen a las locales en el sentido de que desaparecen cuando se acaba de finalizar el método o función en la que fueren creadas pero tienen una ventaja añadida y es que los métodos o funciones que son invocadas desde el método en el que se han creado pueden usar esa información.

---



## Definir variables privadas.

En python no se pueden crear variables privadas, pero se puede simular su implementación utilizando convenciones de nomenclaruta especiales. 

Para implementar una variable privada en Python se utiliza el doble guión bajo `__` antes del nombre de la variable.

```python
class NewClass:
    def __init__(self, name, ager, private_info):
        self.name = name
        self.age = age
        self.__private = private_info
```

Si creamos una instancia `NewClass1` de la clase `NewClass` y accedemos al atributo `__private`, utilizando la sintaxis `NewClass1.__private`, el programa reto`rnará un error lanzando la exepción `AttributeError: 'NewClass' object has no attribute `__private`.

---



## Acceder a variables privadas.

No podemos acceder a una variable "privada" fuera de la definición de clase, pero podemos acceder a ella dentro. Entonces, podemos crear un método dentro de la clase para acceder al valor de la variable privada.

Podemos crear un método llamado `get_private` que devuelva el valor del atributo `__private`.

```python
class NewClass:
    def __init__(self, name, ager, private_info):
        self.name = name
        self.age = age
        self.__private = private_info
        
    def get_private(self):
        return self.__private
```

En lugar de definir un método, podemos acceder directamente a la variable privada, ya que cuando definimos un nombre de variable con la doble barra baja `__`, Python lo interpretará como que no existe dicha variable en memoria.

Para comprender cómo se almacena la variable, comprobaremos todos los atributos del objeto dado. Usando la función `get_private`, que toma un objeto o argumento de entrada y devuelve una lista de todos los atributos del objeto. 

En Python, cuando definimos un atributo usando doble barra baja `__`, el programa agrega el atributo antes del nombre agrega `_className` antes del nombre del atributo. Este proceso se llama __mutilación__ (_Mangling_).

---



## Mutilación - _Mangling_.

El _mangling_ en Python se utiliza para evitar conflictos con los nombres definidos en las subclases al limitar el acceso a las variables de la clase inicial. Cualquier variable cuyo nombre comience con al menos dos barras bajas `__` al inicio y máximo una barra baja al final `_`, es reemplazado con `_classname__variableName`, donde `_classname__`  es el nombre de la clase actual, obviamente exceptuando las barras bajas.

El _mangling_ está diseñado para evitar accidentes o confusiones a la hora de manejar variables, sin embargo sigue siendo posible acceder y modificar las variable que en principio consideramos privadas.

Esto puede ser útil en ciertas circunstancias, especialmente para debugear.  

---



Python entiende que los atributos nombrados usando guiones bajos dobles son variables privadas en mangling. Sin embargo, esto no es cierto ya que podemos acceder a las variables usando la sintaxis `_className__attributeName`.

Por lo que de todos modos no creamos una variable privada, sino que complicamos su acceso al cambiar la manera con la que accedemos a ella, y lo que hacemos es simular la implementación de variables privadas nombrando las variables usando un carácter de subrayado doble.

---

## Referencias.

https://www.delftstack.com/es/howto/python/python-private-variables/

https://www.geeksforgeeks.org/private-variables-python/
