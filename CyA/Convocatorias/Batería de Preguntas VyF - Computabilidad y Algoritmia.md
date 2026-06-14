### Conceptos Básicos, Alfabetos y Cadenas

**Pregunta:** La cadena vacía (ε) siempre pertenece a L⁺ para todo lenguaje L.
* **Respuesta:** Falso.
* **Explicación:** El cierre positivo (L⁺) es la concatenación de un lenguaje consigo mismo una o más veces. La cadena vacía solo pertenecerá a L⁺ si ε ya formaba parte del lenguaje L original.

**Pregunta:** ε pertenece a todos los alfabetos Σ.
* **Respuesta:** Falso.
* **Explicación:** ε representa la "cadena vacía" (longitud cero), no es un símbolo. Por definición, los alfabetos no contienen la cadena vacía. 

**Pregunta:** Todo alfabeto es un lenguaje.
* **Respuesta:** Verdadero.
* **Explicación:** Un alfabeto (Σ) es un conjunto de símbolos. Puede verse como un lenguaje formal básico donde todas las palabras tienen exactamente longitud 1.

**Pregunta:** El conjunto de todos los lenguajes posibles sobre un alfabeto Σ es infinito no numerable.
* **Respuesta:** Verdadero.
* **Explicación:** El conjunto de todas las cadenas posibles (Σ*) es infinito numerable. El conjunto de todos los lenguajes es el conjunto potencia de Σ* (todos sus subconjuntos posibles), lo cual, por el Teorema de Cantor, genera un conjunto infinito no numerable.

**Pregunta:** Σ* es siempre un conjunto infinito.
* **Respuesta:** Verdadero.
* **Explicación:** Siempre que el alfabeto no sea vacío (requisito formal), sus combinaciones de longitud arbitraria generan infinitas cadenas.

**Pregunta:** ∅* = {ε}. (Y su variante: ∅⁰ = {ε}).
* **Respuesta:** Verdadero.
* **Explicación:** Por definición, elevar cualquier lenguaje a la potencia 0 (incluido el conjunto vacío) resulta en el conjunto que contiene únicamente a la cadena vacía.

**Pregunta:** ∅⁰ = ∅.
* **Respuesta:** Falso.
* **Explicación:** Como se explica en la pregunta anterior, el resultado es {ε}, no el conjunto vacío.

**Pregunta:** Si L es un lenguaje, entonces siempre L* es distinto de L⁺.
* **Respuesta:** Falso.
* **Explicación:** Si el lenguaje original L ya contiene a la cadena vacía (ε), entonces L* = L⁺. No siempre son distintos.

**Pregunta:** Un lenguaje L cumple la condición L* = L⁺ si ε ∈ L.
* **Respuesta:** Verdadero.
* **Explicación:** Si la cadena vacía ya está en el lenguaje base, el cierre positivo (que obliga a concatenar al menos una vez) también generará la cadena vacía, igualando así al cierre de Kleene.

**Pregunta:** ¿Cuál de las siguientes opciones NO describe un lenguaje? (Opciones: Diccionario RAE, Racionales en decimal, Programas válidos en C).
* **Respuesta:** Los números racionales escritos en notación decimal.
* **Explicación:** Un lenguaje formal es un conjunto de cadenas finitas. La representación decimal de muchos racionales implica periodos infinitos, lo cual choca con la definición de cadena finita.

---

### Lenguajes Regulares y Autómatas (DFA/NFA)

**Pregunta:** Todo lenguaje con un número finito de palabras es regular. (Variante: Si L es un lenguaje finito, no puede ser independiente del contexto).
* **Respuesta:** Verdadero (a la primera) / Falso (a la variante).
* **Explicación:** Todo lenguaje finito es regular porque siempre se puede construir una expresión regular uniendo todas sus palabras mediante OR. Al ser regular, automáticamente también es independiente del contexto (por la jerarquía de Chomsky).

**Pregunta:** El lema del bombeo para lenguajes regulares es una herramienta que se utiliza para demostrar que un lenguaje es regular.
* **Respuesta:** Falso.
* **Explicación:** El lema del bombeo es una condición necesaria pero no suficiente. Se usa estrictamente por reducción al absurdo para demostrar que un lenguaje NO es regular.

**Pregunta:** Si un lenguaje no es regular, es posible que cumpla el lema del bombeo para lenguajes regulares.
* **Respuesta:** Verdadero.
* **Explicación:** Como el lema no es una condición suficiente, existen lenguajes que no son regulares pero que aun así cumplen las condiciones del lema.

