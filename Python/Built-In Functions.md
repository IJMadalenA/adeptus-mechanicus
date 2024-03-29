# PYTHON - Built-In Functions

[abs()](https://www.programiz.com/python-programming/methods/built-in/abs)

[any()](https://www.programiz.com/python-programming/methods/built-in/any)

[all()](https://www.programiz.com/python-programming/methods/built-in/all)

[ascii()](https://www.programiz.com/python-programming/methods/built-in/ascii)

[bin()](https://www.programiz.com/python-programming/methods/built-in/bin)

[bool()](https://www.programiz.com/python-programming/methods/built-in/bool)

[bytearray()](https://www.programiz.com/python-programming/methods/built-in/bytearray)

[callable()](https://www.programiz.com/python-programming/methods/built-in/callable)

[bytes()](https://www.programiz.com/python-programming/methods/built-in/bytes)

[chr()](https://www.programiz.com/python-programming/methods/built-in/chr)

[compile()](https://www.programiz.com/python-programming/methods/built-in/compile)

[classmethod()](https://www.programiz.com/python-programming/methods/built-in/classmethod)

[complex()](https://www.programiz.com/python-programming/methods/built-in/complex)

[delattr()](https://www.programiz.com/python-programming/methods/built-in/delattr)

[dict()](https://www.programiz.com/python-programming/methods/built-in/dict)

[dir()](https://www.programiz.com/python-programming/methods/built-in/dir)

[divmod()](https://www.programiz.com/python-programming/methods/built-in/divmod)

[enumerate()](https://www.programiz.com/python-programming/methods/built-in/enumerate)

[staticmethod()](https://www.programiz.com/python-programming/methods/built-in/staticmethod)

[filter()](https://www.programiz.com/python-programming/methods/built-in/filter)

[eval()](https://www.programiz.com/python-programming/methods/built-in/eval)

[float()](https://www.programiz.com/python-programming/methods/built-in/float)

[format()](https://www.programiz.com/python-programming/methods/built-in/format)

[frozenset()](https://www.programiz.com/python-programming/methods/built-in/frozenset)

---


## [getattr()](https://www.programiz.com/python-programming/methods/built-in/getattr)

​	The getattr() method returns the value of the named attribute of an object. If not found, it returns the default value provided to the function.

**The syntax of `getattr()` method is:**

```python
getattr(object, name[, default])
```

The above syntax is equivalent to:

```Python
object.name
```

 **Return value from getattr()**

`getattr()` method returns:

- value of the named attribute of the given object

- `default`, if no named attribute is found

- `AttributeError` exception, if named attribute is not found and `default` is not defined

  ---

  

[globals()](https://www.programiz.com/python-programming/methods/built-in/globals)

[exec()](https://www.programiz.com/python-programming/methods/built-in/exec)

[hasattr()](https://www.programiz.com/python-programming/methods/built-in/hasattr)

[help()](https://www.programiz.com/python-programming/methods/built-in/help)

[hex()](https://www.programiz.com/python-programming/methods/built-in/hex)

[hash()](https://www.programiz.com/python-programming/methods/built-in/hash)

[input()](https://www.programiz.com/python-programming/methods/built-in/input)

[id()](https://www.programiz.com/python-programming/methods/built-in/id)

[isinstance()](https://www.programiz.com/python-programming/methods/built-in/isinstance)

[int()](https://www.programiz.com/python-programming/methods/built-in/int)

[issubclass()](https://www.programiz.com/python-programming/methods/built-in/issubclass)

[iter()](https://www.programiz.com/python-programming/methods/built-in/iter)

[list() Function](https://www.programiz.com/python-programming/methods/built-in/list)

[locals()](https://www.programiz.com/python-programming/methods/built-in/locals)

[len()](https://www.programiz.com/python-programming/methods/built-in/len)

When you use built-in data types and many third-party types with `len()`, the function doesn’t need to iterate through the data structure. The length of a container object is stored as an attribute of the object. The value of this attribute is modified each time items are added to or removed from the data structure, and `len()` returns the value of the length attribute. This ensures that `len()` works efficiently.

[max()](https://www.programiz.com/python-programming/methods/built-in/max)

[min()](https://www.programiz.com/python-programming/methods/built-in/min)

[map()](https://www.programiz.com/python-programming/methods/built-in/map)

[next()](https://www.programiz.com/python-programming/methods/built-in/next)

[memoryview()](https://www.programiz.com/python-programming/methods/built-in/memoryview)

[object()](https://www.programiz.com/python-programming/methods/built-in/object)

[oct()](https://www.programiz.com/python-programming/methods/built-in/oct)

[ord()](https://www.programiz.com/python-programming/methods/built-in/ord)

[open()](https://www.programiz.com/python-programming/methods/built-in/open)

[pow()](https://www.programiz.com/python-programming/methods/built-in/pow)

[print()](https://www.programiz.com/python-programming/methods/built-in/print)

[property()](https://www.programiz.com/python-programming/methods/built-in/property)

## [range()](https://www.programiz.com/python-programming/methods/built-in/range)

Se puede generar secuencias inversas, empezando por un número mayor y terminando en uno menor, pero el salto deberá ser negativo, por ejemplo:

```python
for i in range(5, 0, -1):
    print(i)
    
>>> 5
>>> 4
>>> 3
>>> 2
>>> 1
```

[repr()](https://www.programiz.com/python-programming/methods/built-in/repr)

[reversed()](https://www.programiz.com/python-programming/methods/built-in/reversed)

[round()](https://www.programiz.com/python-programming/methods/built-in/round)

[set()](https://www.programiz.com/python-programming/methods/built-in/set)

[setattr()](https://www.programiz.com/python-programming/methods/built-in/setattr)

[slice()](https://www.programiz.com/python-programming/methods/built-in/slice)

[sorted()](https://www.programiz.com/python-programming/methods/built-in/sorted)

[str()](https://www.programiz.com/python-programming/methods/built-in/str)

[sum()](https://www.programiz.com/python-programming/methods/built-in/sum)

[tuple() Function](https://www.programiz.com/python-programming/methods/built-in/tuple)

[type()](https://www.programiz.com/python-programming/methods/built-in/type)

[vars()](https://www.programiz.com/python-programming/methods/built-in/vars)

[zip()](https://www.programiz.com/python-programming/methods/built-in/zip)

[__import__()](https://www.programiz.com/python-programming/methods/built-in/__import__)

[super()](https://www.programiz.com/python-programming/methods/built-in/super)





|                                                              |                                                              | Built-in Functions                                         |                                                              |                                                              |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`abs()`](https://docs.python.org/3/library/functions.html#abs) | [`delattr()`](https://docs.python.org/3/library/functions.html#delattr) | [`hash()`](https://docs.python.org/3/library/functions.html#hash) | [`memoryview()`](https://docs.python.org/3/library/functions.html#func-memoryview) | [`set()`](https://docs.python.org/3/library/functions.html#func-set) |
| [`all()`](https://docs.python.org/3/library/functions.html#all) | [`dict()`](https://docs.python.org/3/library/functions.html#func-dict) | [`help()`](https://docs.python.org/3/library/functions.html#help) | [`min()`](https://docs.python.org/3/library/functions.html#min) | [`setattr()`](https://docs.python.org/3/library/functions.html#setattr) |
| [`any()`](https://docs.python.org/3/library/functions.html#any) | [`dir()`](https://docs.python.org/3/library/functions.html#dir) | [`hex()`](https://docs.python.org/3/library/functions.html#hex) | [`next()`](https://docs.python.org/3/library/functions.html#next) | [`slice()`](https://docs.python.org/3/library/functions.html#slice) |
| [`ascii()`](https://docs.python.org/3/library/functions.html#ascii) | [`divmod()`](https://docs.python.org/3/library/functions.html#divmod) | [`id()`](https://docs.python.org/3/library/functions.html#id) | [`object()`](https://docs.python.org/3/library/functions.html#object) | [`sorted()`](https://docs.python.org/3/library/functions.html#sorted) |
| [`bin()`](https://docs.python.org/3/library/functions.html#bin) | [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) | [`input()`](https://docs.python.org/3/library/functions.html#input) | [`oct()`](https://docs.python.org/3/library/functions.html#oct) | [`staticmethod()`](https://docs.python.org/3/library/functions.html#staticmethod) |
| [`bool()`](https://docs.python.org/3/library/functions.html#bool) | [`eval()`](https://docs.python.org/3/library/functions.html#eval) | [`int()`](https://docs.python.org/3/library/functions.html#int) | [`open()`](https://docs.python.org/3/library/functions.html#open) | [`str()`](https://docs.python.org/3/library/functions.html#func-str) |
| [`breakpoint()`](https://docs.python.org/3/library/functions.html#breakpoint) | [`exec()`](https://docs.python.org/3/library/functions.html#exec) | [`isinstance()`](https://docs.python.org/3/library/functions.html#isinstance) | [`ord()`](https://docs.python.org/3/library/functions.html#ord) | [`sum()`](https://docs.python.org/3/library/functions.html#sum) |
| [`bytearray()`](https://docs.python.org/3/library/functions.html#func-bytearray) | [`filter()`](https://docs.python.org/3/library/functions.html#filter) | [`issubclass()`](https://docs.python.org/3/library/functions.html#issubclass) | [`pow()`](https://docs.python.org/3/library/functions.html#pow) | [`super()`](https://docs.python.org/3/library/functions.html#super) |
| [`bytes()`](https://docs.python.org/3/library/functions.html#func-bytes) | [`float()`](https://docs.python.org/3/library/functions.html#float) | [`iter()`](https://docs.python.org/3/library/functions.html#iter) | [`print()`](https://docs.python.org/3/library/functions.html#print) | [`tuple()`](https://docs.python.org/3/library/functions.html#func-tuple) |
| [`callable()`](https://docs.python.org/3/library/functions.html#callable) | [`format()`](https://docs.python.org/3/library/functions.html#format) | [`len()`](https://docs.python.org/3/library/functions.html#len) | [`property()`](https://docs.python.org/3/library/functions.html#property) | [`type()`](https://docs.python.org/3/library/functions.html#type) |
| [`chr()`](https://docs.python.org/3/library/functions.html#chr) | [`frozenset()`](https://docs.python.org/3/library/functions.html#func-frozenset) | [`list()`](https://docs.python.org/3/library/functions.html#func-list) | [`range()`](https://docs.python.org/3/library/functions.html#func-range) | [`vars()`](https://docs.python.org/3/library/functions.html#vars) |
| [`classmethod()`](https://docs.python.org/3/library/functions.html#classmethod) | [`getattr()`](https://docs.python.org/3/library/functions.html#getattr) | [`locals()`](https://docs.python.org/3/library/functions.html#locals) | [`repr()`](https://docs.python.org/3/library/functions.html#repr) | [`zip()`](https://docs.python.org/3/library/functions.html#zip) |
| [`compile()`](https://docs.python.org/3/library/functions.html#compile) | [`globals()`](https://docs.python.org/3/library/functions.html#globals) | [`map()`](https://docs.python.org/3/library/functions.html#map) | [`reversed()`](https://docs.python.org/3/library/functions.html#reversed) | [`__import__()`](https://docs.python.org/3/library/functions.html#__import__) |
| [`complex()`](https://docs.python.org/3/library/functions.html#complex) | [`hasattr()`](https://docs.python.org/3/library/functions.html#hasattr) | [`max()`](https://docs.python.org/3/library/functions.html#max) | [`round()`](https://docs.python.org/3/library/functions.html#round) |                                                              |



# Anonymous Functions (lambda).

​    It's a function that is defined without a identification name and its writed in one single line, with just one expression and just once.

​    An anonymous functions is a short way to define functions that will be used once and whose returned value will be used as a variable. Tha anonymous functions are defined using the [`lambda`](https://realpython.com/python-lambda/) keyword and these functions don't need to be defined or named afted and they are for one-time usage.

- **Syntax:**

  ```python
  lambda <parameter>: <expression>
  
  # When the function defines the value of a variable.
  <identificator> = lambda <parameter>: <expression> 
  <identificator(parameter)>
  ```

  ​	When the anonymous function is defined within a variable with an identifying name, this name isn't for the function, the name is the identifier of a variable that contains a **function object** whose value,  that of the variable, is the returned value by the [`lambda`](https://realpython.com/python-lambda/) function.

  ​	In other words, when you invoke the variable with a parameter in parentheses, you are not invoking a function, you simply define the `function object` with the entered parameter, and it redefines the variable with the value returned. 

  

- **Example:**

  ```python
  def palindrome(string):
      return string == string[::-1]
  print(palindrome('ana'))
  
  # lambda function:
  palindrome = lambda string: string == string[::-1]
  print(palindrome('ana'))
  ```

  

  # High Order Functions.

A High Order Function (H.O.F.), is a function that receives another function as a parameter.

## filter()

- **Syntax:**

  ```python
  filter(function, iterable)
  var_list = list(filter(function, iterable))
  var_tuple = tuple(filter(function, iterable))
  ```

  

​    `	filter (function, iterable)` is a function that receives two parameters, a function thats return a boolean value and an iterable object, where the function determines which values within the [iterable](https://docs.python.org/3/glossary.html#term-iterable) will remain, depending of the value returned when every value passing through the function. if the value returned is true, the value remains in the iterable object.

​	Note that `list_var = list(filter(function, iterable))` is equivalent to the generator expression: `list_var = (item for item in iterable if function(item))` if function is not `None` and `(item for item in iterable if item)` if function is `None`.

- **Example:**

  ```python
  obj_iterable = [1, 2, 3, 4, 5]
  odd = list(filter(lambda x: x%2 != 0, obj_iterable))
  print(odd)
  ```

​    Every value whose doesn't return Truen after passing through the function, will be remove and not be returned by the `filter()` function. The objects returned by the function `filter()` is an object `<class 'filter'>`



## map()

- **Syntax:** 

  ```python
  map(function, iterable)
  var_list = list(map(function, iterable))
  var_tuple = tuple(map(function, iterable))
  ```

  ​    This function apply a given function to every item within an [iterable](https://docs.python.org/3/glossary.html#term-iterable) object and Return an object `<class 'map'>` thats is convertible to a iterable object like a `list()` or `tuple()`.

  ​    If additional *iterable* arguments are passed, *function* must take that many arguments and is applied to the items from all iterables in parallel. With multiple iterables, the iterator stops when the shortest [iterable](https://docs.python.org/3/glossary.html#term-iterable) is exhausted.

- **Examples:**

  ```python
  numbers = (1, 2, 3, 4)
  result = map(lambda x: x*x, numbers)
  print(result)
  
  # converting map object to set
  numbersSquare = set(result)
  print(numbersSquare)
  
  #-------------------------------------
  
  num1 = [4, 5, 6]
  num2 = [5, 6, 7]
  
  result = map(lambda n1, n2: n1+n2, num1, num2)
  print(list(result))
  ```

  

## reduce()

- **Syntax:**

  ```python
  from functools import reduce
  
  reduce(function, iterable)
  ```

  

​    This function receives as parameters, an iterable object and a function, and reduce the lists of items to a single cumulative value. [`reduce()`](https://realpython.com/python-reduce-function/#getting-started-with-pythons-reduce) operates on any [iterable](https://docs.python.org/3/glossary.html#term-iterable), not just lists. 

​    The function apply the function inserted to the firts two items in an iterable and generate a partial result, then use that partial result, together with the third item in the iterable to generate another partial result and repeat the process until the iterable is exhausted and then return a single cumulative value.

​    [`reduce()`](https://realpython.com/python-reduce-function/#getting-started-with-pythons-reduce) was originally a built-in function (and still is in [Python 2.x](https://docs.python.org/2/library/functions.html#reduce)), but it was moved to `functools.reduce()` module in [Python 3.0](https://docs.python.org/3/whatsnew/3.0.html#builtins). This decision was based on some possible performance and readability issues.

- **Examples:**

  ```
  from functools import reduce
  
  numbers = [3, 5, 2, 4, 7, 1]
  
  # Minimum
  reduce(lambda a, b: a if a < b else b, numbers)
  
  
  # Maximum
  reduce(lambda a, b: a if a > b else b, numbers)
  ```

**Use a dedicated function** to solve use cases for Python’s `reduce()` whenever possible. Functions such as `sum()`, `all()`, `any()`, `max()`, `min()`, `len()`, `math.prod()`, and so on will make your code faster and more readable and maintainable.
<<<<<<< HEAD



# files management:

## **Opening modes**

- **r** = Just **read**.
- **r+** = Write and **read**.
- **w** = Just **write**. Overwrite the file if that exists, if not, its create one.
- **w+** = **Write** and read. Overwrite the file if that exists, if not, its create another.
- **a**  = **Append** content into the file. If the file dosn't exist, its create one.
- **a+** = **Append** and read content into the file, if the file doen't exist, itscreate one. 

```python
with open(".route/of/file.txt", "<opening_mode>", encoding = '<encoding_type') as <optional_name>:
```
=======

>>>>>>> master

