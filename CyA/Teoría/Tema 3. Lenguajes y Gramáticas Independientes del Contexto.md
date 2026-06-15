## 0. Idea general del tema

En el Tema 2 vimos dos formas de describir lenguajes regulares:

- expresiones regulares;
- autómatas finitos.

Las expresiones regulares describen un lenguaje mediante un patrón.

Los autómatas finitos describen un lenguaje como el conjunto de cadenas que llevan al autómata desde el estado inicial hasta un estado de aceptación.

En este tema aparece una nueva forma de describir lenguajes:

$$
\textbf{las gramáticas}
$$

Una gramática no reconoce cadenas como un autómata, sino que las genera.

> [!important]
> Un autómata responde a la pregunta:
>
> ¿Esta cadena pertenece al lenguaje?
>
> Una gramática responde a la pregunta:
>
> ¿Cómo puedo generar las cadenas del lenguaje?

---

# 1. Gramáticas: idea intuitiva

Una gramática es un conjunto de reglas que permiten construir cadenas.

Por ejemplo, queremos generar cadenas del lenguaje:

$$
a(a^*|b^*)b
$$

Es decir, cadenas que:

1. empiezan por una `a`;
2. después tienen cero o más `a`, o cero o más `b`;
3. terminan en `b`.

Una posible gramática es:

$$
S \to aE
$$

$$
E \to A|B
$$

$$
A \to aA|b
$$

$$
B \to bB|b
$$

La idea es:

- `S` genera la estructura inicial;
- `E` decide si vamos por la rama de muchas `a` o muchas `b`;
- `A` genera varias `a` y termina en `b`;
- `B` genera varias `b`.

---

## 1.1 Ejemplo de derivación

Con la gramática:

$$
S \to aE
$$

$$
E \to A|B
$$

$$
A \to aA|b
$$

$$
B \to bB|b
$$

podemos generar la cadena:

$$
aaab
$$

mediante la derivación:

$$
S \Rightarrow aE \Rightarrow aA \Rightarrow aaA \Rightarrow aaaA \Rightarrow aaab
$$

> [!note]
> El símbolo $\Rightarrow$ significa "deriva en un paso".

---

# 2. Elementos de una gramática

Una gramática usa dos tipos de símbolos:

## 2.1 Símbolos terminales

Son los símbolos reales del alfabeto.

Por ejemplo:

$$
\Sigma = \{a,b\}
$$

Los terminales son los símbolos que aparecerán en las cadenas finales.

---

## 2.2 Símbolos no terminales

Son símbolos auxiliares que sirven para generar cadenas.

Normalmente se escriben con mayúsculas:

$$
S, A, B, C, E, \dots
$$

El símbolo más importante suele ser:

$$
S
$$

que representa el símbolo inicial o símbolo de arranque.

---

## 2.3 Producciones

Las producciones son reglas de sustitución.

Tienen la forma:

$$
A \to \alpha
$$

donde:

- $A$ es un símbolo no terminal;
- $\alpha$ es una cadena formada por terminales y no terminales.

Por ejemplo:

$$
A \to aA
$$

significa que podemos sustituir $A$ por $aA$.

---

# 3. Gramáticas regulares

## 3.1 Definición

> [!definition]
> Una gramática regular es una 4-tupla:
>
> $$
> G = (\Sigma, N, S, P)
> $$
>
> donde:
>
> - $\Sigma$ es el alfabeto de símbolos terminales;
> - $N$ es el conjunto de símbolos no terminales;
> - $S$ es el símbolo inicial;
> - $P$ es el conjunto de producciones.

Las producciones deben ser de una de estas dos formas:

## Gramática lineal por la derecha

Todas las producciones tienen la forma:

$$
A \to uB
$$

o

$$
A \to v
$$

donde:

$$
A,B \in N
$$

y

$$
u,v \in \Sigma^*
$$

Es decir, si aparece un no terminal, aparece al final.

Ejemplo:

$$
S \to aA
$$

