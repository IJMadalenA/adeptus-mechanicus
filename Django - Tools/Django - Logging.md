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

Cada mensaje escrito por el _logger_ es un ___Log Record___, el cual tiene un _log level_ que indica la severidad del mensaje. Un ___Log Record___ puede contener metadata muy útil que describe los detalles del evento ocurrido, como el _stack trace_ del proceso afectado o el código del error.

Una ves que el _logger_ determina que un mensaje debe ser procesado, este para al ___Handler___.

### [___Handlers___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-handlers)

El ___handler___ determina que hacer con cada mensaje, el cual describe el comportamiento particular del _logging_, como puede ser escribir un mensaje en consola, en un fichero o a un _network socket_.

Los ___handlers___, al igual que los _loggers_, también tienen un _log level_, aunque si el _log level_ de un _log record_ no coincide o excede al nivel del ___handler___, este ignorará el mensaje.

Un _logger_ puede tener multiples ___handlers___, en donde cada uno puede tener un _log level_ distinto, con una configuración distinta para gestionar el comportamiento y la forma de notificar el _logger_ dependiendo del _log level_. 

### [___Filters___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-filters)

Los ___filters___ se utilizan para proveer control adicional sobre cada _log record_ que el _logger_ pasa el _handler_. Por defecto, cualquier mensaje cuyo _log level_ coincida con el del _handler_, sin embargo, si instalamos un filtro podríamos especificar criterios adicionales en el proceso de _logging_.

Los _filters_ también pueden ser utilizados para modificar el _logging record_ antes de que sea emitido, cambiando el _log level_ si ciertos criterios particulares concuerdan.

### [___Formatters___](https://docs.djangoproject.com/en/4.0/topics/logging/#topic-logging-parts-formatters)

Por ultimo, un _log record_ necesita ser renderizado como texto. El ___Formatters___ describe la forma exacta del formato de dicho texto. Un ___formatter___ usualmente consiste en un formato _string_ de Python que contienen un [LogRecord attributes](https://docs.python.org/3/library/logging.html#logrecord-attributes); sin embargo se puede personalizar el ___formatter___ para implementar un comportamiento especifico. 

---



## Implicaciones de seguridad.

El sistema de _logging_ puede manejar información potencialmente sensible del sistema, con diferentes implicaciones de seguridad hacia el mismo, y de entre la variedad de datos sensibles podría estas el _stack trace_ del proceso afectado o el _web request_. Por lo que debemos estar seguros de:

- Que información se recopila.
- Donde se almacenará posteriormente.
- Como será transferida.
- Quien podrá tener acceso a ella.

Para ayudar al controlar la recopilación de información sensible, se puede designar explícitamente cierta información para que sea filtrada, desde el _filter_, de los reportes de error, diseñando un [filter error report](https://docs.djangoproject.com/en/4.1/howto/error-reporting/#filtering-error-reports). 

### [AdminEmailHandler](https://docs.djangoproject.com/en/4.1/topics/logging/#adminemailhandler)



## Configurar el _logging_.

La librería de _logging_ de Python nos provee de varias técnicas para configurar el sistema de _logging_, desde una interfaz programática hasta archivos de configuración. Por defecto Django usa el [formato dictConfig]](https://docs.python.org/3/library/logging.config.html#logging-config-dictschema).









---

> Este MarkDown es un burdo y fallido intento por resumir, explicar y extender lo ya explicado en la documentación de Django.