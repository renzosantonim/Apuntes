
## Enero 2023

### 1. Expresión regular y DFA mínimo (2 puntos)
Dada la expresión regular:

```text
r = (1|01)*(0|ε)
```

Obtenga un DFA con un número mínimo de estados que reconozca `L(r)`.

**Nota:** Explique los pasos que se siguen al pasar de la expresión regular al autómata finito minimizado. No dibujar directamente el autómata mínimo.

---
### 2. Gramática y regularidad (2 puntos)
Sea un lenguaje `L` sobre el alfabeto `Σ = {0, 1, 2}`, tal que:
### L = { 0$^n$ 1$^{n+m}$ 2$^m$ | n ≥ 0; m ≥ 0; (n + m) % 2 = 0 }

a) Definir una gramática `G`, con no más de 5 símbolos no terminales, que genere dicho lenguaje `L`. (1 punto)

b) ¿Es `L` un lenguaje regular? Justifique su respuesta. (1 punto)

---
### 3. Lenguajes recursivos (2 puntos)
Sea `L ⊂ Σ*` un lenguaje recursivo.

Considere el lenguaje:
### L' = { w ∈ Σ* | v ∈ L  ∧  w = v$^{-1}$ }

¿Es `L'` un lenguaje recursivo? Argumentar la respuesta.

---
### 4. Multiplicación de matrices Divide y Vencerás (2 puntos)
Dada la clase `matrix_t<T>`, con los siguientes métodos ya desarrollados:

- `matrix_t(const int m=0, const int n=0)`: constructor, m filas y n columnas.
    
- `int get_m(void)` y `int get_n(void)`: _getters_ del número de filas y columnas, respectivamente.
    
- `T& operator()(const int i, const int j)`: operador de indexación de la matriz en la fila i y la columna j.
    
- `matrix_t<T> submatrix(const int r_ini, const int r_end, const int c_ini, const int c_end)`: extrae una sub-matriz de la matriz invocante entre las filas `r_ini` y `r_end`, y las columnas `c_ini` y `c_end`.
    
- `matrix_t<T>& operator=(const matrix_t<T>& A)`: operador de asignación.
    
- `matrix_t<T> operator+(const matrix_t<T>& A, const matrix_t<T>& B)`: operador externo que devuelve la suma de dos matrices A y B.

Por otro lado, dadas dos matrices `A` y `B` cuadradas de tamaño `N × N`, donde `N = A.get_m()`, con un número de filas/columnas múltiplo de `2^N`, con `N > 0`, el algoritmo de multiplicación de matrices tipo Divide-y-Vencerás consiste en dividir `A` y `B` en cuatro submatrices de tamaño `N/2 × N/2`como se muestra en la siguiente figura:

```text
    [ a  b ]          [ e  f ]          [ ae + bg   af + bh ]
    [ c  d ]     *    [ g  h ]     =    [ ce + dg   cf + dh ]
		A                 B                       C
```

Donde:

- `A`, `B` y `C` son matrices cuadradas de tamaño `N × N`.
- `a`, `b`, `c` y `d` son submatrices de `A`, de tamaño `N/2 × N/2`.
- `e`, `f`, `g` y `h` son submatrices de `B`, de tamaño `N/2 × N/2`.
- Las filas y columnas se indexan desde 1.

Se pide:

a) Desarrollar un algoritmo recursivo (en pseudo-C++) de tipo Divide-y-Vencerás que implemente el operador de multiplicación `(*)`, con la cabecera:

```cpp
matrix_t<T> operator*(const matrix_t<T>& A, const matrix_t<T>& B)
```

(1.5 puntos)

b) Sabiendo que la suma de dos matrices tiene complejidad  Θ(N$^2$), calcular la tasa de crecimiento `T(N)` del algoritmo anterior y, usando el Teorema Maestro, la complejidad en notación Θ(·). ¿Es mejor este algoritmo recursivo que el clásico método de Θ(N$^3$)? (0.5 puntos)