$$
A \to bA|a
$$

---

## Gramática lineal por la izquierda

Todas las producciones tienen la forma:

$$
A \to Bu
$$

o

$$
A \to v
$$

donde:

$$
A,B \in N
$$

y

$$
u,v \in \Sigma^*
$$

Es decir, si aparece un no terminal, aparece al principio.

Ejemplo:

$$
S \to Sa|b
$$

---

> [!important]
> Una gramática es regular si es:
>
> - lineal por la derecha, o
> - lineal por la izquierda.
>
> Pero no se deben mezclar ambos estilos en una misma gramática regular.

---

# 4. Ejemplo: gramática regular para una expresión regular

Queremos generar el lenguaje:

$$
0(10)^*
$$

Una gramática lineal por la derecha es:

$$
S \to 0A
$$

$$
A \to 10A|\varepsilon
$$

Genera:

$$
0,\ 010,\ 01010,\ 0101010,\dots
$$

Una gramática lineal por la izquierda es:

$$
S \to S10|0
$$

También genera:

$$
0(10)^*
$$

---

# 5. Lenguaje generado por una gramática

> [!definition]
> El lenguaje generado por una gramática $G$ se denota:
>
> $$
> L(G)
> $$
>
> y es el conjunto de todas las cadenas terminales que pueden derivarse desde el símbolo inicial.

Formalmente:

$$
L(G) = \{w \in \Sigma^* \mid S \Rightarrow^* w\}
$$

donde:

$$
\Rightarrow^*
$$

significa "deriva en cero o más pasos".

---

## 5.1 Ejemplo

Sea la gramática:

$$
S \to bA
$$

$$
A \to aaA|b|\varepsilon
$$

Entonces:

$$
L(G) = L(b(aa)^*(b|\varepsilon))
$$

Es decir, genera cadenas que:

1. empiezan por `b`;
2. después tienen cero o más bloques `aa`;
3. finalmente pueden terminar en `b` o no añadir nada más.

Ejemplos de cadenas generadas:

$$
b
$$

$$
bb
$$

$$
baab
$$

$$
baa
$$

$$
baaaab
$$

---

# 6. Relación entre gramáticas regulares y autómatas finitos

Las gramáticas regulares generan exactamente los lenguajes regulares.

Esto significa que:

$$
L \text{ es regular}
$$

si y solo si existe una gramática regular que genera $L$.

También equivale a decir que existe un DFA o NFA que reconoce $L$.

---

## 6.1 De DFA a gramática regular

Si tenemos un DFA:

$$
M = (Q, \Sigma, s, F, \delta)
$$

podemos construir una gramática regular:

$$
G = (\Sigma, N, S, P)
$$

de la siguiente forma:

$$
N = Q
$$

$$
S = s
$$

y para cada transición:

$$
\delta(q,a)=p
$$

añadimos la producción:

$$
q \to ap
$$

Además, para cada estado final:

$$
q \in F
$$

añadimos:

$$
q \to \varepsilon
$$

> [!tip]
> Cada estado del autómata se convierte en un no terminal de la gramática.

---

## 6.2 De gramática regular a NFA

Si tenemos una gramática regular, podemos construir un NFA equivalente.

La idea es:

- cada no terminal se convierte en un estado;
- se añade un estado final nuevo;
- cada producción se convierte en una transición.

Por ejemplo, si tenemos:

$$
A \to aB
$$

añadimos una transición:

$$
A \xrightarrow{a} B
$$

Si tenemos:

$$
A \to a
$$

añadimos una transición hacia el estado final:

$$
A \xrightarrow{a} f
$$

Si tenemos:

$$
A \to \varepsilon
$$

añadimos:

$$
A \xrightarrow{\varepsilon} f
$$

---

# 7. Gramáticas independientes del contexto

Las gramáticas regulares solo pueden generar lenguajes relativamente simples.

Por ejemplo, no pueden generar:

$$
\{a^n b^n \mid n \geq 0\}
$$

