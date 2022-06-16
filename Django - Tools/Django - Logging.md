# Django - logging.

[Django logging documentation](https://docs.djangoproject.com/en/4.0/topics/logging/#logging-explanation)

Las herramientas de _logging_ de Django nos proveen de una manera más elegante, flexible y estructurada de obtener información útil a la hora de _debugear_ nuestra aplicación, su estado, la actividad de los usuarios y  su funcionamiento. 

El _logging_ es una técnica que nos permite registrar y rastrear los eventos ocurridos mientras el código es ejecutado, funcionando como un programa separado que va llevando un registro de aquella información que consideremos relevante, tanto para el mantenimiento como para la monitorización de la aplicación.

Añadir _logging_ a nuestro código implica tres importantes pasos a tener en cuenta:

- Elegir que data generar y en que parte del código hacerlo.
- Elegir la manera en la que queremos formatear los _logs_.
- Elegir como transmitir los _logs_.

# Generalidades sobre el _logging_.

Django utiliza y extiende el modulo de ___logging___ ya incorporado en Python, el cual, obviamente, dispone de su propia documentación.

[Python loggind documentation](https://docs.python.org/3/library/logging.html#module-logging)



La configuración de _logging_ consiste en cuatro partes:

- [___Loggers___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-loggers)
- [___Handlers___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-handlers)
- [___Filters___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-filters)
- [___Formatters___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-formatters)



### [___Loggers___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-loggers)

Es una entrada al sistema de registro. El _logger_ es una parte que, cuando el _logging_ es llamado, registra la información de un evento determinado para su procesamiento.

Los _loggers_ pueden ser configurados para tener un _log level_, es decir, una jerarquía de importancia, que describe la severidad del mensaje que el _logger_ maneja, y estos niveles son:

| Log-Level    | Description                                                  |
| :----------- | ------------------------------------------------------------ |
| **DEBUG**    | Es información del sistema a un bajo nivel con propósitos de _debugging_. Es el nivel más bajo de urgencia. |
| **INFO**     | Similar a _debug_. Proporciona información general para conocer que está ejecutando el sistema. |
| **WARNING**  | Registra problemas menores a un bajo nivel que no implican la detención del código. |
| **ERROR**    | Información que describe un problema mayor que puede haber causado la detención del código. |
| **CRITICAL** | Máximo nivel de urgencia. Describe un problema critico que significó la detención del sistema. |



### [___Handlers___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-handlers)



### [___Filters___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-filters)



### [___Formatters___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-formatters)









---

> Este MarkDown es un burdo y fallido intento por resumir, explicar y extender lo ya explicado en la documentación de Django.