# HTTP - Request methods.

__HTTP__ define una serie de métodos para realizar peticiones en los que se indica el comportamiento o acciones que se pretenden realizar sobre un recurso determinado.

---

## [GET.](https://restfulapi.net/http-methods/#get)

Pide unicamente la representación o información de un recurso específico, y no lo modifica de ninguna manera. Las peticiones que utilicen `GET` solo deberían de retornar datos.

Al no modificar el estado del recurso, este método es llamado como [seguro](https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP).

Adicionalmente, el método `GET` debería ser [idempotente](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent), al permitir realizar múltiples peticiones que retornen el mismo resultado hasta que otro método (como `POST` o `PUT`) modifique su estado en el servidor.

| __Request has body__ | __No__ |
| :------ | :----: |
| __Successful response has body__ | __Yes__  |
| [__Safe__](https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP) | __Yes__  |
| [__Idempotent__](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent) | __Yes__  |
| [__Cacheable__](https://developer.mozilla.org/en-US/docs/Glossary/cacheable) | __Yes__  |
| __Allowed in HTML forms__ | __Yes__ |

En Django REST-Framework, el método `GET` es equivalente a los métodos `list` y `retrieve` de las `APIView`.

### Response code.

- Si el recurso es encontrado en el servidor, se retornará un código [HTTP 200 (OK)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.1).

- En el caso de no encontrarse el recurso en el servidor, se retornará un código HTTP 401 (NOT_FOUND).

- Del mismo modo, si la petición `GET` en si misma es errónea o está mal formada, el servidor retornará un código HTTP 400 (BAD_REQUEST).

### Ejemplo de URI.

```python
HTTP GET http://www.appdomain.com/users
HTTP GET http://www.appdomain.com/users?size=20&page=5
HTTP GET http://www.appdomain.com/users/123
HTTP GET http://www.appdomain.com/users/123/address
```

---



## POST.

Envía una entidad al recurso especificado, lo que a menudo provoca un cambio de estado en el servidor.

Se utiliza para crear un nuevo recurso subordinado, es decir un recurso que depende de otro para ser almacenado, como lo puede ser un archivo el cual está subordinado a un directorio que lo contenga, o una fila que está subordinada a una base de datos que la albergue.

Cuando se habla estrictamente de este método en API's REST, el método `POST` se utiliza para crear un nuevo recurso dentro de una colección de recursos.

Las respuestas a este método no son cacheables a menos que se incluya apropiadamente un Cache-Control o un campo de expiración en el encabezado.

Tener en cuenta que el método `POST` ni es [seguro](https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP) ni es [idempotente](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent), y si este método es invocado dos veces, este retornará dos recursos distintos, que contienen la misma data excepto el id del recurso. 

| Request has body                                             | Yes                                           |
| :----------------------------------------------------------- | --------------------------------------------- |
| __Successful response has body__                             | __Yes__                                       |
| [__Safe__](https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP) | __No__                                        |
| [__Idempotent__](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent) | __No__                                        |
| [__Cacheable__](https://developer.mozilla.org/en-US/docs/Glossary/cacheable) | __Only if freshness information is included__ |
| __Allowed in__ [__HTML forms__](https://developer.mozilla.org/en-US/docs/Learn/Forms) | __Yes__                                       |

En Django REST-Framework, el método `POST` es equivalente al método `create()` de las `APIView`.

La diferencia entre el método `PUT` y `POST` es que el primero de estos es  [idempotente](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent), es decir que si una o muchas veces sucesivas, este tendrá el mismo efecto, sin efectos secundarios, y retornará el mismo recurso con el mismo `id`. 

### Response code.

Si el recurso fue creado satisfactoriamente, la respuesta debería ser un código HTTP [201 (CREATED)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.2), y contener una entidad que describa el estatus de la petición y refiera al nuevo recurso creado.

Muchas veces el recurso creado por el método `POST` no genera un recurso que pueda ser identificado por una [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier), por lo que en estos casos sería correcto el retornar un código HTTP [200 (OK)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.1) o un [204 (NO_CONTENT)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.5).

Este método está diseñado para ser una manera uniforme de realizar funciones para añadir información al sistema, relativo a las siguiente funciones:

- Extender la base de datos a través de una operación de adición.
- Proveer un bloque de datos resultante de enviar un formulario a un proceso de manejo de datos.
- Añadir un nuevo usuario a través de un modulo de registro.
- Añadir nueva información al sistema.

### Ejemplo de URI.

```python
HTTP POST http://www.appdomain.com/users
HTTP POST http://www.appdomain.com/users/123/accounts
```

---



## PUT.

Reemplaza toda la representación de un recurso actual por el provisto dentro del método `PUT`.

Este método es ante todo un método para actualización, y en el caso de que el recurso no exista, la API decidirá si crear un recurso nuevo o no. 

| Request has body                                             | Yes     |
| :----------------------------------------------------------- | ------- |
| __Successful response has body__                             | __May__ |
| [__Safe__](https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP) | __No__  |
| __[Idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)__ | __Yes__ |
| __[Cacheable](https://developer.mozilla.org/en-US/docs/Glossary/cacheable)__ | __No__  |
| __Allowed in__ [__HTML forms__](https://developer.mozilla.org/en-US/docs/Learn/Forms) | __No__  |

En Django REST-Framework, el método `PUT` es equivalente al método `update()` de las `APIView`.

### Response code.

- Si un nuevo recurso es creado por el método `PUT` desde la API, el servidor deberá informar al usuario a través del código [HTTP 201 (CREATED)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.2).
- En el caso de que el recurso exista y sea modificado, la respuesta sería un código [HTTP 200 (OK)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.1) o un [204 (NO_CONTENT)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.5) que indica la petición se completó con exito.
- En el caso de que el recurso no tenga una representación, pero este haya sido modificado exitosamente, el servidor podrá retornar un código [HTTP 200 (OK)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.1) o un [204 (NO_CONTENT)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.5) para indicar el éxito de la operación.

### [Diferencias entre `PUT` y `POST`.](https://restfulapi.net/rest-put-vs-post/)

| `PUT`                                                        | `POST`                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| La URI hace referencia a un objeto.                          | La URI no hace referencia a ningún objeto.                   |
| Si el objeto referido existe, este se debería de sustituirlo con los nuevos datos adjuntos en la petición, y en el caso de que no exista se podría crear uno nuevo. | Esencialmente es un método para añadir nuevos objetos a la base de datos, y no hace referencia a ningún objeto concreto. |
| `PUT/question/{question-id}/`                                | `POST/question/`                                             |
| Es idempotente, por lo que no importa cuantas veces realicemos la llamada, siempre recibiremos la misma respuesta con el mismo identificador del servidor. | No es idempotente, por lo que si realizamos la llamada una $n$ cantidad de veces, recibiremos una $n$ cantidad diferente de respuestas de objetos distintos creados. |
| Utilizamos `PUT` cuando queramos sustituir un único objeto que ya existe en la base de datos. | Utilizamos `POST` cuando queramos adjuntar un objeto en una colección de objetos. |
| `PUT` reemplaza al objeto señalado, para editarlo se utiliza el método `PATH`. | `POST` no debería hacer referencia a ningún objeto.          |

### Ejemplo de URI.

```python
HTTP PUT http://www.appdomain.com/users/123
HTTP PUT http://www.appdomain.com/users/123/accounts/456
```


---



## DELETE.

Elimina el recurso especificado en la URI de la llamada.

| Request has body                                             | __May__ |
| :----------------------------------------------------------- | ------- |
| __Successful response has body__                             | __May__ |
| [__Safe__](https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP) | __No__  |
| [__Idempotent__](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent) | __Yes__ |
| [__Cacheable__](https://developer.mozilla.org/en-US/docs/Glossary/cacheable) | __No__  |
| __Allowed in__ [__HTML forms__](https://developer.mozilla.org/en-US/docs/Learn/Forms) | __No__  |

En Django REST-Framework, el método `DELETE` es equivalente al método `destroy()` de las `APIView`.

### Response code.

Si el método `Delete` se ejecuta satisfactoriamente, este podría retornar diferentes códigos HTTP.

- Un código [202 (ACCEPTED)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.3) significaría que el procedimiento ha sido aceptado pero aún no se ha ejecutado enteramente.
- Un código [204 (NO_CONTENT)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.5) significa que la acción ha sido realizada pero no se proporcionará más contenido. 
- Un código [200 (OK)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.1) significa que la acción se ha ejecutado y el mensaje de respuesta incluye una representación que describe el estado.

### Ejemplo de URI.

```python
HTTP DELETE http://www.appdomain.com/users/123/
HTTP DELETE http://www.appdomain.com/users/123/accounts/456/
```

---



## PATH.

Aplica modificaciones parciales  a un recurso especificado en la URI de la llamada.

Para ser más precisos, el método `PATH` es la elección correcta para realizar modificaciones parciales en recursos existentes, y solo se debería de utilizar `PUT` para reemplazar por completo un recurso.

La compatibilidad con el método `PATH` tanto en navegadores, servidores y _frameworks_ no es universal y es un detalle a investigar y tener en cuenta a la hora de elegir las herramientas con las que se construirá la API.

| Request has body                                             | Yes     |
| :----------------------------------------------------------- | ------- |
| __Successful response has body__                             | __Yes__ |
| [__Safe__](https://developer.mozilla.org/en-US/docs/Glossary/Safe/HTTP) | __No__  |
| [__Idempotent__](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent) | __No__  |
| [__Cacheable__](https://developer.mozilla.org/en-US/docs/Glossary/cacheable) | __No__  |
| __Allowed in__ [__HTML forms__](https://developer.mozilla.org/en-US/docs/Learn/Forms) | __No__  |

En Django REST-Framework, el método `PATH` es equivalente al método `partial_update()` de las `APIView`.

### Response code.

Una respuesta satisfactoria podría ser indicada por cualquiera de los códigos [2xx](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3) de estatus HTTP, aunque esto estaría condicionado por el contenido de la respuesta.

Un código [204 (NO_CONTENT)](https://datatracker.ietf.org/doc/html/rfc7231#section-6.3.5) significaría que el servidor ha cumplido satisfactoriamente la petición pero que no proporciona contenido adicional para enviar en el cuerpo de la respuesta.

### Ejemplo de URI.

```python
HTTP PATH http://www.appdomain.com/users/123
HTTP PATH http://www.appdomain.com/users/123/accounts/456
```



---

## [Códigos de estado HTTP.](https://restfulapi.net/http-status-codes/)

---

## Glosario.

### idempotente.

> Dicho de un elemento de un conjunto: Que tiene la propiedad de que al multiplicarse por si mismo vuelve a obtenerse el mismo elemento.

La __idempotencia__ es la propiedad para realizar una acción determinada varias veces y aun así conseguir el mismo resultado que se obtendría si se realizase una sola vez. 

Formalmente, si $S$ es un conjunto algebraico con una operación binaria $*$, entonces un elemento $s \in S$ se dice idempotente si $s * s = s$. Si todo $s$ fuese idempotente bajo $*$, entonces la operación en sí se denominaría operación idempotente. En particular, cualquier elemento identidad es un idempotente bajo $*$.

$idM: M \to M $

$idM: m \longmapsto n=idM(m)=m$

### Métodos seguros (_Safe methods_).

El método de una llamada es considerado "seguro" si estos son esencialmente de "solo-lectura", donde el cliente no solicita ningún cambio de estado en el servidor como resultado de la ejecución del método seguro.

Los métodos `GET`, `HEAD`, `OPTIONS` y `TRAVE` son considerados como métodos seguros.

---

## Fuente.

https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods

https://restfulapi.net/http-methods/

https://httpwg.org/specs/rfc7231.html#method.definitions

---
