## 1. Conjuntos en la recta real

Un conjunto suele venir dado así:

$$
A = \{x \in \mathbb{R} : \text{condición sobre } x\}
$$

En los exámenes suelen pedir:

- Determinar el conjunto solución.
- Decidir si está acotado superiormente.
- Decidir si está acotado inferiormente.
- Calcular, si existen:
  - $\sup(A)$
  - $\inf(A)$
  - $\max(A)$
  - $\min(A)$

---

## 2. Intervalos

Los conjuntos solución suelen escribirse como intervalos.

| Intervalo     | Significado       |
| ------------- | ----------------- |
| $(a,b)$       | $a < x < b$       |
| $[a,b]$       | $a \leq x \leq b$ |
| $(a,b]$       | $a < x \leq b$    |
| $[a,b)$       | $a \leq x < b$    |
| $(a,+\infty)$ | $x > a$           |
| $(-\infty,a)$ | $x < a$           |

Importante:

- Si un extremo está incluido, se usa corchete.
- Si un extremo no está incluido, se usa paréntesis.
- El infinito nunca se incluye.

---

## 3. Cotas, supremo, ínfimo, máximo y mínimo

### Cota superior

Un número $M$ es cota superior de $A$ si:

$$
x \leq M \quad \forall x \in A
$$

Si existe alguna cota superior, el conjunto está acotado superiormente.

---

### Cota inferior

Un número $m$ es cota inferior de $A$ si:

$$
m \leq x \quad \forall x \in A
$$

Si existe alguna cota inferior, el conjunto está acotado inferiormente.

---

### Supremo

El supremo es la menor cota superior.

$$
\sup(A)
$$

Ejemplo:

$$
A=(1,5)
$$

Entonces:

$$
\sup(A)=5
$$

aunque $5 \notin A$.

---

### Ínfimo

El ínfimo es la mayor cota inferior.

$$
\inf(A)
$$

Ejemplo:

$$
A=(1,5)
$$

Entonces:

$$
\inf(A)=1
$$

aunque $1 \notin A$.

---

### Máximo

Un conjunto tiene máximo si el supremo pertenece al conjunto.

$$
\max(A)=\sup(A)
$$

siempre que:

$$
\sup(A) \in A
$$

Ejemplo:

$$
A=(1,5]
$$

Entonces:

$$
\max(A)=5
$$

---

### Mínimo

Un conjunto tiene mínimo si el ínfimo pertenece al conjunto.

$$
\min(A)=\inf(A)
$$

siempre que:

$$
\inf(A) \in A
$$

Ejemplo:

$$
A=[1,5)
$$

Entonces:

$$
\min(A)=1
$$

---

## 4. Tabla rápida

| Conjunto | $\inf(A)$ | $\min(A)$ | $\sup(A)$ | $\max(A)$ |
|---|---:|---:|---:|---:|
| $(1,5)$ | $1$ | No existe | $5$ | No existe |
| $[1,5]$ | $1$ | $1$ | $5$ | $5$ |
| $(1,5]$ | $1$ | No existe | $5$ | $5$ |
| $[1,5)$ | $1$ | $1$ | $5$ | No existe |
| $(1,+\infty)$ | $1$ | No existe | No existe | No existe |
| $[1,+\infty)$ | $1$ | $1$ | No existe | No existe |

---

# 5. Valor absoluto

El valor absoluto se define como:

$$
|x| =
\begin{cases}
x, & x \geq 0 \\
-x, & x < 0
\end{cases}
$$

Ejemplos:

$$
|3|=3
$$

$$
|-3|=3
$$

---

## 6. Valor absoluto de una expresión

Si tenemos:

$$
|x-a|
$$

entonces:

$$
|x-a| =
\begin{cases}
x-a, & x \geq a \\
a-x, & x < a
\end{cases}
$$

Ejemplo:

$$
|x-3| =
\begin{cases}
x-3, & x \geq 3 \\
3-x, & x < 3
\end{cases}
$$

---

## 7. Método para desigualdades con valores absolutos

Para resolver una desigualdad con varios valores absolutos:

