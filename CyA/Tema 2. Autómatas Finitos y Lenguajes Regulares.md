## 0. Idea general del tema

En este tema estudiamos una de las familias de lenguajes más importantes de Computabilidad:

$$
\textbf{los lenguajes regulares}
$$

Los lenguajes regulares se pueden describir de varias formas equivalentes:

- mediante **expresiones regulares**;
- mediante **autómatas finitos deterministas**, DFA;
- mediante **autómatas finitos no deterministas**, NFA;
- mediante **gramáticas regulares**, que veremos más en el Tema 3.

> [!important]
> Un lenguaje es regular si puede ser reconocido por un autómata finito.

---

# Bloque 1 — Lenguajes regulares y expresiones regulares

## 1. Lenguajes regulares

En el Tema 1 vimos que, dado un alfabeto $\Sigma$, el conjunto $\Sigma^*$ contiene todas las cadenas posibles sobre ese alfabeto.

Por ejemplo, si:

$$
\Sigma = \{a,b\}
$$

entonces:

$$
\Sigma^* = \{\varepsilon, a, b, aa, ab, ba, bb, aaa, \dots\}
$$

Un lenguaje sobre $\Sigma$ es cualquier subconjunto de $\Sigma^*$.

Pero no todos los lenguajes son igual de sencillos de describir o reconocer.

Los lenguajes regulares son los que pueden construirse usando operaciones muy básicas.

---

## 2. Definición recursiva de lenguaje regular

> [!definition]
> Sea $\Sigma$ un alfabeto. Los lenguajes regulares sobre $\Sigma$ se definen así:
>
> 1. $\emptyset$ es regular.
> 2. $\{\varepsilon\}$ es regular.
> 3. Para cada símbolo $a \in \Sigma$, $\{a\}$ es regular.
> 4. Si $A$ y $B$ son regulares, entonces también son regulares:
>
> $$
> A \cup B
> $$
>
> $$
> A \cdot B
> $$
>
> $$
> A^*
> $$
>
> 5. No hay más lenguajes regulares salvo los que se puedan construir aplicando las reglas anteriores.

---

## 3. Operaciones usadas

### Unión

Si:

$$
A = \{a, aa\}
$$

y:

$$
B = \{b\}
$$

entonces:

$$
A \cup B = \{a, aa, b\}
$$

---

### Concatenación

Si:

$$
A = \{a, b\}
$$

y:

$$
B = \{c, d\}
$$

entonces:

$$
AB = \{ac, ad, bc, bd\}
$$

---

### Cierre de Kleene

Si:

$$
A = \{a\}
$$

entonces:

$$
A^* = \{\varepsilon, a, aa, aaa, \dots\}
$$

> [!important]
> El cierre estrella siempre incluye la cadena vacía $\varepsilon$.

---

## 4. Expresiones regulares

> [!definition]
> Una expresión regular es una forma compacta de representar un lenguaje regular.

Las expresiones regulares sobre $\Sigma$ se definen recursivamente:

1. $\emptyset$ es una expresión regular.
2. $\varepsilon$ es una expresión regular.
3. Si $a \in \Sigma$, entonces $a$ es una expresión regular.
4. Si $r$ y $s$ son expresiones regulares, entonces también lo son:
   - $r|s$
   - $rs$
   - $r^*$

---

## 5. Correspondencia entre expresiones regulares y lenguajes

| Expresión regular | Lenguaje representado |
|---|---|
| $\emptyset$ | $\emptyset$ |
| $\varepsilon$ | $\{\varepsilon\}$ |
| $a$ | $\{a\}$ |
| $r|s$ | $L(r) \cup L(s)$ |
| $rs$ | $L(r)L(s)$ |
| $r^*$ | $L(r)^*$ |

---

## 6. Lectura intuitiva

| Operador | Lectura |
|---|---|
| $r|s$ | $r$ o $s$ |
| $rs$ | $r$ seguido de $s$ |
| $r^*$ | cero o más repeticiones de $r$ |
| $r^+$ | una o más repeticiones de $r$ |

> [!tip]
> Antes de operar formalmente con una expresión regular, conviene leerla en lenguaje natural.

---

## 7. Precedencia de operadores

El orden de prioridad es:

$$
* \quad > \quad \cdot \quad > \quad |
$$

Es decir:

1. primero se aplica la estrella;
2. después la concatenación;
3. por último la unión.

### Ejemplo

La expresión:

$$
ab^*c|e
$$

se interpreta como:

$$
(a(b^*)c)|e
$$

---

## 8. Ejemplos básicos

### Ejemplo 1

$$
a^*
$$

representa:

$$
\{\varepsilon, a, aa, aaa, \dots\}
$$

---

### Ejemplo 2

$$
(a|b)^*
$$

representa todas las cadenas sobre $\{a,b\}$:

$$
\{a,b\}^*
$$

---

### Ejemplo 3

$$
(a|b)^*a(a|b)^*
$$

representa todas las cadenas sobre $\{a,b\}$ que contienen al menos una `a`.

---

### Ejemplo 4

$$
(a|b)^*abb
$$

representa todas las cadenas sobre $\{a,b\}$ que terminan en `abb`.

---

## 9. Reglas básicas de simplificación

### Unión

$$
r|\emptyset = r
$$

$$
r|r = r
$$

$$
r|s = s|r
$$

---

### Concatenación

$$
r\varepsilon = \varepsilon r = r
$$

$$
r\emptyset = \emptyset r = \emptyset
$$

> [!warning]
> La concatenación no es conmutativa:
>
> $$
> rs \neq sr
> $$

---

### Estrella

$$
\emptyset^* = \varepsilon
$$

$$
\varepsilon^* = \varepsilon
$$

$$
(r^*)^* = r^*
$$

---

## 10. Ejemplo de simplificación

Simplificar:

$$
\emptyset^* | a^*
$$

Como:

$$
\emptyset^* = \varepsilon
$$

tenemos:

$$
\emptyset^* | a^* = \varepsilon | a^*
$$

Pero:

$$
\varepsilon \in a^*
$$

Por tanto:

$$
\varepsilon | a^* = a^*
$$

Resultado:

$$
\boxed{a^*}
$$

---

## 11. Cómo construir expresiones regulares

### Cadenas que terminan en una subcadena

Cadenas sobre $\{0,1\}$ que terminan en `00`:

$$
(0|1)^*00
$$

---

### Cadenas que contienen una subcadena

Cadenas que contienen `010`:

$$
(0|1)^*010(0|1)^*
$$

---

### Cadenas con número impar de símbolos

Cadenas sobre $\{a,b\}$ con número impar de `b`:

$$
a^*ba^*(ba^*ba^*)^*
$$

Otra forma de pensarlo:

- una primera `b`;
- luego pares de `b`;
- las `a` pueden aparecer en cualquier posición.

---

# Bloque 2 — Autómatas finitos deterministas, DFA

## 1. Idea intuitiva

Un autómata finito determinista, o DFA, es una máquina que:

1. empieza en un estado inicial;
2. lee la cadena de izquierda a derecha;
3. cambia de estado según el símbolo leído;
4. acepta si termina en un estado final.

> [!important]
> Un DFA no tiene memoria auxiliar.
>
> Su única memoria es el estado actual.

