# Python - Tipo y Manejo de Datos.

## Strings.

[Text Sequence Type - str — Python 3.10.5 documentation](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)

Son un tipo de objeto inmutable que permite almacenar secuencias de caracteres.

````python
>>> help(str)

Help on class str in module builtins:
class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |  
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
 |  Otherwise, returns the result of object.__str__() (if defined)
 |  or repr(object).
 |  encoding defaults to sys.getdefaultencoding().
 |  errors defaults to 'strict'.
 |  
 |  Methods defined here:
 |  
 |  __add__(self, value, /)
 |      Return self+value.
 |  
 |  __contains__(self, key, /)
 |      Return key in self.
 |  
 |  __eq__(self, value, /)
 |      Return self==value.
 |  
 |  __format__(self, format_spec, /)
 |      Return a formatted version of the string as described by format_spec.
 |  
 |  __ge__(self, value, /)
 |      Return self>=value.
 |  
 |  __getattribute__(self, name, /)
 |      Return getattr(self, name).
 |  
 |  __getitem__(self, key, /)
 |      Return self[key].
 |  
 |  __getnewargs__(...)
 |  
 |  __gt__(self, value, /)
 |      Return self>value.
 |  
 |  __hash__(self, /)
 |      Return hash(self).
 |  
 |  __iter__(self, /)
 |      Implement iter(self).
 |  
 |  __le__(self, value, /)
 |      Return self<=value.
 |  
 |  __len__(self, /)
 |      Return len(self).
 |  
 |  __lt__(self, value, /)
 |      Return self<value.
 |  
 |  __mod__(self, value, /)
 |      Return self%value.
 |  
 |  __mul__(self, value, /)
 |      Return self*value.
 |  
 |  __ne__(self, value, /)
 |      Return self!=value.
 |  
 |  __repr__(self, /)
 |      Return repr(self).
 |  
 |  __rmod__(self, value, /)
 |      Return value%self.
 |  
 |  __rmul__(self, value, /)
 |      Return value*self.
 |  
 |  __sizeof__(self, /)
 |      Return the size of the string in memory, in bytes.
 |  
 |  __str__(self, /)
 |      Return str(self).
 |  
 |  capitalize(self, /)
 |      Return a capitalized version of the string.
 |      
 |      More specifically, make the first character have upper case and the rest lower
 |      case.
 |  
 |  casefold(self, /)
 |      Return a version of the string suitable for caseless comparisons.
 |  
 |  center(self, width, fillchar=' ', /)
 |      Return a centered string of length width.
 |      
 |      Padding is done using the specified fill character (default is a space).
 |  
 |  count(...)
 |      S.count(sub[, start[, end]]) -> int
 |      
 |      Return the number of non-overlapping occurrences of substring sub in
 |      string S[start:end].  Optional arguments start and end are
 |      interpreted as in slice notation.
 |  
 |  encode(self, /, encoding='utf-8', errors='strict')
 |      Encode the string using the codec registered for encoding.
 |      
 |      encoding
 |        The encoding in which to encode the string.
 |      errors
 |        The error handling scheme to use for encoding errors.
 |        The default is 'strict' meaning that encoding errors raise a
 |        UnicodeEncodeError.  Other possible values are 'ignore', 'replace' and
 |        'xmlcharrefreplace' as well as any other name registered with
 |        codecs.register_error that can handle UnicodeEncodeErrors.
 |  
 |  endswith(...)
 |      S.endswith(suffix[, start[, end]]) -> bool
 |      
 |      Return True if S ends with the specified suffix, False otherwise.
 |      With optional start, test S beginning at that position.
 |      With optional end, stop comparing S at that position.
 |      suffix can also be a tuple of strings to try.
 |  
 |  expandtabs(self, /, tabsize=8)
 |      Return a copy where all tab characters are expanded using spaces.
 |      
 |      If tabsize is not given, a tab size of 8 characters is assumed.
 |  
 |  find(...)
 |      S.find(sub[, start[, end]]) -> int
 |      
 |      Return the lowest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Return -1 on failure.
 |  
 |  format(...)
 |      S.format(*args, **kwargs) -> str
 |      
 |      Return a formatted version of S, using substitutions from args and kwargs.
 |      The substitutions are identified by braces ('{' and '}').
 |  
 |  format_map(...)
 |      S.format_map(mapping) -> str
 |      
 |      Return a formatted version of S, using substitutions from mapping.
 |      The substitutions are identified by braces ('{' and '}').
 |  
 |  index(...)
 |      S.index(sub[, start[, end]]) -> int
 |      
 |      Return the lowest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Raises ValueError when the substring is not found.
 |  
 |  isalpha(self, /)
 |      Return True if the string is an alphabetic string, False otherwise.
 |      
 |      A string is alphabetic if all characters in the string are alphabetic and there
 |      is at least one character in the string.
 |  
 |  isascii(self, /)
 |      Return True if all characters in the string are ASCII, False otherwise.
 |      
 |      ASCII characters have code points in the range U+0000-U+007F.
 |      Empty string is ASCII too.
 |  
 |  isdecimal(self, /)
 |      Return True if the string is a decimal string, False otherwise.
 |      
 |      A string is a decimal string if all characters in the string are decimal and
 |      there is at least one character in the string.
 |  
 |  isdigit(self, /)
 |      Return True if the string is a digit string, False otherwise.
 |      
 |      A string is a digit string if all characters in the string are digits and there
 |      is at least one character in the string.
 |  
 |  isidentifier(self, /)
 |      Return True if the string is a valid Python identifier, False otherwise.
 |      
 |      Call keyword.iskeyword(s) to test whether string s is a reserved identifier,
 |      such as "def" or "class".
 |  
 |  islower(self, /)
 |      Return True if the string is a lowercase string, False otherwise.
 |      
 |      A string is lowercase if all cased characters in the string are lowercase and
 |      there is at least one cased character in the string.
 |  
 |  isnumeric(self, /)
 |      Return True if the string is a numeric string, False otherwise.
 |      
 |      A string is numeric if all characters in the string are numeric and there is at
 |      least one character in the string.
 |  
 |  isprintable(self, /)
 |      Return True if the string is printable, False otherwise.
 |      
 |      A string is printable if all of its characters are considered printable in
 |      repr() or if it is empty.
 |  
 |  isspace(self, /)
 |      Return True if the string is a whitespace string, False otherwise.
 |      
 |      A string is whitespace if all characters in the string are whitespace and there
 |      is at least one character in the string.
 |  
 |  istitle(self, /)
 |      Return True if the string is a title-cased string, False otherwise.
 |      
 |      In a title-cased string, upper- and title-case characters may only
 |      follow uncased characters and lowercase characters only cased ones.
 |  
 |  isupper(self, /)
 |      Return True if the string is an uppercase string, False otherwise.
 |      
 |      A string is uppercase if all cased characters in the string are uppercase and
 |      there is at least one cased character in the string.
 |  
 |  join(self, iterable, /)
 |      Concatenate any number of strings.
 |      
 |      The string whose method is called is inserted in between each given string.
 |      The result is returned as a new string.
 |      
 |      Example: '.'.join(['ab', 'pq', 'rs']) -> 'ab.pq.rs'
 |  
 |  ljust(self, width, fillchar=' ', /)
 |      Return a left-justified string of length width.
 |      
 |      Padding is done using the specified fill character (default is a space).
 |  
 |  lower(self, /)
 |      Return a copy of the string converted to lowercase.
 |  
 |  lstrip(self, chars=None, /)
 |      Return a copy of the string with leading whitespace removed.
 |      
 |      If chars is given and not None, remove characters in chars instead.
 |  
 |  partition(self, sep, /)
 |      Partition the string into three parts using the given separator.
 |      
 |      This will search for the separator in the string.  If the separator is found,
 |      returns a 3-tuple containing the part before the separator, the separator
 |      itself, and the part after it.
 |      
 |      If the separator is not found, returns a 3-tuple containing the original string
 |      and two empty strings.
 |  
 |  removeprefix(self, prefix, /)
 |      Return a str with the given prefix string removed if present.
 |      
 |      If the string starts with the prefix string, return string[len(prefix):].
 |      Otherwise, return a copy of the original string.
 |  
 |  removesuffix(self, suffix, /)
 |      Return a str with the given suffix string removed if present.
 |      
 |      If the string ends with the suffix string and that suffix is not empty,
 |      return string[:-len(suffix)]. Otherwise, return a copy of the original
 |      string.
 |  
 |  replace(self, old, new, count=-1, /)
 |      Return a copy with all occurrences of substring old replaced by new.
 |      
 |        count
 |          Maximum number of occurrences to replace.
 |          -1 (the default value) means replace all occurrences.
 |      
 |      If the optional argument count is given, only the first count occurrences are
 |      replaced.
 |  
 |  rfind(...)
 |      S.rfind(sub[, start[, end]]) -> int
 |      
 |      Return the highest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Return -1 on failure.
 |  
 |  rindex(...)
 |      S.rindex(sub[, start[, end]]) -> int
 |      
 |      Return the highest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Raises ValueError when the substring is not found.
 |  
 |  rjust(self, width, fillchar=' ', /)
 |      Return a right-justified string of length width.
 |      
 |      Padding is done using the specified fill character (default is a space).
 |  
 |  rpartition(self, sep, /)
 |      Partition the string into three parts using the given separator.
 |      
 |      This will search for the separator in the string, starting at the end. If
 |      the separator is found, returns a 3-tuple containing the part before the
 |      separator, the separator itself, and the part after it.
 |      
 |      If the separator is not found, returns a 3-tuple containing two empty strings
 |      and the original string.
 |  
 |  rsplit(self, /, sep=None, maxsplit=-1)
 |      Return a list of the substrings in the string, using sep as the separator string.
 |      
 |        sep
 |          The separator used to split the string.
 |      
 |          When set to None (the default value), will split on any whitespace
 |          character (including \\n \\r \\t \\f and spaces) and will discard
 |          empty strings from the result.
 |        maxsplit
 |          Maximum number of splits (starting from the left).
 |          -1 (the default value) means no limit.
 |      
 |      Splitting starts at the end of the string and works to the front.
 |  
 |  rstrip(self, chars=None, /)
 |      Return a copy of the string with trailing whitespace removed.
 |      
 |      If chars is given and not None, remove characters in chars instead.
 |  
 |  split(self, /, sep=None, maxsplit=-1)
 |      Return a list of the substrings in the string, using sep as the separator string.
 |      
 |        sep
 |          The separator used to split the string.
 |      
 |          When set to None (the default value), will split on any whitespace
 |          character (including \\n \\r \\t \\f and spaces) and will discard
 |          empty strings from the result.
 |        maxsplit
 |          Maximum number of splits (starting from the left).
 |          -1 (the default value) means no limit.
 |      
 |      Note, str.split() is mainly useful for data that has been intentionally
 |      delimited.  With natural text that includes punctuation, consider using
 |      the regular expression module.
 |  
 |  splitlines(self, /, keepends=False)
 |      Return a list of the lines in the string, breaking at line boundaries.
 |      
 |      Line breaks are not included in the resulting list unless keepends is given and
 |      true.
 |  
 |  startswith(...)
 |      S.startswith(prefix[, start[, end]]) -> bool
 |      
 |      Return True if S starts with the specified prefix, False otherwise.
 |      With optional start, test S beginning at that position.
 |      With optional end, stop comparing S at that position.
 |      prefix can also be a tuple of strings to try.
 |  
 |  strip(self, chars=None, /)
 |      Return a copy of the string with leading and trailing whitespace removed.
 |      
 |      If chars is given and not None, remove characters in chars instead.
 |  
 |  swapcase(self, /)
 |      Convert uppercase characters to lowercase and lowercase characters to uppercase.
 |  
 |  title(self, /)
 |      Return a version of the string where each word is titlecased.
 |      
 |      More specifically, words start with uppercased characters and all remaining
 |      cased characters have lower case.
 |  
 |  translate(self, table, /)
 |      Replace each character in the string using the given translation table.
 |      
 |        table
 |          Translation table, which must be a mapping of Unicode ordinals to
 |          Unicode ordinals, strings, or None.
 |      
 |      The table must implement lookup/indexing via __getitem__, for instance a
 |      dictionary or list.  If this operation raises LookupError, the character is
 |      left untouched.  Characters mapped to None are deleted.
 |  
 |  upper(self, /)
 |      Return a copy of the string converted to uppercase.
 |  
 |  zfill(self, width, /)
 |      Pad a numeric string with zeros on the left, to fill a field of the given width.
 |      
 |      The string is never truncated.
 |  
 |  ----------------------------------------------------------------------
 |  Static methods defined here:
 |  
 |  __new__(*args, **kwargs) from builtins.type
 |      Create and return a new object.  See help(type) for accurate signature.
 |  
 |  maketrans(...)
 |      Return a translation table usable for str.translate().
 |      
 |      If there is only one argument, it must be a dictionary mapping Unicode
 |      ordinals (integers) or characters to Unicode ordinals, strings or None.
 |      Character keys will be then converted to ordinals.
 |      If there are two arguments, they must be strings of equal length, and
 |      in the resulting dictionary, each character in x will be mapped to the
 |      character at the same position in y. If there is a third argument, it
 |      must be a string, whose characters will be mapped to None in the result.
