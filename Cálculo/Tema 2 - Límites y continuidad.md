## 1. Idea de límite

El límite de una función describe a qué valor se acerca $f(x)$ cuando $x$ se acerca a un punto $a$.

Se escribe:

$$
\lim_{x \to a} f(x)=L
$$

y significa que, cuando $x$ se acerca a $a$, los valores de $f(x)$ se acercan a $L$.

Importante:

- No importa necesariamente cuánto vale $f(a)$.
- Importa qué ocurre cerca de $a$.
- Una función puede tener límite en $a$ aunque no esté definida en $a$.

---

## 2. Límites laterales

En funciones a trozos, casi siempre hay que estudiar límites laterales.

El límite por la izquierda es:

$$
\lim_{x \to a^-} f(x)
$$

El límite por la derecha es:

$$
\lim_{x \to a^+} f(x)
$$

Para que exista el límite global:

$$
\lim_{x \to a} f(x)
$$

debe cumplirse:

$$
\lim_{x \to a^-} f(x)=\lim_{x \to a^+} f(x)
$$

Si los límites laterales son distintos, el límite no existe.

---

## 3. Ejemplo de límites laterales

Sea:

$$
f(x)=
\begin{cases}
x+1, & x<2 \\
x^2, & x\geq 2
\end{cases}
$$

Queremos estudiar:

$$
\lim_{x \to 2} f(x)
$$

Por la izquierda usamos la expresión $x+1$:

$$
\lim_{x \to 2^-} f(x)=\lim_{x \to 2^-}(x+1)=3
$$

Por la derecha usamos la expresión $x^2$:

$$
\lim_{x \to 2^+} f(x)=\lim_{x \to 2^+}x^2=4
$$

Como:

$$
3 \neq 4
$$

entonces:

$$
\lim_{x \to 2} f(x) \text{ no existe}
$$

---

# 4. Continuidad

Una función $f$ es continua en $x=a$ si se cumplen tres condiciones:

1. Existe $f(a)$.
2. Existe el límite:

$$
\lim_{x \to a} f(x)
$$

3. Se cumple:

$$
\lim_{x \to a} f(x)=f(a)
$$

En resumen:

$$
f \text{ continua en } a
\iff
\lim_{x \to a} f(x)=f(a)
$$

---

## 5. Método para estudiar continuidad en funciones a trozos

En una función a trozos, los únicos puntos problemáticos suelen ser:

- los puntos donde cambia la definición;
- los puntos donde hay denominadores que pueden anularse;
- los puntos donde aparece un logaritmo;
- los puntos donde aparece una raíz par;
- los puntos donde hay expresiones raras como $e^{1/x}$.

Método:

1. Identificar los puntos conflictivos.
2. Estudiar continuidad en cada intervalo.
3. En cada punto conflictivo, calcular:
   - límite por la izquierda;
   - límite por la derecha;
   - valor de la función.
4. Comparar.

---

## 6. Ejemplo de continuidad en función a trozos

Sea:

$$
f(x)=
\begin{cases}
x+1, & x<1 \\
2x, & x\geq 1
\end{cases}
$$

Estudiamos la continuidad en $x=1$.

Límite por la izquierda:

$$
\lim_{x \to 1^-} f(x)=\lim_{x \to 1^-}(x+1)=2
$$

Límite por la derecha:

$$
\lim_{x \to 1^+} f(x)=\lim_{x \to 1^+}2x=2
$$

Valor de la función:

Como en $x=1$ se usa el segundo trozo:

$$
f(1)=2 \cdot 1=2
$$

Como:

$$
\lim_{x \to 1^-} f(x)
=
\lim_{x \to 1^+} f(x)
=
f(1)
=
2
$$

la función es continua en $x=1$.

---

# 7. Discontinuidades típicas

## Discontinuidad evitable

Ocurre cuando existe el límite, pero:

- la función no está definida en el punto;
- o el valor de la función no coincide con el límite.

Ejemplo:

$$
f(x)=\frac{x^2-1}{x-1}
$$

En $x=1$ no está definida, pero:

$$
\frac{x^2-1}{x-1}
=
\frac{(x-1)(x+1)}{x-1}
=
x+1
$$

para $x \neq 1$.

Entonces:

$$
\lim_{x \to 1} f(x)=2
$$

