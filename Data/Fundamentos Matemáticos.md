# Fundamentos Matemáticos.

[Clases del Curso de Fundamentos de Matemáticas - Platzi](https://platzi.com/clases/fundamentos-matematicas/)

## Introducción.

### ¿Qué es la aritmética?

​	La aritmética es la rama de las matemáticas que estudia los números y las operaciones básicas que se pueden efectuar entre ellos. Es entonces la disciplina que se enfoca en las sumas, restas, multiplicaciones y divisiones que se pueden hacer entre los números existentes. Así, se trata del área más básica de las matemáticas.

​	La aritmética básica comprende las operaciones mas fundamentales que se pueden realizar, es decir, la adición, sustracción, multiplicación y división, pudiendo incluir también a la potenciación, radicación y logaritmación.

​	La suma, multiplicación y potenciación forman parte de las __operaciones aritméticas directas__, y la sustracción, división, radicación (raises cuadradas) y logaritmación forman parte de las __operaciones aritméticas indirectas__. 

​	Se conoce como alta aritmética al estudio de las propiedades y las funciones de los números. En este marco se puede hablar de la aritmética binaria (que apela al cero y al uno para representar valores, la aritmética modular (que trabaja con módulos) y la aritmética ordinal (orientada a los números ordinales), entre otras.



### Potenciación y sus propiedades.

​	La potenciación podría ser entendida como una operación en donde se distinguen básicamente tres elementos, los cuales son:

- __Base:__ Entendida como el número que se multiplicará a si mismo, el número de veces que le señale el exponente. En consecuencia será el multiplicador y el multiplicando de la operación que había sido abreviada por la operación de potenciación.
- __Exponente:__ Es el segundo número involucrado en la operación, y el responsable de indicar cuántas veces deberá multiplicarse por sí misma la base de la potenciación.
- __Potencia:__ Constituye el resultado final de la operación, siendo entonces el producto de la multiplicación que ha hecho sobre sí misma la base, tantas veces como le ha señalado el exponente.

​	La potenciación es la operación mediante la cual se multiplica un número por sí mismo una determinada cantidad de veces $(n)$ que se indica en el superíndice. Se representa de la siguiente manera: $x^n$, en donde $x$ es el termino denominado _base_ y $n$ el termino denominado _exponente_. 

**Casos especiales de potenciación**:

- Cualquier potencia de exponente 0, es igual a 1 (siempre que su base no sea 0)
- Cualquier potencia de exponente 1, es igual a la base.
- Cero elevado a cualquier exponente (distinto de cero) es igual a cero.
- Si la base de la potencia es un número positivo, el resultado siempre será positivo
- Si la base de la potencia es un número negativo, el signo del resultado depende del tipo de exponente, a saber: si el exponente es par, el signo será positivo, pero si es impar, el exponente será negativo.

![propiedades-potencias.png](https://static.platzi.com/media/user_upload/propiedades-potencias-0d60fa34-fe9c-4268-8ceb-4b6282496962.jpg)

​	Cuando el exponente es un __numero natural__ $n$, este indica las veces que aparece $a$ multiplicando por sí mismo, siendo $a$ un número cualquiera, entonces:
$$
a^1 = a
\\
a^2 = a \cdot a
\\
a^3 = a \cdot a \cdot a
\\
.\ \ \ \ \ \ \ \ \ \ .
\\
.\ \ \ \ \ \ \ \ \ \ .
\\

a^n = \underbrace{a \ \cdot \ ... \ a,}_{n\rm\ veces}
$$

#### __Multiplicación de potencias de igual base.__

​	Siguiendo la lógica explicada anteriormente, al multiplicar dos bases iguales, se conserva la base y se suman los exponentes, ya que en esencia estamos concatenando las multiplicaciones; es decir:
$$
 a^n . a^m = a^{n+m}
$$
#### __División de potencias de igual base.__

​	El cociente de dos potencias con la misma base es igual a una potencia de dicha base con un exponente igual a la diferencia del exponente del dividendo menor el del divisor, esto es:
$$
\frac{a^m}{a^n}=a^{m-n}
$$

$$
\frac{a^4}{a^3} = a^1
\\
\\
\frac{a \cdot a\cdot a\cdot a}{a \cdot a \cdot a} = a^1
\\
\\
\frac{\cancel{a} \cdot \cancel{a} \cdot \cancel{a} \cdot a}{\cancel{a} \cdot \cancel{a} \cdot \cancel{a}} = a^1
\\
\\
\frac{2^4}{2^3} = 2^1
\\
\\
\frac{16}{8}=2^1
$$



#### __Potencia de exponente 0.__

​	Por convención, un __número distinto de 0__ ($a\ne0$) elevado al exponente 0 da como resultado la unidad (1), puesto que:
$$
a \ne 0
\\
\\
1 = \frac{a^n}{a^n}=a^{n-n}=a^0
\\
\\
\frac{a^3}{a^3} = a^0 = 1
\\
\\
\frac{a \cdot a\cdot  a}{a \cdot a \cdot a} = a^0
\\
\\
\frac{\cancel{a} \cdot \cancel{a} \cdot \cancel{a}}{\cancel{a} \cdot \cancel{a} \cdot \cancel{a}} = a^0
\\
\\
\frac{2^3}{2^3} = 1
\\
\\
\frac{8}{8}=1
$$
​	El resultado no es equivalente a multiplicar el numero por 0, sino el equivalente al de dividirlo por si mismo

#### __Potencia de una potencia.__

​	La potencia de una potencia en matriz cuadrada, es igual a la potencia de base.
$$
(a^m)^n = a^{m \cdot n}
\\
\\
[(a^m)^n]^o = (a^{m \cdot n})^o = a^{m \cdot n \cdot o}
\\
\\
\\
(2^2)^3 = 2^{2 \cdot 3}=2^{6}=64
\\
\\
(2^2)^3 = 4^{3}=64
$$
​	En este ejemplo tenemos una base elevada al cuadrado y posteriormente elevada al cubo. Como una potencia es la abreviación de una serie de multiplicaciones, la segunda potencia se aplica al resultado de la primera, es decir, si mi primer paso es multiplicar $2 \cdot 2$, ya que está elevado al cuadrado, cuando lo elevamos al cubo simplemente estamos multiplicando 2 al cubo tres veces consecutivas, lo equivalente a: $(2 \cdot 2) \cdot (2 \cdot 2) \cdot (2 \cdot 2)$, que no es más que elevar 2 a la 6.

#### __Potencia de un producto positivo.__

​	La potencia de un producto es igual al producto de cada uno de los factores elevado al mismo exponente, es decir:
$$
(a \cdot b)^{n} = a^{n} \cdot b^{n}
\\
\\
(2 \cdot 3)^{3} = 2^3 \cdot 3^3 = [(2 \cdot 2 \cdot 2) \cdot (3 \cdot 3 \cdot 3)]= 8 \cdot 27 = 216
\\
\\
(2 \cdot 3)^3 = 6^3 = (6 \cdot 6 \cdot 6) = 216
\\
\\
(2 \cdot 3)^3 = [(2 \cdot 3) \cdot (2 \cdot 3) \cdot (2 \cdot 3)] = (6 \cdot 6 \cdot 6) = 216
$$
​	Primero debemos comenzar entendiendo que una multiplicación no es más que la suma de un numero, un multiplicando, tantas veces como le indique el multiplicador, por lo que posee propiedad conmutativa, ya que el orden en el que se efectúe la operación no modificará su resultado, entonces, cuando elevamos una multiplicación lo que hacemos es multiplicar por si misma durante tantas veces como lo indique el exponente al resultado de dicha operación, es decir el producto de dicha multiplicación durante $n$ veces, por lo tanto, el resultado de elevar por $n$ una multiplicación es el mismo al de elevar por $n$ a cada uno de sus factores individualmente, y luego multiplicar el resultado de dicha potenciación individualizada, ya que simplemente se está afectando al orden de las operaciones.

​	Ya que simplemente se expresa la relación entre los números, ya que $2 \cdot 3 $ como operación en si misma es una manera de expresar $6$, es decir $(2 \cdot 3) = 6$. Otra manera de verlo es con la siguiente operación: $(4 \cdot 3)^3 = (6 \cdot 2)^3$ = 1728, en ambos casos podemos aplicar las mismas variaciones descritas al inicio, podemos tanto elevar al cubo el resultado de la multiplicación o podemos elevar al cubo individualmente cada factor perteneciente a la multiplicación y luego multiplicarlos, a fin de cuentas la propiedad conmutativa sigue intacta.

#### Potencia de un cociente.

​	La potencia de un cociente es igual al cociente de cada uno de los números elevado al mismo exponente, es decir:
$$
(\frac{a}{b})^{n} = \frac{a^n}{b^n}
\\
\\
(\frac{20}{4})^3 = (\frac{20}{4} \cdot \frac{20}{4} \cdot \frac{20}{4}) = (5 \cdot 5 \cdot 5) = 5^3 = 125
\\
\\
(\frac{20}{4})^3 = \frac{20^3}{4^3} = \frac{8000}{64} = 125
$$
​	Este caso es muy similar al anterior. Podemos entender a la división como una manera de expresar un numero a través de una operación, en donde la potencia multiplica dicho resultado $n$ cantidad de veces, por lo tanto es indiferente que multipliquemos el numero resultante o aquellos números que a través de una operación lo expresan, ya que se sigue manteniendo la relación.

​	A pesar de ser una división no se viola la propiedad conmutativa debido a que en ningún momento cambia la posición del numerador respecto al denominador, solo cambian sus magnitudes y siempre en relación con el exponente. 

#### Propiedades que no cumple la potenciación.

- No es distributiva con respecto a la adición y sustracción, es decir, no se puede distribuir cuando dentro del paréntesis es suma o resta:
   $$
   (a + b)^n \ne a^n + b^n
   \\
   \\
   (a - b)^n \ne a^n - b^n
   $$

- No cumple la propiedad conmutativa:
   $$
   a^b \ne b^a
   $$

### Radicación y sus propiedades.

​	Es la operación inversa a la potenciación, y consiste en que dados dos números, llamados radicando e indice, hallar un tercero , llamado raíz, tal que, elevado al índice, sea igual al radicando.
$$
\sqrt[n]{a}=x
$$

#### Raíz de un producto.

​	La raíz de un producto es igual al producto de las raíces de los factores nombrados anteriormente, es decir:
$$
\sqrt[n]{a \cdot b} = \sqrt[n]{a} \cdot \sqrt[n]{b}
$$

#### Raíz de un cociente.

​	La raíz de una facción es igual al cociente de la raíz del numerador entre la raíz del denominador.
$$
\sqrt[n]{\frac{a}{b}} = \frac{a^{\frac{1}{n}}}{b^{\frac{1}{n}}} = \frac{\sqrt[n]{a}}{\sqrt[n]{b}}
$$

#### Raíz de una raíz.

​	Para calcular la raíz de una raíz se multiplican los índices de las raíces y se conserva el radicando.
$$
\sqrt[n]{\sqrt[m]{a}} = \sqrt[n \cdot m]{a}
$$

#### Potencia de una raíz.

​	Para calcular la potencia de una raíz se eleva el radicando a esa potencia.
$$
(\sqrt[n]{x})^m = \sqrt[n]{a^{m}} = a^{\frac{m}{n}}
$$

### Orden de las operaciones:

​	El orden de las operaciones nace de la necesidad de estandarizar la jerarquía y orden de las operaciones, con el fin de que dos personas puedan obtener los mismos resultados de un problema. Estas son las reglas que determinan la secuencia de cálculos en una expresión con más de un tipo de calculo. El orden en el que se realizan las operaciones es el siguiente:

- Operaciones dentro de paréntesis y corchetes.

- Exponentes (Potenciación y Radicación).
- Multiplicación y división.
- Adición y sustracción.

Todo esto siempre de izquierda a derecha siguiendo el orden de las operaciones.

### Factorización.

​	Es una técnica que consiste en la descomposición en factores de una expresión algebraica (que pude ser un número, una suma o resta, una matriz, un polinomio, etc.) en forma de producto.

​	La factorización consiste en el proceso de encontrar factores. Para un numero $x$, los factores serán los números que al multiplicarse, su resultado sea igual al número $x$, es decir, que descomponemos una expresión en todos los factores que la compongan, desmenuzándola, por ejemplo:
$$
x^2 = x \cdot x
\\
\\
ax^2 + ay^2 + bx^2 + by^2
\\
\\
(ax^2 + ay^2) + (bx^2 + by^2)
\\
\\
x^2(a + b) + y^2(a + b)
\\
\\
(a + b)(x^2 + y^2)
$$

### Recta numérica y ley de signos.

​	la ley de signos o regla de los signos son indicaciones que nos permiten determinar el signo de un resultado final cuando se realizan operaciones con los números enteros. 

#### Ley de signos en la suma.

​	Cuando se realizan operaciones de suma con números enteros, se siguen las siguientes reglas:

- Si los dos números son positivos (mayor que cero): se suman y mantienen su signo $+$.
- Si los dos números son negativos (menores que cero): se suman y se mantienen el signo $-$.
- Si se suma un número mayor que cero y un número menor que cero: se restan y se deja el signo del número con mayor valor absoluto.

#### Ley de signos en la resta.

​	Cuando se realizan operaciones de resta con números enteros, el signo de resta cambia el signo del número que lo sigue.

#### Ley de signos en la multiplicación.

​	Cuando se realizan operaciones de multiplicación con números enteros, se siguen las siguientes reglas:

- Si se multiplican dos números con signo $+$, el resultado tendrá el signo $+$.
- Si se multiplican dos números con signo $-$, el resultado tendrá el signo $+$.
- Si se multiplican un número con signo $+$ y otro con signo $-$, el resultado tendrá el signo $-$.
- Si se multiplican un número con signo $-$ y otro con signo $+$, el resultado tendrá el signo $-$.

#### Ley de signos en la división.

​	Cuando se realizan operaciones de división con números enteros, se siguen las siguientes reglas:

- Si se dividen dos números con signo $+$, el resultado tendrá el signo $+$.
- Si se dividen dos números con signo $-$, el resultado tendrá el signo $+$.
- Si se dividen un número con signo $+$ y otro con signo $-$, el resultado tendrá el signo $-$.



## Principios de algebra.

​	Es la rama de la matemática que estudia la combinación de elementos de estructuras abstractas acorde a ciertas reglas. Originalmente esos elementos podían ser interpretados como números o cantidades, por lo que el álgebra en cierto modo originalmente fue una generalización y extensión de la aritmética. En el algebra moderna existen áreas del álgebra que en modo alguno pueden considerarse extensiones de la aritmética, como el álgebra abstracta, álgebra homológica, álgebra exterior, etc.

​	Hoy entendemos como álgebra al área matemática que se centra en las relaciones, estructuras y cantidades (las reglas de las operaciones) y en resolver ecuaciones. En ella, las operaciones se realizan empleando números, letras y signos que representan simbólicamente otro número o entidad matemática. Estas “letras” se llaman, en álgebra, __variables__ o __incógnitas__.

	### Ecuaciones.

​	Una ecuación es una igualdad matemática entre dos expresiones, denominadas miembros y separadas por el signo igual $=$, en las que aparecen elementos conocidos y datos desconocidos o incógnitas, relacionados mediante operaciones matemáticas.

​	Los valores conocidos pueden ser números, coeficientes o constantes; también variables o incluso objetos complejos como funciones o vectores, los elementos desconocidos pueden ser establecidos mediante otras ecuaciones de un sistema, o algún otro procedimiento de resolución de ecuaciones. Las incógnitas, representadas generalmente por letras, constituyen los valores que se pretende hallar (en ecuaciones complejas en lugar de valores numéricos podría tratarse de elementos de un cierto conjunto abstracto, como sucede en las ecuaciones diferenciales).