---
### 5. Verdadero/Falso y test (2 puntos)
Contestar Verdadero (V) o Falso (F), o elegir la/s respuesta/s correcta/s para cada una de las siguientes preguntas.

Notas aclaratorias:

- Por cada respuesta correcta se sumará 0.2 puntos.
- Por cada respuesta incorrecta se restará 0.2 puntos.
- Las preguntas sin responder se considerarán incorrectas.
- La puntuación mínima de esta pregunta es de 0 puntos.

1. ∅$^0$ = {ε}.
2. Todo alfabeto es un lenguaje.
3. Si `L` cumple el lema del bombeo para lenguajes regulares, entonces `L` es regular.
4. El cierre de Kleene de un lenguaje independiente de contexto es siempre independiente de contexto.
5. La intersección de un lenguaje regular con un lenguaje independiente del contexto es siempre un lenguaje regular.
6. Si `L1` y `L2` son lenguajes recursivamente enumerables, entonces `L1 ∪ L2` también lo es.
7. Si `L` es un lenguaje independiente del contexto entonces es recursivo.
8. Θ(n$^5$ log n) < Θ(9n$^5$ log n$^7$).
9. `T(n) = 2T(n/4) + 1 = Θ(√n)`.
10. La complejidad del siguiente bloque de código es Θ(n$^2$ log n):

```cpp
int suma = 0;
for (int x = 1; x <= n; x++)
  for (int y = 1; y <= n; y *= 2)
    for (int z = 1; z <= y; z++)
      suma++;
```

---

## Enero 2024/2025

### 1. Expresión regular y DFA mínimo (2 puntos)
Dada la expresión regular:

```text
(a|b*)* ca * c
```

Utilice los algoritmos necesarios para obtener un DFA con un número mínimo de estados que reconozca el lenguaje representado por la expresión.

Explique los pasos que se siguen para pasar de la expresión regular al DFA minimizado. No exponga directamente el autómata minimizado.

---
### 2. Gramática ambigua, autómata y gramática regular (2 puntos)
Dada la siguiente gramática `G`:

```text
S → A | B
A → aaA | aa
B → aaaB | aaa
```

a) (0.4 puntos) Encuentre una cadena de `L(G)`, lo más corta posible, que demuestre que `G` es ambigua. 

b) (0.8 puntos) A partir del lenguaje que genera `G`, obtenga un autómata finito (determinista o no, pero sin transiciones vacías) que reconozca `L(G)`. 

c) (0.8 puntos) Obtenga, a partir del autómata anterior, una gramática regular `G'` equivalente a `G`.

---
### 3. Intersección de lenguajes independientes del contexto (2 puntos)
Considere la siguiente afirmación:

> La intersección de dos lenguajes independientes del contexto es siempre un lenguaje recursivo.

Indique si la afirmación es cierta o no y argumente su respuesta.

---
### 5. Verdadero/Falso y test (2 puntos)
Preguntas detectadas:

1. ∅* = {ε}.
2. La concatenación de un lenguaje regular con su complementario es siempre regular.
3. El lenguaje L = {0$^n$ 1$^m$ | m ≥ n}  es regular.
4. Dada una gramática `G`, si `G` no es regular, `L(G)` no será regular.
5. Si `L` es un lenguaje finito, no puede ser independiente del contexto.
6. Si `L` es independiente del contexto, entonces su complementario es recursivo.
7. Si `L` es recursivamente enumerable, entonces Σ* - L es recursivamente enumerable.
8. Θ(11n$^3$ log n$^{10}$) = Θ(8n$^3$ log n$^7$).
9. T(n) = 16T(n/4) + √n = Θ(n$^2$).
10. La complejidad del siguiente bloque de código es Θ(n^3):

```cpp
int suma = 0;
for (int i = 1; i <= n; i++)
  for (int j = 1; j <= n; j *= 2)
    for (int k = 1; k <= j; k++)
      suma++;
```

---

## Febrero 2022

