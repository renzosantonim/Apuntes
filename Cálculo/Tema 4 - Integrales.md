## 1. Idea de integral

La integral indefinida sirve para encontrar primitivas.

Una primitiva de una función $f(x)$ es otra función $F(x)$ tal que:

$$
F'(x)=f(x)
$$

Se escribe:

$$
\int f(x)\,dx = F(x)+C
$$

donde $C$ es la constante de integración.

Ejemplo:

$$
\int 2x\,dx=x^2+C
$$

porque:

$$
(x^2)'=2x
$$

---

# 2. Integrales inmediatas

Conviene saberse estas de memoria.

| Integral | Resultado |
|---|---|
| $\int x^n\,dx$ | $\frac{x^{n+1}}{n+1}+C$, si $n\neq -1$ |
| $\int \frac{1}{x}\,dx$ | $\ln|x|+C$ |
| $\int e^x\,dx$ | $e^x+C$ |
| $\int a^x\,dx$ | $\frac{a^x}{\ln a}+C$ |
| $\int \sin x\,dx$ | $-\cos x+C$ |
| $\int \cos x\,dx$ | $\sin x+C$ |
| $\int \frac{1}{1+x^2}\,dx$ | $\arctan x+C$ |
| $\int \frac{1}{\sqrt{1-x^2}}\,dx$ | $\arcsin x+C$ |

---

## 3. Regla de la potencia

Si $n\neq -1$:

$$
\int x^n\,dx=\frac{x^{n+1}}{n+1}+C
$$

Ejemplos:

$$
\int x^3\,dx=\frac{x^4}{4}+C
$$

$$
\int \sqrt{x}\,dx=\int x^{1/2}\,dx=\frac{x^{3/2}}{3/2}+C
$$

Por tanto:

$$
\int \sqrt{x}\,dx=\frac{2}{3}x^{3/2}+C
$$

---

## 4. Cuidado con $\int \frac{1}{x}\,dx$

La regla de la potencia no se puede usar cuando $n=-1$.

En ese caso:

$$
\int \frac{1}{x}\,dx=\ln|x|+C
$$

No es:

$$
\frac{x^0}{0}
$$

Eso no tiene sentido.

---

# 5. Integral definida

La integral definida entre $a$ y $b$ se escribe:

$$
\int_a^b f(x)\,dx
$$

Se calcula usando una primitiva $F(x)$:

$$
\int_a^b f(x)\,dx=F(b)-F(a)
$$

Esto se conoce como la Regla de Barrow.

---

## 6. Ejemplo de integral definida

Calcular:

$$
\int_0^2 x^2\,dx
$$

Una primitiva de $x^2$ es:

$$
F(x)=\frac{x^3}{3}
$$

Entonces:

$$
\int_0^2 x^2\,dx=
\left[\frac{x^3}{3}\right]_0^2
$$

$$
=
\frac{2^3}{3}-\frac{0^3}{3}
$$

$$
=
\frac{8}{3}
$$

---

# 7. Propiedades básicas

## Linealidad

$$
\int (f(x)+g(x))\,dx=
\int f(x)\,dx+\int g(x)\,dx
$$

$$
\int kf(x)\,dx=k\int f(x)\,dx
$$

Ejemplo:

$$
\int (3x^2+2x)\,dx
=
3\int x^2\,dx+2\int x\,dx
$$

$$
=x^3+x^2+C
$$

---

## Cambio de límites

$$
\int_a^b f(x)\,dx=-\int_b^a f(x)\,dx
$$

---

## Integral en un punto

$$
\int_a^a f(x)\,dx=0
$$

---

# 8. Cambio de variable

El cambio de variable se usa cuando aparece una función compuesta y su derivada.

La idea es tomar:

$$
u=g(x)
$$

Entonces:

$$
du=g'(x)\,dx
$$

---

## 9. Método de cambio de variable

1. Elegir una parte de la integral como $u$.
2. Calcular $du$.
3. Sustituir todo en función de $u$.
4. Integrar.
5. Volver a la variable $x$.

---

## 10. Ejemplo de cambio de variable

Calcular:

$$
\int 2x e^{x^2}\,dx
$$

Tomamos:

$$
u=x^2
$$

Entonces:

$$
du=2x\,dx
$$

La integral queda:

$$
\int e^u\,du
$$

Por tanto:

$$
\int e^u\,du=e^u+C
$$

Volvemos a $x$:

$$
e^{x^2}+C
$$

Así:

$$
\int 2x e^{x^2}\,dx=e^{x^2}+C
$$

---

# 11. Integrales con logaritmo por cambio de variable

Si aparece algo de la forma:

$$
\int \frac{f'(x)}{f(x)}\,dx
$$

entonces:

$$
\int \frac{f'(x)}{f(x)}\,dx=\ln|f(x)|+C
$$

Ejemplo:

$$
\int \frac{2x}{x^2+1}\,dx
$$

Tomamos:

$$
u=x^2+1
$$

Entonces:

$$
du=2x\,dx
$$

Por tanto:

$$
\int \frac{2x}{x^2+1}\,dx
=
\ln|x^2+1|+C
$$

Como $x^2+1>0$, también podemos escribir:

$$
\ln(x^2+1)+C
$$

---

# 12. Integración por partes

La integración por partes se usa cuando aparece un producto de funciones.

La fórmula es:

$$
\int u\,dv=uv-\int v\,du
$$

Suele usarse con productos como:

- polinomio por exponencial;
- polinomio por trigonométrica;
- logaritmo;
- arco tangente.

---

## 13. Cómo elegir $u$

Una regla útil es elegir como $u$ la función que se simplifica al derivar.

Prioridad típica:

1. Logarítmicas: $\ln x$
2. Inversas trigonométricas: $\arctan x$, $\arcsin x$
3. Algebraicas: $x$, $x^2$, etc.
4. Trigonométricas: $\sin x$, $\cos x$
5. Exponenciales: $e^x$

---

## 14. Ejemplo de integración por partes

Calcular:

$$
\int x e^x\,dx
$$

Elegimos:

$$
u=x
$$

$$
dv=e^x\,dx
$$

Entonces:

$$
du=dx
$$

$$
v=e^x
$$

Aplicamos:

$$
\int u\,dv=uv-\int v\,du
$$

$$
\int x e^x\,dx=xe^x-\int e^x\,dx
$$

$$
=xe^x-e^x+C
$$

Sacando factor común:

$$
\int x e^x\,dx=e^x(x-1)+C
$$

---

# 15. Ejemplo con logaritmo

Calcular:

$$
\int \ln x\,dx
$$

Aquí no parece un producto, pero podemos escribir:

$$
\ln x = \ln x \cdot 1
$$

Elegimos:

$$
u=\ln x
$$

$$
dv=dx
$$

Entonces:

$$
du=\frac{1}{x}\,dx
$$

$$
v=x
$$

Aplicamos por partes:

$$
\int \ln x\,dx=x\ln x-\int x\frac{1}{x}\,dx
$$

$$
=x\ln x-\int 1\,dx
$$

$$
=x\ln x-x+C
$$

---

# 16. Integrales racionales

Una integral racional es una integral donde aparece un cociente de polinomios:

$$
\int \frac{P(x)}{Q(x)}\,dx
$$

Ejemplo:

$$
\int \frac{x}{x^4-1}\,dx
$$

Este tipo ha aparecido en exámenes.

---

## 17. Método general para racionales

1. Si el grado del numerador es mayor o igual que el del denominador, hacer división de polinomios.
2. Factorizar el denominador.
3. Intentar cambio de variable si aparece algo parecido a la derivada del denominador.
4. Si no, descomponer en fracciones simples.

---

# 18. Ejemplo tipo examen

Calcular:

$$
\int \frac{x}{x^4-1}\,dx
$$

Observamos que:

$$
x^4-1=(x^2-1)(x^2+1)
$$

También podemos hacer un cambio útil:

$$
u=x^2
$$

Entonces:

$$
du=2x\,dx
$$

Por tanto:

$$
x\,dx=\frac{1}{2}du
$$

Además:

$$
x^4-1=(x^2)^2-1=u^2-1
$$

La integral queda:

$$
\int \frac{x}{x^4-1}\,dx
=
\frac{1}{2}\int \frac{1}{u^2-1}\,du
$$

Factorizamos:

$$
u^2-1=(u-1)(u+1)
$$

Descomponemos:

$$
\frac{1}{u^2-1}
=
\frac{A}{u-1}+\frac{B}{u+1}
$$

Multiplicamos por $(u-1)(u+1)$:

$$
1=A(u+1)+B(u-1)
$$

Sustituimos $u=1$:

$$
1=2A
$$

$$
A=\frac{1}{2}
$$

Sustituimos $u=-1$:

$$
1=-2B
$$

$$
B=-\frac{1}{2}
$$

Entonces:

$$
\frac{1}{u^2-1}
=
\frac{1}{2}\frac{1}{u-1}
-
\frac{1}{2}\frac{1}{u+1}
$$

La integral queda:

$$
\frac{1}{2}\int \frac{1}{u^2-1}\,du
=
\frac{1}{2}\int
\left(
\frac{1}{2}\frac{1}{u-1}
-
\frac{1}{2}\frac{1}{u+1}
\right)du
$$

$$
=
\frac{1}{4}\ln|u-1|-\frac{1}{4}\ln|u+1|+C
$$

Volvemos a $x$:

$$
=
\frac{1}{4}\ln|x^2-1|
-
\frac{1}{4}\ln|x^2+1|
+C
$$

Como $x^2+1>0$:

$$
\int \frac{x}{x^4-1}\,dx
=
\frac{1}{4}\ln\left|\frac{x^2-1}{x^2+1}\right|+C
$$

---

# 19. Integrales trigonométricas básicas

Conviene recordar:

$$
\int \sin x\,dx=-\cos x+C
$$

$$
\int \cos x\,dx=\sin x+C
$$

$$
\int \tan x\,dx=-\ln|\cos x|+C
$$

También:

$$
\int \sin(ax)\,dx=-\frac{1}{a}\cos(ax)+C
$$

$$
\int \cos(ax)\,dx=\frac{1}{a}\sin(ax)+C
$$

---

# 20. Integrales con $\ln(x)$ y trigonométricas

A veces aparecen integrales como:

$$
\int (1+x)\sin(\ln x)\,dx
$$

La clave es detectar que aparece $\ln x$ dentro de una trigonométrica.

Una estrategia habitual es usar cambio:

$$
t=\ln x
$$

Entonces:

$$
x=e^t
$$

y:

$$
dx=e^t\,dt
$$

Este tipo puede complicarse, así que lo importante es reconocer que no es inmediata y que seguramente requiere cambio de variable y/o partes.

---

# 21. Área bajo una curva

Si $f(x)\geq 0$ en $[a,b]$, el área bajo la curva es:

$$
A=\int_a^b f(x)\,dx
$$

Ejemplo:

Área bajo $y=x^2$ entre $x=0$ y $x=2$:

$$
A=\int_0^2 x^2\,dx
$$

$$
A=\frac{8}{3}
$$

---

# 22. Área entre dos curvas

Si tenemos dos curvas:

$$
y=f(x)
$$

y:

$$
y=g(x)
$$

el área entre ellas es:

$$
A=\int_a^b |\text{arriba} - \text{abajo}|\,dx
$$

Si sabemos que $f(x)\geq g(x)$ en $[a,b]$:

$$
A=\int_a^b (f(x)-g(x))\,dx
$$

---

## 23. Método para áreas entre curvas

1. Hallar los puntos de corte resolviendo:

$$
f(x)=g(x)
$$

2. Determinar cuál función está arriba.
3. Plantear:

$$
A=\int_a^b (\text{arriba}-\text{abajo})\,dx
$$

4. Calcular la integral definida.

---

## 24. Ejemplo de área entre curvas

Calcular el área entre:

$$
y=x
$$

y:

$$
y=x^2
$$

Puntos de corte:

$$
x=x^2
$$

$$
x^2-x=0
$$

$$
x(x-1)=0
$$

Por tanto:

$$
x=0, \qquad x=1
$$

En $[0,1]$, la función de arriba es:

$$
y=x
$$

y la de abajo:

$$
y=x^2
$$

Área:

$$
A=\int_0^1 (x-x^2)\,dx
$$

$$
A=\left[\frac{x^2}{2}-\frac{x^3}{3}\right]_0^1
$$

$$
A=\frac{1}{2}-\frac{1}{3}
$$

$$
A=\frac{1}{6}
$$

---

# 25. Volúmenes de revolución

Los volúmenes de revolución son de lo más importante del tema.

Aparecen cuando una región del plano gira alrededor de un eje.

En los exámenes suelen pedir giros alrededor de:

- eje $OX$;
- eje $OY$.

---

# 26. Giro alrededor del eje $OX$

Si una región bajo la curva:

$$
y=f(x)
$$

entre $x=a$ y $x=b$ gira alrededor del eje $OX$, el volumen es:

$$
V=\pi \int_a^b [f(x)]^2\,dx
$$

Esto se llama método de discos.

---

## 27. Ejemplo giro alrededor de $OX$

Calcular el volumen generado al girar alrededor del eje $OX$ la región bajo:

$$
y=x^2
$$

entre:

$$
x=0
$$

y:

$$
x=2
$$

Usamos:

$$
V=\pi \int_0^2 (x^2)^2\,dx
$$

$$
V=\pi \int_0^2 x^4\,dx
$$

$$
V=\pi \left[\frac{x^5}{5}\right]_0^2
$$

$$
V=\pi \frac{32}{5}
$$

Por tanto:

$$
V=\frac{32\pi}{5}
$$

---

# 28. Giro alrededor del eje $OX$ con dos curvas

Si la región está entre dos curvas:

$$
y=f(x)
$$

y:

$$
y=g(x)
$$

y gira alrededor de $OX$, usamos arandelas:

$$
V=\pi \int_a^b \left(R(x)^2-r(x)^2\right)\,dx
$$

donde:

- $R(x)$ es el radio exterior;
- $r(x)$ es el radio interior.

Normalmente:

$$
R(x)=\text{función de arriba}
$$

$$
r(x)=\text{función de abajo}
$$

si ambas están por encima del eje $X$.

---

## 29. Ejemplo con dos curvas alrededor de $OX$

Región limitada por:

$$
y=x^2
$$

$$
y=-x^2+2
$$

y:

$$
y=0
$$

girando alrededor de $OX$.

Primero vemos los puntos de corte relevantes.

Las curvas $y=x^2$ y $y=-x^2+2$ se cortan cuando:

$$
x^2=-x^2+2
$$

$$
2x^2=2
$$

$$
x^2=1
$$

$$
x=\pm 1
$$

La región con $y=0$ queda entre:

$$
x=-\sqrt{2}
$$

y:

$$
x=\sqrt{2}
$$

pero se parte en tramos.

Para este tipo de ejercicios, lo más importante es dibujar o razonar qué curva está arriba y qué curva limita la región.

Si la región gira alrededor de $OX$, se usa:

$$
V=\pi\int (R^2-r^2)\,dx
$$

partiendo en intervalos si cambia la curva exterior o interior.

---

# 30. Giro alrededor del eje $OY$

Para girar alrededor del eje $OY$ hay dos métodos habituales:

1. Método de capas cilíndricas, integrando respecto de $x$.
2. Método de discos/arandelas, integrando respecto de $y$.

En los exámenes suele ser más cómodo usar capas cilíndricas cuando la función está dada como $y=f(x)$.

---

# 31. Capas cilíndricas alrededor de $OY$

Si una región bajo:

$$
y=f(x)
$$

entre $x=a$ y $x=b$ gira alrededor del eje $OY$, el volumen es:

$$
V=2\pi \int_a^b x f(x)\,dx
$$

Aquí:

- $x$ es el radio de la capa;
- $f(x)$ es la altura de la capa.

---

## 32. Ejemplo giro alrededor de $OY$

Calcular el volumen generado al girar alrededor de $OY$ la región bajo:

$$
y=x^2
$$

entre:

$$
x=0
$$

y:

$$
x=2
$$

Usamos capas cilíndricas:

$$
V=2\pi \int_0^2 x(x^2)\,dx
$$

$$
V=2\pi \int_0^2 x^3\,dx
$$

$$
V=2\pi \left[\frac{x^4}{4}\right]_0^2
$$

$$
V=2\pi \cdot \frac{16}{4}
$$

$$
V=8\pi
$$

---

# 33. Comparación rápida: giro alrededor de $OX$ y $OY$

Para una región bajo $y=f(x)$ entre $x=a$ y $x=b$:

## Al girar alrededor de $OX$

$$
V=\pi \int_a^b [f(x)]^2\,dx
$$

## Al girar alrededor de $OY$

$$
V=2\pi \int_a^b x f(x)\,dx
$$

si usamos capas cilíndricas.

---

# 34. Volumen entre curva y eje $X$

Si la región está comprendida entre:

$$
y=f(x)
$$

y el eje $X$, entre $x=a$ y $x=b$, entonces:

## Giro alrededor de $OX$

$$
V_{OX}=\pi\int_a^b [f(x)]^2\,dx
$$

## Giro alrededor de $OY$

$$
V_{OY}=2\pi\int_a^b x f(x)\,dx
$$

si $a\geq 0$.

---

## 35. Ejemplo tipo examen

La región comprendida entre:

$$
y=x^3
$$

y el eje $X$, entre:

$$
x=2
$$

y:

$$
x=5
$$

gira alrededor del eje $OX$.

Calculamos:

$$
V_{OX}=\pi\int_2^5 (x^3)^2\,dx
$$

$$
V_{OX}=\pi\int_2^5 x^6\,dx
$$

$$
V_{OX}=\pi\left[\frac{x^7}{7}\right]_2^5
$$

$$
V_{OX}=\frac{\pi}{7}(5^7-2^7)
$$

---

## 36. El mismo ejemplo alrededor de $OY$

Ahora gira alrededor de $OY$.

Usamos capas cilíndricas:

$$
V_{OY}=2\pi\int_2^5 x(x^3)\,dx
$$

$$
V_{OY}=2\pi\int_2^5 x^4\,dx
$$

$$
V_{OY}=2\pi\left[\frac{x^5}{5}\right]_2^5
$$

$$
V_{OY}=\frac{2\pi}{5}(5^5-2^5)
$$

---

# 37. Volumen entre dos curvas alrededor de $OY$

Si la región está entre:

$$
y=f(x)
$$

y:

$$
y=g(x)
$$

y gira alrededor de $OY$, usando capas cilíndricas:

$$
V=2\pi\int_a^b x(\text{altura})\,dx
$$

donde:

$$
\text{altura}=\text{función de arriba}-\text{función de abajo}
$$

Por tanto:

$$
V=2\pi\int_a^b x(f(x)-g(x))\,dx
$$

si $f(x)\geq g(x)$ en $[a,b]$.

---

# 38. Cuidado con giros alrededor de $OY$

El método de capas:

$$
V=2\pi\int_a^b x f(x)\,dx
$$

funciona directamente cuando la región está a la derecha del eje $OY$, es decir, cuando $x\geq 0$.

Si la región está en valores negativos de $x$, el radio es:

$$
|x|
$$

porque una distancia no puede ser negativa.

En ejercicios de examen suelen elegir intervalos positivos o regiones simétricas para evitar complicaciones, pero hay que estar atento.

---

# 39. Longitud de arco

Aunque no parece lo más prioritario para este año, ha aparecido en exámenes antiguos.

La longitud de arco de una curva:

$$
y=f(x)
$$

entre $x=a$ y $x=b$ es:

$$
L=\int_a^b \sqrt{1+[f'(x)]^2}\,dx
$$

---

## 40. Método para longitud de arco

1. Derivar la función.
2. Calcular $[f'(x)]^2$.
3. Sustituir en:

$$
L=\int_a^b \sqrt{1+[f'(x)]^2}\,dx
$$

4. Simplificar la raíz si es posible.
5. Integrar.

Este tipo suele estar preparado para que la raíz se simplifique.

---

# 41. Integrales impropias

Una integral impropia aparece cuando:

- el intervalo es infinito;
- la función tiene una discontinuidad infinita en el intervalo.

Ejemplo con intervalo infinito:

$$
\int_1^{+\infty} \frac{1}{x^2}\,dx
$$

Se calcula como límite:

$$
\int_1^{+\infty} \frac{1}{x^2}\,dx
=
\lim_{b\to+\infty}\int_1^b \frac{1}{x^2}\,dx
$$

No parecen ser lo más importante para este examen, pero conviene reconocerlas.

---

# 42. Errores frecuentes

## Error 1: olvidar la constante $C$

En integrales indefinidas siempre hay que poner:

$$
+C
$$

Ejemplo:

$$
\int 2x\,dx=x^2+C
$$

---

## Error 2: usar mal la regla de la potencia

La fórmula:

$$
\int x^n\,dx=\frac{x^{n+1}}{n+1}+C
$$

no sirve para $n=-1$.

Para $n=-1$:

$$
\int \frac{1}{x}\,dx=\ln|x|+C
$$

---

## Error 3: olvidar el valor absoluto en logaritmos

En general:

$$
\int \frac{1}{x}\,dx=\ln|x|+C
$$

y:

$$
\int \frac{f'(x)}{f(x)}\,dx=\ln|f(x)|+C
$$

---

## Error 4: confundir área con integral

Si la función es negativa, la integral definida puede ser negativa, pero el área siempre es positiva.

Para áreas:

$$
A=\int_a^b |\text{función}|\,dx
$$

o:

$$
A=\int_a^b (\text{arriba}-\text{abajo})\,dx
$$

---

## Error 5: olvidar elevar al cuadrado en volúmenes alrededor de $OX$

Para giro alrededor de $OX$:

$$
V=\pi\int_a^b [f(x)]^2\,dx
$$

No es:

$$
V=\pi\int_a^b f(x)\,dx
$$

---

## Error 6: confundir giro alrededor de $OX$ y de $OY$

Alrededor de $OX$:

$$
V=\pi\int_a^b [f(x)]^2\,dx
$$

Alrededor de $OY$, usando capas:

$$
V=2\pi\int_a^b x f(x)\,dx
$$

---

## Error 7: no partir la región en tramos

Si la curva superior cambia, o si la región tiene varias partes, hay que partir la integral.

---

# 43. Checklist del Tema 4

Antes del examen tengo que saber:

- [ ] Calcular integrales inmediatas.
- [ ] Usar la regla de la potencia.
- [ ] Recordar que $\int \frac{1}{x}\,dx=\ln|x|+C$.
- [ ] Aplicar cambio de variable.
- [ ] Aplicar integración por partes.
- [ ] Resolver racionales sencillas.
- [ ] Factorizar denominadores.
- [ ] Usar fracciones simples básicas.
- [ ] Calcular integrales definidas con Barrow.
- [ ] Calcular áreas bajo una curva.
- [ ] Calcular áreas entre dos curvas.
- [ ] Hallar puntos de corte.
- [ ] Plantear volúmenes alrededor de $OX$.
- [ ] Plantear volúmenes alrededor de $OY$.
- [ ] Usar discos, arandelas o capas cilíndricas.
- [ ] Distinguir cuándo hay que partir en tramos.
- [ ] No olvidar unidades cúbicas en volúmenes.

---

# 44. Ejercicios tipo

## Ejercicio 1

Calcular:

$$
\int \frac{x}{x^4-1}\,dx
$$

---

## Ejercicio 2

Calcular:

$$
\int 2x e^{x^2}\,dx
$$

---

## Ejercicio 3

Calcular:

$$
\int x e^x\,dx
$$

---

## Ejercicio 4

Calcular el área limitada por:

$$
y=x
$$

y:

$$
y=x^2
$$

---

## Ejercicio 5

La región comprendida entre la curva:

$$
y=x^2
$$

y el eje $X$, entre:

$$
x=0
$$

y:

$$
x=2
$$

gira alrededor del eje $OX$.

Calcular el volumen generado.

---

## Ejercicio 6

La misma región del ejercicio anterior gira alrededor del eje $OY$.

Calcular el volumen generado.

---

## Ejercicio 7

La región comprendida entre:

$$
y=x^3
$$

y el eje $X$, entre:

$$
x=2
$$

y:

$$
x=5
$$

gira alrededor del eje $OX$.

Calcular el volumen.

Después calcular el volumen si gira alrededor del eje $OY$.

---

## Ejercicio 8

Calcular el volumen del sólido al girar alrededor del eje $OX$ la región comprendida entre:

$$
y=x^2
$$

$$
y=-x^2+2
$$

y:

$$
y=0
$$

---

# 45. Resumen final de fórmulas clave

## Integrales

$$
\int x^n\,dx=\frac{x^{n+1}}{n+1}+C
$$

$$
\int \frac{1}{x}\,dx=\ln|x|+C
$$

$$
\int e^x\,dx=e^x+C
$$

$$
\int \sin x\,dx=-\cos x+C
$$

$$
\int \cos x\,dx=\sin x+C
$$

---

## Barrow

$$
\int_a^b f(x)\,dx=F(b)-F(a)
$$

---

## Cambio de variable

$$
u=g(x)
$$

$$
du=g'(x)\,dx
$$

---

## Integración por partes

$$
\int u\,dv=uv-\int v\,du
$$

---

## Área entre curvas

$$
A=\int_a^b (\text{arriba}-\text{abajo})\,dx
$$

---

## Volumen alrededor de $OX$

$$
V=\pi\int_a^b [f(x)]^2\,dx
$$

---

## Volumen alrededor de $OX$ con dos curvas

$$
V=\pi\int_a^b (R(x)^2-r(x)^2)\,dx
$$

---

## Volumen alrededor de $OY$ por capas

$$
V=2\pi\int_a^b x f(x)\,dx
$$

---

## Volumen alrededor de $OY$ entre dos curvas

$$
V=2\pi\int_a^b x(\text{arriba}-\text{abajo})\,dx
$$

---

## Longitud de arco

$$
L=\int_a^b \sqrt{1+[f'(x)]^2}\,dx
$$