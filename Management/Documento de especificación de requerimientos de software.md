# Documento de especificación de requerimientos de software.

Es la declaración oficial a la cual deben guiarse los desarrolladores para la implementación de funciones del software y/o sistema.

Es una fase del desarrollo donde se obtiene la descripción completa del comportamiento del futuro software a desarrollar.

Debe incluir desde los requerimientos a nivel de usuario para el sistema hasta un apartado detallado de los requerimientos del sistema, los requerimientos funcionales y no funcionales. Intentando ser lo más claro posible en la redacción y recopilación de la información.

El documento __ERS__ será en donde se registran las necesidades del negocio, los requisitos del cliente y necesidades del usuario, y se definen los requerimientos. Por tanto, es el medio de comunicación entre los clientes, usuarios y desarrolladores.

Para conocer y entender cuáles son las necesidades del proyecto, se tienen que definir primero cuáles de las técnicas de __obtención de requisitos__ se van a emplear.

- Entrevistas estructuradas, semi-estructuradas o no-estructuradas.
- Observaciones.
- Estudio de documentación.
- Cuestionario o encuesta.

---

Luego de conocer cuales son las necesidades del cliente, es necesario definir los requerimientos que deben cumplir el software, identificando cuales requisitos son funcionales y no funcionales.

Los __requisitos no funcionales__ o __atributos de calidad__ son propiedades o cualidades que el producto debe tener, es decir, restricciones o condiciones que el producto que está siendo desarrollado debe cumplir.

> Siempre que se pueda, tienen que ser especificados cuantitativamente para que se pueda verificar su cumplimiento.

Los __requisitos funcionales__ son las necesidades que el software debe cumplir de manera satisfactoria, es decir, las funciones que el software será capaz de realizar. Estos requerimientos son cálculos, detalles técnicos, manipulaciones de datos (entrada y salida) y otras funciones específicas que se supone, que el software debe cumplir.

> Estos deben de redactarse de manera comprensible para usuarios sin conocimientos técnicos.



El documento se divide en tres secciones:

__Introducción:__ Se definen puntos como el propósito del documento, el alcance del producto, las definiciones, acrónimos abreviaturas utilizadas para identificar al software y sus componentes, referencias utilizadas para el desarrollo y diseño del software, y una descripción del resto de documento.

__Descripción general:__ indaga en puntos como la perspectiva del software, las funciones del software, las características de los usuarios, las restricciones generales y las suposiciones y dependencias. 

__Requerimientos específicos:__ Incluye los requerimientos funcionales, requerimientos no funcionales y requerimientos del sistema.

---

## Técnicas de análisis.

### Descomposición funcional.

Se refiere al proceso de identificar y resolver las relaciones funcionales en sus partes constituyentes, de tal forma que la función global pueda ser reconstruida a partir de sus partes. 

Por lo general, la descomposición funcional se realiza para identificar y entender os componentes o partes que constituyen un todo o una función global, y en este proceso es fundamental identificar las interacciones entre componentes.

Consiste en tomar los requerimientos de software, dividirlos en partes y analizarlos individualmente. De ser necesario, se pueden descomponer en más partes hasta lograr un nivel adecuado de detalle.

Se define el sistema en términos funcionales, para luego definir funciones de más bajo nivel y establecer las relaciones con estas funciones de alto nivel. La intención es dividir un sistema de tal forma que cada componente se pueda describir sin necesidad de referir a otro componente. De esta forma, cada parte del sistema tendrá funciones independientes, que pueden rehusarse y reemplazarse. 

### Modelo de proceso.

Comprende la elaboración de diagramas de flujo de procesos o flujogramas a partir de los requerimientos del software.

Es muy útil para entender el trabajo realizado en múltiples pasos, tareas, roles y departamentos intervinientes. Los procesos son iniciados por eventos y pueden abarcar actividades automatizadas, manuales o combinación entre ambas.

Su naturaleza visual ayuda a la comprensión y comunicación a terceros.

Cuando los procesos son complejos, deben desglosarse en componentes o subprocesos.  

### Prototipos

Consiste en elaborar representaciones visuales de los requerimientos de software. Es muy útil para validar con los usuarios, clientes e interesados de proyecto que el diseño funcional corresponde con los requerimientos de software y que existe un entendimiento común entre desarrolladores y usuarios.

Permite a desarrolladores y usuarios entender mejor los requerimientos, determinar cuáles son indispensables y cuales deseables, e identificar riesgos de forma temprana. Puede enfocarse en toda la solución o sólo en áreas especificas.

Puede extenderse innecesariamente en el tiempo si las discusiones se realizan en torno al como en lugar de en torno al que.

La elaboración de prototipos conlleva iteraciones entre desarrolladores y usuarios, en los cuales se van elaborando varios prototipos y sometidos a evaluación del cliente.

## Esquema de documento de requerimiento.

1. __Sistema a construir.__

   ​	< Descripción del sistema a desarrollar, de sus principales funcionalidades y de los posibles usos del producto. >

2. __Descripción de los usuarios.__

   ​	< Caracterización de los principales usuarios del sistema a desarrollar. >

3. __Requerimientos funcionales.__

   ​	< Se detallan todos los requerimientos funcionales del sistema. >

   1. __Funcionalidad 1.__

      ​	< Explicación de la funcionalidad 1 del sistema >

   2. __Funcionalidad 2.__

      ​	< Explicación de la funcionalidad 2 del sistema >

4. __Requerimientos no funcionales o atributos de calidad.__

   ​	< Se detallan todos los requerimientos no funcionales del sistema, éstos pueden tratarse de requerimientos necesarios para el uso del sistema, de performance, de mantenimiento, soporte, testeo, etc. >

   1. __Requerimiento no funcional 1.__

      ​	< Explicación del requerimiento no funcional 1 del sistema >

   2. __Requerimiento no funcional 2.__

      ​	< Explicación del requerimiento no funcional 2 del sistema >

5. __Restricciones.__

   ​	< Detalle de las restricciones impuestas sobre el proyecto pero que no son restricciones sobre el producto. Ejemplos sobre procesos de software a seguir, fechas de entrega, hitos de entrega fijos, etc. >

   1. __Restricción 1.__

      ​	< Explicación de la restricción 1 >

   2. __Restricción 2.__

      ​	< Explicación de la restricción 2 >

6. __Interfaces.__

   ​	< Se detallan las interfaces que debe proveer o utilizar la aplicación >

   1. __Interfaz de usuario.__

      ​	< Describe las interfaces de usuario que deben ser implementadas >

   2. __Interfaz de hardware.__

      ​	< Incluye cualquier interfaz con el hardware que debe ser provista por el software, si es que son necesarias >

   3. __Interfaz de software.__

      ​	< Describe las interfaces del sistema con cualquier otro sistema de software, pueden ser componentes reusados, componentes del mercado o cualquier otro tipo con el cual el sistema debe interactuar.

   4. __Interfaz de comunicación.__

      ​	< Describe cualquier interfaz de comunicación con otro sistema o dispositivo, tales como redes, dispositivos remotos, etc >

   