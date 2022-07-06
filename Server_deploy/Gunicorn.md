# Gunicorn.

https://gunicorn.org/

https://docs.gunicorn.org/en/latest/index.html

Es un __WSGI__ de python (_Python Web Server Gateway Interface_) de servidores __HTTP__. A menudo se implementa con __NGINX__, ya que los dos tienen características complementarias. El servidor __Gunicorn__ generalmente es compatible con diversos _frameworks_ web, como __Django__, de simple implementación, ligero en su uso de recursos y bastante rápido. 



## WSGI.

> Pronunciado <<whiskey>> o <<wiz-ghee>>.

El __WSGI__ es una convención realizada para diseñar las llamadas realizadas a los servidores web, para que estos reenvíen solicitudes a aplicaciones web o marcos escritos en Python.

Originalmente fue descrito como el [PEP-333](https://peps.python.org/pep-3333/#preface-for-readers-of-pep-333) en el 2003, y en el 2010 se actualizaron sus especificaciones para Python3 dando cabida al [PEP-3333](https://peps.python.org/pep-3333/).

En el [PEP-333](https://peps.python.org/pep-3333/#preface-for-readers-of-pep-333) describen la razón del desarrollo de esta convención de la siguiente manera:

> Python currently boasts a wide variety of web application frameworks, such as Zope, Quixote, Webware, SkunkWeb, PSO, and Twisted Web -- to name just a few. This wide variety of choices can be a problem for new Python users, because generally speaking, their choice of web framework will limit their choice of usable web servers, and vice versa... By contrast, although Java has just as many web application frameworks available, Java's "servlet" API makes it possible for applications written with any Java web application framework to run in any web server that supports the servlet API.

__WSGI__ fue creado como una interfaz de implementación neutral y de uso común entre servidores web, aplicaciones y _frameworks_, para promover un campo estándar para el desarrollo de aplicaciones web. Permitiendo un despliegue más estable, siendo capas de manejar más llamadas a la vez y ser más rápido. 



---

https://gunicorn.org/#docs

https://pypi.org/project/gunicorn/

https://docs.gunicorn.org/en/stable/