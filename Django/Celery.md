# Celery.

Es una biblioteca de Python, escrita en Python, que sirve para gestionar colas de tareas distribuidas, es decir, trabajar con diferentes tareas y distribuirlas en diferentes procesos, en diferentes ordenadores.

- Dividir el _back-end_ de una aplicación en _receptor_ y _realizadores de tareas_.
- Uniformizar la respuesta del _back-end_.
- Crear arquitecturas de microservicios.

__Celery es útil para las siguientes tareas__:

- Registro, almacenamiento o cualquier tipo de evento que no requiera de respuesta al origen.
- Intermediario entre servicio web y otros microservicios.
- Ejecución retrasada de tareas, como programar tareas para que se ejecuten cada cierto tiempo, como monitorización o ejecución de tareas programadas.

---

## Broker de tareas.

> Las colas de tareas, brokers de tareas o brokers de mensajes son servicios de mensajería que actúan como intermediarios.

Permite sincronizar los datos entre diferentes partes de un sistema. Podemos tener diferentes servicios, y estos vana poder compartir datos a través del _broker_ de mensajería que se encargará de que cada vez que reciba un dato un servicio, este se distribuya a los otros.

También elimina el almacenamiento central de datos, ya que evita que se formen cuellos de botella por donde tengan que entrar muchísimos datos a la vez y que se tenga que escalar, sino que cada microservicio se encargará de manejar y almacenar sus datos.

Sirve para activar de forma segura microservicios.

Se asegura de que el mensaje sea enviado y recibido.

Los _brokers_ actúan como mediadores de eventos, fundamental para desarrollar arquitecturas dirigidas por eventos.

---