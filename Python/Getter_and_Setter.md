# Getter, Setter and Deletter.

El principal propósito de utilizar ___getters___, ___setters___ y ___deletter___ en python, es asegurar el encapsulamiento de los datos y poder actuar sobre ellos de manera segura y según las necesidades específicas del desarrollo.

[Las variables privadas](./Variables_privadas) (o encapsuladas) en Python no son realmente campos ocultos y privados, como en otros lenguajes orientados a objetos, ya que estos siguen sido accesibles, pero su accesibilidad cambia .

Los ___getters___, ___setters___ y ___deletters___ habitualmente se utilizan de la siguiente manera:

- Añadir validaciones lógicas al rededor del valor obtenido y establecido (_getting, setting and deletting value_).
- Para evitar directamente el acceso al campo de una clase, por ejemplo, variables privadas a las que no se puede acceder directamente o modificar por usuarios externos.

Para crear una función ___getter___, ___setter___ o ___deletter___ basta con definir un método dentro de la clase para que acceda a la variable privada y opere sobre ella, sin embargo aquí utilizaremos los [decoradores](./Decoradores.md) `@property.gettet`, `@property.setter` y `@property.deletter`.

## Getter.



---



## Setter.



---



## Deletter.



---



## Referencia:

https://www.geeksforgeeks.org/getter-and-setter-in-python/

https://docs.python.org/3/library/functions.html#property

---