La discontinuidad es evitable.

---

## Discontinuidad de salto

Ocurre cuando los límites laterales existen pero son distintos.

Ejemplo:

$$
f(x)=
\begin{cases}
1, & x<0 \\
2, & x\geq 0
\end{cases}
$$

Entonces:

$$
\lim_{x \to 0^-}f(x)=1
$$

$$
\lim_{x \to 0^+}f(x)=2
$$

Como son distintos, hay salto.

---

## Discontinuidad infinita

Ocurre cuando algún límite lateral tiende a infinito.

Ejemplo:

$$
f(x)=\frac{1}{x}
$$

En $x=0$:

$$
\lim_{x \to 0^+}\frac{1}{x}=+\infty
$$

$$
\lim_{x \to 0^-}\frac{1}{x}=-\infty
$$

---

# 8. Indeterminaciones

Las indeterminaciones más comunes son:

$$
\frac{0}{0}
$$

$$
\frac{\infty}{\infty}
$$

$$
0 \cdot \infty
$$

$$
\infty-\infty
$$

$$
1^\infty
$$

$$
0^0
$$

$$
\infty^0
$$

Cuando aparece una indeterminación, no se puede sustituir directamente. Hay que transformar la expresión.

---

## 9. Indeterminación $\frac{0}{0}$

Suele resolverse con:

- factorización;
- simplificación;
- racionalización;
- equivalencias;
- L'Hôpital, si está permitido.

Ejemplo:

$$
\lim_{x \to 1} \frac{x^2-1}{x-1}
$$

Sustituyendo:

$$
\frac{1^2-1}{1-1}=\frac{0}{0}
$$

Factorizamos:

$$
x^2-1=(x-1)(x+1)
$$

Entonces:

$$
\lim_{x \to 1} \frac{(x-1)(x+1)}{x-1}
$$

Simplificamos:

$$
\lim_{x \to 1} (x+1)=2
$$

---

## 10. Indeterminación $\frac{\infty}{\infty}$

En cocientes de polinomios, manda el grado mayor.

Ejemplo:

$$
\lim_{x \to +\infty}\frac{3x^2+1}{x^2-5x}
$$

Dividimos entre $x^2$:

$$
\lim_{x \to +\infty}\frac{3+\frac{1}{x^2}}{1-\frac{5}{x}}
$$

Como:

$$
\frac{1}{x^2} \to 0
$$

y:

$$
\frac{5}{x} \to 0
$$

queda:

$$
\frac{3}{1}=3
$$

---

## 11. Indeterminación $\infty-\infty$

Suele aparecer con raíces o fracciones.

Métodos típicos:

- sacar factor común;
- racionalizar;
- reducir a una sola fracción.

Ejemplo:

$$
\lim_{x \to +\infty} \left(\sqrt{x^2+x}-x\right)
$$

Es una indeterminación:

$$
\infty-\infty
$$

Racionalizamos:

$$
\sqrt{x^2+x}-x
\cdot
\frac{\sqrt{x^2+x}+x}{\sqrt{x^2+x}+x}
$$

Entonces:

$$
\frac{x^2+x-x^2}{\sqrt{x^2+x}+x}
$$

$$
\frac{x}{\sqrt{x^2+x}+x}
$$

Sacamos $x$ de la raíz:

$$
\frac{x}{x\sqrt{1+\frac{1}{x}}+x}
$$

$$
\frac{x}{x\left(\sqrt{1+\frac{1}{x}}+1\right)}
$$

Simplificamos:

$$
\frac{1}{\sqrt{1+\frac{1}{x}}+1}
$$

Al tomar límite:

$$
\frac{1}{1+1}=\frac{1}{2}
$$

---

# 12. Límites con exponenciales

Hay que recordar estos comportamientos:

$$
e^x \to +\infty \quad \text{cuando } x \to +\infty
$$

$$
e^x \to 0 \quad \text{cuando } x \to -\infty
$$

También:

$$
e^{-x} \to 0 \quad \text{cuando } x \to +\infty
$$

$$
e^{-x} \to +\infty \quad \text{cuando } x \to -\infty
$$

---

## 13. Límites con $e^{1/x}$

Este tipo aparece mucho en funciones a trozos.

Cuando:

