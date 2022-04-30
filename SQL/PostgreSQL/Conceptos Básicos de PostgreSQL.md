# Conceptos Básicos de PostgreSQL.

__PostgreSQL__ es un sistema de gestión de bases de datos relacional orientado a objetos y de código abierto. 

Cumple el estándar __ACID__:

- __A__: Atomicity.
  - Significa que existe la garantía de que, o todas las operaciones se ejecutan correctamente, o ninguna de ellas lo hace. No existe una parte de las operaciones que se realice con éxito y otra que no, en este caso o todo resulta satisfactorio o nada lo hará, de eso se trata la atomicidad. 
- __C__: Consistency.
  - Asegura que toda la data sea consistente. Toda será validada de acuerdo a las reglas definidas en la base de datos.
- __I__: Isolation.
  - Garantiza que todas las transacciones ocurran de manera aislada, es decir, una operación no afectará a otra porque una transacción no puede leer la data de otra hasta que esta no haya sido completada.
- __D__: Durability.
  - Una vez una transacción ha sido completada, esta permanecerá en el sistema, incluso si el sistema se rompe inmediatamente después de la operación. Cualquier cambio realizado por una transacción debe ser almacenado permanentemente. 