1. Buscar los puntos donde cada valor absoluto se anula.
2. Dividir la recta en intervalos.
3. Quitar los valores absolutos en cada intervalo.
4. Resolver la desigualdad en cada caso.
5. Unir las soluciones.
6. Estudiar cotas, supremo, ínfimo, máximo y mínimo.

---

## 8. Ejemplo típico

Resolver:

$$
|x-1|+|x-2|<x
$$

Los puntos conflictivos son:

$$
x=1, \qquad x=2
$$

Dividimos en:

$$
(-\infty,1), \quad [1,2), \quad [2,+\infty)
$$

---

### Caso 1: $x<1$

$$
|x-1|=1-x
$$

$$
|x-2|=2-x
$$

Entonces:

$$
1-x+2-x<x
$$

$$
3-2x<x
$$

$$
3<3x
$$

$$
x>1
$$

Pero estamos en $x<1$, así que no hay solución.

---

### Caso 2: $1 \leq x<2$

$$
|x-1|=x-1
$$

$$
|x-2|=2-x
$$

Entonces:

$$
x-1+2-x<x
$$

$$
1<x
$$

Como estamos en $1 \leq x<2$:

$$
1<x<2
$$

---

### Caso 3: $x \geq 2$

$$
|x-1|=x-1
$$

$$
|x-2|=x-2
$$

Entonces:

$$
x-1+x-2<x
$$

$$
2x-3<x
$$

$$
x<3
$$

Como estamos en $x \geq 2$:

$$
2 \leq x<3
$$

---

### Solución

$$
A=(1,2)\cup[2,3)
$$

Por tanto:

$$
A=(1,3)
$$

Entonces:

$$
\inf(A)=1
$$

$$
\sup(A)=3
$$

Como $1 \notin A$, no existe mínimo.

Como $3 \notin A$, no existe máximo.

El conjunto está acotado superior e inferiormente.

---

# 9. Desigualdades con valor absoluto y fracciones

Si aparece algo como:

$$
\left|\frac{x+1}{x-2}\right|>2
$$

primero hay que mirar el dominio:

$$
x-2 \neq 0
$$

Por tanto:

$$
x \neq 2
$$

Después usamos:

$$
|A|>k \iff A>k \quad \text{o} \quad A<-k
$$

si $k>0$.

Así:

$$
\left|\frac{x+1}{x-2}\right|>2
$$

equivale a:

$$
\frac{x+1}{x-2}>2
$$

o bien:

$$
\frac{x+1}{x-2}<-2
$$

---

## 10. Cómo resolver inecuaciones racionales

Para resolver una inecuación racional:

$$
\frac{P(x)}{Q(x)}>0
$$

o parecida:

1. Pasar todo a un lado.
2. Factorizar numerador y denominador.
3. Buscar puntos críticos:
   - ceros del numerador;
   - ceros del denominador.
4. Hacer tabla de signos.
5. Elegir los intervalos que cumplen.
6. Excluir siempre los puntos que anulan el denominador.

---

# 11. Números complejos

Un número complejo tiene la forma:

$$
z=a+bi
$$

donde:

- $a$ es la parte real.
- $b$ es la parte imaginaria.
- $i$ cumple que $i^2=-1$.

Ejemplo:

$$
z=3-2i
$$

Entonces:

$$
\operatorname{Re}(z)=3
$$

$$
\operatorname{Im}(z)=-2
$$

---

## 12. Conjugado

Si:

$$
z=a+bi
$$

entonces su conjugado es:

$$
\overline{z}=a-bi
$$

Ejemplo:

$$
z=3+2i
$$

Entonces:

$$
\overline{z}=3-2i
$$

Propiedad importante:

$$
z\overline{z}=|z|^2
$$

---

## 13. Módulo

El módulo de:

$$
z=a+bi
$$

es:

$$
|z|=\sqrt{a^2+b^2}
$$

Ejemplo:

$$
z=3+4i
$$

Entonces:

$$
|z|=5
$$

---

## 14. Argumento

El argumento es el ángulo que forma el complejo con el eje real positivo.

Si:

$$
z=a+bi
$$

entonces:

$$
\tan(\theta)=\frac{b}{a}
$$

