# Stripe - Basic

[Stripe API documentacion](https://stripe.com/docs/api?lang=python)

## Estructura de la suscripción.

- __¿Cuantos niveles de precios diferentes tendrá el producto y cuáles serán los precios?__
- __¿Habrá un nivel gratuito o de prueba?__
- __¿Qué se incluirá en cada nivel?__
- __¿Qué opciones de facturación se ofrecerán?__ Frecuentemente se utiliza el modelo de pago mensual o pago anual.
- __¿Se ofrecerá una estructura de precios única o se cobrará según el uso?__



## Subscription data modeling.

El sistema de facturación/suscripción es complicado e involucra muchas  partes, tanto del lado de la configuración (las suscripciones que ofrecemos) como del pago (los datos necesarios para registrar el pago de un cliente e inscribirlo en uno de los planes).

Del lado de la configuración se deben diseñar los niveles que existen, como se les asignarán las diferentes características a las que tendrán acceso en la aplicación y cuanto costará cada intervalo de tiempo.

Del lado de los pagos se necesita modelar los detalles de los pagos individuales como también la información sobre el cliente y su suscripción, incluyendo el plan que tienen, el estatus del pago y los detalles de la renovación.

[Stripe billing documentation](https://stripe.com/docs/billing)

[Stripe - products and prices](https://stripe.com/docs/products-prices/overview#create-product)

Los __productos__ no tienen información sobre su precio, en cambio, tienen uno o más precios que determinan por cuanto y como se facturará el producto. Crear más de un __precio__ por el producto permite variar el intervalo de facturación o la moneda de pago.

___Products___ es el principal modelo que define los niveles y permisos, por ejemplo Pro, Basic, etc. Y ___Prices___ son las opciones que los usuarios tienen para suscribirse a esos productos, por ejemplo mensual, anual o plan estudiantil. 

[Stripe - Subscriptions API documentation](https://stripe.com/docs/api/subscriptions)

[Stripe - Customers API documentation](https://stripe.com/docs/api/customers/object)

El modelo principal sera el de ___Subscription___, el cual nos permitirá cobrar a los usuarios de forma recurrente.

### Modelado y sincronización de datos entre la aplicación y Stripe. 

Desde un alto nivel, mantendremos los __productos__, __precios__, __suscripciones__ y __clientes__ en _Stripe_. Pero necesitaremos poder hacer referencia a ellos para poder utilizar esta información en nuestra propia aplicación, para poder:

- Mostrar el _pricing_ en una pagina con los diferentes niveles.
- Determinar si un usuario tiene una suscripción activa para que pueda acceder a una función en particular. 
- Enviar factoras o recordatorios de pago a los clientes.

Podemos pensar a _Stripe_ como una "copia maestra" de nuestros datos y tratar a nuestra aplicación como una copia _read_only_. 

#### Abordajes de Stripe.

##### 1. Stripe ID's.

__Almacenar los _Stripe ID's_ de los objetos que utilizaremos__.

Todo lo que almacenaremos es el ___Stripe ID___ del objeto en cuestión. Entonces, cuando necesitemos más información sobre este objeto, como averiguar su precio en particular, consultaremos la __API__ de ___Stripe___ con el ___ID___ apropiado y obtendríamos la información que necesitamos. 

```python

class MyStripeModel(models.Model):
    name = models.CharField(max_length=100)
    stripe_subscription_id = models.CharField(max_length=100)
    
```

Esto mantiene las cosas bastante simples de nuestro lado, ya que no necesitaremos almacenar nada en nuestro local ni necesitaremos preocuparnos porque nuestra base de datos este sincronizada con la de ___Stripe___. Sin embargo, cada vez que necesitemos datos lo deberemos conseguir de ___Stripe___, con la garantía de que esta estará actualizada. 

El principal problema de este abordaje es el desempeño. Las solicitudes remotas son costosas y, por lo tanto, si intentamos mantener al mínimo los tiempos de carga de la página, puede ser importante minimizar la cantidad de llamadas a la __API__.

Los problemas de rendimiento se pueden mitigar con el almacenamiento en caché, pero esta no siempre es una opción fácil. 

##### 2. Copia local.

__Mantener una copia de los modelos de _Stripe_ en la base de datos de nuestra aplicación local__.

En este abordaje mantenemos nuestros datos de _Stripe_ sincronizados con la base de datos de la aplicación. Entonces, en vez de tener que llamar a _Stripe_ cada vez que necesitemos información de un producto en particular, simplemente podemos buscar en nuestra propia base de datos.

Esto resuelve los problemas de rendimiento y hace mucho más fácil trabajar con los datos de _Stripe_, simplemente utilizando el __ORM__ como con el resto de datos. 

```python

class StripeSubscription(models.Model):
    start_date = models.DateTimeField(help_text="The start date of the subscription")
    status = models.CharField(max_length=20, help_text="The status of this subscription.")
    # other data we need about the Subscription from Stripe goes here.
    
    
class MyStripeModel(models.Model):
    name = models.CharField(max_length=100)
    stripe_subscription = models.ForeignKey(StripeSubscription, on_delete=models.SET_NULL)
    
```

El problema con este abordaje es que la sincronización de los datos es complicada.

Si no tenemos cuidado, nuestra copia local puede dejar de estar sincronizada con _Stripe_, y entonces podrían ocurrir cosas como que alguien se suscriba a un plan de 10€ mensuales y se le facturen 20€ por el primer mes ya que nuestros datos no están sincronizados.

El primer enfoque puede ser recomendables para configuraciones sencillas, y limitarse simplemente a almacenar los ___Stripe ID___ de los productos, sin embargo, para aplicaciones hechas con _Django_ es mucho mejor el segundo enfoque, especialmente gracias a herramientas como la librería [dj-stripe](https://dj-stripe.dev/dj-stripe/2.6/), que permite mantener nuestros datos sincronizados con _Stripe_ con muy poco esfuerzo, lo cual nos brinda el beneficio del rendimiento de tener los datos de forma local y obtener nuestros datos de _Stripe_ de forma sencilla a través del ORM de _Django_.

[dj-stripe - Django + Stripe Made Easy](https://dj-stripe.dev/dj-stripe/2.6/)



## Configuración del modelo de facturación.

Para comenzar: [Stripe's guide to setting up a Subscription](https://stripe.com/docs/billing/subscriptions/fixed-price)



## Instalación y configuración de _dj-stripe_.

[Instalación de _dj-stripe_](https://dj-stripe.dev/en/stable/installation.html)

Luego de la descarga, registrar la aplicación en el archivo `settings.py` en el `INSTALLED_APPS` y todo lo habitual, necesitamos configurar las ___API KEYS___ de _Stripe_ en el `settings.py` de la aplicación. 

 [Obtener ___Test API Keys__](https://dashboard.stripe.com/test/apikeys)

```python

STRIPE_TEST_PUBLIC_KEY = os.environ.get("STRIPE_TEST_PUBLIC_KEY", "pk_test_51LFcKTEHjgRCeapN4zieoQc9j97O2ifGGTEq8J17kJC0AofQfzbZIhInot51EGCfqR1RTkTwKiLlbD1RoO1klTzi00JtutDSuG")
STRIPE_TEST_SECRET_KEY = os.environ.get("STRIPE_TEST_SECRET_KEY", "sk_test_51LFcKTEHjgRCeapNvdXKCvMv3TQYuEkXt4Fa7ppXmF2D7TF4lC7lrFDMxYX5FEMRipEsSHoWXyijWGuYHTvmBBjL00xxwTYwFy")
STRIPE_LIVE_MODE = False
DJSTRIPE_WEBHOOK_SECRET = "whsec_xxx"
DJSTRIPE_USE_NATIVE_JSONFIELD = True  # We recommend setting to True for new installations
DJSTRIPE_FOREIGN_KEY_TO_FIELD = "id"

```

Al agregar los _Keys_, necesitamos crear la base de datos de ___dj-stripe___.

```shell
python manage.py migrate
```

---

Ahora con ___dj-stripe___ configurado, sincronizar nuestros productos y precios es una tarea sencilla.

Simplemente debemos correr el siguiente comando:

```shell
python manage.py djstripe_sync_plans_from_stripe
```



Si tienes el server levantado puedes acceder a la base de datos desde esta dirección: [Stripe local Admin direction](http://localhost:8000/admin/djstripe/product/)

## Trabajar con productos y precios.

> Para la librería de `dj-stripe`, los el _pricing_ es definido como _plans_, por lo que hay que tener en cuenta que son campos con el mismo significado y utilidad. 

# Crear una pagina de _pricing_.

El esquema para crear una pagina de _pricing_ es idéntico a cualquier otro _endpoint_ en _Django_.

### Metadata para los objetos _Stripe_.

Es necesario añadir información para crear la pagina de _pricing_, lo cual podemos afrontar de tres maneras diferentes. 

#### 1. Almacenar la información en _Stripe_.

_Stripe_ permite adjuntar metadatos arbitrarios a los objetos, de modo que podamos almacenarlos allí, sincronizarlos con la base de datos y luego mostrarlos, de manera similar a las otras piezas de información.

#### 2. Almacenar la información en la B.DD. 

Debido a que todos los datos son específicos de la aplicación, no hay necesidad de obtenerlos de _Stripe_. Por lo que simplemente podríamos crear una base de datos local para almacenarlo. Entonces no tendremos que utilizar la metadata de _Stripe_ ni preocuparnos por la sincronización.

#### 3. Almacenar la información en el codigo.

 Si de todas maneras la data va a estar acoplada a la aplicación, podríamos omitir la consulta a la base de datos directamente y simplemente mantenerla en nuestro código fuente. Esto simplificaría aún más las cosas, aunque tiene la desventaja de requerir código para realizar cambios. 

> En este caso implementaremos la tercera opción. 

---

Primero debemos definir las _features_ como constantes en un archivo llamado `features.py`.

```python

UNLIMITED_WIDGETS = 'Unlimites Widgets'
LUDICROUS_MODE = 'Ludicrous Mode'
PRIORITY_SUPPORT = 'Priority Support'

```

Este paso nos permite tener un código más flexible y con una mejor practica que nos permite referenciar más fácilmente sin preocuparnos de cometer errores. En este ejemplo solo se desplegarán nombres, sin embargo se pueden desplegar estructuras arbitrarias también.

Esto lo podemos adjuntar in un archivo llamado `metadata.py`:

```python

@dataclass
class ProductMetadata(object):
    """
    Metadata for a Stripe product.
    """
    stripe_id: str
    name: str
    features: List[str]
    description: str = ''
    is_default: bool = False


PREMIUM = ProductMetadata(
    stripe_id='prod_GqvWupK96UxUaG',
    name='Premium',
    description='For small businesses and teams',
    is_default=False,
    features=[
        features.UNLIMITED_WIDGETS,
        features.LUDICROUS_MODE,
        features.PRIORITY_SUPPORT,
    ],
)
# other plans go here

```

> El ejemplo expuesto utiliza [Python data classes](https://docs.python.org/3/library/dataclasses.html)

Creamos una clase _metadata_ la cual asociamos con el producto de _Stripe_ que manualmente enlazamos con el `stripe_id`.

Ahora que tenemos esta estructura, podemos, fácilmente, escribir código para activar o desactivar características en la aplicación.

Regresando al ejemplo, podemos implementar una función para el `ludicrous_mode_enabled`.

```python

def ludicrous_mode_enabled(user):
    return features.LUFICROUS_MODE in user.product.metadata.features

```

Esto mantiene la gestión de nuestras suscripciones y funciones en un solo lugar, y podemos utilizar esta estructura de _metadata_ para crear una página de _pricing_.



## Configuración del modelos de suscripción. 

El plan básico será:

1. Un usuario paso por el _workflow_ de suscripción en el sitio. 
2. Crear una objeto suscripción en _Stripe_.
3. Sincronizar la suscripción en nuestra base de datos.
4. Finalmente, adjuntamos la suscripción a nuestra base de datos local.

---

### user-based SaaS (B2C).

En un _user-based SaaS_ (_business-to-consumer_), cada persona tiene su propia cuenta y maneja su propia suscripción.

```python

class CustomUser(AbstractUser):
    customer = models.ForeignKey(
        'djstripe.Customer', null=True, blank=True, on_delete=models.SET_NULL,
        help_text="The user's Stripe Customer object, if it exists"
    )
    subscription = models.ForeignKey(
        'djstripe.Subscription', null=True, blank=True, on_delete=models.SET_NULL,
        help_text="The user's Stripe Subscription object, if it exists"
    )
    
```



### team-based SaaS (B2B).

En un _team-based Saas_ (_business-to-business_) el servicio no se orienta al consumidor, sino que se dirige a otros negocios. Este modelo maneja el concepto de _"Team"_ o "_Organizations_"  que contiene múltiples usuarios.

En este caso necesitamos asociar la suscripción con el modelo de `Team`.

```python

class Team(models.Model):
    """
    A Team, with members.
    """
    team_name = models.CharField(
        max_length=100
    )
    members = models.ManyToManyField(
        settings.AUTH_USER_MODEL, 
        related_name='teams', 
        through='Membership'
    )
    subscription = models.ForeignKey(
        'djstripe.Subscription', 
        null=True, 
        blank=True, 
        on_delete=models.SET_NULL,
        help_text="The team's Stripe Subscription object, if it exists"
    )
    
```



En este punto hay varios métodos para asociar a cada usuario con su respectiva suscripción adquirida por pertenecer a un grupo en específico. La forma más simple es asociar el objeto objeto `User` con el `Customer`, lo cual suele funcionar, pero puede traer problemas en el caso de que alguien  utilice un mismo `User` pero administre varios `Team`.



```python

class Membership(models.Model):
    """
    A user's team membership
    """
    team = models.ForeignKey(
        Team, 
        on_delete=models.CASCADE
    )
    user = models.ForeignKey(
        settings.AUTH_USER_MODEL, 
        on_delete=models.CASCADE
    )
    role = models.CharField(
        max_length=100, 
        choices=roles.ROLE_CHOICES
    )
    customer = models.ForeignKey(
        'djstripe.Customer', 
        null=True, 
        blank=True, 
        on_delete=models.SET_NULL,
        help_text="The member's Stripe Customer object for this team, if it exists"
    )
 
```







---

## Creando suscripciones.

[Guia de _Stripe_](https://stripe.com/docs/billing/subscriptions/fixed-price)



### Guardar detalles de pago