### 1. Expresión regular y autómata finito (2 puntos)
Considere el lenguaje L = { 0$^n$ 1$^m$ | n + m es impar } sobre el alfabeto `Σ = {0, 1}`.

a) Especificar una expresión regular que represente a `L`. (1 punto)

b) Diseñar un autómata finito que reconozca `L`. (1 punto)

### 2. Lenguajes independientes del contexto y cierre (2 puntos) ==verificar==
Sea `P(x)` el prefijo de `x` de longitud 5 si |x| > 5, o `x` si |x| < 5.

Se define:

P$_5$(L) = { P$_5$(x) | x ∈ L }

¿Es el conjunto de los lenguajes independientes del contexto cerrado bajo la operación P$_5$? Justificar la respuesta.

### 3. Máquina de Turing (2 puntos)
Construir una máquina de Turing que reconozca el lenguaje:

```text
L = { w ∈ {0, 1}* | n0(w) = n1(w) }
```

Es decir, cadenas con el mismo número de ceros que de unos.

Antes de diseñar la máquina, explicar brevemente el modo de funcionamiento que se propone para la misma. Para cada transición o conjunto de transiciones de la máquina de Turing, describir lo que se pretende hacer con las transiciones en cuestión. Dibujar el diagrama de transiciones de la máquina.

### 4. Programación dinámica: coeficiente binomial (2 puntos)
Diseñe un algoritmo de Programación Dinámica, en pseudo-código o C++, que calcule el valor de un coeficiente binomial `C(n, k)`. Para ello, construya una tabla `C[0..n, 0..k]` tal que:

```text
C[i, j] = 1                         si j = 0
C[i, j] = 0                         si i = 0 y j ≥ 1
C[i, j] = C[i - 1, j - 1] + C[i - 1, j]   en otro caso
```

La solución estará en la celda `C[n, k]`.

Calcule el orden de complejidad del algoritmo diseñado. (0.5 puntos)

Muestre la tabla correspondiente al coeficiente binomial `C(7, 4)`. (0.5 puntos)

---

## Junio 2023

### 1. Expresión regular, autómata y gramática independiente del contexto (2 puntos)
Sea `L` el lenguaje formado por todas las cadenas binarias `w`, con `|w| % 4 = 0`, en las que cada bloque de cuatro símbolos contiene al menos dos ceros consecutivos. Los bloques comenzarán siempre en posiciones múltiplo de 4.

(a) Obtener una expresión regular que represente a `L`. (0.5 puntos)

(b) Obtener un autómata finito que reconozca `L`. (1 punto)

(c) ¿Existe una gramática independiente del contexto que genere el lenguaje `L`? En caso afirmativo, indique cuál sería. En caso contrario, justifique su respuesta. (0.5 puntos)

### 2. Lenguajes independientes del contexto y regularidad (2 puntos)
Sea `L` un lenguaje independiente del contexto pero no regular, y sea `L'` otro lenguaje tal que:

```text
(i)  L' ∩ L es infinito
(ii) L' ≠ L
```

Demuestre la verdad o falsedad de las siguientes afirmaciones:

1. `L'` no es regular.
2. Dado cualquier lenguaje `L` independiente del contexto pero no regular, siempre existe un lenguaje `L'` regular que cumple (i) y (ii).

### 3. Máquina de Turing (2 puntos)
Construir una máquina de Turing que, dada una cadena binaria de entrada, añada a la cadena un `0` entre cada pareja de `1`s.

Antes de diseñar la máquina, explicar brevemente el modo de funcionamiento que se plantea para la misma. Para cada transición o conjunto de transiciones de la máquina de Turing, describir lo que se pretende hacer con las transiciones en cuestión. Dibujar el diagrama de transiciones de la máquina.

### 4. Algoritmo de Strassen (2 puntos)

Dada la clase `matrix_t<T>`, con los siguientes métodos ya desarrollados:
- `matrix_t(const int m=0, const int n=0)`: constructor, m filas y n columnas.
    
