# Django - Signals.

Una señal es una forma limitada de comunicación entre procesos. Es esencialmente una notificación asíncrona enviada a un proceso para informarle de un evento. cuando se le manda una señal a un proceso, el sistema modifica su ejecución normal. 

Las señales son vulnerables a que se produzcan [condiciones de carrera](https://es.wikipedia.org/wiki/Condici%C3%B3n_de_carrera) puesto que las señales son asíncronas y puede ocurrir que llegue otra señal (incluso del mismo tipo) al proceso mientras transcurre la ejecución de la función que manipula la señal.

> La __condición de carrera__ hace referencia a cuando el resultado de un proceso depende de la consecución de dos o mas eventos que se ejecutan en un orden arbitrario y que van a trabajar sobre el mismo recurso compartido. Se puede producir dicho problema cuando estos eventos no se terminan de ejecutar en el orden adecuado.

Las señales de Django son una forma de informar a las aplicaciones de ciertas tareas cuando estas se llevan a cabo, permitiendo realizar acciones inmediatamente después de que se libere la señal.

- Existen tres tipos de señales:
  - __pre_save / post_save__.
  - __pre_delete / post_delete__.
  - __pre_init / post_init__.