---

## 2. Definición formal

> [!definition]
> Un autómata finito determinista es una 5-tupla:
>
> $$
> M = (Q, \Sigma, \delta, s, F)
> $$
>
> donde:
>
> - $Q$ es un conjunto finito de estados.
> - $\Sigma$ es el alfabeto de entrada.
> - $\delta$ es la función de transición.
> - $s \in Q$ es el estado inicial.
> - $F \subseteq Q$ es el conjunto de estados finales.

La función de transición es:

$$
\delta : Q \times \Sigma \to Q
$$

Es decir, dado un estado y un símbolo, el autómata sabe exactamente a qué estado ir.

---

## 3. Qué significa determinista

Un DFA es determinista porque para cada par:

$$
(q,a)
$$

hay exactamente un estado destino.

Es decir:

$$
\delta(q,a)
$$

siempre está definido y tiene un único resultado.

---

## 4. Diagrama de transición

Un DFA se puede representar mediante un diagrama:

- cada estado es un nodo;
- el estado inicial se marca con una flecha de entrada;
- los estados finales se marcan con doble círculo;
- las transiciones son flechas etiquetadas con símbolos.

---

## 5. Lenguaje aceptado por un DFA

> [!definition]
> El lenguaje aceptado por un DFA $M$ se denota $L(M)$ y es el conjunto de cadenas que llevan al autómata desde el estado inicial hasta un estado final.

Formalmente:

$$
L(M)=\{w \in \Sigma^* \mid \delta^*(s,w) \in F\}
$$

---

## 6. Función extendida de transición

La función $\delta$ lee un símbolo.

Para leer cadenas completas usamos:

$$
\delta^*
$$

Se define así:

$$
\delta^*(q,\varepsilon)=q
$$

y:

$$
\delta^*(q,wa)=\delta(\delta^*(q,w),a)
$$

---

## 7. Ejemplo: cadenas que acaban en 00

Queremos un DFA que acepte:

$$
L = \{w \in \{0,1\}^* \mid w \text{ acaba en } 00\}
$$

Necesitamos recordar cuántos ceros consecutivos hay al final.

Estados:

| Estado | Significado |
|---|---|
| $q_0$ | No acaba en 0 |
| $q_1$ | Acaba en exactamente un 0 |
| $q_2$ | Acaba en 00 |

Estado inicial:

$$
q_0
$$

Estado final:

$$
q_2
$$

Transiciones:

| Estado | Con 0 | Con 1 |
|---|---|---|
| $q_0$ | $q_1$ | $q_0$ |
| $q_1$ | $q_2$ | $q_0$ |
| $q_2$ | $q_2$ | $q_0$ |

---

## 8. Ejemplo: cadenas con número impar de `b`

Lenguaje:

$$
L = \{w \in \{a,b\}^* \mid w \text{ tiene número impar de } b\}
$$

Estados:

| Estado | Significado |
|---|---|
| $q_0$ | número par de `b` |
| $q_1$ | número impar de `b` |

Estado inicial:

$$
q_0
$$

Estado final:

$$
q_1
$$

Transiciones:

| Estado | Con a | Con b |
|---|---|---|
| $q_0$ | $q_0$ | $q_1$ |
| $q_1$ | $q_1$ | $q_0$ |

> [!tip]
> Cada vez que aparece una `b`, cambiamos de par a impar o de impar a par.
>
> Las `a` no cambian nada.

---

## 9. Ejemplo: cadenas que no contienen 11

Lenguaje:

$$
L = \{w \in \{0,1\}^* \mid w \text{ no contiene } 11\}
$$

Estados:

| Estado | Significado |
|---|---|
| $q_0$ | no he visto peligro |
| $q_1$ | la última letra fue `1` |
| $q_2$ | ya apareció `11` |

Estados finales:

$$
F = \{q_0,q_1\}
$$

Transiciones:

| Estado | Con 0 | Con 1 |
|---|---|---|
| $q_0$ | $q_0$ | $q_1$ |
| $q_1$ | $q_0$ | $q_2$ |
| $q_2$ | $q_2$ | $q_2$ |

El estado $q_2$ es un estado sumidero de rechazo.

---

## 10. Estado sumidero

> [!definition]
> Un estado sumidero es un estado del que no se sale.

Sirve para representar situaciones en las que ya es imposible aceptar.

Ejemplo:

Si el lenguaje son cadenas sin `11`, en cuanto aparece `11`, la cadena ya no podrá aceptarse aunque sigamos leyendo.

---

## 11. Cómo diseñar un DFA

Para diseñar un DFA, pregunta clave:

> ¿Qué información mínima necesito recordar mientras leo la cadena?

Esa información se convierte en estados.

---

## 12. Patrones típicos de DFA

### 12.1 Cadenas que terminan en una subcadena

Ejemplo:

$$
(a|b)^*abb
$$

Hay que recordar cuánto del sufijo `abb` llevo acumulado.

Estados típicos:

| Estado | Significado |
|---|---|
| $q_0$ | no llevo nada útil |
| $q_1$ | he visto `a` |
| $q_2$ | he visto `ab` |
| $q_3$ | he visto `abb` |

$q_3$ será final.

---

### 12.2 Cadenas que contienen una subcadena

Ejemplo:

$$
(0|1)^*010(0|1)^*
$$

Hay que recordar cuánto del patrón `010` se ha detectado.

Una vez llegamos al estado final, normalmente nos quedamos ahí con cualquier símbolo.

---

### 12.3 Paridad

Ejemplo:

- número par de `a`;
- número impar de `b`;
- longitud múltiplo de 3.

Se usan estados que representan restos módulo algún número.

---

### 12.4 Condiciones combinadas

Ejemplo:

> número par de `a` y no contener `bbb`.

Se suelen combinar estados.

Si una condición necesita $m$ estados y otra necesita $n$ estados, el DFA combinado puede necesitar hasta:

$$
m \cdot n
$$

estados.

---

## 13. Lenguaje infinito reconocido por un DFA

Un DFA reconoce un lenguaje infinito si existe un ciclo que:

1. es alcanzable desde el estado inicial;
2. desde el ciclo se puede llegar a un estado final.

> [!important]
> Si puedo dar vueltas en un ciclo y luego aceptar, puedo construir cadenas arbitrariamente largas.

---

# Bloque 3 — Autómatas finitos no deterministas, NFA

## 1. Idea intuitiva

Un NFA es como un DFA, pero con más libertad.

Desde un estado y con un símbolo puede:

- ir a varios estados posibles;
- no tener transición;
- usar transiciones $\varepsilon$, que no consumen símbolo.

> [!important]
> Un NFA acepta una cadena si existe al menos un camino que acaba en un estado final.

---

## 2. Definición formal

> [!definition]
> Un autómata finito no determinista es una 5-tupla:
>
> $$
> M = (Q, \Sigma, \delta, s, F)
> $$
>
> donde:
>
> - $Q$ es un conjunto finito de estados.
> - $\Sigma$ es el alfabeto.
> - $s$ es el estado inicial.
> - $F$ es el conjunto de estados finales.
> - $\delta$ es la función de transición.

Para un NFA sin transiciones $\varepsilon$:

