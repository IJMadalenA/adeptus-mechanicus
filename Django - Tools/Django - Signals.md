# Django - Signals.

Una señal es una forma limitada de comunicación entre procesos. Es esencialmente una notificación asíncrona enviada a un proceso para informarle de un evento. cuando se le manda una señal a un proceso, el sistema modifica su ejecución normal. 

Las señales son vulnerables a que se produzcan [condiciones de carrera](https://es.wikipedia.org/wiki/Condici%C3%B3n_de_carrera) puesto que las señales son asíncronas y puede ocurrir que llegue otra señal (incluso del mismo tipo) al proceso mientras transcurre la ejecución de la función que manipula la señal.

> La __condición de carrera__ hace referencia a cuando el resultado de un proceso depende de la consecución de dos o mas eventos que se ejecutan en un orden arbitrario y que van a trabajar sobre el mismo recurso compartido. Se puede producir dicho problema cuando estos eventos no se terminan de ejecutar en el orden adecuado.

Las señales de Django son una forma de informar a las aplicaciones de ciertas tareas cuando estas se llevan a cabo, permitiendo realizar acciones inmediatamente después de que se libere la señal.

- Existen tres tipos de señales:
  - __pre_save / post_save__.
  - __pre_delete / post_delete__.
  - __pre_init / post_init__.



## Cuando usar o no las señales.

### Cuando están bien las señales:

- El receptor de la señal necesita realizar cambios en más de un modelo.
- Desea enviar la misma señal desde varias aplicaciones y hacer que se manejen de la misma manera por un receptor común.
- Desea invalidar un caché después de guardar un modelo.
- Tiene un escenario inusual que necesita una devolución de llamada, y no hay otra manera de manejarlo además de usar una señal. Por ejemplo, desea activar algo en función del `save()` o `init()` del modelo de una aplicación de terceros la cual no se puede modificar y su extensión podría ser imposible, por lo que una señal proporciona un desencadenante para una devolución de llamada.

### Cuando no están bien las señales:

- La señal se relaciona con un modelo en particular y se puede mover a uno de los métodos de ese modelo, posiblemente llamado por el `save()`.
- La señal se puede reemplazar con un método de administrador de modelos personalizados.
- La señal se relaciona con una vista particular y se puede mover a esa vista.