````

Las cadenas no están limitadas en tamaño, y puede estar tanto vacía como ser tan extensa que el único límite sea la memoria del ordenador.

Una situación común es la de querer introducir una comilla, bien sea simple `''` o doble ``""`` dentro de una cadena formada por el mismo tipo de comilla. Para ello recurrimos a las secuencias de escape, ``\"`` o ``\'``, que nos permite incrustar comillas dentro de una cadena.

````python
>>> s = "Comilla \" dentro del str."
>>> print(s)

Comilla " dentro del str.
````

También podemos usar ``\`` para incluir un salgo de línea dentro de una cadena:

````python
>>> s = "Primera linea\nSegunda linea"
>>> print(s)

Primera linea
Segunda linea
````

También podemos usar ``\`` acompañado de un número, lo que imprimirá el carácter asoaciado.

````python
>>> print("\111\123")

IS
````

Se puede definir una cadena que ocupe varias líneas usando triple comillas dobles ``"""``. 

````python
>>> print("""Linea Uno,
... Linea Dos,
... Linea Tres.
... """)

Linea Uno,
Linea Dos,
Linea Tres.
````

Si utilizamos el prefijo ``r``, lo que la define como ``raw strings``, la cadena ignora todas las secuencias de escape.

````python
>>> print(r"\111\123")

\111\123
````

### Formateo de str's.

 [String Formatting — Python 3.10.5 documentation](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting)

Es posible declarar cadenas con variables en su interior, como ``int`` o incluso otros ``str``, y existen varias maneras de hacerlo.

La primera es con el operador ``+`` seguido del ``str``.

````python
>>> x = 5
>>> s = "El valor de x es: " + str(x)
print(2)

El valor de x es: 5
````

Otra forma es usando ``%``, el cual al principio y dentro del ``str`` le indicamos con un sufijo la manera en la que representará la variable y posterior indicamos la variable a representar.

````python
>>> x = 5
>>> s = "El valor de x es: %d" % x
>>> print(s)

El valor de x es: 5
````

Si el sufijo que define el formato recibe un tipo de objeto incompatible, retorna un ``TypeError``.

````python
>>> x = "string."
>>> s = "El valor de x es: %d" % x
>>> print(s)

TypeError: %d format: a real number is required, not str
````

---

The conversion types are:

| Conversion | Meaning                                                      |
| :--------- | :----------------------------------------------------------- |
| `'d'`, `'i'`      | Signed integer decimal.                                      |
| `'o'`      | Signed octal value.                                          |
| `'u'`      | Obsolete type – it is identical to `'d'`.                    |
| `'x'`      | Signed hexadecimal (lowercase).                              |
| `'X'`      | Signed hexadecimal (uppercase).                              |
| `'e'`      | Floating point exponential format (lowercase).               |
| `'E'`      | Floating point exponential format (uppercase).               |
| `'f'`, `'F'` | Floating point decimal format.                               |
| `'g'`      | Floating point format. Uses lowercase exponential format if exponent is less than -4 or not less than precision, decimal format otherwise. |
| `'G'`      | Floating point format. Uses uppercase exponential format if exponent is less than -4 or not less than precision, decimal format otherwise. |
| `'c'`      | Single character (accepts integer or single character string). |
| `'r'`      | String (converts any Python object using [`repr()`](https://docs.python.org/3/library/functions.html#repr)). |
| `'s'`      | String (converts any Python object using [`str()`](https://docs.python.org/3/library/stdtypes.html#str)). |
| `'a'`      | String (converts any Python object using [`ascii()`](https://docs.python.org/3/library/functions.html#ascii)). |
| `'%'`      | No argument is converted, results in a `'%'` character in the result. |

---

También podemos ingresar más de una variable para ser representadas dentro de un ``str``.

La primera, y no muy moderna, manera de hacerlo lo es ingresarlos dentro de una tupla ``()``.

````python
>>> s = "Los numeros son %d y %d." % (5, 10)
>>> print(s)

Los numeros son 5 y 10.
````

Una mejor forma de hacerlo es utilizando ``format()``.

````python
>>> s = "Los numeros son {} y {}.".format(5, 10)
>>> print(s)

Los numeros son 5 y 10.
````

````python
>>> s = "Los numeros son {a} y {b}.".format(b=10, a=5)
>>> print(s)

Los numeros son 5 y 10.
````

También podemos utilizar el prefijo ``f``, que recibe el nombre de cadenas literales o ``f-strings``, que puede representar tanto variables, operaciones aritméticas o incluso llamar a una función.

````python
>>> a = 5
>>> b = 10
>>> s = f"Los numeros son {a} y {b}."
>>> print(s)

Los numeros son 5 y 10.
````

````python
>>> a = 5
>>> b = 10
>>> s = f"a + b = {a+b}"
>>> print(s)

a + b = 15
````

````python
>>> def funcion():
...    return 20

>>> s = f"El resultado de la función es {funcion()}."
>>> print(s)

El resultado de la función es 20.
````

---

### Operadores sobre ``str``'s.

Los objetos ``str`` tienen diversos comportamientos, donde podemos tanto sumar, multiplicar, aplicar condicionales entre otras utilidades.

#### Sumar ``str``'s con ``+``.

````python
>>> str_1 = "Parte_1"
>>> str_2 = "Parte_2"
>>> print(str_1 + " " + str_2)

Parte_1 Parte_2
````

#### Multiplicar ``str``'s con ``*``.

````python
>>> s = "var "
>>> print(s*3)

var var var
````

#### Condicional en ``str``'s.

Con este condicional podremos conocer si una cadena ``str`` contiene una secuencia especifica de caracteres.

````python
>>> print("code" in "Python code")

True
````

### _Slicing_ sobre ``str``.

Se pueden indexar las cadenas ``str`` de la misma forma en la que se hace con las listas.

````python
>>> x = "Python"
>>> print(x[0]) # Seleccionar un solo caracter dentro del str. Siempre comenzamos desde el '0'.

P

>>> print(x[-1]) # Seleccionar el ultimo caracter dentro del str.

n

>>> print(x[0:2]) # Seleccionar una longitud especifica del str.

Pyt

>>> print(x[2:]) # Seleccionar los caracteres desde un punto inicial específico hasta el final del str.

thon

>>> print(x[0:5:2]) # Seleccionar una longitud especifica definiendo saltos entre la selección. 
>>> print(x[0::2])
>>> print(x[::2])

Pto
Pto
Pto
````

---

### Métodos ``str``.

[String Methods — Python 3.10.5 documentation](https://docs.python.org/3/library/stdtypes.html#string-methods)



#### Transformar los caracteres del ``str``.

##### [``.capitalize()``](https://docs.python.org/3/library/stdtypes.html#str.capitalize)

Retorna la cadena con su primera letra en mayúscula.

````python
>>> s = "cadena de texto."
>>> print(s.capitalize())

Cadena de texto.
````

##### [``.lower()``](https://docs.python.org/3/library/stdtypes.html#str.lower)

Retorna la cadena con todos sus caracteres alfabéticos en minuscula.

````python
>>> s = "CADENA DE TEXTO."
>>> print(s.lower())

cadena de texto.
````

#####  [``.swapcase()``](https://docs.python.org/3/library/stdtypes.html#str.swapcase)

Retorna la cadena convirtiendo los caracteres en minúsculas a mayúsculas y viceversa.

````python
>>> s = "CadENA dE teXtO."
>>> print(s.swapcase())

cADena De TExTO.
````

##### [``.upper()``](https://docs.python.org/3/library/stdtypes.html#str.upper)

Retorna todos los caracteres alfabéticos en mayúsculas.

````python
>>> s = "cadena de texto."
>>> print(s.upper())

CADENA DE TEXTO.
````

---



#### [``.count()``](https://docs.python.org/3/library/stdtypes.html#str.upper)

Permite contar las veces que un caracter o una secuencia de caracteres se encuentra dentro de un ``str``, permitiendo definir en donde se debe comenzar a buscar y hasta que punto.

````python
s = "cadena de texto."
print(s.count("e"))

3
````

---



#### - Identificar los caracteres del ``str``.

##### [``.isalnum()``](https://docs.python.org/3/library/stdtypes.html#str.isalnum)

Retorna ``True`` si todos los caracteres en el ``str`` son alfanuméricos y hay al menos un caracter. Si encuentra espacios en blanco ``" " `` o caracteres especiales tales como ``!, $, %, &, ...``, o si está vacía, retornará ``False``.

````python
>>> s = "Texto123"
>>> print(s.isalnum())

True

>>> s = "Cadena 123"
>>> print(s.isalnum())

False
````

##### [`.isalpha()`](https://docs.python.org/3/library/stdtypes.html#str.isalpha)

Retorna ``True`` si todos los caracteres en el ``str`` son alfabéticos y hay al menos un carácter, retornando ``False`` en caso contrario.

##### [``.isdecimal()``](https://docs.python.org/3/library/stdtypes.html#str.isdecimal)

Retorna ``True`` si todos los caracteres en el ``str`` son decimales y hay al menos un carácter, retornando ``False`` en caso contrario.

##### [``.isdigit()``](https://docs.python.org/3/library/stdtypes.html#str.isdigit)

Retorna ``True`` si todos los caracteres en el ``str`` son dígitos y hay al menos un carácter, retornando ``False`` en caso contrario.

##### [``.isidentifier()``](https://docs.python.org/3/library/stdtypes.html#str.isidentifier)

Retorna ``True`` si el ``str`` es un identificador válido según la definición de Python. [Identifiers and keywords](https://docs.python.org/3/reference/lexical_analysis.html#identifiers).

##### [``.islower()``](https://docs.python.org/3/library/stdtypes.html#str.islower)

Retorna ``True`` si todos los _cased characters_[^1] en el ``str`` están en minúsculas y hay al menos un carácter, retornando ``False`` en caso contrario.

##### [``.isnumeric()``](https://docs.python.org/3/library/stdtypes.html#str.isnumeric)

Retorna ``True`` si todos los caracteres en el ``str`` son numéricos y hay al menos un carácter, y retornará ``False`` en el caso contrario.

##### [``.isprintable()``](https://docs.python.org/3/library/stdtypes.html#str.isprintable)

Retorna ``True`` si todos los caracteres en el ``str`` son imprimibles o la cadena está vacía y retornará ``False`` en caso contrario.

##### [``.isspace()``](https://docs.python.org/3/library/stdtypes.html#str.isspace)

Retorna ``True`` si solo hay espacios en blanco conformando la totalidad del ``str`` y al menos un espacio en blanco como carácter, de lo contrario será ``False``. 

##### [``.istitle()``](https://docs.python.org/3/library/stdtypes.html#str.istitle)

Retorna ``True`` si el ``str`` es _titlecased_, es decir que la primera letra de cada conjunto de caracteres dentro del ``str`` está en mayúsculas.

##### [``.isupper()``](https://docs.python.org/3/library/stdtypes.html#str.isupper)

Retorna ``True`` si __todos los caracteres__ en el ``str`` están en mayúsculas, y hay al menos un carácter en el ``str``. De lo contrario será ``False``.

````python
>>> 'BANANA'.isupper()
True

>>> 'banana'.isupper()
False

>>> 'baNana'.isupper()
False

>>> ' '.isupper()
False
````

---



#### [``.strip()``](https://ellibrodepython.com/cadenas-python#stripchars)

Elimina a la izquierda y derecha el carácter que se ingresa. Si se llama sin parámetro elimina los espacios.

````python
>>> s = " texto "
>>> print(s.strip())

texto
````

#### [``.zfill()``](https://docs.python.org/3/library/stdtypes.html#str.zfill)

Rellena la cadena con ceros a la izquierda hasta llegar a la longitud ingresada como parametro.

````python
>>> s = "123"
>>> print(s.zfill(6))

001234
````

#### [``.join(<iterable>)``](https://docs.python.org/3/library/stdtypes.html#str.join)

Retorna la primera cadena unida a cada uno de los elementos de la lista que se ingresa como parámetro.

````python
>>> s = " y ".join(["1", "2", "3"])
>>> print(s)

1 y 2 y 3
````

#### [``.split(set=None, maxsplit=-1)``](https://docs.python.org/3/library/stdtypes.html#str.split)

Divide una cadena en subcadenas y las retorna almacenadas en un objeto ``list``. La división es realizada de acuerdo a el primer parámetro, y el segundo parámetro indica el número máximo de divisiones a realizar.

````python
>>> s = "Cadena de texto."
>>> print(s.split(","))

["Cadena", "de", "texto."]
````



---

## Footnotes.

[^1]: Los _"Cased characters"_ son todos aquellos cuya propiedad general es "Lu" (Letter, uppercase), "LI" (Letter, lowercase), or "Lt" (Letter, titlecase).