$$
\delta : Q \times \Sigma \to \mathcal{P}(Q)
$$

Para un NFA con transiciones $\varepsilon$:

$$
\delta : Q \times (\Sigma \cup \{\varepsilon\}) \to \mathcal{P}(Q)
$$

---

## 3. Diferencia entre DFA y NFA

| DFA | NFA |
|---|---|
| Una única transición por símbolo | Puede haber varias |
| Siempre sabe a dónde ir | Puede tener varias opciones |
| No usa $\varepsilon$ | Puede usar $\varepsilon$ |
| Acepta si el único camino acepta | Acepta si algún camino acepta |

---

## 4. Ejemplo de NFA

Lenguaje:

$$
L = (0|1)^*010(0|1)^*
$$

Cadenas que contienen la subcadena `010`.

Una idea de NFA:

- permanece en el estado inicial leyendo cualquier cosa;
- cuando ve un `0`, puede decidir que empieza el patrón;
- intenta leer `1`;
- intenta leer `0`;
- si completa `010`, acepta y consume lo que quede.

Estados:

| Estado | Significado |
|---|---|
| $q_0$ | esperando posible inicio |
| $q_1$ | he visto `0` |
| $q_2$ | he visto `01` |
| $q_3$ | he visto `010` |

Transiciones principales:

$$
\delta(q_0,0)=\{q_0,q_1\}
$$

$$
\delta(q_0,1)=\{q_0\}
$$

$$
\delta(q_1,1)=\{q_2\}
$$

$$
\delta(q_2,0)=\{q_3\}
$$

$$
\delta(q_3,0)=\{q_3\}
$$

$$
\delta(q_3,1)=\{q_3\}
$$

Estado final:

$$
q_3
$$

> [!tip]
> Los NFA son muy cómodos para lenguajes que contienen una subcadena.

---

## 5. Transiciones epsilon

Una transición $\varepsilon$ permite cambiar de estado sin consumir ningún símbolo.

Ejemplo:

$$
q_0 \xrightarrow{\varepsilon} q_1
$$

Significa que el autómata puede pasar de $q_0$ a $q_1$ gratis.

---

## 6. Epsilon-clausura

> [!definition]
> La $\varepsilon$-clausura de un estado $q$ es el conjunto de estados a los que se puede llegar desde $q$ usando cero o más transiciones $\varepsilon$.

Se denota:

$$
\varepsilon\text{-clausura}(q)
$$

Incluye siempre al propio estado $q$.

---

## 7. Epsilon-clausura de un conjunto

Si tenemos un conjunto de estados $A$, entonces:

$$
\varepsilon\text{-clausura}(A)
$$

es la unión de las clausuras de todos sus estados.

Es decir:

$$
\varepsilon\text{-clausura}(A)
=
\bigcup_{q \in A}
\varepsilon\text{-clausura}(q)
$$

---

## 8. Lenguaje aceptado por un NFA

Un NFA acepta una cadena $w$ si existe algún camino que:

1. parte del estado inicial;
2. consume toda la cadena;
3. termina en un estado final.

Formalmente:

$$
w \in L(M)
$$

si después de leer $w$ el conjunto de estados alcanzables contiene algún estado final.

---

## 9. Ventaja del NFA

Los NFA no reconocen más lenguajes que los DFA.

Pero son más fáciles de diseñar.

> [!important]
> Todo NFA tiene un DFA equivalente.
>
> Por tanto, DFA y NFA reconocen exactamente los mismos lenguajes: los lenguajes regulares.

---

# Bloque 4 — Conversión de NFA a DFA

## 1. Idea general

Un NFA puede estar en varios estados posibles a la vez.

Para simularlo con un DFA, hacemos que cada estado del DFA represente un conjunto de estados del NFA.

Es decir:

$$
Q_{DFA} \subseteq \mathcal{P}(Q_{NFA})
$$

---

## 2. Algoritmo de construcción por subconjuntos

Dado un NFA:

$$
M = (Q,\Sigma,\delta,s,F)
$$

construimos un DFA:

$$
M' = (Q',\Sigma,\delta',s',F')
$$

donde:

### Estados

Los estados del DFA son subconjuntos de estados del NFA:

$$
Q' = \mathcal{P}(Q)
$$

En la práctica solo usamos los subconjuntos alcanzables.

---

### Estado inicial

Si no hay transiciones $\varepsilon$:

$$
s' = \{s\}
$$

Si hay transiciones $\varepsilon$:

$$
s' = \varepsilon\text{-clausura}(s)
$$

---

### Transiciones

Para cada subconjunto $A \subseteq Q$ y cada símbolo $a \in \Sigma$:

$$
\delta'(A,a)
=
\varepsilon\text{-clausura}
\left(
\bigcup_{q \in A} \delta(q,a)
\right)
$$

Si no hay transiciones $\varepsilon$, queda simplemente:

$$
\delta'(A,a)
=
\bigcup_{q \in A} \delta(q,a)
$$

---

### Estados finales

Un subconjunto $A$ del DFA es final si contiene algún estado final del NFA:

$$
A \in F'
\iff
A \cap F \neq \emptyset
$$

---

## 3. Interpretación intuitiva

Un estado del DFA como:

$$
\{q_0,q_2,q_5\}
$$

significa:

> Después de leer cierta parte de la cadena, el NFA podría estar en $q_0$, en $q_2$ o en $q_5$.

---

## 4. Ejemplo sencillo

Supongamos un NFA con:

$$
Q = \{q_0,q_1\}
$$

$$
\Sigma = \{0,1\}
$$

Transiciones:

$$
\delta(q_0,0)=\{q_0,q_1\}
$$

$$
\delta(q_0,1)=\{q_1\}
$$

$$
\delta(q_1,0)=\emptyset
$$

$$
\delta(q_1,1)=\{q_0,q_1\}
$$

Los estados posibles del DFA son:

$$
\emptyset,\ \{q_0\},\ \{q_1\},\ \{q_0,q_1\}
$$

Transiciones:

| Estado DFA | Con 0 | Con 1 |
|---|---|---|
| $\emptyset$ | $\emptyset$ | $\emptyset$ |
| $\{q_0\}$ | $\{q_0,q_1\}$ | $\{q_1\}$ |
| $\{q_1\}$ | $\emptyset$ | $\{q_0,q_1\}$ |
| $\{q_0,q_1\}$ | $\{q_0,q_1\}$ | $\{q_0,q_1\}$ |

---

## 5. Procedimiento práctico para ejercicios

Cuando conviertas un NFA en DFA:

1. Calcula el estado inicial.
2. Haz una tabla.
3. Para cada estado-conjunto y cada símbolo:
   - mira a dónde va cada estado del conjunto;
   - une los resultados;
   - aplica $\varepsilon$-clausura si procede.
4. Añade nuevos conjuntos que aparezcan.
5. Repite hasta que no aparezcan nuevos estados.
6. Marca como finales los conjuntos que contengan algún estado final original.

---

## 6. Error frecuente

> [!warning]
> No todos los subconjuntos de $Q$ tienen por qué aparecer en el DFA final.
>
> Solo se dibujan normalmente los subconjuntos alcanzables desde el estado inicial.

---

# Bloque 5 — Minimización de DFA

