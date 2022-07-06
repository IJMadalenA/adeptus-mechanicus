# Apuntes sobre el despliegue.

__Apuntes sobre el despliegue de una aplicación Django con NGINX, Gunicorn y Supervisor.__



Comenzamos con lo básico:

```shell
:~$ sudo apt-get update
```

Instalamos directamente en la raíz las dependencias y actualizaciones de Python necesarias.

``` shell
~$ sudo apt-get -y install build-essential libpq-dev python-dev
```

Luego instalamos los paquetes necesarios y también el __NGINX__ y el __VirtualENV__, aún continuamos instalando todo en la raíz de Ubuntu.

```shell
~$ sudo apt-get -y install nginx supervisor python3 python3-virtualenv
```

Ahora si creamos el ___venv___ y lo activamos.

```shell
# Creamos el entorno virtual, la sintaxis del comando es la siguiente:
# ~$ virtualenv <nombre del entorno> -p python3.
~$ virtualenv venv -p python3

# Luego procedemos a activarlo para continuar desde el.
~$ source venv/bin/activate
```

Ahora instalamos __Gunicorn__ el cual, a diferencia del __NGINX__, si va dentro del __venv__.

```shell
(venv) root:~$ pip install gunicorn
```

Ahora, dentro del __venv__ procedemos a instalar __Django__ y todos los paquetes y dependencias necesarias para la aplicación.

```shell
(venv) root:~$ python -m pip install Django
(venv) root:~$ django-admin startproject <django_app_name>
(venv) root:~$ mkdir logs
(venv) root:~$ cd <new_project>

(venv) root:~/<new_project>$ python manage.py runserver
```



## ___Gunicorn___ Configuración.

Dentro del directorio __venv/bin__ creamos el archivo `gunicorn_configuration`.

```sh
:~$ cd venv/bin/
:~/venv/bin$ touch gunicorn_configuration
```

Ahora si ingresamos el comando `ls` podremos ver que hemos creado un archivo llamado `gunicorn_configuration`, el cual contiene todos los comandos necesarios para la configuración de __Gunicorn__. Cada uno de los comandos contenidos tiene un nombre bastante descriptivo que facilita entender el fin y la utilidad de cada uno.

Para esto tendremos que abrir el archivo:

```sh
:~/venv/bin$ nano gunicorn_configuration
```

Y una vez dentro del archivo copiamos los siguientes comandos:

```markdown
#!/bin/bash

NAME="<django_app_name>"  #Django application name
DIR=/home/ubuntu/django_deploy_app/test_django_app   #Directory where project is located
USER=ubuntu   #User to run this script as
GROUP=ubuntu  #Group to run this script as
WORKERS=3     #Number of workers that Gunicorn should spawn
SOCKFILE=unix:/home/ubuntu/django_deploy_app/gunicorn.sock   #This socket file will communicate with Nginx 
DJANGO_SETTINGS_MODULE=test_django_app.settings   #Which Django setting file should use
DJANGO_WSGI_MODULE=<django_app_name>.wsgi           #Which WSGI file should use
LOG_LEVEL=debug
cd $DIR
source /home/ubuntu/django_deploy_app/venv/bin/activate  #Activate the virtual environment
export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
export PYTHONPATH=$DIR:$PYTHONPATH


#Command to run the progam under supervisor
exec /home/ubuntu/django_deploy_app/venv/bin/gunicorn ${DJANGO_WSGI_MODULE}:application \
--name $NAME \
--workers $WORKERS \
--user=$USER \
--group=$GROUP \
--bind=$SOCKFILE \
--log-level=$LOG_LEVEL \
--log-file=-
```

Haremos que el archivo `gunicorn_configuration` sea un ejecutable utilizando el siguiente comando:

```sh
:~/venv/bin$ chmod u+x gunicorn_configuration
```



## Supervisor Configuración.

Primero habilitaremos el __Supervisor__ y lo ejecutaremos con los siguientes comandos:

```sh
# Tener en cuenta que esto es desde el root del ubuntu.
:~$ sudo systemctl enable supervisor
	Synchronizing state of supervisor.service with SysV service script with /lib/systemd/systemd-sysv-install.
	Executing: /lib/systemd/systemd-sysv-install enable supervisor


:~$ sudo systemctl start supervisor
```

Para configurar el __Supervisor__, creamos un archivo de configuración dentro de la siguiente dirección: `/supervisor/conf.d/`.

```sh
:~$ sudo touch /etc/supervisor/conf.d/<django_app_name>.conf
```

Abrimos el archivo de configuración y escribimos las siguientes instrucciones en el:

```sh
:~$ sudo nano /etc/supervisor/conf.d/<django_app_name>.conf
```

```markdown
[program:<django_app_name>]
command=/home/ismaelm/venv/bin/gunicorn_configuration
user=sohaib
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/home/ubuntu/<django_app_name>/logs/gunicorn-error.log
```

Ahora debemos releer el archivo de configuración de __Supervisor__ y hacer que las nuevas configuraciones estén disponibles. Con los siguientes comandos:

```sh
:~$ sudo supervisorctl reread

# Asegurate que el output sea más o menos así:
<django_app_name>: available
```

Actualizar y reiniciar el __Supervisor__:

```sh
:~$ sudo supervisorctl update

# output
<django_app_name>: added process group

:~$ sudo supervisorctl restart <django_app_name>
```

Para comprobar y verificar sus status, debemos correr el siguiente comando:

```sh
:~$ sudo supervisorctl status
```



## NGINX Configuración.