Hay que tener cuidado con el cuadrante.

Ejemplo:

$$
z=1+i
$$

Entonces:

$$
|z|=\sqrt{2}
$$

y:

$$
\arg(z)=\frac{\pi}{4}
$$

---

## 15. Forma polar

Un complejo puede escribirse como:

$$
z=r(\cos\theta+i\sin\theta)
$$

o también:

$$
z=re^{i\theta}
$$

donde:

$$
r=|z|
$$

y:

$$
\theta=\arg(z)
$$

Ejemplo:

$$
1+i=\sqrt{2}e^{i\pi/4}
$$

---

# 16. Operaciones en forma polar

Si:

$$
z_1=r_1e^{i\theta_1}
$$

y:

$$
z_2=r_2e^{i\theta_2}
$$

entonces:

## Producto

$$
z_1z_2=r_1r_2e^{i(\theta_1+\theta_2)}
$$

Se multiplican los módulos y se suman los argumentos.

---

## Cociente

$$
\frac{z_1}{z_2}=\frac{r_1}{r_2}e^{i(\theta_1-\theta_2)}
$$

Se dividen los módulos y se restan los argumentos.

---

## Potencias

Si:

$$
z=re^{i\theta}
$$

entonces:

$$
z^n=r^ne^{in\theta}
$$

---

# 17. Raíces complejas

Para resolver:

$$
z^n=w
$$

escribimos $w$ en forma polar:

$$
w=re^{i\theta}
$$

Entonces las soluciones son:

$$
z_k=\sqrt[n]{r}e^{i\frac{\theta+2k\pi}{n}}
$$

donde:

$$
k=0,1,2,\dots,n-1
$$

Hay exactamente $n$ raíces complejas.

---

## Ejemplo

Resolver:

$$
z^3=8
$$

Escribimos:

$$
8=8e^{i0}
$$

Entonces:

$$
z_k=\sqrt[3]{8}e^{i\frac{0+2k\pi}{3}}
$$

$$
z_k=2e^{i\frac{2k\pi}{3}}
$$

con:

$$
k=0,1,2
$$

Soluciones:

$$
z_0=2
$$

$$
z_1=2e^{i2\pi/3}=-1+\sqrt{3}i
$$

$$
z_2=2e^{i4\pi/3}=-1-\sqrt{3}i
$$

---

# 18. Polinomios con coeficientes reales

Si un polinomio tiene coeficientes reales, las raíces complejas no reales aparecen por parejas conjugadas.

Es decir, si:

$$
z=a+bi, \qquad b \neq 0
$$

es raíz, entonces:

$$
\overline{z}=a-bi
$$

también es raíz.

Ejemplo:

Si un polinomio con coeficientes reales tiene como raíz:

$$
2+3i
$$

entonces también tiene como raíz:

$$
2-3i
$$

---

## 19. Ejemplo típico de examen

Sea $p(x)$ un polinomio de grado $5$ con coeficientes reales. Sabemos que $p(x)$ tiene como mínimo una raíz real y otra raíz compleja no real.

¿Cuántas raíces reales puede tener en total?

Como tiene coeficientes reales, si tiene una raíz compleja no real, también tiene su conjugada.

Por tanto, ya tenemos:

- una raíz compleja no real;
- su conjugada;
- al menos una raíz real.

Eso suma $3$ raíces.

Como el polinomio es de grado $5$, quedan $2$ raíces más.

Esas dos raíces pueden ser:

- dos raíces reales;
- o dos raíces complejas conjugadas.

Por tanto, el número total de raíces reales puede ser:

$$
1 \quad \text{o} \quad 3
$$

---

# 20. Ecuaciones con conjugados

Si aparece una ecuación con $\overline{z}$, lo normal es escribir:

$$
z=a+bi
$$

y entonces:

$$
\overline{z}=a-bi
$$

Después se igualan partes reales e imaginarias.

---

## Ejemplo

Resolver:

$$
z^2=\overline{z}
$$

Sea:

$$
z=a+bi
$$

Entonces:

$$
z^2=(a+bi)^2
$$

