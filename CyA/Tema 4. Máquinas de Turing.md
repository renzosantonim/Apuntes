# Tema 4 — Máquinas de Turing

## 0. Idea general del tema

Hasta ahora hemos estudiado modelos de computación con potencia limitada:

| Tipo de lenguaje | Modelo asociado |
|---|---|
| Lenguajes regulares | Autómatas finitos |
| Lenguajes independientes del contexto | Autómatas de pila |
| Lenguajes más generales | Máquinas de Turing |

Los autómatas finitos no tienen memoria auxiliar.

Los autómatas de pila tienen una pila, pero siguen sin ser un modelo general de computación.

Por ejemplo, el lenguaje:

$$
L = \{a^n b^n c^n \mid n \geq 0\}
$$

no es independiente del contexto, así que no puede ser reconocido por un autómata de pila.

Por eso necesitamos un modelo más potente:

$$
\textbf{la Máquina de Turing}
$$

> [!important]
> La Máquina de Turing es el modelo matemático básico de lo que entendemos por algoritmo.

---

# 1. ¿Qué es una Máquina de Turing?

Una Máquina de Turing, o MT, es un modelo abstracto de computación formado por:

- una cinta infinita;
- una cabeza de lectura/escritura;
- un conjunto finito de estados;
- una función de transición.

La cinta actúa como memoria.

La cabeza puede:

- leer el símbolo actual;
- escribir un nuevo símbolo;
- moverse a la izquierda o a la derecha.

---

# 2. Definición formal

> [!definition]
> Una Máquina de Turing es una tupla:
>
> $$
> M = (Q, \Sigma, \Gamma, q_0, \blank, F, \delta)
> $$
>
> donde:
>
> - $Q$ es el conjunto finito de estados.
> - $\Sigma$ es el alfabeto de entrada.
> - $\Gamma$ es el alfabeto de cinta.
> - $q_0 \in Q$ es el estado inicial.
> - $\blank \in \Gamma$ es el símbolo blanco.
> - $F \subseteq Q$ es el conjunto de estados de aceptación.
> - $\delta$ es la función de transición.

La función de transición tiene la forma:

$$
\delta : Q \times \Gamma \to Q \times \Gamma \times \{L,R\}
$$

Es decir:

$$
\delta(q,a) = (p,c,X)
$$

significa:

> Si la máquina está en el estado $q$ y lee el símbolo $a$, entonces:
>
> 1. pasa al estado $p$;
> 2. escribe el símbolo $c$;
> 3. mueve la cabeza en dirección $X$, donde $X \in \{L,R\}$.

---

# 3. Componentes de una MT

## 3.1 Estados

El conjunto $Q$ contiene los estados internos de la máquina.

Ejemplo:

$$
Q = \{q_1, q_2, q_3\}
$$

Uno de ellos es el estado inicial:

$$
q_0
$$

Algunos pueden ser estados finales o de aceptación:

$$
F \subseteq Q
$$

---

## 3.2 Alfabeto de entrada

El alfabeto de entrada se denota por:

$$
\Sigma
$$

Contiene los símbolos que pueden aparecer inicialmente en la cadena de entrada.

Ejemplo:

$$
\Sigma = \{a,b\}
$$

---

## 3.3 Alfabeto de cinta

El alfabeto de cinta se denota por:

$$
\Gamma
$$

Contiene:

- los símbolos de entrada;
- símbolos auxiliares;
- el símbolo blanco.

Normalmente:

$$
\Sigma \subseteq \Gamma
$$

pero:

$$
\blank \notin \Sigma
$$

Ejemplo:

$$
\Sigma = \{a,b\}
$$

$$
\Gamma = \{a,b,c,d,\blank\}
$$

Aquí $c$ y $d$ podrían usarse como marcas auxiliares.

---

## 3.4 Símbolo blanco

El símbolo blanco se suele representar como:

$$
\blank
$$

Indica que una celda está vacía.

> [!warning]
> El blanco pertenece al alfabeto de cinta, pero no al alfabeto de entrada:
>
> $$
> \blank \in \Gamma
> $$
>
> $$
> \blank \notin \Sigma
> $$

---

# 4. Funcionamiento básico

En cada paso, la MT hace exactamente tres cosas:

1. Lee el símbolo bajo la cabeza.
2. Según el estado actual y el símbolo leído, aplica una transición.
3. Escribe un símbolo, cambia de estado y mueve la cabeza.

Una transición:

$$
\delta(q_1,a) = (q_2,b,R)
$$

se lee así:

> Si estoy en $q_1$ y leo $a$, escribo $b$, paso a $q_2$ y me muevo a la derecha.

---

# 5. Ejemplo sencillo

Consideremos la MT:

$$
Q = \{q_1,q_2\}
$$

$$
\Sigma = \{a,b\}
$$

