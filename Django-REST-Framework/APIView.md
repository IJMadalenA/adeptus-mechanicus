# APIView.

`APIView` es la instancia que menos abstracción nos supone de entre las tres alternativas que ofrece `REST-Framework`, que serían: 

-  `APIView`.
- `GenericView`.
- `ViewSets`.

Lo que nos ofrece mucha libertad para personalizar los métodos de acuerdo a nuestras propias necesidades, sin embargo esto significa que deberemos de escribir mucho más código.

Todas las solicitudes entrantes se envían a los métodos adecuados mediante `REST-Framework APIView`. Las solicitudes web pasadas a los métodos del controlador serán instancias de solicitud del marco `REST`, no instancias `HTTPRequest` de Django, y la respuesta que devolverá la vista será del tipo de respuesta `REST-Framework`, no Django `HTTPResponse`.

---

En `Django REST-Framework` existen dos maneras de definir vistas, una es basada en clases y la otra es basada en funciones, sin embargo en Django la preferencia es hacerlo de la primera manera, y es la manera en la que las vamos a desarrollar, por considerarlas más eficientes y permite un mayor control y complejidad. 

---

`Django REST-Framework` posee algo llamado [_policy attributes_](https://www.django-rest-framework.org/api-guide/views/#api-policy-attributes), que son variables de clase que permiten modificar el comportamiento de las vistas, y disponemos de seis en total:

- `rendere_classes`: Utilizada para definir el set de clases que serán usadas para renderizar el _endpoint_. 

- `parser_classes`: Determina los _parsers_ permitidos para diferentes tipos de datos.
- `authentication_classes`: Establece los esquemas de autenticación por los que se regirá la vista.
- `throttle_classes`: Determina si una solicitud debe ser autorizada en función de la tasa de solicitudes.
- `permission_classes`: Establece los permisos que usa la vista para determinar si el usuario está autorizado para acceder.
- `content_negotiation`: Selecciona una de las múltiples representaciones posibles del recurso para devolverlo al cliente.

---



## Referencias.

https://python.plainenglish.io/all-about-views-in-django-rest-framework-apiview-e3f6a3847d37

https://dev.to/chokshiroshan/what-is-an-apiview-2g8o



[Django REST-Framework Doc - API Guide](https://www.django-rest-framework.org/api-guide/views/)

[Django REST-Framework Doc - Setting the permission policy](https://www.django-rest-framework.org/api-guide/permissions/#setting-the-permission-policy)