$$
z^2=a^2-b^2+2abi
$$

Además:

$$
\overline{z}=a-bi
$$

Igualamos:

$$
a^2-b^2+2abi=a-bi
$$

Parte real:

$$
a^2-b^2=a
$$

Parte imaginaria:

$$
2ab=-b
$$

De la parte imaginaria:

$$
2ab+b=0
$$

$$
b(2a+1)=0
$$

Por tanto:

$$
b=0
$$

o bien:

$$
a=-\frac{1}{2}
$$

---

### Caso 1: $b=0$

La parte real queda:

$$
a^2=a
$$

$$
a(a-1)=0
$$

Por tanto:

$$
a=0
$$

o:

$$
a=1
$$

Soluciones:

$$
z=0
$$

$$
z=1
$$

---

### Caso 2: $a=-\frac{1}{2}$

Usamos:

$$
a^2-b^2=a
$$

Sustituimos:

$$
\left(-\frac{1}{2}\right)^2-b^2=-\frac{1}{2}
$$

$$
\frac{1}{4}-b^2=-\frac{1}{2}
$$

$$
b^2=\frac{3}{4}
$$

$$
b=\pm\frac{\sqrt{3}}{2}
$$

Soluciones:

$$
z=-\frac{1}{2}+\frac{\sqrt{3}}{2}i
$$

$$
z=-\frac{1}{2}-\frac{\sqrt{3}}{2}i
$$

---

### Solución final

$$
z=0
$$

$$
z=1
$$

$$
z=-\frac{1}{2}+\frac{\sqrt{3}}{2}i
$$

$$
z=-\frac{1}{2}-\frac{\sqrt{3}}{2}i
$$

---

# 21. Lugares geométricos

A veces, después de calcular raíces complejas, preguntan qué lugar geométrico describen.

Ideas básicas:

- Si todos tienen el mismo módulo, están en una circunferencia centrada en el origen.
- Si todos tienen el mismo argumento, están en una semirrecta.
- Si cumplen una condición de distancia a un punto, suele ser una circunferencia.

Ejemplo:

Si:

$$
|z|=2
$$

entonces los puntos están en la circunferencia:

$$
x^2+y^2=4
$$

centrada en el origen y de radio $2$.

---

# 22. Checklist del Tema 1

Antes del examen tengo que saber:

- [ ] Resolver desigualdades con valor absoluto.
- [ ] Resolver desigualdades con valor absoluto y fracciones.
- [ ] Expresar soluciones como intervalos.
- [ ] Decidir si un conjunto está acotado.
- [ ] Calcular $\sup(A)$ e $\inf(A)$.
- [ ] Saber cuándo existe máximo y mínimo.
- [ ] Calcular conjugados de complejos.
- [ ] Calcular módulos y argumentos.
- [ ] Pasar complejos a forma polar.
- [ ] Resolver raíces complejas.
- [ ] Usar que las raíces complejas de polinomios reales van por conjugadas.
- [ ] Igualar parte real e imaginaria cuando aparece $\overline{z}$.
- [ ] Reconocer lugares geométricos básicos.

---

# 23. Ejercicios tipo

## Ejercicio 1

Determinar:

$$
A=\{x \in \mathbb{R}: |x-3|-|x+3|<2x\}
$$

Estudiar si está acotado superior e inferiormente. Calcular supremo, ínfimo, máximo y mínimo si existen.

---

## Ejercicio 2

Determinar:

$$
A=\left\{x \in \mathbb{R}:\left|\frac{x+1}{x-2}\right|>2\right\}
$$

Estudiar si está acotado superior e inferiormente. Calcular supremo, ínfimo, máximo y mínimo si existen.

---

## Ejercicio 3

Resolver:

$$
z^2=\overline{z}
$$

---

## Ejercicio 4

Resolver:

$$
z^6+1-i=0
$$

Indicar qué lugar geométrico describen las soluciones.

---

## Ejercicio 5

Sea un polinomio cúbico:

$$
z^3+Az^2+Bz+26=0
$$

con $A,B \in \mathbb{R}$.

Sabiendo que $1+i$ es raíz, determinar las otras dos raíces.