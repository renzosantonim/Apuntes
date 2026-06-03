## 1. Derivada: idea básica

La derivada mide la razón de cambio instantánea de una función.

Se escribe:

$$
f'(x)
$$

Geométricamente, representa la pendiente de la recta tangente a la gráfica de la función.

- Si $f'(x)>0$, la función crece.
- Si $f'(x)<0$, la función decrece.
- Si $f'(x)=0$, puede haber un máximo, un mínimo o un punto de inflexión.

---

## 2. Definición de derivada

La derivada de $f$ en $x=a$ se define como:

$$
f'(a)=\lim_{h \to 0}\frac{f(a+h)-f(a)}{h}
$$

También puede escribirse como:

$$
f'(a)=\lim_{x \to a}\frac{f(x)-f(a)}{x-a}
$$

La función es derivable en $a$ si ese límite existe y es finito.

---

## 3. Relación entre continuidad y derivabilidad

Si una función es derivable en un punto, entonces es continua en ese punto.

$$
f \text{ derivable en } a \Rightarrow f \text{ continua en } a
$$

Pero una función puede ser continua y no derivable.

Ejemplo:

$$
f(x)=|x|
$$

es continua en $x=0$, pero no es derivable en $x=0$.

---

# 4. Derivabilidad en funciones a trozos

En funciones a trozos, antes de estudiar derivabilidad hay que estudiar continuidad.

Si una función no es continua en un punto, entonces no puede ser derivable en ese punto.

---

## 5. Derivadas laterales

En un punto donde cambia la definición de la función, por ejemplo $x=a$, hay que estudiar:

Derivada por la izquierda:

$$
f'_-(a)
$$

Derivada por la derecha:

$$
f'_+(a)
$$

Para que la función sea derivable en $a$, debe cumplirse:

$$
f'_-(a)=f'_+(a)
$$

y además la función debe ser continua en $a$.

---

## 6. Método para estudiar derivabilidad en funciones a trozos

Si la función cambia de expresión en $x=a$:

1. Estudiar continuidad en $x=a$.
2. Si no es continua, no es derivable.
3. Si es continua, derivar cada trozo.
4. Calcular la derivada lateral izquierda.
5. Calcular la derivada lateral derecha.
6. Igualar ambas.
7. Si coinciden, la función es derivable.
8. Si no coinciden, no es derivable.

---

## 7. Ejemplo de derivabilidad con parámetros

Sea:

$$
f(x)=
\begin{cases}
x^2, & x<1 \\
ax+b, & x\geq 1
\end{cases}
$$

Queremos que sea derivable en todo $\mathbb{R}$.

El único punto problemático es:

$$
x=1
$$

---

### Paso 1: continuidad en $x=1$

Límite por la izquierda:

$$
\lim_{x \to 1^-}x^2=1
$$

Límite por la derecha:

$$
\lim_{x \to 1^+}(ax+b)=a+b
$$

Para que sea continua:

$$
1=a+b
$$

---

### Paso 2: derivabilidad en $x=1$

Derivamos cada trozo.

Si $x<1$:

$$
f'(x)=2x
$$

Por tanto:

$$
f'_-(1)=2
$$

Si $x>1$:

$$
f'(x)=a
$$

Por tanto:

$$
f'_+(1)=a
$$

Para que sea derivable:

$$
2=a
$$

Sustituimos en la condición de continuidad:

$$
1=a+b
$$

$$
1=2+b
$$

$$
b=-1
$$

Por tanto:

$$
a=2, \qquad b=-1
$$

---

# 8. Reglas básicas de derivación

## Potencias

$$
\frac{d}{dx}(x^n)=nx^{n-1}
$$

Ejemplos:

$$
\frac{d}{dx}(x^3)=3x^2
$$

$$
\frac{d}{dx}(x^{-1})=-x^{-2}
$$

---

## Constantes

Si $c$ es constante:

$$
\frac{d}{dx}(c)=0
$$

---

## Constante por función

$$
\frac{d}{dx}(cf(x))=cf'(x)
$$

---

## Suma y resta

$$
(f+g)'=f'+g'
$$