$$
x \to 0^+
$$

entonces:

$$
\frac{1}{x} \to +\infty
$$

por tanto:

$$
e^{1/x} \to +\infty
$$

Cuando:

$$
x \to 0^-
$$

entonces:

$$
\frac{1}{x} \to -\infty
$$

por tanto:

$$
e^{1/x} \to 0
$$

Resumen:

| Límite | Resultado |
|---|---:|
| $x \to 0^+$ | $e^{1/x} \to +\infty$ |
| $x \to 0^-$ | $e^{1/x} \to 0$ |
| $x \to +\infty$ | $e^{1/x} \to 1$ |
| $x \to -\infty$ | $e^{1/x} \to 1$ |

---

## 14. Ejemplo con $e^{1/x}$

Calcular:

$$
\lim_{x \to 0^-} \frac{1-e^{1/x}}{1+e^{1/x}}
$$

Como:

$$
x \to 0^- \Rightarrow \frac{1}{x}\to -\infty
$$

entonces:

$$
e^{1/x}\to 0
$$

Por tanto:

$$
\lim_{x \to 0^-} \frac{1-e^{1/x}}{1+e^{1/x}}
=
\frac{1-0}{1+0}
=
1
$$

---

# 15. Límites con logaritmos

El logaritmo natural $\ln(x)$ solo está definido para:

$$
x>0
$$

Comportamientos importantes:

$$
\ln(x) \to -\infty \quad \text{cuando } x \to 0^+
$$

$$
\ln(x) \to +\infty \quad \text{cuando } x \to +\infty
$$

También:

$$
\ln(1)=0
$$

---

## 16. Comparación de crecimiento

Cuando $x \to +\infty$, las funciones crecen a distinta velocidad.

De menor a mayor crecimiento:

$$
\ln(x) \ll x^a \ll e^x
$$

para $a>0$.

Es decir:

- el logaritmo crece muy lento;
- las potencias crecen más rápido que el logaritmo;
- la exponencial crece más rápido que cualquier potencia.

Ejemplos:

$$
\lim_{x \to +\infty}\frac{\ln x}{x}=0
$$

$$
\lim_{x \to +\infty}\frac{x^2}{e^x}=0
$$

$$
\lim_{x \to +\infty}\frac{e^x}{x^2}=+\infty
$$

---

# 17. Límites tipo $1^\infty$

Aparecen expresiones del tipo:

$$
\left(g(x)\right)^{h(x)}
$$

donde:

$$
g(x)\to 1
$$

y:

$$
h(x)\to \infty
$$

Entonces tenemos una indeterminación:

$$
1^\infty
$$

Método:

Si:

$$
L=\lim_{x\to a} \left(g(x)\right)^{h(x)}
$$

tomamos logaritmos:

$$
\ln L = \lim_{x\to a} h(x)\ln(g(x))
$$

Después calculamos ese límite y finalmente:

$$
L=e^{\ln L}
$$

---

## 18. Límite fundamental

Un límite muy usado es:

$$
\lim_{x \to \infty}\left(1+\frac{a}{x}\right)^x=e^a
$$

También:

$$
\lim_{x \to 0}(1+x)^{1/x}=e
$$

---

## 19. Ejemplo tipo $1^\infty$

Calcular:

$$
\lim_{x \to +\infty}\left(\frac{x^2+x}{x^2+2}\right)^{3x-1}
$$

Primero miramos la base:

$$
\frac{x^2+x}{x^2+2}
\to
\frac{1}{1}=1
$$

El exponente:

$$
3x-1 \to +\infty
$$

Por tanto es:

$$
1^\infty
$$

Sea:

$$
L=
\lim_{x \to +\infty}\left(\frac{x^2+x}{x^2+2}\right)^{3x-1}
$$

Tomamos logaritmos:

$$
\ln L =
\lim_{x \to +\infty}
(3x-1)\ln\left(\frac{x^2+x}{x^2+2}\right)
$$

Observamos que:

$$
\frac{x^2+x}{x^2+2}
=
1+\frac{x-2}{x^2+2}
$$

Para $x$ grande:

$$
\frac{x-2}{x^2+2}\sim \frac{1}{x}
$$

Usando que:

$$
\ln(1+u)\sim u
$$

cuando $u \to 0$, queda:

$$
\ln\left(1+\frac{x-2}{x^2+2}\right)
\sim
\frac{x-2}{x^2+2}
$$

Entonces:

$$
\ln L
=
\lim_{x \to +\infty}
(3x-1)\frac{x-2}{x^2+2}
$$

Como el grado de arriba es $2$ y el de abajo también, queda:

$$
\ln L = 3
$$

Por tanto:

$$
L=e^3
$$

---

# 20. Comportamiento cuando $x \to +\infty$ o $x \to -\infty$

Cuando piden estudiar el comportamiento de una función en infinito, normalmente quieren calcular:

$$
\lim_{x \to +\infty} f(x)
$$

y/o:

$$
\lim_{x \to -\infty} f(x)
$$

Según el resultado:

- Si el límite es un número real $L$, la función se acerca a la recta horizontal $y=L$.
- Si el límite es $+\infty$, la función crece sin límite.
- Si el límite es $-\infty$, la función decrece sin límite.
- Si no existe, hay que justificarlo.

---

## 21. Asíntotas horizontales

Si:

$$
\lim_{x \to +\infty} f(x)=L
$$

entonces hay asíntota horizontal:

$$
y=L
$$

cuando $x \to +\infty$.

Si:

$$
\lim_{x \to -\infty} f(x)=M
$$

entonces hay asíntota horizontal:

$$
y=M
$$

cuando $x \to -\infty$.

Puede haber asíntotas horizontales distintas en $+\infty$ y en $-\infty$.

---

## 22. Asíntotas verticales

Si:

$$
\lim_{x \to a^+} f(x)=\pm\infty
$$

o:

$$
\lim_{x \to a^-} f(x)=\pm\infty
$$

entonces:

$$
x=a
$$

es una asíntota vertical.

Suelen aparecer cuando el denominador se anula y el numerador no.

Ejemplo:

$$
f(x)=\frac{1}{x-2}
$$

Tiene asíntota vertical en:

$$
x=2
$$

---

# 23. Funciones equivalentes

Las equivalencias sirven para simplificar límites.

Cuando $x \to 0$:

$$
\sin x \sim x
$$

$$
\tan x \sim x
$$

$$
1-\cos x \sim \frac{x^2}{2}
$$

$$
\ln(1+x) \sim x
$$

$$
e^x-1 \sim x
$$

$$
(1+x)^\alpha -1 \sim \alpha x
$$

---

## 24. Ejemplo con equivalencias

Calcular:

$$
\lim_{x \to 0} \frac{e^x-1}{x}
$$

Como:

$$
e^x-1 \sim x
$$

entonces:

$$
\lim_{x \to 0} \frac{e^x-1}{x}
=
\lim_{x \to 0} \frac{x}{x}
=
1
$$

---

# 25. Posibilidad de definir una función en un punto

A veces preguntan:

> ¿Se puede definir la función en $x=a$?

Eso significa:

- Si existe un límite finito cuando $x \to a$, podemos definir $f(a)$ igual a ese límite para hacerla continua.
- Si el límite no existe o es infinito, no se puede definir de forma continua en ese punto.

Ejemplo:

$$
f(x)=x\ln x
$$

con dominio inicial:

$$
x>0
$$

Nos preguntan si se puede definir en $x=0$.

Calculamos:

$$
\lim_{x \to 0^+} x\ln x
$$

Este límite es:

$$
0
$$

Por tanto, sí se puede definir:

$$
f(0)=0
$$

para hacerla continua en $0$.

---

## 26. Límite importante: $x\ln x$

Hay que recordar:

$$
\lim_{x \to 0^+} x\ln x = 0
$$

Aunque:

$$
\ln x \to -\infty
$$

el producto $x\ln x$ tiende a $0$.

Una forma rápida de verlo:

$$
x\ln x = \frac{\ln x}{1/x}
$$

Cuando $x \to 0^+$:

$$
\ln x \to -\infty
$$

y:

$$
\frac{1}{x}\to +\infty
$$

Aplicando L'Hôpital:

$$
\lim_{x \to 0^+}\frac{\ln x}{1/x}
=
\lim_{x \to 0^+}\frac{1/x}{-1/x^2}
=
\lim_{x \to 0^+}(-x)=0
$$

---