## 1. Idea general

Dos DFA pueden reconocer el mismo lenguaje aunque tengan distinto número de estados.

Minimizar un DFA significa encontrar un DFA equivalente con el menor número posible de estados.

---

## 2. Estados equivalentes

> [!definition]
> Dos estados $p$ y $q$ son equivalentes si, empezando desde cualquiera de ellos, las mismas continuaciones llevan a aceptación o rechazo.

Formalmente:

$$
p \equiv q
$$

si para toda cadena $w \in \Sigma^*$:

$$
\delta^*(p,w) \in F
\iff
\delta^*(q,w) \in F
$$

---

## 3. Estados distinguibles

> [!definition]
> Dos estados $p$ y $q$ son distinguibles si existe alguna cadena $w$ tal que desde uno se acepta y desde el otro se rechaza.

Es decir:

$$
\exists w \in \Sigma^*
$$

tal que:

$$
\delta^*(p,w) \in F
$$

y:

$$
\delta^*(q,w) \notin F
$$

o al revés.

---

## 4. Idea intuitiva

Si dos estados se comportan exactamente igual frente a cualquier continuación, podemos fusionarlos.

Si existe alguna continuación que los diferencia, no se pueden fusionar.

---

## 5. Algoritmo de tabla de distinguibilidad

Dado un DFA:

$$
M = (Q,\Sigma,\delta,s,F)
$$

seguimos estos pasos:

### Paso 1

Construimos una tabla con todos los pares de estados distintos.

---

### Paso 2

Marcamos directamente todos los pares:

$$
(p,q)
$$

donde uno es final y el otro no.

Esos estados son distinguibles porque con la cadena vacía $\varepsilon$ uno acepta y el otro no.

---

### Paso 3

Para cada par no marcado $(p,q)$, miramos sus transiciones con cada símbolo $a$:

$$
\delta(p,a)
$$

y:

$$
\delta(q,a)
$$

Si el par resultante ya está marcado, entonces $(p,q)$ también se marca.

---

### Paso 4

Repetimos hasta que no se puedan marcar más pares.

---

### Paso 5

Los pares no marcados son equivalentes y pueden fusionarse.

---

## 6. Ejemplo conceptual

Supongamos que tenemos dos estados $A$ y $B$.

Si:

$$
A \notin F
$$

y:

$$
B \in F
$$

entonces $A$ y $B$ son distinguibles inmediatamente.

La cadena que los distingue es:

$$
\varepsilon
$$

Porque desde $B$ aceptamos sin leer nada y desde $A$ no.

---

## 7. Otro caso

Supongamos:

$$
A \notin F,\quad B \notin F
$$

No se distinguen de entrada.

Pero si con símbolo `0`:

$$
\delta(A,0)=C
$$

$$
\delta(B,0)=D
$$

y el par $(C,D)$ ya es distinguible, entonces $(A,B)$ también lo es.

La cadena que distingue a $A$ y $B$ empieza por `0`.

---

## 8. Construcción del DFA mínimo

Una vez encontrados los grupos de estados equivalentes:

1. Cada grupo se convierte en un estado del DFA mínimo.
2. El estado inicial será el grupo que contiene al estado inicial original.
3. Los estados finales serán los grupos que contienen algún estado final original.
4. Las transiciones se definen usando cualquier representante del grupo.

---

## 9. Estados inaccesibles

Antes de minimizar conviene eliminar estados inaccesibles.

> [!definition]
> Un estado es inaccesible si no se puede llegar a él desde el estado inicial.

Los estados inaccesibles no afectan al lenguaje reconocido.

---

## 10. Procedimiento completo para minimizar

1. Eliminar estados inaccesibles.
2. Crear tabla de pares.
3. Marcar pares final/no final.
4. Propagar marcas usando transiciones.
5. Agrupar estados no distinguibles.
6. Construir el DFA mínimo.

---

# Bloque 6 — Relación entre autómatas y expresiones regulares

## 1. Teorema fundamental

Los siguientes modelos son equivalentes:

1. Expresiones regulares.
2. Autómatas finitos deterministas, DFA.
3. Autómatas finitos no deterministas, NFA.

Esto significa que todos describen exactamente la misma familia de lenguajes:

$$
\textbf{los lenguajes regulares}
$$

> [!important]
> Para un lenguaje $L$, son equivalentes:
>
> - $L$ es regular.
> - Existe una expresión regular que representa $L$.
> - Existe un DFA que reconoce $L$.
> - Existe un NFA que reconoce $L$.

---

## 2. Esquema general de equivalencias

Podemos pasar de una representación a otra:

$$
\text{ER} \Rightarrow \text{NFA}
$$

$$
\text{NFA} \Rightarrow \text{DFA}
$$

$$
\text{DFA} \Rightarrow \text{ER}
$$

Por tanto:

$$
\text{ER} \equiv \text{NFA} \equiv \text{DFA}
$$

---

## 3. De expresión regular a NFA

Toda expresión regular puede transformarse en un NFA.

La construcción se hace recursivamente, según la forma de la expresión regular.

Casos básicos:

- $\emptyset$
- $\varepsilon$
- $a$, con $a \in \Sigma$

Casos recursivos:

- unión;
- concatenación;
- cierre de Kleene.

---

## 4. NFA para $\emptyset$

La expresión:

$$
\emptyset
$$

representa el lenguaje vacío.

Un NFA para $\emptyset$ puede tener:

- un estado inicial;
- ningún estado final.

Por tanto, no acepta ninguna cadena.

Diagrama conceptual:

`q0`

con:

$$
F = \emptyset
$$

---

## 5. NFA para $\varepsilon$

La expresión:

$$
\varepsilon
$$

representa:

$$
\{\varepsilon\}
$$

Un NFA para $\varepsilon$ puede tener un único estado que sea inicial y final.

Diagrama conceptual:

`q0`

con:

$$
q_0 \in F
$$

Así acepta la cadena vacía sin consumir ningún símbolo.

---

## 6. NFA para un símbolo

Para la expresión regular:

$$
a
$$

construimos un NFA con dos estados:

`q0 --a--> q1`

donde:

- $q_0$ es inicial;
- $q_1$ es final.

Este NFA acepta exactamente la cadena:

$$
a
$$

---

## 7. Construcción para la unión

Si tenemos dos expresiones regulares:

$$
r
$$

y:

$$
s
$$

queremos construir un NFA para:

$$
r|s
$$

La idea es crear un nuevo estado inicial que pueda elegir, mediante transiciones $\varepsilon$, si seguir el autómata de $r$ o el de $s$.

Esquema conceptual:

`q_ini --ε--> inicio_r ... final_r --ε--> q_fin`

`q_ini --ε--> inicio_s ... final_s --ε--> q_fin`

> [!note]
> La unión representa una elección: o se genera algo de $r$, o se genera algo de $s$.

---

## 8. Construcción para la concatenación

Para construir un NFA de:

$$
rs
$$

unimos el final del NFA de $r$ con el inicio del NFA de $s$ mediante una transición $\varepsilon$.

Esquema conceptual:

`inicio_r ... final_r --ε--> inicio_s ... final_s`

La idea es:

1. primero se reconoce una cadena de $L(r)$;
2. después se reconoce una cadena de $L(s)$.