**Pregunta:** Si L no cumple el lema del bombeo para lenguajes regulares, entonces L no es regular.
* **Respuesta:** Verdadero.
* **Explicación:** Es la aplicación lógica (contrapositiva) correcta del teorema. Si falla el lema, está garantizado que el lenguaje no es regular.

**Pregunta:** Todo autómata finito determinista (DFA) con |Q|=n y con |Σ|=m ha de tener m × n transiciones.
* **Respuesta:** Verdadero.
* **Explicación:** Por definición formal, un DFA debe tener exactamente una y solo una transición definida para cada estado y para cada símbolo del alfabeto.

**Pregunta:** Si M es un DFA con k estados que acepta una cadena de longitud ≥ k, entonces el lenguaje reconocido por M tiene un número infinito de cadenas.
* **Respuesta:** Verdadero.
* **Explicación:** Por el principio del palomar (base del Lema del Bombeo), procesar k o más símbolos en k estados significa que obligatoriamente se ha pasado por el mismo estado más de una vez, creando un ciclo que puede repetirse infinitas veces.

**Pregunta:** Hay lenguajes que puede aceptar un autómata finito no determinista (NFA) para los cuales no existe una gramática lineal por la izquierda que los genere.
* **Respuesta:** Falso.
* **Explicación:** Los NFA, los DFA y las gramáticas regulares (lineales por la izquierda o derecha) tienen exactamente el mismo poder expresivo: reconocen la familia de Lenguajes Regulares.

**Pregunta:** Todo lenguaje generado por una gramática lineal por la derecha es generado también por una gramática lineal por la izquierda.
* **Respuesta:** Verdadero.
* **Explicación:** Ambas definen formalmente los Lenguajes Regulares, por lo que son totalmente equivalentes.

**Pregunta:** Los lenguajes regulares son cerrados respecto a la intersección.
* **Respuesta:** Verdadero.
* **Explicación:** Si se interseccionan dos lenguajes regulares, el lenguaje resultante siempre será regular (demostrable mediante la construcción del autómata producto).

**Pregunta:** La concatenación de un lenguaje regular con su complementario es siempre regular.
* **Respuesta:** Verdadero.
* **Explicación:** Los lenguajes regulares son cerrados tanto bajo la operación de complemento como bajo la operación de concatenación.

**Pregunta:** El lenguaje L = { 0ⁿ 1ᵐ | m ≥ n } es regular.
* **Respuesta:** Falso.
* **Explicación:** Requiere llevar una cuenta de cuántos ceros han aparecido para asegurar que haya al menos la misma cantidad de unos. Los autómatas finitos no tienen memoria, se necesita un autómata a pila (LIC).

---

### Gramáticas y Lenguajes Independientes del Contexto (LIC)

**Pregunta:** El cierre de Kleene de un lenguaje independiente del contexto es siempre independiente del contexto.
* **Respuesta:** Verdadero.
* **Explicación:** Los LIC son cerrados bajo la unión, la concatenación y el cierre de Kleene (estrella).

**Pregunta:** Si L₁ y L₂ son lenguajes independientes del contexto, entonces L₁L₂ (su concatenación) también lo es.
* **Respuesta:** Verdadero.
* **Explicación:** Los LIC son cerrados respecto a la concatenación.

**Pregunta:** El resultado de concatenar un lenguaje regular con uno independiente del contexto es siempre independiente del contexto.
* **Respuesta:** Verdadero.
* **Explicación:** Todo lenguaje regular es también un LIC. La concatenación de dos LIC siempre da como resultado un LIC.

**Pregunta:** La intersección de un lenguaje regular con un lenguaje independiente del contexto es siempre un lenguaje regular.
* **Respuesta:** Falso.
* **Explicación:** La intersección de un Regular y un LIC da como resultado siempre un LIC. No se puede garantizar que el resultado vaya a ser regular.

**Pregunta:** Dada una gramática G, si G no es regular, L(G) no será regular.
* **Respuesta:** Falso.
* **Explicación:** Una gramática muy compleja o no regular puede generar un lenguaje extremadamente simple que sí sea regular (por ejemplo, una gramática libre de contexto que simplemente termine generando L = Σ*).

**Pregunta:** Una gramática regular es una gramática independiente del contexto expresada en Forma Normal de Chomsky.
* **Respuesta:** Falso.
* **Explicación:** La Forma Normal de Chomsky (FNC) es un estándar estructural para gramáticas independientes del contexto (producciones del tipo A → BC o A → a), no una definición de gramática regular.

**Pregunta:** El algoritmo CYK permite decidir si una cadena pertenece o no a un lenguaje generado por una gramática en Forma Normal de Chomsky.
* **Respuesta:** Verdadero.
* **Explicación:** El algoritmo Cocke-Younger-Kasami (CYK) está diseñado específicamente para resolver el problema de pertenencia en gramáticas libres de contexto que estén estrictamente en FNC.