porque para generar este lenguaje hay que "recordar" cuántas `a` se han producido para luego producir el mismo número de `b`.

Para eso necesitamos gramáticas más potentes:

$$
\textbf{gramáticas independientes del contexto}
$$

---

## 7.1 Definición formal

> [!definition]
> Una gramática independiente del contexto, o CFG, es una 4-tupla:
>
> $$
> G = (V, \Sigma, S, P)
> $$
>
> donde:
>
> - $V$ es el conjunto de símbolos no terminales;
> - $\Sigma$ es el conjunto de símbolos terminales;
> - $S \in V$ es el símbolo inicial;
> - $P$ es un conjunto de producciones de la forma:
>
> $$
> A \to \alpha
> $$
>
> donde:
>
> $$
> A \in V
> $$
>
> y
>
> $$
> \alpha \in (V \cup \Sigma)^*
> $$

La diferencia clave respecto a las gramáticas regulares es que ahora el lado derecho puede tener una estructura mucho más general.

---

## 7.2 Ejemplo fundamental

La gramática:

$$
S \to aSb|\varepsilon
$$

genera el lenguaje:

$$
L(G)=\{a^n b^n \mid n \geq 0\}
$$

Veamos algunas derivaciones:

Para $n=0$:

$$
S \Rightarrow \varepsilon
$$

Para $n=1$:

$$
S \Rightarrow aSb \Rightarrow ab
$$

Para $n=2$:

$$
S \Rightarrow aSb \Rightarrow aaSbb \Rightarrow aabb
$$

Para $n=3$:

$$
S \Rightarrow aSb \Rightarrow aaSbb \Rightarrow aaaSbbb \Rightarrow aaabbb
$$

> [!important]
> Esta gramática genera el mismo número de `a` que de `b` porque cada vez que añade una `a` al principio, también añade una `b` al final.

---

# 8. Diferencia entre lenguaje regular y lenguaje independiente del contexto

Todo lenguaje regular es independiente del contexto.

Pero no todo lenguaje independiente del contexto es regular.

La relación es:

$$
\text{Lenguajes regulares} \subset \text{Lenguajes independientes del contexto}
$$

Ejemplo:

$$
\{a^n b^n \mid n \geq 0\}
$$

es independiente del contexto, pero no regular.

---

# 9. Derivaciones

## 9.1 Derivación en un paso

Si tenemos una producción:

$$
A \to \gamma
$$

entonces podemos sustituir $A$ por $\gamma$ dentro de una cadena.

Formalmente:

$$
\alpha A \beta \Rightarrow \alpha \gamma \beta
$$

---

## 9.2 Derivación en varios pasos

Si:

$$
\alpha_1 \Rightarrow \alpha_2 \Rightarrow \dots \Rightarrow \alpha_n
$$

entonces decimos que:

$$
\alpha_1 \Rightarrow^* \alpha_n
$$

---

## 9.3 Notación

| Notación | Significado |
|---|---|
| $\Rightarrow$ | deriva en un paso |
| $\Rightarrow^*$ | deriva en cero o más pasos |
| $\Rightarrow^+$ | deriva en uno o más pasos |

---

# 10. Formas sentenciales y frases

> [!definition]
> Una forma sentencial es cualquier cadena de símbolos terminales y no terminales que puede obtenerse desde el símbolo inicial.

Formalmente, $\alpha$ es forma sentencial si:

$$
S \Rightarrow^* \alpha
$$

---

> [!definition]
> Una frase, sentencia o cadena es una forma sentencial formada solo por símbolos terminales.

Es decir:

$$
w \in \Sigma^*
$$

---

# 11. Árboles de análisis sintáctico

Un árbol de análisis sintáctico, o AAS, es una representación gráfica de una derivación.

Cumple:

- la raíz es el símbolo inicial;
- los nodos internos son no terminales;
- las hojas son terminales o $\varepsilon$;
- si se usa una producción $A \to X_1X_2\dots X_n$, entonces $A$ tiene como hijos a $X_1, X_2, \dots, X_n$;
- la cadena generada se lee en las hojas de izquierda a derecha.