Por tanto:

$$
L(rs) = L(r)L(s)
$$

---

## 9. Construcción para el cierre de Kleene

Para construir un NFA de:

$$
r^*
$$

necesitamos permitir:

- cero repeticiones;
- una repetición;
- varias repeticiones.

Esquema conceptual:

- `q_ini --ε--> q_fin`
- `q_ini --ε--> inicio_r`
- `final_r --ε--> inicio_r`
- `final_r --ε--> q_fin`

La transición:

$$
q_{ini} \xrightarrow{\varepsilon} q_{fin}
$$

permite aceptar $\varepsilon$.

La transición:

$$
final_r \xrightarrow{\varepsilon} inicio_r
$$

permite repetir el patrón.

> [!important]
> El cierre de Kleene siempre incluye cero repeticiones, por eso $r^*$ siempre contiene $\varepsilon$.

---

## 10. De NFA a DFA

Todo NFA puede transformarse en un DFA equivalente mediante la construcción por subconjuntos.

La idea es:

> Un estado del DFA representa un conjunto de posibles estados del NFA.

Si el NFA tiene estados:

$$
Q = \{q_0,q_1,q_2\}
$$

entonces los estados del DFA serán subconjuntos como:

$$
\{q_0\}
$$

$$
\{q_0,q_1\}
$$

$$
\{q_1,q_2\}
$$

$$
\emptyset
$$

---

## 11. Regla de conversión NFA $\to$ DFA

Dado un NFA:

$$
M = (Q,\Sigma,\delta,s,F)
$$

construimos un DFA:

$$
M' = (Q',\Sigma,\delta',s',F')
$$

donde:

### Estados

$$
Q' \subseteq \mathcal{P}(Q)
$$

Es decir, los estados del DFA son subconjuntos de estados del NFA.

---

### Estado inicial

Si no hay transiciones $\varepsilon$:

$$
s' = \{s\}
$$

Si hay transiciones $\varepsilon$:

$$
s' = \varepsilon\text{-clausura}(s)
$$

---

### Transiciones

Para cada subconjunto $A \subseteq Q$ y símbolo $a \in \Sigma$:

$$
\delta'(A,a) =
\bigcup_{q \in A} \delta(q,a)
$$

Si hay transiciones $\varepsilon$, entonces:

$$
\delta'(A,a) =
\varepsilon\text{-clausura}
\left(
\bigcup_{q \in A} \delta(q,a)
\right)
$$

---

### Estados finales

Un estado del DFA es final si contiene algún estado final del NFA.

Es decir:

$$
A \in F'
\iff
A \cap F \neq \emptyset
$$

---

## 12. Procedimiento práctico

Para convertir un NFA en DFA:

1. Empieza por el estado inicial:

$$
\{s\}
$$

o su $\varepsilon$-clausura.

2. Calcula sus transiciones para cada símbolo del alfabeto.

3. Cada nuevo conjunto que aparezca se convierte en un nuevo estado del DFA.

4. Repite hasta que no aparezcan nuevos conjuntos.

5. Marca como finales los conjuntos que contengan algún estado final del NFA.

---

## 13. Error frecuente

> [!warning]
> No hace falta dibujar todos los subconjuntos de $Q$.
>
> Solo se dibujan los subconjuntos alcanzables desde el estado inicial.

---

## 14. De DFA a expresión regular

También se puede obtener una expresión regular a partir de un DFA.

La idea general es eliminar estados intermedios y sustituir caminos por expresiones regulares.

Aunque el método formal puede ser largo, la intuición es:

- caminos alternativos se traducen como unión;
- caminos consecutivos se traducen como concatenación;
- ciclos se traducen como estrella de Kleene.

---

## 15. Ejemplo sencillo

Supongamos el siguiente autómata:

`q0 --a--> q1`

`q1 --b--> q1`

`q1 --c--> q2`

donde $q_2$ es final.

El lenguaje reconocido está formado por cadenas que:

1. empiezan por `a`;
2. tienen cero o más `b`;
3. terminan en `c`.

Por tanto, la expresión regular es:

$$
ab^*c
$$

---

# Bloque 7 — Regularidad y no regularidad

## 1. Cómo demostrar que un lenguaje es regular

Para demostrar que un lenguaje es regular basta con construir una de estas cosas:

1. Una expresión regular.
2. Un DFA.
3. Un NFA.
4. Una gramática regular.

Como todas estas representaciones son equivalentes, cualquiera de ellas sirve.

> [!tip]
> En examen, lo más rápido suele ser:
>
> - expresión regular si el patrón es sencillo;
> - DFA si hay que recordar estados;
> - NFA si aparece “contiene una subcadena” o hay elecciones.

---

## 2. Ejemplo usando expresión regular

Lenguaje:

$$
L = \{w \in \{a,b\}^* \mid w \text{ contiene la subcadena } ab\}
$$

Este lenguaje es regular porque se representa mediante:

$$
(a|b)^*ab(a|b)^*
$$

---

## 3. Ejemplo usando DFA

Lenguaje:

$$
L = \{w \in \{0,1\}^* \mid |w| \text{ es par}\}
$$

Usamos dos estados:

| Estado | Significado |
|---|---|
| $q_0$ | longitud par |
| $q_1$ | longitud impar |

El estado inicial es:

$$
q_0
$$

El único estado final es:

$$
q_0
$$

Transiciones:

| Estado | Con 0 | Con 1 |
|---|---|---|
| $q_0$ | $q_1$ | $q_1$ |
| $q_1$ | $q_0$ | $q_0$ |

Cada símbolo leído cambia la paridad de la longitud.

---

## 4. Ejemplo usando NFA

Lenguaje:

$$
L = \{w \in \{0,1\}^* \mid w \text{ contiene } 010\}
$$

Un NFA puede adivinar dónde empieza la subcadena `010`.

Estados:

| Estado | Significado |
|---|---|
| $q_0$ | todavía no he empezado el patrón |
| $q_1$ | he leído `0` |
| $q_2$ | he leído `01` |
| $q_3$ | he leído `010` |

Transiciones:

$$
\delta(q_0,0)=\{q_0,q_1\}
$$

$$
\delta(q_0,1)=\{q_0\}
$$

$$
\delta(q_1,1)=\{q_2\}
$$

$$
\delta(q_2,0)=\{q_3\}
$$

$$
\delta(q_3,0)=\{q_3\}
$$

$$
\delta(q_3,1)=\{q_3\}
$$

Estado final:

$$
q_3
$$

---

## 5. Lenguajes no regulares

No todos los lenguajes son regulares.

Un ejemplo fundamental es:

$$
L = \{a^n b^n \mid n \geq 0\}
$$

Este lenguaje no es regular porque un autómata finito no puede recordar un número arbitrariamente grande de `a` para compararlo después con el número de `b`.

---

## 6. Intuición de no regularidad

Un DFA tiene memoria finita.

Eso significa que solo puede recordar una cantidad limitada de información.

Por tanto, no puede resolver problemas que requieren contar de forma ilimitada.

Ejemplos típicos de lenguajes no regulares:

$$
\{a^n b^n \mid n \geq 0\}
$$

$$
\{a^n b^{2n} \mid n \geq 0\}
$$

