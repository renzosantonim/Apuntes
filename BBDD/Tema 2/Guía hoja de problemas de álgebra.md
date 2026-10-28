# Base de Datos - Guía de la hoja de problemas de álgebra

Esta guía analiza `prob_Algebra.pdf`, comprueba si los apuntes contienen las herramientas necesarias y desarrolla por completo el **problema 1**. No sustituye a la hoja: su objetivo es enseñarte el método para que puedas seguir la resolución en clase.

## 1. Diagnóstico de preparación

La hoja contiene cuatro problemas y aumenta progresivamente de dificultad.

| Problema | Qué exige | Dónde se prepara |
|---|---|---|
| **1. Evaluar expresiones** | Unión, diferencia, producto, yunción natural, selección, proyección y yunción con condición. | Apuntes de álgebra, secciones 3.2-3.9; solución completa en esta guía. |
| **2. Empresa** | Interpretar claves, unir tres relaciones, comparar una tabla consigo misma y renombrar copias. | Modelo relacional 2.5-2.6; álgebra 3.17-3.18. |
| **3. Simpatías** | Intersección, diferencia, renombrado y traducción de «ninguno» y «solo». | Álgebra 3.6-3.8 y 3.17-3.18. |
| **4. Videoclubs** | Consultas anidadas, «alguno», «solamente» y «todas»; diferencia y cociente. | Álgebra 3.10 y 3.18. |

### Veredicto

> [!important]
> Con las ampliaciones realizadas, los apuntes contienen todos los conceptos necesarios para abordar la hoja.
>
> Antes de la revisión faltaba explicar formalmente el renombrado y apenas se desarrollaban los patrones «solo», «ninguno» y «todos». Esos huecos ya están cubiertos en las secciones 3.17 y 3.18 del tema de álgebra.

### Qué debes dominar antes del lunes

1. Distinguir selección de proyección.
2. Comprobar compatibilidad antes de unión, diferencia o intersección.
3. Ejecutar un producto cartesiano y luego filtrar.
4. Entender que la yunción natural compara atributos homónimos.
5. Renombrar dos copias de la misma relación.
6. Traducir «ninguno» mediante diferencia y «todos» mediante cociente o ausencia de contraejemplos.

---

# 2. Método para evaluar una expresión

Cuando te entreguen relaciones concretas y una expresión:

1. Empieza por los paréntesis más interiores.
2. Escribe el esquema de cada resultado intermedio.
3. Calcula las filas sin olvidar que una relación es un conjunto: no conserva duplicados.
4. En un producto, califica los atributos repetidos como `R.B` y `S.B`.
5. En una yunción natural, identifica primero todos los nombres comunes.
6. En una proyección, elimina filas que se vuelvan iguales.
7. Comprueba el tamaño esperado: un producto de `m` por `n` filas debe tener `m·n` filas.

---

# 3. Problema 1 resuelto paso a paso

Las relaciones son:

**R(A, B)**

| A | B |
|---|---|
| a | b |
| c | d |
| d | e |

**S(B, C)**

| B | C |
|---|---|
| b | c |
| b | d |
| e | a |

La hoja indica que los dominios de los atributos de la misma posición coinciden. Esto permite aplicar unión y diferencia **por posición**, aunque los encabezados de R y S no tengan los mismos nombres.

## 3.1 Apartado a - `R ∪ S`

La unión contiene todas las filas de ambos operandos y elimina duplicados.

No hay ninguna pareja repetida entre R y S:

| A | B |
|---|---|
| a | b |
| c | d |
| d | e |
| b | c |
| b | d |
| e | a |

> [!note]
> Se conservan como encabezados los atributos del primer operando. Los valores de `S.B` ocupan la primera posición y los de `S.C`, la segunda.

---

## 3.2 Apartado b - `R - S`

La diferencia conserva las filas de R que no aparecen en S, comparadas por posición.

- `(a,b)` no está en S.
- `(c,d)` no está en S.
- `(d,e)` no está en S.

Por tanto:

| A | B |
|---|---|
| a | b |
| c | d |
| d | e |

El resultado coincide con R.

---

## 3.3 Apartado c - `R × S`

R tiene 3 filas y S tiene 3, de modo que deben aparecer:

```text
3 · 3 = 9 filas
```

El atributo `B` aparece en ambas relaciones, así que lo calificamos:

| R.A | R.B | S.B | S.C |
|---|---|---|---|
| a | b | b | c |
| a | b | b | d |
| a | b | e | a |
| c | d | b | c |
| c | d | b | d |
| c | d | e | a |
| d | e | b | c |
| d | e | b | d |
| d | e | e | a |

> [!tip]
> Para no saltarte combinaciones, toma la primera fila de R y recorre S completa; después repite con cada fila de R.

---

## 3.4 Apartado d - `R * S`

`*` es la yunción natural. R y S comparten el atributo `B`, por lo que se combinan las filas donde:

```text
R.B = S.B
```

Comprobación:

- La fila `(a,b)` de R encuentra dos filas de S con `B=b`.
- La fila `(c,d)` no encuentra ninguna con `B=d`.
- La fila `(d,e)` encuentra una fila con `B=e`.

El atributo común se escribe una sola vez:

| A | B | C |
|---|---|---|
| a | b | c |
| a | b | d |
| d | e | a |

---

## 3.5 Apartado e - `P(A)(R)`

La proyección conserva únicamente la columna A:

| A |
|---|
| a |
| c |
| d |

No aparecen duplicados. Si dos filas de R hubieran tenido el mismo A, tras proyectar se conservaría una sola copia.

---

## 3.6 Apartado f - `S(A=C)(R × S)`

Ya calculamos las nueve filas del producto. Ahora conservamos aquellas donde `R.A = S.C`:

- `a = a` en la combinación de `(a,b)` con `(e,a)`.
- `c = c` en la combinación de `(c,d)` con `(b,c)`.
- `d = d` en la combinación de `(d,e)` con `(b,d)`.

Resultado:

| R.A | R.B | S.B | S.C |
|---|---|---|---|
| a | b | e | a |
| c | d | b | c |
| d | e | b | d |

> [!important]
> La condición no compara los dos atributos llamados B. Compara `R.A` con `S.C`, exactamente como indica el predicado.

---

## 3.7 Apartado g - `P(R.B, C)(R Y(S.B=b) S)`

La yunción `Y(F)` equivale a seleccionar el producto cartesiano con el predicado `F`.

Aquí el predicado solo exige:

```text
S.B = b
```

S tiene dos filas que cumplen la condición:

| S.B | C |
|---|---|
| b | c |
| b | d |

Cada una se combina con las tres filas de R. Después se proyectan `R.B` y `C`:

| R.B | C |
|---|---|
| b | c |
| b | d |
| d | c |
| d | d |
| e | c |
| e | d |

> [!warning]
> Esta no es una yunción por igualdad entre R y S. El predicado no contiene `R.B = S.B`; únicamente filtra las filas de S cuyo B vale `b`.

---

## 3.8 Apartado h - `P(A)((P(B)(S)) * R)`

Hay que trabajar desde dentro hacia fuera.

### Paso 1 - `P(B)(S)`

Proyectamos el atributo B de S y eliminamos el duplicado `b`:

| B |
|---|
| b |
| e |

### Paso 2 - `(P(B)(S)) * R`

La yunción natural usa el atributo común B. Conserva las filas de R cuyo B esté en `{b,e}`:

| B | A |
|---|---|
| b | a |
| e | d |

### Paso 3 - `P(A)`

| A |
|---|
| a |
| d |

> [!tip]
> Esta expresión equivale a preguntar qué valores de A de R tienen un valor B que aparece también en S.

---

# 4. Qué practicar después del problema 1

## 4.1 Para el problema 2

Repasa:

- qué informa una clave primaria y una clave ajena;
- yunción de `VIVE`, `TRABAJA` y `LOCALIZACIÓN`;
- dos copias renombradas de `TRABAJA` para «más de una compañía»;
- dos copias de `SUPERVISA` para comparar supervisores.

## 4.2 Para el problema 3

Construye primero relaciones auxiliares:

```text
MUTUO = HSIM ∩ MSIM
```

Después aplica yunciones con `MATRIMONIO` y diferencias respecto de los conjuntos de hombres o mujeres. Para «ninguna» y «solo», identifica primero los contraejemplos que deben excluirse.

> [!warning]
> Aunque `HSIM` y `MSIM` tienen el mismo esquema, sus significados se leen en sentidos opuestos. La intersección representa simpatía mutua porque una misma pareja aparece en ambos conjuntos.

## 4.3 Para el problema 4

Conviene crear relaciones de apoyo:

```text
DISPONIBLE_Y_GUSTA = GUSTA * VIDEOTECA
```

Después se relaciona con `SOCIO`. Las preguntas con «todas las películas de su gusto» requieren cociente o el patrón «no existe una película que le guste y falte en el videoclub».

---

# 5. Plan breve para llegar preparado a clase

1. Lee la hoja rápida de operadores del repaso global.
2. Rehaz el problema 1 sin mirar esta solución y comprueba las ocho tablas.
3. Estudia las secciones 3.17 y 3.18 del tema de álgebra.
4. Intenta los apartados 2b, 2c y 2e: selección/proyección, yunción y autorrenombrado.
5. Lee después el nuevo tema de cálculo relacional, porque es la teoría que enlaza con las consultas mediante lógica.

> [!summary]
> Si entiendes por qué el apartado 1g produce seis filas y por qué el 1h debe resolverse de dentro hacia fuera, ya tienes la mecánica básica. El salto siguiente consiste en traducir lenguaje natural a combinaciones de yunciones, diferencias, renombrados y cocientes.
