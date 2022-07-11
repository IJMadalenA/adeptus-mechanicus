# GeoDjango.

Es un módulo incluido en Django que permite convertirlo en un _framework_ para aplicaciones geográficas, con una base de datos espacial mediante tres características:

- Tipos de datos espaciales.
- Indices espaciales.
- Funciones que operan sobre ellos.

PostGis añade soporte de objetos geográficos a la base de datos relacional de PostgreSQL, convirtiéndola en una base de datos espacial para su utilización en sistemas de información geográfica.

## Configuración e Instalación.

### [PostGIS](https://docs.djangoproject.com/es/4.0/ref/contrib/gis/install/postgis/).

El PostGis requiere de varias instalaciones antes de poder funcionar, un par de ellas serán dentro del __venv__ de Python y otras directamente en nuestro sistema. 

Lo primero que instalaremos será [GDAL](https://docs.djangoproject.com/es/4.0/ref/contrib/gis/install/geolibs/#gdalbuild), una librería geoespacial, el cual depende de otras dos librerías, que son: [GEOS](https://docs.djangoproject.com/es/4.0/ref/contrib/gis/install/geolibs/#geosbuild) y [PROJ](https://docs.djangoproject.com/es/4.0/ref/contrib/gis/install/geolibs/#proj4).

```shell
$ sudo apt-get install gdal-bin

$ sudo apt-get install geos

$ sudo apt-get install proj-bin

$ sudo apt-get install gdal-bin
```

Ahora dentro del __venv__ de Python instalaremos el [psycpg2](https://pypi.org/project/psycopg2/), que es un adaptador de Python con PostgreSQL, lo que nos permitirá manejar y operar sobre la base de datos.

```python
(venv) $ pip install psycopg2
(venv) $ pip install psycopg2-binary
```

---

Ahora si podremos instalar PostGIS ejecutando el siguiente comando:

```shell
$ sudo apt-get install postgis
```

Ya con todo instalado podemos crear la base de datos en __PostgreSQL__ con la extensión de __PostGIS__.

Primero creamos la base de datos con alguno de estos dos comandos:

- Este primero desde la terminal de Ubuntu, sin tener que ingresar a PostgreSQL.

```shell
sudo -u postgres createdb <db_name>
```

- También lo podemos hacer desde dentro de __PostgreSQL__.

```sql
$ sudo su - postgres

~$ createdb <db_name>
```

Si seguimos la segunda opción ya estaremos dentro de __PostgreSQL__, por lo que el primer comando será innecesario.

```sql
$ sudo su - postgres

~$ psql <db_name> 
~$ CREATE EXTENSION postgis;
```

---

Suponiendo que ya a tenemos la aplicación creada, ahora debemos conectarla con la base de datos de __PostgreSQL__, desde el archivo de __settings.py__

```
DATABASES = {
    'default': {
        'ENGINE': 'django.contrib.gis.db.backends.postgis',
        'NAME': 'geodjango',
        'USER': 'geo',
        'PASSWORD': '123456',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    },
}
```

Ahora que la base de datos está conectada con nuestra aplicación de Django, podemos aplicar las migraciones. 

```shell
(venv) $ python manage.py makemigrations

(venv) $ python manage.py migrate
```



```shell
service postgresql status
```



```

```