$$
\{ww \mid w \in \{a,b\}^*\}
$$

$$
\{w \in \{0,1\}^* \mid w = w^I\}
$$

---

# Bloque 8 — Lema de bombeo para lenguajes regulares

## 1. Para qué sirve

El lema de bombeo se usa para demostrar que ciertos lenguajes no son regulares.

> [!warning]
> El lema de bombeo no sirve para demostrar que un lenguaje es regular.
>
> Solo sirve para demostrar que un lenguaje no es regular.

---

## 2. Enunciado

> [!definition]
> Si $L$ es un lenguaje regular, entonces existe una constante $p \geq 1$ tal que toda cadena $w \in L$ con $|w| \geq p$ puede escribirse como:
>
> $$
> w = xyz
> $$
>
> cumpliendo:
>
> 1. $|xy| \leq p$
> 2. $|y| > 0$
> 3. Para todo $i \geq 0$:
>
> $$
> xy^iz \in L
> $$

---

## 3. Intuición

Si un lenguaje es regular, entonces lo reconoce algún DFA.

Como el DFA tiene un número finito de estados, al leer una cadena suficientemente larga, necesariamente repite algún estado.

Eso significa que hay un ciclo.

La parte de la cadena que recorre ese ciclo se puede repetir varias veces, y la cadena debería seguir siendo aceptada.

A eso se le llama bombear.

---

## 4. Qué significa $w = xyz$

La descomposición:

$$
w = xyz
$$

se interpreta así:

- $x$ es la parte anterior al ciclo;
- $y$ es la parte que corresponde al ciclo;
- $z$ es la parte posterior al ciclo.

La parte que se bombea es:

$$
y
$$

---

## 5. Condición $|xy| \leq p$

Esta condición significa que $x$ e $y$ están dentro de los primeros $p$ símbolos de la cadena.

En muchos ejercicios elegimos una cadena donde los primeros $p$ símbolos son todos iguales.

Por ejemplo:

$$
w = a^p b^p
$$

Así sabemos que $y$ solo puede estar formada por símbolos `a`.

---

## 6. Condición $|y| > 0$

Esta condición significa que $y$ no puede ser vacía.

Por tanto, si $y$ está dentro de un bloque de `a`, entonces:

$$
y = a^k
$$

con:

$$
k > 0
$$

---

## 7. Condición $xy^iz \in L$

Esta condición debe cumplirse para todo:

$$
i \geq 0
$$

Valores habituales:

- $i = 0$: elimina $y$.
- $i = 2$: duplica $y$.

> [!tip]
> Normalmente basta con encontrar un único valor de $i$ que haga que la cadena salga del lenguaje.

---

## 8. Plantilla de examen

> Supongamos, por reducción al absurdo, que $L$ es regular.
>
> Entonces existe una constante de bombeo $p$.
>
> Elegimos la cadena $w = \dots \in L$ con $|w| \geq p$.
>
> Por el lema de bombeo, $w$ puede escribirse como $w = xyz$, cumpliendo:
>
> 1. $|xy| \leq p$
> 2. $|y| > 0$
> 3. $xy^iz \in L$ para todo $i \geq 0$
>
> Como $|xy| \leq p$, la subcadena $y$ está formada solo por $\dots$
>
> Además, como $|y| > 0$, $y$ contiene al menos un símbolo.
>
> Tomamos $i = \dots$
>
> Entonces $xy^iz = \dots$
>
> Pero esta cadena no pertenece a $L$.
>
> Contradicción.
>
> Por tanto, $L$ no es regular.

---

## 9. Ejemplo: $\{a^n b^n \mid n \geq 0\}$ no es regular

Queremos demostrar que:

$$
L = \{a^n b^n \mid n \geq 0\}
$$

no es regular.

### Demostración

Supongamos que $L$ es regular.

Entonces existe una constante de bombeo $p$.

Elegimos:

$$
w = a^p b^p
$$

Claramente:

$$
w \in L
$$

y:

$$
|w| = 2p \geq p
$$

Por el lema de bombeo:

$$
w = xyz
$$

con:

$$
|xy| \leq p
$$

y:

$$
|y| > 0
$$

Como los primeros $p$ símbolos son todos `a`, entonces $y$ está formada solo por `a`.

Por tanto:

$$
y = a^k
$$

con:

$$
k > 0
$$

Tomamos:

$$
i = 0
$$

Entonces:

$$
xy^0z = xz
$$

Esto elimina al menos una `a`, pero no elimina ninguna `b`.

Por tanto, la cadena resultante tiene menos `a` que `b`, así que:

$$
xz \notin L
$$

Esto contradice el lema de bombeo.

Por tanto:

$$
L
$$

no es regular.

---

## 10. Ejemplo: palíndromos

Sea:

$$
L = \{w \in \{0,1\}^* \mid w = w^I\}
$$

Queremos demostrar que $L$ no es regular.

Supongamos que $L$ es regular.

Entonces existe una constante de bombeo $p$.

Elegimos:

$$
w = 0^p10^p
$$

Esta cadena es un palíndromo.

Por tanto:

$$
w \in L
$$

Además:

$$
|w| = 2p+1 \geq p
$$

Por el lema:

$$
w = xyz
$$

con:

$$
|xy| \leq p
$$

y:

$$
|y| > 0
$$

Como los primeros $p$ símbolos son ceros, entonces:

$$
y = 0^k
$$

con:

$$
k > 0
$$

Tomamos:

$$
i = 2
$$

Entonces:

$$
xy^2z
$$

tiene más ceros a la izquierda del `1` que a la derecha.

Por tanto, ya no es un palíndromo.

Así que:

$$
xy^2z \notin L
$$

Contradicción.

Por tanto:

$$
L
$$

no es regular.

---

## 11. Ejemplo: $\{ww \mid w \in \{a,b\}^*\}$ no es regular

Sea:

$$
L = \{ww \mid w \in \{a,b\}^*\}
$$

Supongamos que $L$ es regular.

Entonces existe una constante de bombeo $p$.

Elegimos:

$$
w = a^pba^pb
$$

Esta cadena pertenece a $L$, porque es de la forma:

$$
xx
$$

con:

$$
x = a^pb
$$

Por el lema:

$$
w = xyz
$$

con:

$$
|xy| \leq p
$$

y:

$$
|y| > 0
$$

Como los primeros $p$ símbolos son todos `a`, entonces:

$$
y = a^k
$$

con:

$$
k > 0
$$

Tomamos:

$$
i = 2
$$

Entonces:

$$
xy^2z
$$

añade `a` solo en la primera mitad de la cadena.

La cadena resultante ya no puede escribirse como dos copias iguales de una misma cadena.

Por tanto:

$$
xy^2z \notin L
$$

Contradicción.

Así que:

$$
L
$$

no es regular.

---

# Bloque 9 — Propiedades de cierre de los lenguajes regulares

## 1. Qué significa cierre

Una familia de lenguajes es cerrada bajo una operación si al aplicar esa operación a lenguajes de la familia, el resultado sigue perteneciendo a la misma familia.

Ejemplo:

Si $L_1$ y $L_2$ son regulares y $L_1 \cup L_2$ también es regular, entonces decimos que los lenguajes regulares son cerrados bajo unión.