- `int get_m(void)` y `int get_n(void)`: _getters_ del número de filas y columnas, respectivamente.
    
- `T& operator()(const int i, const int j)`: operador de indexación de la matriz en la fila i y la columna j.
    
- `matrix_t<T> submatrix(const int r_ini, const int r_end, const int c_ini, const int c_end)`: extrae una sub-matriz de la matriz invocante entre las filas `r_ini` y `r_end`, y las columnas `c_ini` y `c_end`.
    
- `matrix_t<T>& operator=(const matrix_t<T>& A)`: operador de asignación.
    
- `matrix_t<T> operator+(const matrix_t<T>& A, const matrix_t<T>& B)`: operador externo que devuelve la suma de dos matrices A y B.
    
- `matrix_t<T> operator-(const matrix_t<T>& A, const matrix_t<T>& B)`: operador externo que devuelve la resta (diferencia) de dos matrices A y B.

Por otro lado, dadas dos matrices `A` y `B` cuadradas de tamaño `N × N`, donde `N = A.get_m()`, con un número de filas/columnas múltiplo de 2$^N$, con `N > 0`, el algoritmo de Strassen para la multiplicación de matrices tipo Divide-y-Vencerás consiste en dividir `A` y `B` en cuatro submatrices de tamaño `N/2 × N/2`, como se muestra en la siguiente figura:

```text
[ a  b ]      [ e  f ]     [ p5 + p4 - p2 + p6          p1 + p2       ]
[ c  d ]   *  [ g  h ]  =  [     p3 + p4            p1 + p5 - p3 - p7 ]
   A              B                             C
```

_Donde:_
- `A, B y C` son matrices cuadradas de tamaño N×N
    
- `a, b, c y d` son sub-matrices de A, de tamaño `N/2 × N/2`
    
- `e, f, g y h` son sub-matrices de B, de tamaño `N/2 × N/2`
    
- p1 = a ∗ (f − h)
    
- p2 = (a + b) ∗ h
    
- p3 = (c + d) ∗ e
    
- p4 = d ∗ (g − e)
    
- p5 = (a + d) ∗ (e + h)
    
- p6 = (b − d) ∗ (g + h)
    
- p7 = (a − c) ∗ (e + f)
    
- Las filas y columnas se indexan desde 1

Se pide:

a) Desarrollar el algoritmo de Strassen recursivo (en pseudo-C++) de tipo Divide-y-Vencerás, que implemente la multiplicación de matrices con la cabecera:

```cpp
matrix_t<T> Strassen(const matrix_t<T>& A, const matrix_t<T>& B)
```

(1.5 puntos)

b) Calcular la tasa de crecimiento `T(N)` del algoritmo del apartado anterior y, usando el Teorema Maestro, la complejidad en notación Θ(·). ¿Es mejor este algoritmo recursivo que el clásico método de Θ(N$^3$)? (0.5 puntos)

### 5. Verdadero/Falso y test (2 puntos)
Preguntas detectadas:

1. ∅$^0$ = ∅.
2. Si `L` no cumple el lema del bombeo para lenguajes regulares, entonces `L` no es regular.
3. Los lenguajes regulares son cerrados respecto a la intersección.
4. Si L$_1$ y L$_2$ son lenguajes independientes del contexto => L$_1$L$_2$ también lo es.
5. El resultado de concatenar un lenguaje regular con uno independiente del contexto es siempre independiente del contexto.
6. Si `L` es recursivamente enumerable, entonces  Σ* - L es recursivamente enumerable.
7. Si `L` es un lenguaje independiente del contexto, entonces es recursivamente enumerable.
8. 5n + 8n$^2$ + 100n$^3$ = O(n$^4$).
9. T(n) = 16T(n/4) + n = Θ(n).
10. La complejidad del siguiente bloque de código es Θ(n$^3$):

```cpp
int suma = 0;
for (int a = 1; a <= n; a++)
  for (int b = 1; b <= n; b++)
    for (int c = 1; c <= b; c++)
      suma++;
```