$$
\Gamma = \{a,b,\blank\}
$$

$$
F = \{q_2\}
$$

$$
q_0 = q_1
$$

con transiciones:

$$
\delta(q_1,a) = (q_1,a,R)
$$

$$
\delta(q_1,b) = (q_1,a,R)
$$

$$
\delta(q_1,\blank) = (q_2,\blank,L)
$$

## ¿Qué hace esta máquina?

Recorre la cadena de izquierda a derecha.

- Si lee `a`, la deja igual.
- Si lee `b`, la cambia por `a`.
- Cuando encuentra un blanco, se mueve una posición a la izquierda y acepta.

Por tanto, transforma cualquier cadena de $\{a,b\}^*$ en una cadena formada solo por aes.

Ejemplo:

$$
abba \mapsto aaaa
$$

---

# 6. Descripciones instantáneas

Una configuración de una MT viene determinada por tres cosas:

1. el estado actual;
2. el contenido de la cinta;
3. la posición de la cabeza.

Se pueden representar de dos formas.

---

## 6.1 Notación con estado separado

$$
(q_i, w_1aw_2)
$$

donde:

- $q_i$ es el estado actual;
- $w_1$ es lo que hay a la izquierda de la cabeza;
- $a$ es el símbolo leído por la cabeza;
- $w_2$ es lo que hay a la derecha.

---

## 6.2 Notación insertando el estado en la cinta

También se puede escribir:

$$
w_1 q_i a w_2
$$

El estado se coloca justo antes del símbolo que está leyendo la cabeza.

Por ejemplo:

$$
aaq_1ba
$$

significa que:

- a la izquierda de la cabeza está `aa`;
- la máquina está en $q_1$;
- la cabeza lee `b`;
- a la derecha está `a`.

---

# 7. Paso de cómputo

Usamos el símbolo:

$$
\vdash
$$

para representar un paso de cómputo.

Por ejemplo:

$$
q_1abba \vdash aq_1bba
$$

Significa que la máquina ha pasado de una configuración a otra en un paso.

También se usa:

| Notación | Significado |
|---|---|
| $\vdash$ | un paso |
| $\vdash^*$ | cero o más pasos |
| $\vdash^+$ | uno o más pasos |

---

# 8. Lenguaje aceptado por una MT

> [!definition]
> El lenguaje aceptado por una MT $M$ se denota:
>
> $$
> L(M)
> $$
>
> y está formado por todas las cadenas que hacen que $M$ alcance un estado de aceptación.

Formalmente:

$$
L(M) =
\{w \in \Sigma^* \mid q_0w \vdash^* w_1 p w_2,\ p \in F\}
$$

Es decir, una cadena $w$ es aceptada si, al ejecutar la MT con entrada $w$, la máquina llega a algún estado final.

---

# 9. Parada de una Máquina de Turing

Una MT se para cuando no puede aplicar ninguna transición.

Esto ocurre si:

$$
\delta(q,a)
$$

no está definida para el estado actual $q$ y el símbolo leído $a$.

Una máquina puede parar de dos formas:

## 9.1 Parada aceptando

La máquina se detiene en un estado final:

$$
q \in F
$$

Entonces la cadena se acepta.

---

## 9.2 Parada rechazando

La máquina se detiene en un estado no final:

$$
q \notin F
$$

Entonces la cadena no se acepta.

---

# 10. Rechazo en Máquinas de Turing

A diferencia de los DFA, una MT puede no aceptar una cadena de dos formas distintas:

1. parando en un estado no final;
2. entrando en un bucle infinito.

> [!warning]
> En una MT, que una cadena no sea aceptada no significa necesariamente que la máquina pare y diga "no".
>
> Puede ocurrir que la máquina nunca pare.

Esto será clave para distinguir entre:

- lenguajes recursivos;
- lenguajes recursivamente enumerables.

---

# 11. Máquina que nunca para

Una MT puede entrar en un bucle infinito.

Ejemplo intuitivo:

- en $q_1$ se mueve a la derecha;
- en $q_2$ se mueve a la izquierda;
- vuelve a la misma configuración;
- repite indefinidamente.

Esto se representa como:

$$
(q,w) \vdash^* \infty
$$

---

# 12. Diferencias entre MT y autómatas finitos

| Autómata finito | Máquina de Turing |
|---|---|
| Solo lee la entrada | Lee y escribe |
| Se mueve solo hacia la derecha | Puede moverse a izquierda y derecha |
| Entrada finita | Cinta infinita |
| No modifica la entrada | Puede modificar la cinta |
| Siempre consume la entrada | Puede aceptar antes, rechazar o no parar |

> [!important]
> La gran diferencia es que la MT tiene memoria modificable e ilimitada.

---

# 13. Ejemplo: MT para $a^*$