$$
(f-g)'=f'-g'
$$

---

## Producto

$$
(fg)'=f'g+fg'
$$

---

## Cociente

$$
\left(\frac{f}{g}\right)'=\frac{f'g-fg'}{g^2}
$$

---

## Regla de la cadena

Si:

$$
h(x)=f(g(x))
$$

entonces:

$$
h'(x)=f'(g(x))g'(x)
$$

Ejemplo:

$$
h(x)=e^{x^2}
$$

Entonces:

$$
h'(x)=e^{x^2}\cdot 2x
$$

---

# 9. Derivadas frecuentes

| Función | Derivada |
|---|---|
| $x^n$ | $nx^{n-1}$ |
| $e^x$ | $e^x$ |
| $e^{g(x)}$ | $e^{g(x)}g'(x)$ |
| $\ln x$ | $\frac{1}{x}$ |
| $\ln(g(x))$ | $\frac{g'(x)}{g(x)}$ |
| $\sin x$ | $\cos x$ |
| $\cos x$ | $-\sin x$ |
| $\tan x$ | $\frac{1}{\cos^2 x}$ |

---

# 10. Crecimiento y decrecimiento

Para estudiar dónde una función crece o decrece:

1. Calcular $f'(x)$.
2. Resolver:

$$
f'(x)=0
$$

3. Estudiar el signo de $f'(x)$ en los intervalos.
4. Concluir:

Si:

$$
f'(x)>0
$$

la función es creciente.

Si:

$$
f'(x)<0
$$

la función es decreciente.

---

## 11. Ejemplo de crecimiento

Estudiar dónde crece y decrece:

$$
f(x)=x^3-3x
$$

Derivamos:

$$
f'(x)=3x^2-3
$$

Igualamos a cero:

$$
3x^2-3=0
$$

$$
x^2-1=0
$$

$$
x=\pm 1
$$

Estudiamos signos:

- En $(-\infty,-1)$, $f'(x)>0$.
- En $(-1,1)$, $f'(x)<0$.
- En $(1,+\infty)$, $f'(x)>0$.

Por tanto:

- Crece en $(-\infty,-1)$.
- Decrece en $(-1,1)$.
- Crece en $(1,+\infty)$.

---

# 12. Máximos y mínimos relativos

Un punto crítico aparece cuando:

$$
f'(x)=0
$$

o cuando la derivada no existe.

Para clasificarlo, podemos usar el cambio de signo de $f'$:

- Si $f'$ pasa de positiva a negativa, hay máximo relativo.
- Si $f'$ pasa de negativa a positiva, hay mínimo relativo.

En el ejemplo anterior:

$$
f(x)=x^3-3x
$$

En $x=-1$, $f'$ pasa de positiva a negativa, así que hay máximo relativo.

En $x=1$, $f'$ pasa de negativa a positiva, así que hay mínimo relativo.

---

# 13. Concavidad

La concavidad se estudia con la segunda derivada.

Si:

$$
f''(x)>0
$$

la función es convexa o cóncava hacia arriba.

Si:

$$
f''(x)<0
$$

la función es cóncava hacia abajo.

---

## 14. Puntos de inflexión

Un punto de inflexión ocurre cuando cambia la concavidad.

Método:

1. Calcular $f''(x)$.
2. Resolver:

$$
f''(x)=0
$$

3. Estudiar el signo de $f''(x)$.
4. Si cambia de signo, hay punto de inflexión.

---

## 15. Ejemplo de concavidad

Estudiar la concavidad de:

$$
f(x)=x^3
$$

Derivamos:

$$
f'(x)=3x^2
$$

Segunda derivada:

$$
f''(x)=6x
$$

Igualamos:

$$
6x=0
$$

$$
x=0
$$

Estudiamos signos:

- Si $x<0$, $f''(x)<0$.
- Si $x>0$, $f''(x)>0$.

Como cambia la concavidad en $x=0$, hay punto de inflexión.

---

# 16. Ejemplo tipo examen: crecimiento y concavidad de $\frac{e^x}{x}$

Sea:

$$
f(x)=\frac{e^x}{x}
$$

Dominio:

$$
x \neq 0
$$

Derivamos usando la regla del cociente:

$$
f'(x)=\frac{xe^x-e^x}{x^2}
$$

Sacamos factor común:

$$
f'(x)=\frac{e^x(x-1)}{x^2}
$$

Como:

$$
e^x>0
$$

y:

$$
x^2>0
$$

para $x \neq 0$, el signo depende de:

$$
x-1
$$

Por tanto:

- Si $x<1$, entonces $f'(x)<0$.
- Si $x>1$, entonces $f'(x)>0$.

Teniendo en cuenta que $x=0$ no pertenece al dominio:

- Decrece en $(-\infty,0)$.
- Decrece en $(0,1)$.
- Crece en $(1,+\infty)$.

---

## Segunda derivada

Partimos de:

$$
f'(x)=\frac{e^x(x-1)}{x^2}
$$

Escribimos:

$$
f'(x)=e^x(x-1)x^{-2}
$$

Derivamos usando producto:

$$
f''(x)=e^x(x-1)x^{-2}+e^x x^{-2}+e^x(x-1)(-2x^{-3})
$$

Sacamos factor común:

$$
f''(x)=e^x x^{-3}\left[x(x-1)+x-2(x-1)\right]
$$

Simplificamos:

$$
x(x-1)+x-2(x-1)
$$

$$
x^2-x+x-2x+2
$$

$$
x^2-2x+2
$$

Por tanto:

$$
f''(x)=\frac{e^x(x^2-2x+2)}{x^3}
$$

Observamos que:

$$
x^2-2x+2=(x-1)^2+1>0
$$

y:

$$
e^x>0
$$

Así que el signo de $f''(x)$ depende de:

$$
x^3
$$

Por tanto:

- Si $x<0$, $f''(x)<0$.
- Si $x>0$, $f''(x)>0$.

Conclusión:

- Cóncava hacia abajo en $(-\infty,0)$.
- Convexa en $(0,+\infty)$.

No hay punto de inflexión en $x=0$ porque $0$ no pertenece al dominio.

---

# 17. Teorema de Bolzano

Si $f$ es continua en $[a,b]$ y:

$$
f(a)f(b)<0
$$

entonces existe al menos un punto $c \in (a,b)$ tal que:

$$
f(c)=0
$$

Es decir, si la función cambia de signo y es continua, corta al eje $X$.

---

## 18. Cómo usar Bolzano para demostrar existencia de raíz

Para demostrar que una función tiene una raíz:

1. Buscar un intervalo $[a,b]$.
2. Comprobar que $f$ es continua en ese intervalo.
3. Calcular $f(a)$ y $f(b)$.
4. Ver que tienen signos opuestos.
5. Concluir que existe al menos una raíz en $(a,b)$.

---

## 19. Ejemplo de Bolzano

Demostrar que:

$$
f(x)=x^3+x-1
$$

tiene una raíz en $(0,1)$.

La función es polinómica, luego es continua en $\mathbb{R}$.

Calculamos:

$$
f(0)=-1
$$

$$
f(1)=1
$$

Como:

$$
f(0)<0
$$

y:

$$
f(1)>0
$$

por Bolzano existe al menos un $c \in (0,1)$ tal que:

$$
f(c)=0
$$

---

# 20. Unicidad de raíz

Para demostrar que una función tiene una única raíz, normalmente se hace:

1. Demostrar existencia con Bolzano.
2. Demostrar que la función es estrictamente creciente o estrictamente decreciente.

Si:

$$
f'(x)>0
$$

en todo el dominio, entonces $f$ es estrictamente creciente.

Si:

$$
f'(x)<0
$$

en todo el dominio, entonces $f$ es estrictamente decreciente.

Una función estrictamente monótona solo puede cortar una vez el eje $X$.

---

## 21. Ejemplo de unicidad

Demostrar que:

$$
f(x)=2x^5+3x^3+10x-5
$$

posee una única raíz real.

Como $f$ es polinómica, es continua en $\mathbb{R}$.

Primero vemos existencia.

Calculamos:

$$
f(0)=-5
$$

$$
f(1)=2+3+10-5=10
$$

Como cambia de signo, por Bolzano existe al menos una raíz en $(0,1)$.

Ahora demostramos unicidad.

Derivamos:

$$
f'(x)=10x^4+9x^2+10
$$

Observamos que:

$$
10x^4 \geq 0
$$

$$
9x^2 \geq 0
$$

y además:

$$
10>0
$$

Por tanto:

$$
f'(x)>0 \quad \forall x \in \mathbb{R}
$$

Luego $f$ es estrictamente creciente en $\mathbb{R}$.

Por tanto, solo puede tener una raíz real.

Conclusión:

$$
f(x)=2x^5+3x^3+10x-5
$$

posee una única raíz real.

---

# 22. Teorema de Rolle

El Teorema de Rolle dice:

Si $f$ cumple:

1. $f$ es continua en $[a,b]$.
2. $f$ es derivable en $(a,b)$.
3. $f(a)=f(b)$.

Entonces existe al menos un punto $c \in (a,b)$ tal que:

$$
f'(c)=0
$$

---

## 23. Cuándo se puede aplicar Rolle

Para aplicar Rolle hay que comprobar las tres hipótesis.

No basta con que:

$$
f(a)=f(b)
$$

También debe ser continua en todo el intervalo cerrado y derivable en todo el intervalo abierto.

---

## 24. Ejemplo donde no se aplica Rolle

Sea:

$$
f(x)=\sqrt[3]{x^2}
$$

en el intervalo:

$$
[-1,1]
$$

Observamos:

$$
f(-1)=1
$$

$$
f(1)=1
$$

Parece que podría aplicarse Rolle.

Pero:

$$
f(x)=|x|^{2/3}
$$

no es derivable en $x=0$.

Como $0 \in (-1,1)$, no se cumple la hipótesis de derivabilidad en todo el intervalo abierto.

Por tanto, no se puede aplicar Rolle.

No contradice el Teorema de Rolle.

---

# 25. Teorema del Valor Medio

Si $f$ cumple:

1. $f$ es continua en $[a,b]$.
2. $f$ es derivable en $(a,b)$.

Entonces existe al menos un $c \in (a,b)$ tal que:

$$
f'(c)=\frac{f(b)-f(a)}{b-a}
$$

Rolle es un caso particular del Teorema del Valor Medio cuando:

$$
f(a)=f(b)
$$

---

# 26. Interpretación de derivadas

A veces una derivada se interpreta como razón de cambio.

Ejemplo:

La producción $P$ depende de la temperatura $T$.

Si:

$$
\frac{dP}{dT}=-2
$$

significa que, por cada unidad que aumenta $T$, la producción $P$ disminuye aproximadamente en $2$ unidades.

Si además:

$$
\frac{dT}{dt}=0.15
$$

entonces, por la regla de la cadena:

$$
\frac{dP}{dt}=\frac{dP}{dT}\cdot \frac{dT}{dt}
$$

Sustituimos:

$$
\frac{dP}{dt}=(-2)(0.15)
$$

$$
\frac{dP}{dt}=-0.3
$$

La producción está disminuyendo a razón de $0.3$ unidades por año.

---

# 27. Método de Newton-Raphson

Newton-Raphson sirve para aproximar raíces de una ecuación:

$$
f(x)=0
$$

La fórmula es:

$$
x_{n+1}=x_n-\frac{f(x_n)}{f'(x_n)}
$$

Hay que elegir un valor inicial $x_0$ cercano a la raíz.

---

## 28. Método para ejercicios de Newton-Raphson

1. Definir la función $f(x)$.
2. Calcular $f'(x)$.
3. Demostrar que la raíz existe y es única.
4. Elegir un valor inicial $x_0$.
5. Aplicar:

$$
x_{n+1}=x_n-\frac{f(x_n)}{f'(x_n)}
$$

6. Parar cuando el error sea menor que el pedido.

En exámenes suelen pedir errores como:

$$
0.0001
$$

o:

$$
0.0005
$$

---

## 29. Criterio práctico de parada

Si se calculan dos aproximaciones consecutivas:

$$
x_n
$$

y:

$$
x_{n+1}
$$

se suele parar cuando:

$$
|x_{n+1}-x_n|<\text{tolerancia}
$$

Por ejemplo, si piden error menor que $0.0005$, paramos cuando:

$$
|x_{n+1}-x_n|<0.0005
$$

---

## 30. Ejemplo Newton-Raphson

Aproximar la raíz de:

$$
f(x)=2x^5+3x^3+10x-5
$$

con error menor que $0.0005$.

Ya vimos que tiene una única raíz en $(0,1)$.

Derivada:

$$
f'(x)=10x^4+9x^2+10
$$

Tomamos:

$$
x_0=0.5
$$

Fórmula:

$$
x_{n+1}=x_n-\frac{2x_n^5+3x_n^3+10x_n-5}{10x_n^4+9x_n^2+10}
$$

Calculamos:

$$
x_1 \approx 0.3714
$$

$$
x_2 \approx 0.3711
$$

Como:

$$
|x_2-x_1|\approx 0.0003<0.0005
$$

podemos tomar:

$$
x \approx 0.3711
$$

---

# 31. Polinomio de Taylor y Maclaurin

El polinomio de Taylor aproxima una función cerca de un punto.

Si el punto es $a$, el polinomio de Taylor de grado $n$ es:

$$
P_n(x)=f(a)+f'(a)(x-a)+\frac{f''(a)}{2!}(x-a)^2+\cdots+\frac{f^{(n)}(a)}{n!}(x-a)^n
$$

Si el punto es $a=0$, se llama polinomio de Maclaurin:

$$
P_n(x)=f(0)+f'(0)x+\frac{f''(0)}{2!}x^2+\cdots+\frac{f^{(n)}(0)}{n!}x^n
$$

---

# 32. Maclaurin frecuentes

## Exponencial

$$
e^x=1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+\cdots
$$

---

## Seno

$$
\sin x=x-\frac{x^3}{3!}+\frac{x^5}{5!}-\cdots
$$

---

## Coseno

$$
\cos x=1-\frac{x^2}{2!}+\frac{x^4}{4!}-\cdots
$$

---

## Logaritmo

$$
\ln(1+x)=x-\frac{x^2}{2}+\frac{x^3}{3}-\frac{x^4}{4}+\cdots
$$

válido para valores de $x$ cercanos a $0$.

---

## Binomial

Para funciones del tipo:

$$
(1+x)^\alpha
$$

el desarrollo es:

$$
(1+x)^\alpha =
1+\alpha x+\frac{\alpha(\alpha-1)}{2!}x^2+
\frac{\alpha(\alpha-1)(\alpha-2)}{3!}x^3+\cdots
$$

---

# 33. Ejemplo Maclaurin tipo examen

Aproximar:

$$
\frac{1}{\sqrt{1.03}}
$$

usando Maclaurin.

Observamos:

$$
\frac{1}{\sqrt{1.03}}=(1.03)^{-1/2}
$$

Lo escribimos como:

$$
(1+x)^{-1/2}
$$

con:

$$
x=0.03
$$

Usamos el desarrollo binomial:

$$
(1+x)^\alpha =
1+\alpha x+\frac{\alpha(\alpha-1)}{2!}x^2+
\frac{\alpha(\alpha-1)(\alpha-2)}{3!}x^3+
\frac{\alpha(\alpha-1)(\alpha-2)(\alpha-3)}{4!}x^4
$$

Aquí:

$$
\alpha=-\frac{1}{2}
$$

Por tanto:

$$
(1+x)^{-1/2}
\approx
1-\frac{1}{2}x+\frac{3}{8}x^2-\frac{5}{16}x^3+\frac{35}{128}x^4
$$

Sustituimos:

$$
x=0.03
$$

Entonces:

$$
\frac{1}{\sqrt{1.03}}
\approx
1-\frac{1}{2}(0.03)+\frac{3}{8}(0.03)^2-\frac{5}{16}(0.03)^3+\frac{35}{128}(0.03)^4
$$

---

# 34. Error en Taylor

El error al aproximar con Taylor suele estimarse con el resto de Lagrange:

$$
R_n(x)=\frac{f^{(n+1)}(c)}{(n+1)!}(x-a)^{n+1}
$$

donde $c$ está entre $a$ y $x$.

Para estimar el error, usamos:

$$
|R_n(x)|\leq \frac{M}{(n+1)!}|x-a|^{n+1}
$$

donde $M$ es una cota de:

$$
|f^{(n+1)}(t)|
$$

en el intervalo entre $a$ y $x$.

---

## 35. Método para error de Taylor

1. Identificar el grado $n$.
2. Calcular o acotar la derivada de orden $n+1$.
3. Buscar una cota $M$ en el intervalo.
4. Aplicar:

$$
|R_n(x)|\leq \frac{M}{(n+1)!}|x-a|^{n+1}
$$

---

# 36. Optimización

Los problemas de optimización piden maximizar o minimizar una magnitud.

Ejemplos típicos:

- caja de coste mínimo;
- volumen máximo;
- área máxima;
- cono de volumen máximo.

---

## 37. Método para optimización

1. Identificar qué se quiere maximizar o minimizar.
2. Definir variables.
3. Escribir la función objetivo.
4. Usar la restricción para dejar la función con una sola variable.
5. Derivar.
6. Igualar a cero.
7. Comprobar si es máximo o mínimo.
8. Responder con las unidades correctas.

---

## 38. Ejemplo de optimización

Un rectángulo tiene perímetro $20$. Hallar las dimensiones que maximizan el área.

Sean:

$$
x=\text{base}
$$

$$
y=\text{altura}
$$

Restricción:

$$
2x+2y=20
$$

Simplificamos:

$$
x+y=10
$$

Despejamos:

$$
y=10-x
$$

Área:

$$
A=xy
$$

Sustituimos:

$$
A(x)=x(10-x)
$$

$$
A(x)=10x-x^2
$$

Derivamos:

$$
A'(x)=10-2x
$$

Igualamos a cero:

$$
10-2x=0
$$

$$
x=5
$$

Entonces:

$$
y=10-5=5
$$

El área máxima se obtiene con un cuadrado de lados:

$$
5 \times 5
$$

---

# 39. Interpolación

La interpolación sirve para aproximar el valor de una función a partir de una tabla de datos.

Si tenemos puntos:

$$
(x_0,y_0), (x_1,y_1), \dots, (x_n,y_n)
$$

existe un polinomio de grado como máximo $n$ que pasa por esos puntos.

---

## 40. Polinomio de Lagrange

El polinomio interpolador es:

$$
P_n(x)=\sum_{i=0}^{n} y_i L_i(x)
$$

donde:

$$
L_i(x)=\prod_{\substack{j=0 \\ j\neq i}}^{n}
\frac{x-x_j}{x_i-x_j}
$$

---

## 41. Interpolación lineal

Si solo usamos dos puntos:

$$
(x_0,y_0)
$$

y:

$$
(x_1,y_1)
$$

el polinomio es una recta.

Fórmula:

$$
P_1(x)=y_0+\frac{y_1-y_0}{x_1-x_0}(x-x_0)
$$

---

## 42. Ejemplo de interpolación lineal

Aproximar $f(4.2)$ usando los puntos:

$$
(4,5.2)
$$

y:

$$
(5,-1.2)
$$

Usamos:

$$
P_1(x)=5.2+\frac{-1.2-5.2}{5-4}(x-4)
$$

$$
P_1(x)=5.2-6.4(x-4)
$$

Entonces:

$$
P_1(4.2)=5.2-6.4(0.2)
$$

$$
P_1(4.2)=5.2-1.28
$$

$$
P_1(4.2)=3.92
$$

---

## 43. Error de interpolación

Si interpolamos con un polinomio de grado $n$, el error viene dado por:

$$
E_n(x)=\frac{f^{(n+1)}(c)}{(n+1)!}(x-x_0)(x-x_1)\cdots(x-x_n)
$$

donde $c$ está en el intervalo que contiene los nodos y el punto $x$.

Para estimar:

$$
|E_n(x)|\leq
\frac{M}{(n+1)!}
|(x-x_0)(x-x_1)\cdots(x-x_n)|
$$

donde $M$ es una cota de:

$$
|f^{(n+1)}(t)|
$$

en el intervalo.

---

# 44. Errores frecuentes

## Error 1: estudiar derivabilidad sin continuidad

Si una función no es continua en un punto, automáticamente no es derivable.

---

## Error 2: olvidar puntos fuera del dominio

Por ejemplo:

$$
f(x)=\frac{e^x}{x}
$$

no está definida en:

$$
x=0
$$

No se puede decir que hay punto de inflexión en $x=0$.

---

## Error 3: aplicar Rolle sin revisar hipótesis

Para Rolle hacen falta tres cosas:

- continuidad en $[a,b]$;
- derivabilidad en $(a,b)$;
- igualdad $f(a)=f(b)$.

Si falla una, no se puede aplicar.

---

## Error 4: decir que hay máximo solo porque $f'(x)=0$

Que:

$$
f'(a)=0
$$

solo significa que $a$ es punto crítico.

Hay que comprobar cambio de signo o usar la segunda derivada.

---

## Error 5: olvidar las unidades en optimización

Si el problema habla de metros, centímetros, euros, volumen, etc., la respuesta final debe tener unidades.

---

# 45. Checklist del Tema 3

Antes del examen tengo que saber:

- [ ] Derivar funciones básicas.
- [ ] Usar producto, cociente y regla de la cadena.
- [ ] Estudiar continuidad antes que derivabilidad.
- [ ] Calcular derivadas laterales en funciones a trozos.
- [ ] Resolver parámetros para que una función sea derivable.
- [ ] Estudiar crecimiento y decrecimiento con $f'(x)$.
- [ ] Estudiar concavidad con $f''(x)$.
- [ ] Reconocer máximos, mínimos y puntos de inflexión.
- [ ] Aplicar Bolzano para demostrar existencia de raíces.
- [ ] Usar monotonía para demostrar unicidad de raíces.
- [ ] Aplicar correctamente Rolle.
- [ ] Saber cuándo Rolle no se puede aplicar.
- [ ] Interpretar derivadas como razones de cambio.
- [ ] Usar la regla de la cadena en razones de cambio.
- [ ] Aplicar Newton-Raphson.
- [ ] Construir polinomios de Maclaurin.
- [ ] Estimar errores de Taylor.
- [ ] Resolver problemas de optimización.
- [ ] Hacer interpolación básica.
- [ ] Estimar errores de interpolación.

---

# 46. Ejercicios tipo

## Ejercicio 1

Estudiar la derivabilidad en $\mathbb{R}$ de:

$$
f(x)=
\begin{cases}
a\cos x+2x, & x\leq 0 \\
a^2\ln(x+1)+\frac{b}{x+1}, & x>0
\end{cases}
$$

en función de $a$ y $b$.

---

## Ejercicio 2

Demostrar que:

$$
f(x)=2x^5+3x^3+10x-5
$$

posee una única raíz real.

Después aproximarla con Newton-Raphson con error menor que $0.0005$.

---

## Ejercicio 3

Demostrar que la función:

$$
f(x)=\sqrt[3]{x^2}
$$

cumple:

$$
f(-1)=f(1)
$$

pero no existe ningún $c \in (-1,1)$ tal que:

$$
f'(c)=0
$$

¿Contradice esto el Teorema de Rolle?

---

## Ejercicio 4

Aproximar:

$$
\frac{1}{\sqrt{1.03}}
$$

mediante el polinomio de Maclaurin de grado $4$.

Estimar el error cometido.

---

## Ejercicio 5

Un triángulo isósceles de perímetro $10$ m gira alrededor de la altura correspondiente al lado desigual, formando un cono.

Hallar sus lados para que el cono tenga volumen máximo.

---

## Ejercicio 6

Dada la tabla:

| $x$ | $1$ | $4$ | $5$ | $9$ |
|---|---:|---:|---:|---:|
| $f(x)$ | $2.3$ | $5.2$ | $-1.2$ | $0.5$ |

Aproximar $f(4.2)$ mediante el polinomio de interpolación de grado mínimo conveniente.

Estimar el error si se conoce una cota de la derivada correspondiente.