---

## 2. Cierre bajo unión

Si $L_1$ y $L_2$ son regulares, entonces:

$$
L_1 \cup L_2
$$

también es regular.

### Justificación

Si $L_1$ y $L_2$ tienen expresiones regulares $r_1$ y $r_2$, entonces:

$$
r_1 | r_2
$$

representa:

$$
L_1 \cup L_2
$$

---

## 3. Cierre bajo concatenación

Si $L_1$ y $L_2$ son regulares, entonces:

$$
L_1L_2
$$

también es regular.

### Justificación

Si $r_1$ representa $L_1$ y $r_2$ representa $L_2$, entonces:

$$
r_1r_2
$$

representa:

$$
L_1L_2
$$

---

## 4. Cierre bajo estrella de Kleene

Si $L$ es regular, entonces:

$$
L^*
$$

también es regular.

### Justificación

Si $r$ representa $L$, entonces:

$$
r^*
$$

representa:

$$
L^*
$$

---

## 5. Cierre bajo complemento

Si $L$ es regular, entonces:

$$
\overline{L}
$$

también es regular.

### Construcción

1. Tomamos un DFA completo que reconoce $L$.
2. Convertimos en finales los estados no finales.
3. Convertimos en no finales los estados finales.

> [!warning]
> Para complementar un autómata, debe ser un DFA completo.
>
> Si falta alguna transición, primero se añade un estado sumidero.

---

## 6. Cierre bajo intersección

Si $L_1$ y $L_2$ son regulares, entonces:

$$
L_1 \cap L_2
$$

también es regular.

Se puede demostrar con leyes de De Morgan:

$$
L_1 \cap L_2 =
\overline{\overline{L_1} \cup \overline{L_2}}
$$

Como los regulares son cerrados bajo complemento y unión, también lo son bajo intersección.

---

## 7. Producto de autómatas

Otra forma de demostrar unión e intersección es usando producto de autómatas.

Dados:

$$
M_1 = (Q_1,\Sigma,\delta_1,s_1,F_1)
$$

$$
M_2 = (Q_2,\Sigma,\delta_2,s_2,F_2)
$$

construimos:

$$
M = (Q,\Sigma,\delta,s,F)
$$

donde:

$$
Q = Q_1 \times Q_2
$$

El estado inicial es:

$$
s = (s_1,s_2)
$$

La transición es:

$$
\delta((p,q),a)
=
(\delta_1(p,a),\delta_2(q,a))
$$

---

## 8. Producto para intersección

Para reconocer:

$$
L_1 \cap L_2
$$

los estados finales son:

$$
F = F_1 \times F_2
$$

Es decir, aceptamos si ambos autómatas aceptan.

---

## 9. Producto para unión

Para reconocer:

$$
L_1 \cup L_2
$$

los estados finales son:

$$
F =
(F_1 \times Q_2)
\cup
(Q_1 \times F_2)
$$

Es decir, aceptamos si al menos uno de los dos autómatas acepta.

---

## 10. Cierre bajo diferencia

Si $L_1$ y $L_2$ son regulares, entonces:

$$
L_1 - L_2
$$

también es regular.

Porque:

$$
L_1 - L_2 = L_1 \cap \overline{L_2}
$$

Como los regulares son cerrados bajo complemento e intersección, también lo son bajo diferencia.

---

## 11. Cierre bajo inversa

Si $L$ es regular, entonces:

$$
L^I
$$

también es regular.

Donde:

$$
L^I = \{w^I \mid w \in L\}
$$

Es decir, el lenguaje formado por las cadenas invertidas.

### Ejemplo

Si:

$$
L = L(ab^*c)
$$

entonces:

$$
L^I = L(cb^*a)
$$

---

# Bloque 10 — Resumen práctico para examen

## 1. Si te piden una expresión regular

Busca primero el patrón del lenguaje.

| Lenguaje | Expresión regular típica |
|---|---|
| Todas las cadenas sobre $\{a,b\}$ | $(a|b)^*$ |
| Cadenas que contienen `ab` | $(a|b)^*ab(a|b)^*$ |
| Cadenas que terminan en `ab` | $(a|b)^*ab$ |
| Cadenas que empiezan por `ab` | $ab(a|b)^*$ |
| Cadenas con número par de `a` | $b^*(ab^*ab^*)^*$ |
| Cadenas con número impar de `a` | $b^*ab^*(ab^*ab^*)^*$ |
| Cadenas sin `11` | $(0|10)^*(\varepsilon|1)$ |

---

## 2. Si te piden un DFA

Pregunta clave:

> ¿Qué necesito recordar mientras leo la cadena?

| Condición | Qué recordar |
|---|---|
| Termina en `00` | últimos símbolos leídos |
| Contiene `010` | progreso dentro del patrón |
| Número par de `a` | paridad de aes |
| Longitud múltiplo de 3 | longitud módulo 3 |
| No contiene `11` | si el último símbolo fue `1` |
| Empieza y termina igual | primer símbolo y último leído |

---

## 3. Si te piden un NFA

Conviene usar NFA cuando el lenguaje tenga una condición del tipo:

- contiene cierta subcadena;
- termina con cierta subcadena;
- existe una posición con cierta propiedad;
- unión de varios patrones.

Ejemplo:

$$
(0|1)^*010(0|1)^*
$$

es muy natural con NFA, porque el autómata puede adivinar dónde empieza `010`.

---

## 4. Si te piden convertir NFA a DFA

Usa construcción por subconjuntos.

Pasos:

1. Estado inicial:

$$
\{q_0\}
$$

o:

$$
\varepsilon\text{-clausura}(q_0)
$$

2. Para cada conjunto de estados y cada símbolo:

$$
\delta'(A,a)
=
\bigcup_{q \in A}\delta(q,a)
$$

3. Si hay $\varepsilon$, aplicar clausura.

4. Añadir nuevos conjuntos que aparezcan.

5. Marcar como finales los conjuntos que contengan algún estado final del NFA.

---

## 5. Si te piden minimizar un DFA

Pasos:

1. Eliminar estados inaccesibles.
2. Separar estados finales y no finales.
3. Refinar grupos según transiciones.
4. Repetir hasta que no cambie.
5. Fusionar estados equivalentes.
6. Construir el DFA mínimo.

---

## 6. Si te piden demostrar que un lenguaje es regular

Puedes hacer cualquiera de estas cosas:

- dar una expresión regular;
- construir un DFA;
- construir un NFA;
- usar propiedades de cierre.

Ejemplo:

$$
L = \{w \in \{0,1\}^* \mid w \text{ contiene } 00 \text{ y termina en } 1\}
$$

Sabemos que:

$$
L_1 = \{w \mid w \text{ contiene } 00\}
$$

es regular.

Y:

$$
L_2 = \{w \mid w \text{ termina en } 1\}
$$

es regular.

Entonces:

$$
L = L_1 \cap L_2
$$

es regular por cierre bajo intersección.

---

## 7. Si te piden demostrar que un lenguaje no es regular

Normalmente usa el lema de bombeo.

Plantilla:

