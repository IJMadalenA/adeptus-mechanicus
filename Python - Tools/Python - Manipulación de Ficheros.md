# Python - Manipulación de Ficheros.

​	Python permite escribir, leer o editar cadenas de caracteres desde archivos (otros tipos deben ser convertidas a cadenas de caracteres). Para esto Python incorpora un tipo integrado llamado [file](https://entrenamiento-python-basico.readthedocs.io/es/latest/leccion9/clases_integradas.html#python-cls-file), el cual es manipulado mediante un objeto archivo el cual fue generado a través de una función integrada en Python, a continuación se describen los procesos típicos y sus referencias a funciones propias del lenguaje:

## 1 - Abrir archivos:

​	La mejor forma de abrir un archivo es mediante la función integrada [`open()`](https://entrenamiento-python-basico.readthedocs.io/es/latest/leccion5/funciones_integradas.html#python-fun-open)

`open( ‘path’, mode )`

​	La función `open()` sirve para definir dentro de una variable un objeto file, es decir, esta sirve para transformar un archivo en un objeto manipulable por Python, el cual debemos de almacenar en una variable para poder trabajar sobre ella. 

- El primer argumento de la función `open()` debe de ser un `str` que especifique la ruta del archivo o solo el nombre en el caso de que el archivo se encuentre en una ruta distinta a la del archivo Python. 

- El segundo argumento de la función `open()` es el modo en el que se manipulará el fichero y se ingresa como un `str`.

   - | Modo. | Función.                                                     |
      | ----- | ------------------------------------------------------------ |
      | ‘r’   | Modo de solo lectura, no se puede escribir sobre el fichero y es el argumento por defecto. |
      | ‘w’   | Modo de solo escritura. Si ya existe un archivo con el mismo nombre, este se eliminará y se creará uno nuevo. |
      | ‘a’   | Modo de agregado (append). Los datos escritos se agregan al final del archivo. |
      | ‘r+’  | Modo de lectura y escritura.                                 |
      | ‘b’   | El archivo se abre en modo binario, para almacenar cualquier cosa que no sea texto. |
      | ‘U’   | El archivo se abre con soporte a nueva línea universal, cualquier fin de línea ingresada será como un \n en Python. |

```python
>>> archivo = open('datos.txt', 'w')
>>> type(archivo)
<type 'file'>
```