---

### Máquinas de Turing, Decidibilidad y Computabilidad

**Pregunta:** La Tesis de Church-Turing es un teorema matemático que ha sido demostrado formalmente.
* **Respuesta:** Falso.
* **Explicación:** Es una tesis o hipótesis que afirma que todo lo que es intuitivamente computable puede ser computado por una Máquina de Turing. Como apela a un concepto intuitivo ("lo computable por un humano"), no puede demostrarse matemáticamente, aunque se acepta universalmente como cierta.

**Pregunta:** Un lenguaje es recursivo si existe una Máquina de Turing que acepta sus cadenas.
* **Respuesta:** Falso.
* **Explicación:** Que exista una máquina que "acepte" sus cadenas define a un lenguaje Recursivamente Enumerable. Para que sea Recursivo (decidible), la máquina debe estar garantizada a *parar* siempre (aceptando o rechazando), sin entrar en bucles infinitos.

**Pregunta:** Si L está especificado mediante una expresión regular, entonces L es recursivo.
* **Respuesta:** Verdadero.
* **Explicación:** Según la jerarquía de Chomsky, todo lenguaje Regular es Independiente del Contexto, y todo LIC es Recursivo (decidible por una máquina de Turing). Por transitividad, es verdadero.

**Pregunta:** Si L es independiente del contexto, entonces es recursivo. (Variante: entonces es recursivamente enumerable).
* **Respuesta:** Verdadero (para ambas).
* **Explicación:** Jerarquía de Chomsky: Todos los LIC son Recursivos (decidibles), y a su vez, todos los lenguajes Recursivos son Recursivamente Enumerables.

**Pregunta:** Si existe una Máquina de Turing que reconoce L, entonces L puede ser generado por una gramática independiente del contexto.
* **Respuesta:** Falso.
* **Explicación:** Las Máquinas de Turing reconocen lenguajes Recursivamente Enumerables. Esta familia es mucho más amplia e incluye lenguajes que las gramáticas independientes del contexto no pueden generar (como L = {aⁿ bⁿ cⁿ}).

**Pregunta:** Dados un lenguaje L y su complementario, es imposible que ambos sean recursivos.
* **Respuesta:** Falso.
* **Explicación:** Por definición de decidibilidad, si un lenguaje es recursivo, su complementario obligatoriamente también lo es.

**Pregunta:** Si L es independiente del contexto, entonces su complementario es recursivo.
* **Respuesta:** Verdadero.
* **Explicación:** Los LIC son recursivos. Como los lenguajes recursivos son cerrados respecto al complemento, el complementario de un LIC siempre será recursivo.

**Pregunta:** Si L es recursivamente enumerable, entonces Σ* - L (su complementario) es recursivamente enumerable.
* **Respuesta:** Falso.
* **Explicación:** La clase de lenguajes Recursivamente Enumerables NO es cerrada bajo complemento. Solo se cumple si L es además recursivo.

**Pregunta:** Si L₁ y L₂ son lenguajes recursivamente enumerables, entonces L₁ ∪ L₂ también lo es.
* **Respuesta:** Verdadero.
* **Explicación:** Los lenguajes Recursivamente Enumerables son cerrados respecto a la unión.

**Pregunta:** Una Máquina de Turing para cuando su cabeza de lectura/escritura alcanza el final de la cadena que se le suministra como entrada.
* **Respuesta:** Falso.
* **Explicación:** La cinta de una Máquina de Turing es infinita. La máquina solo se detiene cuando transita a un estado explícito de aceptación o a un estado de rechazo.

---

### Complejidad Algorítmica y Teorema Maestro

**Pregunta:** ¿Cuál de estos órdenes es menor? O(n³ log n³) o O(3n³ log n)
* **Respuesta:** Son del mismo orden.
* **Explicación:** Por las propiedades de los logaritmos, log(n³) equivale a 3 log n. Dado que en la notación asintótica Big-O las constantes se desprecian, O(3n³ log n) = O(n³ log n).

**Pregunta:** ¿Cuál de estos órdenes es menor? O(n¹²) o O(3n⁶·⁴ + 25n⁵·⁶)
* **Respuesta:** O(3n⁶·⁴ + 25n⁵·⁶) es el menor.
* **Explicación:** En un polinomio, el orden de crecimiento lo dicta el término de mayor grado. El crecimiento asintótico de n⁶·⁴ es inmensamente menor que el de n¹².