> Supongamos que $L$ es regular.
>
> Sea $p$ la constante de bombeo.
>
> Elegimos $w = \dots \in L$ con $|w| \geq p$.
>
> Por el lema, $w = xyz$, con $|xy| \leq p$ y $|y| > 0$.
>
> Como $|xy| \leq p$, $y$ está dentro de $\dots$
>
> Por tanto, $y = \dots$
>
> Tomamos $i = \dots$
>
> Entonces $xy^iz$ no pertenece a $L$.
>
> Contradicción.
>
> Luego $L$ no es regular.

---

## 8. Cadenas típicas para el lema de bombeo

| Lenguaje | Cadena elegida |
|---|---|
| $\{a^n b^n\}$ | $a^p b^p$ |
| $\{a^n b^{2n}\}$ | $a^p b^{2p}$ |
| Palíndromos | $0^p10^p$ |
| $\{ww\}$ | $a^pba^pb$ |
| Igual número de `a` y `b` en bloques | $a^p b^p$ |

---

## 9. Errores frecuentes

> [!warning]
> Error 1:
>
> Decir que un lenguaje no es regular porque "parece difícil".
>
> Hay que demostrarlo formalmente.

---

> [!warning]
> Error 2:
>
> Usar el lema de bombeo para demostrar que un lenguaje es regular.
>
> El lema de bombeo no sirve para eso.

---

> [!warning]
> Error 3:
>
> Elegir una cadena que no pertenece al lenguaje.
>
> La cadena elegida para bombear debe estar en $L$.

---

> [!warning]
> Error 4:
>
> Elegir una descomposición concreta de $w = xyz$.
>
> En una demostración correcta, debes razonar para cualquier descomposición que cumpla las condiciones del lema.

---

## 10. Checklist del Tema 2

Antes de pasar a ejercicios de examen, deberías saber hacer:

- [ ] Leer una expresión regular.
- [ ] Escribir una expresión regular para un lenguaje sencillo.
- [ ] Simplificar expresiones regulares.
- [ ] Diseñar DFA.
- [ ] Interpretar DFA.
- [ ] Diseñar NFA.
- [ ] Calcular $\varepsilon$-clausuras.
- [ ] Convertir NFA a DFA.
- [ ] Minimizar DFA.
- [ ] Demostrar que un lenguaje es regular.
- [ ] Usar el lema de bombeo para demostrar no regularidad.
- [ ] Usar cierres de lenguajes regulares.

---

# Bloque 11 — Ejercicios recomendados del Tema 2

## 1. Expresiones regulares

Practicar:

- escribir expresiones regulares;
- interpretar expresiones;
- simplificar expresiones.

Ejercicios recomendados:

- Ejercicio 1.
- Ejercicio 2.
- Ejercicio 3.
- Ejercicio 4.
- Ejercicio 5.

---

## 2. DFA

Practicar:

- diseño de autómatas deterministas;
- interpretación de lenguajes aceptados;
- estados sumidero;
- condiciones de paridad;
- condiciones sobre prefijos, sufijos y subcadenas.

Ejercicios recomendados:

- Ejercicio 6.
- Ejercicio 7.
- Ejercicio 8.
- Ejercicio 13.

---

## 3. NFA

Practicar:

- no determinismo;
- transiciones $\varepsilon$;
- diseño de autómatas más compactos.

Ejercicios recomendados:

- Ejercicio 9.
- Ejercicio 12.
- Ejercicio 14.
- Ejercicio 17.

---

## 4. Conversión NFA a DFA

Practicar:

- construcción por subconjuntos;
- estado $\emptyset$;
- clausuras $\varepsilon$;
- identificación de estados finales.

Ejercicios recomendados:

- Ejercicio 10.
- Ejercicio 11.

---

## 5. Minimización

Practicar:

- eliminar estados inaccesibles;
- distinguir estados;
- fusionar equivalentes;
- obtener DFA mínimo.

Ejercicios recomendados:

- Ejercicio 15.
- Ejercicio 16.

---

## 6. Regularidad y no regularidad

Practicar:

- demostrar regularidad mediante ER, DFA o NFA;
- demostrar no regularidad con lema de bombeo;
- usar propiedades de cierre.

Ejercicio recomendado:

- Ejercicio 18.

---

# Bloque 12 — Resumen final del Tema 2

## 1. Equivalencias fundamentales

$$
L \text{ es regular}
$$

si y solo si:

$$
L \text{ es reconocido por un DFA}
$$

si y solo si:

$$
L \text{ es reconocido por un NFA}
$$

si y solo si:

$$
L \text{ es representado por una expresión regular}
$$

---

## 2. Jerarquía práctica

Expresión regular  
$\Updownarrow$  
NFA  
$\Updownarrow$  
DFA

Todos tienen la misma potencia, pero distinta comodidad.

---

## 3. Cuándo usar cada herramienta

| Herramienta | Cuándo usarla |
|---|---|
| Expresión regular | Si el patrón es claro |
| DFA | Si hay que recordar información finita |
| NFA | Si hay elecciones o subcadenas |
| Lema de bombeo | Para demostrar que no es regular |
| Cierres | Para combinar lenguajes conocidos |

---

## 4. Ideas clave

> [!summary]
> - Los lenguajes regulares son los más simples de la jerarquía.
> - Los DFA tienen memoria finita.
> - Los NFA no son más potentes que los DFA, pero suelen ser más cómodos.
> - Toda expresión regular tiene un NFA equivalente.
> - Todo NFA tiene un DFA equivalente.
> - Todo DFA puede minimizarse.
> - El lema de bombeo sirve para demostrar que un lenguaje no es regular.
> - Los lenguajes regulares son cerrados bajo muchas operaciones.

---

## 5. Fórmulas importantes

### Lenguaje aceptado por un DFA

$$
L(M)=\{w \in \Sigma^* \mid \delta^*(s,w) \in F\}
$$

---

### Función extendida

$$
\delta^*(q,\varepsilon)=q
$$

$$
\delta^*(q,wa)=\delta(\delta^*(q,w),a)
$$

---

### Construcción por subconjuntos

$$
Q_{DFA} \subseteq \mathcal{P}(Q_{NFA})
$$

---

### Estados finales en NFA $\to$ DFA

$$
A \in F'
\iff
A \cap F \neq \emptyset
$$

---

### Lema de bombeo

Si $L$ es regular, entonces:

$$
\exists p \geq 1
$$

tal que toda cadena $w \in L$ con $|w| \geq p$ se puede escribir como:

$$
w = xyz
$$

cumpliendo:

$$
|xy| \leq p
$$

$$
|y| > 0
$$

$$
xy^iz \in L,\ \forall i \geq 0
$$

---

## 6. Lenguajes que debes reconocer al instante

### Regulares

$$
(a|b)^*
$$

$$
(a|b)^*abb
$$

$$
(a|b)^*ab(a|b)^*
$$

$$
\{w \mid |w| \text{ es par}\}
$$

$$
\{w \mid w \text{ contiene } 00\}
$$

$$
\{w \mid w \text{ no contiene } 11\}
$$

---

### No regulares

$$
\{a^n b^n \mid n \geq 0\}
$$

$$
\{a^n b^{2n} \mid n \geq 0\}
$$

$$
\{ww \mid w \in \{a,b\}^*\}
$$

$$
\{w \mid w = w^I\}
$$