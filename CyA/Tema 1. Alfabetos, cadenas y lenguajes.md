```
Símbolos → Cadenas → Lenguajes
```
# 1. Alfabetos

## Definición

Un alfabeto Σ es un conjunto finito y no vacío de símbolos.

Ejemplos:

```
Σ = {0,1}
Σ = {a,b,c}
Σ = {♠, ♥, ♦, ♣}
```

---
## Ejemplo intuitivo

Piensa en el alfabeto español:

```
Σ = {a,b,c,d,...,z}
```

Las letras son símbolos.

Los símbolos por sí solos no tienen por qué significar nada.

Por ejemplo:

```
aqx
```

son simplemente símbolos.

---
## Muy importante

Un símbolo NO es un conjunto.

Por ejemplo:

```
a   →  símbolo{a}  →   conjunto que contiene el símbolo a
```

Son cosas completamente distintas.

Esto aparece directamente en la hoja de problemas.

---
# 2. Cadenas

## Definición

Una cadena es una secuencia finita de símbolos de un alfabeto.

Ejemplos sobre:

```
Σ = {0,1}
```

cadenas válidas:

```
0101111010101
```

---
## Longitud

La longitud de una cadena w se denota:

```
|w|
```

Ejemplos:

```
|0| = 1
|101| = 3
|010101| = 6
```

---
# 3. La cadena vacía ε

## Definición

La cadena vacía es la cadena que no contiene ningún símbolo.

Se representa por:

```
ε
```

y cumple:

```
|ε| = 0
```

---
## Ejemplo

Imagina una hoja de papel.

Escribir:

```
abc
```

produce una cadena de longitud 3.

No escribir nada produce:

```
ε
```

---
## Error clásico de examen

Mucha gente cree:

```
ε ∈ Σ
```

FALSO.

La cadena vacía no es un símbolo.

Por tanto:

```
ε ∉ Σ
```

---
# 4. Lenguajes

## Definición

Un lenguaje es un conjunto de cadenas.

Ejemplo:

```
L = {a, aa, aaa}
```

Es un lenguaje.

---
## Intuición

Si:

```
Σ = {a,b}
```

entonces:

```
ab
```

es una cadena.

Mientras que:

```
{ab, aa, b}
```

es un lenguaje.

---
## Jerarquía completa

Debes visualizar:

```
Símbolo → Cadena → Lenguaje
```

Ejemplo:

```
a           símbolo 
aba         cadena
{a,aba}     lenguaje
```

---
# 5. Lenguaje vacío ∅

## Definición

Es el lenguaje que no contiene ninguna cadena.

```
∅
```

---
## Diferencia crítica

### Lenguaje vacío

```
∅
```

contiene:

```
nada
```

---
### Lenguaje con la cadena vacía

```
{ε}
```

contiene:

```
la cadena ε
```

---
## Resultado fundamental

```
∅ ≠ {ε}
```

Este resultado aparece constantemente en ejercicios y exámenes.

---
# 6. Lenguaje universal Σ*

## Definición

Σ* es el conjunto de TODAS las cadenas que pueden construirse con símbolos de Σ.

---

Ejemplo:

```
Σ = {a}
```

Entonces:

```
Σ* ={ε,a,aa,aaa,aaaa,...}
```

---

Ejemplo:

```
Σ = {0,1}
```

Entonces:

```
Σ* ={ε,0,1,00,01,10,11,000,...}
```

---
## Idea clave

Todo lenguaje sobre Σ cumple:

```
L ⊆ Σ*
```

---
# Resumen de la Parte 1

Debes saber distinguir instantáneamente:

| Expresión | Significado                |
| --------- | -------------------------- |
| a         | símbolo                    |
| aa        | cadena                     |
| ε         | cadena vacía               |
| {a}       | lenguaje                   |
| {aa}      | lenguaje                   |
| ∅         | lenguaje vacío             |
| {ε}       | lenguaje con una cadena    |
| Σ         | alfabeto                   |
| Σ*        | todas las cadenas posibles |