Queremos una MT tal que:

$$
L(M) = L(a^*)
$$

sobre:

$$
\Sigma = \{a,b\}
$$

Es decir, acepta exactamente:

$$
\varepsilon, a, aa, aaa, \dots
$$

y rechaza cualquier cadena que contenga alguna `b`.

## Idea

La máquina recorre la cadena:

- si ve `a`, sigue avanzando;
- si ve blanco, acepta;
- si ve `b`, se queda sin transición o pasa a un estado de rechazo.

---

## MT por parada en estado no final

Definimos:

$$
Q = \{q_1,q_2\}
$$

$$
F = \{q_2\}
$$

$$
q_0 = q_1
$$

Transiciones:

$$
\delta(q_1,a) = (q_1,a,R)
$$

$$
\delta(q_1,\blank) = (q_2,\blank,R)
$$

No definimos transición para:

$$
\delta(q_1,b)
$$

Entonces:

- si la cadena contiene solo `a`, llega al blanco y acepta;
- si aparece una `b`, la máquina se para en $q_1$, que no es final.

---

# 14. Ejemplo importante: MT para $\{a^n b^n \mid n \geq 1\}$

Queremos reconocer:

$$
L = \{a^n b^n \mid n \geq 1\}
$$

Ejemplos aceptados:

$$
ab,\ aabb,\ aaabbb
$$

Ejemplos rechazados:

$$
a,\ b,\ abb,\ aab,\ ba,\ aba
$$

---

## 14.1 Idea de la máquina

La estrategia es marcar parejas.

1. Buscar la primera `a` sin marcar.
2. Cambiarla por `c`.
3. Buscar hacia la derecha la primera `b` sin marcar.
4. Cambiarla por `d`.
5. Volver hacia la izquierda hasta la última `c`.
6. Repetir.
7. Cuando no queden `a`, comprobar que todas las `b` han sido marcadas como `d`.

Usamos:

- `c` para marcar aes ya usadas;
- `d` para marcar bes ya usadas.

---

## 14.2 Transiciones principales

Cambiar la primera `a` por `c`:

$$
\delta(q_1,a) = (q_2,c,R)
$$

Buscar una `b` sin marcar:

$$
\delta(q_2,a) = (q_2,a,R)
$$

$$
\delta(q_2,d) = (q_2,d,R)
$$

$$
\delta(q_2,b) = (q_3,d,L)
$$

Volver hacia la izquierda:

$$
\delta(q_3,d) = (q_3,d,L)
$$

$$
\delta(q_3,a) = (q_3,a,L)
$$

$$
\delta(q_3,c) = (q_1,c,R)
$$

Cuando ya no quedan aes, comprobar que solo quedan des:

$$
\delta(q_1,d) = (q_4,d,R)
$$

$$
\delta(q_4,d) = (q_4,d,R)
$$

$$
\delta(q_4,\blank) = (q_5,\blank,L)
$$

Estado final:

$$
F = \{q_5\}
$$

---

# 15. Transformación de cadenas

Una MT no solo sirve para aceptar o rechazar lenguajes.

También puede transformar una cadena de entrada en una cadena de salida.

Por ejemplo, una MT puede complementar cadenas de:

$$
\{a,b\}^*
$$

cambiando:

$$
a \leftrightarrow b
$$

Ejemplo:

$$
aabba \mapsto bbaab
$$

---

# 16. Función Turing-computable

> [!definition]
> Una función de cadena es una función:
>
> $$
> f:\Sigma^* \to \Sigma^*
> $$

> [!definition]
> Una función de cadena es Turing-computable si existe una MT que, para cada entrada $w$, termina dejando en la cinta $f(w)$.

Formalmente, si:

$$
f(w)=u
$$

entonces la máquina debe cumplir:

$$
q_0w \vdash^* q_f u
$$

para algún estado final $q_f$.

---

# 17. Resumen del bloque

> [!summary]
> En este bloque hemos visto:
>
> - qué es una Máquina de Turing;
> - su definición formal;
> - cómo funciona una transición;
> - qué es una configuración o descripción instantánea;
> - qué significa aceptar una cadena;
> - qué significa que una MT pare;
> - la diferencia entre rechazar parando y no parar;
> - cómo diseñar MT sencillas;
> - cómo usar marcas auxiliares en la cinta;
> - cómo una MT puede transformar cadenas.

---

# 18. Ejercicios recomendados de la hoja

Para practicar esta primera parte:

- Ejercicio 5: MT para $L = \{a^n b^n \mid n \geq 0\}$.
- Ejercicio 7: MT para $L = \{a^n b^{2n} \mid n \geq 0\}$.
- Ejercicio 8: MT para palíndromos.
- Ejercicio 10: MT para cadenas de longitud par.
- Ejercicio 14: MT que multiplica por dos un número binario.