# 27. Funciones a trozos con parámetros

A veces una función depende de un parámetro $a$ o $b$ y te piden que sea continua.

Ejemplo:

$$
f(x)=
\begin{cases}
a+x, & x<0 \\
2x+1, & x\geq 0
\end{cases}
$$

Para que sea continua en $x=0$:

Límite por la izquierda:

$$
\lim_{x \to 0^-}(a+x)=a
$$

Límite por la derecha:

$$
\lim_{x \to 0^+}(2x+1)=1
$$

Valor de la función:

$$
f(0)=1
$$

Para continuidad:

$$
a=1
$$

---

# 28. Método resumen para continuidad con parámetros

Si piden valores de parámetros para continuidad:

1. Identifica el punto donde cambia la función.
2. Calcula el límite por la izquierda.
3. Calcula el límite por la derecha.
4. Igualas ambos.
5. Si el valor de la función está en uno de los trozos, comprueba que coincide.

Si hay dos parámetros, normalmente habrá dos condiciones:

- una por continuidad;
- otra por derivabilidad, si también la piden.

La derivabilidad se verá en el Tema 3.

---

# 29. Errores frecuentes

## Error 1: sustituir directamente en funciones a trozos

En un punto de cambio, no se sustituye sin más. Hay que mirar límites laterales.

---

## Error 2: olvidar el dominio

Ejemplos:

$$
\ln(x)
$$

solo existe si:

$$
x>0
$$

$$
\sqrt{x}
$$

solo existe si:

$$
x\geq 0
$$

$$
\frac{1}{x-a}
$$

no existe si:

$$
x=a
$$

---

## Error 3: confundir límite con valor de la función

Puede pasar que:

$$
\lim_{x \to a}f(x)=L
$$

pero:

$$
f(a)\neq L
$$

En ese caso, no es continua.

---

## Error 4: decir que una función no es continua sin justificar

En el examen hay que justificar con límites laterales o con el dominio.

---

# 30. Checklist del Tema 2

Antes del examen tengo que saber:

- [ ] Calcular límites sustituyendo cuando no hay indeterminación.
- [ ] Reconocer indeterminaciones.
- [ ] Resolver límites tipo $\frac{0}{0}$ factorizando.
- [ ] Resolver límites tipo $\frac{\infty}{\infty}$ comparando grados.
- [ ] Resolver límites tipo $\infty-\infty$ racionalizando o simplificando.
- [ ] Calcular límites laterales.
- [ ] Estudiar continuidad en funciones a trozos.
- [ ] Saber cuándo una función es continua en un punto.
- [ ] Manejar límites con $e^{1/x}$.
- [ ] Manejar límites con logaritmos.
- [ ] Resolver límites tipo $1^\infty$ usando logaritmos.
- [ ] Estudiar comportamiento cuando $x \to +\infty$ y $x \to -\infty$.
- [ ] Reconocer asíntotas horizontales y verticales.
- [ ] Saber si una función puede definirse en un punto para ser continua.

---

# 31. Ejercicios tipo

## Ejercicio 1

Estudiar la continuidad en $\mathbb{R}$ de:

$$
f(x)=
\begin{cases}
\dfrac{1-e^{1/x}}{1+e^{1/x}}, & x<0 \\
\sqrt{x^2+4}-\sqrt{x^2+1}, & x\geq 0
\end{cases}
$$

---

## Ejercicio 2

Calcular el comportamiento cuando $x \to +\infty$ y cuando $x \to -\infty$ de:

$$
f(x)=
\begin{cases}
\dfrac{1-e^{1/x}}{1+e^{1/x}}, & x<0 \\
\sqrt{x^2+4}-\sqrt{x^2+1}, & x\geq 0
\end{cases}
$$

---

## Ejercicio 3

Calcular:

$$
\lim_{x \to +\infty}
\left(\frac{x^2+x}{x^2+2}\right)^{3x-1}
$$

---

## Ejercicio 4

Estudiar si se puede definir en $x=0$ la función:

$$
f(x)=x\ln x
$$

para que sea continua.

---

## Ejercicio 5

Determinar el valor de $a$ para que la función sea continua:

$$
f(x)=
\begin{cases}
x+2, & x<1 \\
ax, & x\geq 1
\end{cases}
$$