---

## 11.1 Ejemplo

Gramática:

$$
S \to AB
$$

$$
A \to aA|\varepsilon
$$

$$
B \to bB|\varepsilon
$$

Una derivación posible es:

$$
S \Rightarrow AB \Rightarrow aAB \Rightarrow aAbB \Rightarrow abB \Rightarrow abbB \Rightarrow abb
$$

La cadena generada es:

$$
abb
$$

---

# 12. Derivaciones canónicas

En cada paso de una derivación hay dos decisiones:

1. qué no terminal sustituir;
2. qué producción aplicar.

Una derivación puede hacerse de muchas formas distintas.

Para ordenar el proceso se usan derivaciones canónicas.

---

## 12.1 Derivación más a la izquierda

> [!definition]
> Una derivación más a la izquierda sustituye siempre el no terminal más a la izquierda de la forma sentencial.

---

## 12.2 Derivación más a la derecha

> [!definition]
> Una derivación más a la derecha sustituye siempre el no terminal más a la derecha de la forma sentencial.

---

# 13. Ambigüedad

> [!definition]
> Una gramática es ambigua si existe alguna cadena del lenguaje que tiene más de un árbol de análisis sintáctico distinto.

Equivalencias importantes:

Una gramática es ambigua si alguna cadena tiene:

- más de un AAS;
- más de una derivación más a la izquierda;
- más de una derivación más a la derecha.

---

## 13.1 Ejemplo de gramática ambigua

Sea:

$$
S \to SbS|ScS|a
$$

La cadena:

$$
abaca
$$

puede derivarse de dos formas distintas.

Primera derivación:

$$
S \Rightarrow ScS \Rightarrow SbScS \Rightarrow abScS \Rightarrow abacS \Rightarrow abaca
$$

Segunda derivación:

$$
S \Rightarrow SbS \Rightarrow abS \Rightarrow abScS \Rightarrow abacS \Rightarrow abaca
$$

Por tanto, la gramática es ambigua.

---

# 14. Clasificación de Chomsky

Las gramáticas se clasifican en cuatro tipos:

| Tipo | Nombre | Lenguajes generados |
|---|---|---|
| Tipo 0 | Gramáticas sin restricciones | Lenguajes recursivamente enumerables |
| Tipo 1 | Gramáticas sensibles al contexto | Lenguajes sensibles al contexto |
| Tipo 2 | Gramáticas independientes del contexto | Lenguajes independientes del contexto |
| Tipo 3 | Gramáticas regulares | Lenguajes regulares |

La inclusión es:

$$
L(G_3) \subset L(G_2) \subset L(G_1) \subset L(G_0)
$$

> [!important]
> Las gramáticas regulares son las más simples.
>
> Las gramáticas de tipo 0 son las más generales.

---

# 15. Resumen de este primer bloque

> [!summary]
> En este bloque hemos visto:
>
> - qué es una gramática;
> - qué son terminales y no terminales;
> - qué es una producción;
> - qué es una gramática regular;
> - qué es una gramática independiente del contexto;
> - cómo se define $L(G)$;
> - qué son derivaciones;
> - qué son árboles de análisis sintáctico;
> - qué significa que una gramática sea ambigua;
> - cómo se relacionan las clases de la jerarquía de Chomsky.

---

# 16. Ejercicios recomendados de la hoja

Para practicar esta primera parte del Tema 3, conviene hacer:

- Ejercicio 1: describir lenguajes generados por gramáticas.
- Ejercicio 2: pasar de gramática regular a DFA.
- Ejercicio 3: obtener gramáticas lineales por derecha e izquierda.
- Ejercicio 5: encontrar gramática regular equivalente a una CFG cuyo lenguaje es regular.
- Ejercicio 10: demostrar ambigüedad.
- Ejercicio 11: comprobar si unas cadenas son generadas por una CFG.