**Pregunta:** 5n + 8n² + 100n³ = O(n⁴)
* **Respuesta:** Verdadero.
* **Explicación:** La notación Big-O (O mayúscula) establece una cota superior. Dado que el grado máximo del polinomio es 3, la función crece asintóticamente más lento que n⁴, por lo que está acotada superiormente por O(n⁴).

**Pregunta:** Θ(n⁵ log n) < Θ(9n⁵ log n⁷)
* **Respuesta:** Falso.
* **Explicación:** Son exactamente del mismo orden. El log n⁷ es 7 log n. Al descartar las constantes (9 y 7), la parte derecha queda como Θ(n⁵ log n), igual que la izquierda.

**Pregunta:** Θ(9n² log n⁸) = Θ(√(9n²) log n⁸)
* **Respuesta:** Falso.
* **Explicación:** La parte izquierda es Θ(n² log n). En la parte derecha, la raíz cuadrada convierte √(9n²) en 3n, quedando Θ(n log n). Tienen distinta tasa de crecimiento.

**Pregunta:** T(n) = 2T(n/4) + 1 = Θ(√n)
* **Respuesta:** Verdadero.
* **Explicación:** Aplicando el Teorema Maestro: a=2, b=4. Calculamos log₄(2) = 1/2. Comparamos n^(1/2) (que es √n) con f(n) = 1. Como √n > 1, estamos en el Caso 1 del teorema, y la complejidad es Θ(n^(log_b a)) = Θ(√n).

**Pregunta:** T(n) = 16T(n/4) + √n = Θ(n²)
* **Respuesta:** Verdadero.
* **Explicación:** Teorema Maestro: a=16, b=4. log₄(16) = 2. Comparamos n² con f(n) = n^(1/2). Como n² > n^(1/2), aplica el Caso 1, por lo que la complejidad manda y el resultado es Θ(n²).

**Pregunta:** T(n) = 16T(n/4) + n = Θ(n)
* **Respuesta:** Falso.
* **Explicación:** Igual que el anterior (a=16, b=4), el logaritmo da 2. Comparamos n² con f(n)=n. Gana n², por lo que la complejidad real es Θ(n²), no Θ(n).

**Pregunta:** T(n) = 2T(n/4) + 1,  T(n) = Θ(log n).
* **Respuesta:** Falso.
* **Explicación:** Como se calculó anteriormente, la complejidad real aplicando el Teorema Maestro es Θ(√n), no logarítmica.

**Pregunta:** La complejidad del siguiente bloque de código es Θ(n² log n):
```cpp
int suma = 0;
for (int x = 1; x <= n; x++)
  for (int y = 1; y <= n; y *= 2)
    for (int z = 1; z <= y; z++)
      suma++;
```
- **Respuesta:** Falso.
    
- **Explicación:** El bucle interior `z` se ejecuta `y` veces. El bucle `y` suma las potencias de 2 (1+2+4+...+n), lo que da como resultado O(n). El bucle `x` exterior se repite `n` veces. Al multiplicar, n * O(n) da como resultado una complejidad exacta de Θ(n²).


**Pregunta:** La complejidad del siguiente bloque de código es Θ(n³):
```cpp
int suma = 0;
for (int i = 1; i <= n; i++)
  for (int j = 1; j <= n; j *= 2)
    for (int k = 1; k <= j; k++)
      suma++;
```
- **Respuesta:** Falso.
    
- **Explicación:** Es exactamente el mismo bucle de la pregunta anterior con distintos nombres de variables. Su complejidad es Θ(n²), no cúbica.


**Pregunta:** La complejidad del siguiente bloque de código es Θ(n³):
```cpp
int suma = 0;
for (int a = 1; a <= n; a++)
  for (int b = 1; b <= n; b++)
    for (int c = 1; c <= b; c++)
      suma++;
```
- **Respuesta:** Verdadero.
    
- **Explicación:** El bucle `c` se ejecuta `b` veces. El bucle `b` se ejecuta de 1 a `n`. La suma de 1 a `n` es n(n+1)/2, lo que equivale a O(n²). El bucle exterior `a` itera `n` veces multiplicando ese costo. n * O(n²) resulta en una complejidad global de Θ(n³).

**Pregunta:** La complejidad del siguiente bloque de código es Θ(n):
```cpp
int suma = 0;
for (int i = 1; i <= n; i *= 2)
  for (int j = 1; j <= n; j++)
    suma++;
```
- **Respuesta:** Falso.
    
- **Explicación:** El bucle exterior `i` se multiplica por 2 en cada paso, por lo que se ejecuta log(n) veces. El bucle interior `j` va de 1 a `n` linealmente (n veces). Se multiplican ambos bucles, resultando en una complejidad exacta de Θ(n log n).