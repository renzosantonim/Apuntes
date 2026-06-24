
## 1. Sistemas combinacionales y sistemas secuenciales

En Sistemas Electrónicos Digitales hay dos grandes familias de circuitos:

- **Circuitos combinacionales**
    
- **Circuitos secuenciales**
    

Un **circuito combinacional** es aquel cuya salida depende solamente de las entradas actuales.

Por ejemplo:

$$  
F = A \cdot B + C  
$$

Si cambian (A), (B) o (C), cambia (F). No hay memoria. No importa qué ocurrió antes.

Ejemplos típicos de circuitos combinacionales:

- Puertas lógicas
    
- Multiplexores
    
- Decodificadores
    
- Codificadores
    
- Comparadores
    
- Sumadores
    
- Visualizadores
    
- Decodificadores de 7 segmentos


Un **circuito secuencial** es aquel cuya salida depende de las entradas actuales y también del estado anterior del circuito.

Por ejemplo, un contador no solo depende del reloj, sino también del número en el que estaba antes. Si estaba en 3, pasa a 4. Si estaba en 9, puede pasar a 0 o quedarse en 9, según el diseño.

Ejemplos típicos de circuitos secuenciales:

- Biestables
    
- Registros
    
- Contadores
    
- Máquinas de estados
    
- Detectores de secuencia
    
- Cronogramas temporales

Frase clave:

**Combinacional: salida = función de entradas.**

**Secuencial: salida = función de entradas + memoria/estado.**

---

## 2. Variables lógicas y puertas básicas

Las variables lógicas solo pueden valer 0 o 1.

Normalmente:

$$  
0 = falso / apagado / nivel bajo  
$$

$$  
1 = verdadero / encendido / nivel alto  
$$

Pero cuidado: en algunos ejercicios las salidas o entradas pueden ser **activas a nivel bajo**. Eso significa que el valor activo no es 1, sino 0.

Esto es muy importante en:

- Displays de 7 segmentos
    
- Reset
    
- Preset
    
- Algunos decodificadores
    

---

## 3. Puerta NOT

La puerta NOT invierte la señal.

$$  
\overline{A}  
$$

Tabla:

|A|NOT A|
|---|---|
|0|1|
|1|0|

Si (A = 0), entonces:

$$  
\overline{A}=1  
$$

Si (A = 1), entonces:

$$  
\overline{A}=0  
$$

---

## 4. Puerta AND

La puerta AND vale 1 solamente si todas sus entradas valen 1.

$$  
A \cdot B  
$$

Tabla:

|A|B|A · B|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

---

## 5. Puerta OR

La puerta OR vale 1 si al menos una entrada vale 1.

$$  
A + B  
$$

Tabla:

|A|B|A + B|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

---

## 6. Puerta NAND

La puerta NAND es una AND negada.

$$  
\overline{A \cdot B}  
$$

Tabla:

|A|B|NAND|
|---|---|---|
|0|0|1|
|0|1|1|
|1|0|1|
|1|1|0|

Vale 0 solo cuando todas sus entradas valen 1.

Las puertas NAND son muy importantes porque son **universales**, es decir, con solo puertas NAND se puede construir cualquier función lógica.

---

## 7. Puerta NOR

La puerta NOR es una OR negada.

$$  
\overline{A + B}  
$$

Tabla:

|A|B|NOR|
|---|---|---|
|0|0|1|
|0|1|0|
|1|0|0|
|1|1|0|

Vale 1 solo cuando todas sus entradas valen 0.

Las puertas NOR también son **universales**.

---

## 8. Puerta XOR

La puerta XOR vale 1 cuando las entradas son distintas.

$$  
A \oplus B  
$$

Tabla:

|A|B|A ⊕ B|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

La XOR se usa mucho para detectar diferencias, cambios o conmutaciones.

Por ejemplo, en biestables tipo T:

$$  
T = Q \oplus Q^+  
$$

donde:

- (Q) es el estado actual.
    
- (Q^+) es el estado siguiente.
    

---

## 9. Tabla de verdad

Una tabla de verdad enumera todas las combinaciones posibles de entradas y muestra la salida para cada una.

Si tienes (n) variables, hay:

$$  
2^n  
$$

combinaciones.

Por ejemplo, con 3 variables (A), (B) y (C):

$$  
2^3 = 8  
$$

combinaciones.

|A|B|C|
|---|---|---|
|0|0|0|
|0|0|1|
|0|1|0|
|0|1|1|
|1|0|0|
|1|0|1|
|1|1|0|
|1|1|1|

El orden habitual es contar en binario, considerando normalmente la variable de la izquierda como la más significativa.

Por ejemplo, si las variables son:

$$  
x_3, x_2, x_1, x_0  
$$

entonces:

$$  
x_3x_2x_1x_0 = 0000 \rightarrow 0  
$$

$$  
x_3x_2x_1x_0 = 0101 \rightarrow 5  
$$

$$  
x_3x_2x_1x_0 = 1111 \rightarrow 15  
$$

Esto es esencial para:

- Minitérminos
    
- Maxitérminos
    
- Decodificadores
    
- Mapas de Karnaugh
    
- Multiplexores
    
- Displays de 7 segmentos
    

---

## 10. Minitérminos

Un **minitérmino** es un producto AND que representa una fila concreta de la tabla donde la función vale 1.

Por ejemplo, para tres variables (A), (B), (C), la combinación:

$$  
A=0,\ B=1,\ C=0  
$$

corresponde al binario:

$$  
010  
$$

Es decir, al índice 2.

El minitérmino sería:

$$  
\overline{A}B\overline{C}  
$$

Regla para minitérminos:

- Si la variable vale 1, aparece normal.
    
- Si la variable vale 0, aparece negada.
    

Ejemplo:

Si una función vale 1 en las filas 1, 3 y 6, se escribe:

$$  
F(A,B,C)=\sum m(1,3,6)  
$$

Eso significa “suma de minitérminos”.

---

## 11. Maxitérminos

Un **maxitérmino** representa una fila donde la función vale 0.

Se usa para escribir la función como producto de sumas.

Si una función vale 0 en las filas 0, 2, 5 y 7:

$$  
F(A,B,C)=\prod M(0,2,5,7)  
$$

Regla para maxitérminos:

- Si la variable vale 0, aparece normal.
    
- Si la variable vale 1, aparece negada.
    

Ejemplo: fila 010, es decir:

$$  
A=0,\ B=1,\ C=0  
$$

El maxitérmino sería:

$$  
(A + \overline{B} + C)  
$$

Parece al revés que en los minitérminos, y por eso suele confundir.

Resumen:

Para minitérminos:

$$  
0 \rightarrow \text{variable negada}  
$$

$$  
1 \rightarrow \text{variable normal}  
$$

Para maxitérminos:

$$  
0 \rightarrow \text{variable normal}  
$$

$$  
1 \rightarrow \text{variable negada}  
$$

---

## 12. Suma de productos

Una **suma de productos**, también llamada SOP, tiene esta forma:

$$  
F = AB + \overline{A}C + BC  
$$

Es una OR de términos AND.

Se usa mucho cuando simplificas agrupando unos en Karnaugh.

---

## 13. Producto de sumas

Un **producto de sumas**, también llamado POS, tiene esta forma:

$$  
F = (A+B)(\overline{A}+C)(B+\overline{C})  
$$

Es una AND de términos OR.

Se usa mucho cuando simplificas agrupando ceros en Karnaugh.

Para el examen, hay que dominar ambas formas porque pueden pedir explícitamente:

- “Como suma de productos simplificada”
    
- “Como producto de sumas simplificado”
    

---

## 14. Leyes básicas del álgebra de Boole

### Identidad

$$  
A + 0 = A  
$$

$$  
A \cdot 1 = A  
$$

### Dominación

$$  
A + 1 = 1  
$$

$$  
A \cdot 0 = 0  
$$

### Idempotencia

$$  
A + A = A  
$$

$$  
A \cdot A = A  
$$

### Complemento

$$  
A + \overline{A} = 1  
$$

$$  
A \cdot \overline{A} = 0  
$$

### Doble negación

$$  
\overline{\overline{A}} = A  
$$

### Absorción

$$  
A + AB = A  
$$

$$  
A(A+B)=A  
$$

### Distributiva

$$  
A(B+C)=AB+AC  
$$

$$  
A+BC=(A+B)(A+C)  
$$

### Leyes de De Morgan

$$  
\overline{A \cdot B} = \overline{A} + \overline{B}  
$$

$$  
\overline{A + B} = \overline{A} \cdot \overline{B}  
$$

De Morgan es clave para pasar funciones a NAND o NOR.

---

## 15. Mapas de Karnaugh

El mapa de Karnaugh sirve para simplificar funciones booleanas visualmente.

Para 2 variables hay 4 casillas.

Para 3 variables hay 8 casillas.

Para 4 variables hay 16 casillas.

La idea es agrupar unos o ceros en potencias de dos:

$$  
1,\ 2,\ 4,\ 8,\ 16  
$$

Los grupos pueden rodear los bordes del mapa, porque los extremos son adyacentes.

Para obtener suma de productos, agrupas los **1**.

Para obtener producto de sumas, agrupas los **0**.

Los valores “don’t care”, normalmente escritos como (X) o (d), se pueden usar como 0 o como 1 según convenga para hacer grupos más grandes.

Regla fundamental:

**Cuanto más grande el grupo, más simple será el término.**

Ejemplo:

Si agrupas cuatro unos donde solo cambia (B) y (C), pero (A) permanece siempre 1, el término será simplemente:

$$  
A  
$$

porque las variables que cambian desaparecen.

En Karnaugh, una variable permanece en el término solo si mantiene el mismo valor en todo el grupo.

- Si (A) siempre vale 1, aparece (A).
    
- Si (A) siempre vale 0, aparece ($\overline{A}$).
    
- Si (A) cambia, desaparece.
    

---

## 16. Implementación con NAND

Las puertas NAND son universales.

Eso significa que con solo NAND puedes construir cualquier circuito lógico.

Operaciones básicas con NAND:

### NOT con NAND

$$  
\overline{A} = A \text{ NAND } A  
$$

### AND con NAND

Primero:

$$  
A \text{ NAND } B = \overline{A \cdot B}  
$$

Luego se niega otra vez:

$$  
A \cdot B = (A \text{ NAND } B) \text{ NAND } (A \text{ NAND } B)  
$$

### OR con NAND

Usando De Morgan:

$$  
A + B = \overline{\overline{A}\cdot \overline{B}}  
$$

Por tanto:

$$  
A + B = \overline{A} \text{ NAND } \overline{B}  
$$

En la práctica, si tienes una función en suma de productos:

$$  
F = AB + CD  
$$

puedes implementarla fácilmente con NAND-NAND.

Primero haces:

$$  
\overline{AB}  
$$

$$  
\overline{CD}  
$$

Y luego:

$$  
F = \overline{\overline{AB}\cdot \overline{CD}}  
$$

Eso es una NAND final.

Por eso, para implementar con NAND, suele convenir obtener la función como **suma de productos**.

Regla práctica:

**NAND combina bien con suma de productos.**

---

## 17. Implementación con NOR

Las puertas NOR también son universales.

Operaciones básicas con NOR:

### NOT con NOR

$$  
\overline{A} = A \text{ NOR } A  
$$

### OR con NOR

Primero:

$$  
A \text{ NOR } B = \overline{A+B}  
$$

Luego se niega otra vez:

$$  
A+B = (A \text{ NOR } B) \text{ NOR } (A \text{ NOR } B)  
$$

### AND con NOR

Usando De Morgan:

$$  
A \cdot B = \overline{\overline{A}+\overline{B}}  
$$

Por tanto:

$$  
A \cdot B = \overline{A} \text{ NOR } \overline{B}  
$$

Para implementar con NOR, suele convenir tener la función en **producto de sumas**.

Ejemplo:

$$  
F = (A+B)(C+D)  
$$

Primero generas:

$$  
\overline{A+B}  
$$

$$  
\overline{C+D}  
$$

Y luego haces una NOR final:

$$  
F = \overline{\overline{A+B}+\overline{C+D}}  
$$

Por eso, regla práctica de examen:

**NOR combina bien con producto de sumas.**

---

## 18. Multiplexores

Un multiplexor, MUX, selecciona una de varias entradas y la manda a la salida.

Un MUX 2 a 1 tiene:

- Entradas: (D_0, D_1)
    
- Selección: (S)
    
- Salida: (Y)
    

Funcionamiento:

- Si (S=0), sale (D_0).
    
- Si (S=1), sale (D_1).
    

Tabla:

|S|Y|
|---|---|
|0|D0|
|1|D1|

Un MUX 4 a 1 tiene cuatro entradas:

$$  
D_0,D_1,D_2,D_3  
$$

y dos señales de selección:

$$  
S_1,S_0  
$$

Tabla:

|S1|S0|Salida|
|---|---|---|
|0|0|D0|
|0|1|D1|
|1|0|D2|
|1|1|D3|

Un MUX 8 a 1 tiene tres señales de selección:

$$  
S_2,S_1,S_0  
$$

y entradas:

$$  
D_0,D_1,D_2,D_3,D_4,D_5,D_6,D_7  
$$

---

## 19. Cómo implementar funciones con MUX

Para implementar una función con MUX, se sigue este procedimiento:

1. Elegir qué variables serán las señales de selección.
    
2. Construir una tabla reducida.
    
3. Rellenar las entradas del MUX con:
    
    - 0
        
    - 1
        
    - una variable
        
    - una variable negada
        

Caso fácil:

Función de 3 variables con MUX 8 a 1.

Si tienes:

$$  
F(A,B,C)  
$$

puedes usar:

$$  
S_2=A,\ S_1=B,\ S_0=C  
$$

Entonces cada entrada del MUX será 0 o 1 según la tabla de verdad.

Caso medio:

Función de 4 variables con MUX 8 a 1.

Si tienes:

$$  
F(A,B,C,D)  
$$

puedes usar:

$$  
S_2=A,\ S_1=B,\ S_0=C  
$$

Entonces (D) queda como variable restante.

Para cada combinación de (ABC), miras qué hace la función cuando:

$$  
D=0  
$$

y cuando:

$$  
D=1  
$$

Según el resultado, cada entrada del MUX puede ser:

- 0
    
- 1
    
- (D)
    
- (\overline{D})
    

Regla:

|F cuando D=0|F cuando D=1|Entrada del MUX|
|---|---|---|
|0|0|0|
|1|1|1|
|0|1|D|
|1|0|D'|

Esta técnica es muy importante porque en los exámenes aparecen apartados del tipo:

- “Implementar usando exclusivamente un MUX8a1”
    
- “Implementar usando un MUX4a1”
    

---

## 20. Decodificadores

Un decodificador convierte un código binario de entrada en una salida “uno entre muchos”.

Un decodificador 2 a 4 tiene:

- 2 entradas
    
- 4 salidas
    

Un decodificador 3 a 8 tiene:

- 3 entradas
    
- 8 salidas
    

Un decodificador 4 a 16 tiene:

- 4 entradas
    
- 16 salidas
    

Ejemplo: DEC 3 a 8 con entradas (x_2,x_1,x_0):

|x2|x1|x0|Salida activa|
|---|---|---|---|
|0|0|0|O0|
|0|0|1|O1|
|0|1|0|O2|
|0|1|1|O3|
|1|0|0|O4|
|1|0|1|O5|
|1|1|0|O6|
|1|1|1|O7|

Si el decodificador es activo a nivel alto, la salida seleccionada vale 1 y las demás valen 0.

Si el decodificador es activo a nivel bajo, la salida seleccionada vale 0 y las demás valen 1.

Esto cambia totalmente la puerta que conviene usar.

---

## 21. Decodificador activo a nivel alto

Con decodificador activo a nivel alto, sus salidas representan minitérminos.

Ejemplo:

$$  
O_0 = \overline{x_2}\overline{x_1}\overline{x_0}  
$$

$$  
O_1 = \overline{x_2}\overline{x_1}x_0  
$$

$$  
O_2 = \overline{x_2}x_1\overline{x_0}  
$$

etc.

Entonces, si:

$$  
F=\sum m(1,3,6)  
$$

puedes conectar:

$$  
F = O_1 + O_3 + O_6  
$$

Normalmente se usaría una puerta OR.

Si el enunciado obliga a usar NOR, hay que tener cuidado con la polaridad de la función y aplicar De Morgan cuando haga falta.

---

## 22. Decodificador activo a nivel bajo

Con decodificador activo a nivel bajo, la salida seleccionada vale 0 y las demás valen 1.

Esto significa que las salidas representan minitérminos negados.

Por eso muchas veces se combinan con puertas NAND.

Regla práctica:

**DEC activo alto + OR/NOR según polaridad de salida.**

**DEC activo bajo + NAND suele venir bien.**

---

## 23. Displays de 7 segmentos

Un display de 7 segmentos tiene segmentos llamados:

- A: arriba
    
- B: arriba derecha
    
- C: abajo derecha
    
- D: abajo
    
- E: abajo izquierda
    
- F: arriba izquierda
    
- G: centro
    

Para representar un número o letra, se encienden ciertos segmentos.

Por ejemplo, para mostrar 0 normalmente se encienden:

$$  
A,B,C,D,E,F  
$$

y se apaga:

$$  
G  
$$

Para mostrar 1 se encienden:

$$  
B,C  
$$

Para mostrar 8 se encienden:

$$  
A,B,C,D,E,F,G  
$$

La parte clave del examen es la **polaridad**.

Si el display es activo a nivel alto:

$$  
1 = segmento encendido  
$$

$$  
0 = segmento apagado  
$$

Si el display tiene polaridad negativa o es activo a nivel bajo:

$$  
0 = segmento encendido  
$$

$$  
1 = segmento apagado  
$$

Por tanto, cuando construyas la tabla de verdad de un display activo a bajo, debes poner 0 en los segmentos que se encienden.

Ejemplo para el número 0 en activo bajo:

|Segmento|Valor|
|---|---|
|A|0|
|B|0|
|C|0|
|D|0|
|E|0|
|F|0|
|G|1|

Porque G está apagado.

Error típico:

Hacer la tabla como si 1 significara encendido cuando el display es activo a bajo.

---

## 24. Señales activas a nivel alto y activas a nivel bajo

Una señal activa a nivel alto se activa con 1.

Ejemplo:

$$  
CE = 1  
$$

significa “chip enable activado”.

Una señal activa a nivel bajo se activa con 0.

Normalmente se dibuja con una burbuja o se escribe con una barra encima.

Ejemplo:

$$  
\overline{reset}  
$$

Si reset es activo a bajo:

$$  
reset = 0 \rightarrow \text{reinicia}  
$$

$$  
reset = 1 \rightarrow \text{funcionamiento normal}  
$$

Lo mismo ocurre con preset.

Reset suele poner el biestable a 0.

Preset suele poner el biestable a 1.

Si son asíncronos, actúan inmediatamente, sin esperar al reloj.

Si son síncronos, actúan solo en el flanco del reloj.

---

## 25. Biestables

Un biestable almacena un bit.

Tiene una salida actual:

$$  
Q  
$$

y una salida complementaria:

$$  
\overline{Q}  
$$

El valor siguiente suele escribirse como:

$$  
Q^+  
$$

o:

$$  
Q(t+1)  
$$

Los biestables cambian normalmente en un flanco de reloj.

Si el flanco es de subida, cambian cuando el reloj pasa de 0 a 1.

Si el flanco es de bajada, cambian cuando el reloj pasa de 1 a 0.

---

## 26. Biestable D

El biestable D es el más sencillo.

Su regla es:

$$  
Q^+ = D  
$$

Lo que pongas en D antes del flanco de reloj será el próximo valor de Q.

Tabla:

|D|Q+|
|---|---|
|0|0|
|1|1|

Cuando diseñas con biestables D, es muy cómodo porque directamente:

$$  
D = Q^+  
$$

Es decir:

- Si quieres que el próximo estado sea 1, pones (D=1).
    
- Si quieres que el próximo estado sea 0, pones (D=0).
    

---

## 27. Biestable T

El biestable T sirve para conmutar.

Su regla es:

|T|Acción|
|---|---|
|0|Mantiene|
|1|Cambia|

Tabla:

|Q|T|Q+|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

La fórmula más importante es:

$$  
T = Q \oplus Q^+  
$$

Si (Q) y (Q^+) son iguales, entonces:

$$  
T=0  
$$

Si (Q) y (Q^+) son distintos, entonces:

$$  
T=1  
$$

Por eso, para diseñar contadores con biestables T:

1. Escribes la secuencia.
    
2. Pones estado actual y estado siguiente.
    
3. Comparas cada bit.
    
4. Si el bit cambia, (T=1).
    
5. Si el bit no cambia, (T=0).
    

---

## 28. Biestable JK

El JK es más general.

Tabla de funcionamiento:

|J|K|Acción|
|---|---|---|
|0|0|Mantiene|
|0|1|Reset, pone Q=0|
|1|0|Set, pone Q=1|
|1|1|Toggle, cambia|

Tabla de excitación JK:

|Q|Q+|J|K|
|---|---|---|---|
|0|0|0|X|
|0|1|1|X|
|1|0|X|1|
|1|1|X|0|

Esta tabla se usa muchísimo en diseños de máquinas de estados con JK.

Ejemplo:

Si el bit actual es 0 y quieres que siga siendo 0:

$$  
J=0,\ K=X  
$$

(K) da igual, porque desde 0 no importa si (K) vale 0 o 1 mientras (J) sea 0.

Si el bit actual es 1 y quieres que pase a 0:

$$  
J=X,\ K=1  
$$

---

## 29. Biestable RS

El RS tiene dos entradas:

- (S): set, poner a 1.
    
- (R): reset, poner a 0.
    

Tabla típica activa a nivel alto:

|S|R|Acción|
|---|---|---|
|0|0|Mantiene|
|0|1|Reset|
|1|0|Set|
|1|1|Prohibido / no válido|

Tabla de excitación RS:

|Q|Q+|S|R|
|---|---|---|---|
|0|0|0|X|
|0|1|1|0|
|1|0|0|1|
|1|1|X|0|

Con RS hay que evitar la combinación prohibida.

---

## 30. Contadores

Un contador es un circuito secuencial que recorre una secuencia de estados.

Ejemplo de contador binario de 2 bits:

$$  
00 \rightarrow 01 \rightarrow 10 \rightarrow 11 \rightarrow 00  
$$

Un contador BCD cuenta de 0 a 9:

$$  
0000 \rightarrow 0001 \rightarrow 0010 \rightarrow ... \rightarrow 1001 \rightarrow 0000  
$$

Los estados:

$$  
1010, 1011, 1100, 1101, 1110, 1111  
$$

no pertenecen al BCD.

Pueden tratarse como “don’t care” o forzarse a un estado seguro, según el enunciado.

Para diseñar un contador:

1. Escribes la secuencia.
    
2. Pasas cada número a binario.
    
3. Haces tabla de estado actual y estado siguiente.
    
4. Según el tipo de biestable, calculas las entradas necesarias.
    
5. Simplificas con Karnaugh.
    
6. Dibujas el circuito.
    

Ejemplo de tabla base:

|Estado actual Q2 Q1 Q0|Estado siguiente Q2+ Q1+ Q0+|
|---|---|
|000|001|
|001|010|
|010|011|
|011|100|

Si usas biestables D:

$$  
D_2 = Q_2^+  
$$

$$  
D_1 = Q_1^+  
$$

$$  
D_0 = Q_0^+  
$$

Si usas biestables T:

$$  
T_2 = Q_2 \oplus Q_2^+  
$$

$$  
T_1 = Q_1 \oplus Q_1^+  
$$

$$  
T_0 = Q_0 \oplus Q_0^+  
$$

Si usas JK, usas la tabla de excitación JK.

---

## 31. Chip enable, reset y preset en contadores

El **CE**, chip enable, permite que el contador avance.

Si CE está activo:

$$  
\text{el contador cuenta}  
$$

Si CE no está activo:

$$  
\text{el contador se congela}  
$$

El reset pone el contador a un valor inicial, normalmente 0.

El preset pone algunos bits a 1.

Por ejemplo, si quieres reiniciar un contador a 5:

$$  
5 = 0101  
$$

Entonces necesitas:

$$  
Q_3=0,\ Q_2=1,\ Q_1=0,\ Q_0=1  
$$

Para eso, puedes usar reset en los bits que deben quedar a 0 y preset en los bits que deben quedar a 1, teniendo cuidado con si son activos a bajo o activos a alto.

---

## 32. Máquinas de estados finitos

Una máquina de estados finitos, FSM, es un circuito secuencial que se puede representar mediante estados y transiciones.

Tiene:

- Entradas
    
- Estados
    
- Salidas
    
- Reloj
    
- Lógica de próximo estado
    
- Lógica de salida
    
- Biestables para guardar el estado
    

Hay dos tipos principales:

- Moore
    
- Mealy
    

---

## 33. Máquina de Moore

En una máquina de Moore, la salida depende solo del estado actual.

$$  
Z = f(Q)  
$$

No depende directamente de la entrada.

En el diagrama de estados, la salida se suele poner dentro del estado.

Ejemplo:

$$  
S_0 / Z=0  
$$

$$  
S_1 / Z=1  
$$

Ventaja:

La salida es más estable.

Desventaja:

A veces necesita más estados o reacciona un ciclo más tarde.

---

## 34. Máquina de Mealy

En una máquina de Mealy, la salida depende del estado actual y de la entrada.

$$  
Z = f(Q, X)  
$$

En el diagrama de estados, las transiciones se etiquetan como:

$$  
entrada/salida  
$$

Ejemplo:

$$  
0/0  
$$

significa que si entra 0, se toma esa transición y la salida vale 0.

$$  
1/1  
$$

significa que si entra 1, se toma esa transición y la salida vale 1.

Ventaja:

Suele necesitar menos estados y puede responder antes.

Desventaja:

La salida puede cambiar directamente al cambiar la entrada.

---

## 35. Cómo diseñar una máquina de estados desde cero

Esta es una plantilla clave para el examen.

### Paso 1: entender qué debe recordar la máquina

Por ejemplo, si la salida depende de cuántos ceros se han recibido módulo 7, entonces los estados representan:

$$  
0 \text{ ceros módulo } 7  
$$

$$  
1 \text{ cero módulo } 7  
$$

$$  
2 \text{ ceros módulo } 7  
$$

...

$$  
6 \text{ ceros módulo } 7  
$$

### Paso 2: dibujar los estados

Por ejemplo:

$$  
S_0,S_1,S_2,S_3,S_4,S_5,S_6  
$$

### Paso 3: poner transiciones

Si entra un 0, aumenta el contador de ceros:

$$  
S_0 \xrightarrow{x=0} S_1  
$$

$$  
S_1 \xrightarrow{x=0} S_2  
$$

...

$$  
S_6 \xrightarrow{x=0} S_0  
$$

Si entra un 1, no cambia la cantidad de ceros, así que se queda en el mismo estado:

$$  
S_i \xrightarrow{x=1} S_i  
$$

### Paso 4: poner salidas

Si es Mealy, las salidas van en las transiciones.

Si es Moore, las salidas van en los estados.

### Paso 5: codificar los estados en binario

Si hay 7 estados, necesitas:

$$  
2^2 = 4 < 7  
$$

$$  
2^3 = 8 \geq 7  
$$

Por tanto, hacen falta 3 biestables.

### Paso 6: tabla de transiciones

La tabla debe tener:

- Estado actual
    
- Entrada
    
- Estado siguiente
    
- Salida
    

### Paso 7: calcular entradas de los biestables

Si son D:

$$  
D_i = Q_i^+  
$$

Si son T:

$$  
T_i = Q_i \oplus Q_i^+  
$$

Si son JK, usas la tabla de excitación JK.

Si son RS, usas la tabla de excitación RS.

### Paso 8: simplificar las funciones con Karnaugh

Aquí simplificas las funciones de entrada de cada biestable y la salida.

### Paso 9: implementar con las puertas que pida el enunciado

Si pide NOR, intentas obtener producto de sumas o adaptar con De Morgan.

Si pide NAND, intentas obtener suma de productos o adaptar con De Morgan.

---

## 36. Detectores de trama

Un detector de trama es una máquina que detecta una secuencia de bits.

Por ejemplo, detectar:

$$  
111  
$$

o:

$$  
000  
$$

La salida vale 1 cuando los últimos bits recibidos coinciden con la secuencia.

En una máquina Mealy, la detección ocurre en la transición que completa la secuencia.

Ejemplo: detectar 111.

Estados posibles:

$$  
S_0: \text{no llevo nada útil}  
$$

$$  
S_1: \text{he visto un 1}  
$$

$$  
S_2: \text{he visto 11}  
$$

Cuando estando en (S_2) entra otro 1, he detectado 111 y saco (Z=1).

La transición sería:

$$  
S_2 \xrightarrow{1/1} S_2  
$$

¿Por qué vuelve a (S_2)?

Porque si acabo de leer 111, los dos últimos bits son 11, así que puedo detectar otra vez con solapamiento.

---

## 37. Solapamiento en detectores

“Con solapamiento” significa que una parte de la secuencia detectada puede servir para detectar la siguiente.

Ejemplo: detectar 111 en la cadena:

$$  
1111  
$$

Hay dos detecciones:

- Bits 1-2-3: 111
    
- Bits 2-3-4: 111
    

Por tanto, la salida sería 1 al leer el tercer bit y también al leer el cuarto.

Sin solapamiento, después de detectar se reiniciaría todo y solo habría una detección.

Regla para construir detectores con solapamiento:

**Después de detectar, no vuelves necesariamente al estado inicial. Vuelves al estado que representa el mayor sufijo de la cadena leída que también sea prefijo de la secuencia buscada.**

Esto parece complicado al principio, pero con práctica se vuelve mecánico.

---

## 38. Cronogramas

Un cronograma muestra cómo cambian las señales con el tiempo.

Se usa mucho en circuitos secuenciales.

Para completar un cronograma:

1. Identifica el tipo de biestable.
    
2. Mira si cambia en flanco de subida o de bajada.
    
3. Mira si reset/preset están activos.
    
4. Mira si CE permite cambiar.
    
5. Justo antes del flanco, evalúas las entradas del biestable.
    
6. En el flanco, actualizas Q.
    
7. Las señales combinacionales se recalculan a partir de las nuevas Q.
    

Regla de oro:

**Los biestables solo cambian en el flanco activo del reloj, salvo reset/preset asíncronos.**

Si hay reset o preset asíncrono activo, (Q) cambia inmediatamente, aunque no haya flanco.

Si CE está inactivo, (Q) se mantiene aunque haya flanco.

---

## 39. Cómo analizar un circuito secuencial dado

Cuando el examen te da un circuito ya dibujado, no empiezas inventando estados.

Empiezas sacando ecuaciones.

Plantilla:

### Paso 1: identificar las variables de estado

Por ejemplo:

$$  
Q_2,Q_1,Q_0  
$$

### Paso 2: identificar qué tipo de biestable hay en cada variable

Puede ser:

- D
    
- T
    
- JK
    
- RS
    

### Paso 3: sacar las ecuaciones de entrada de cada biestable

Por ejemplo:

$$  
D_0 = X + Q_1  
$$

$$  
T_1 = Q_0 \cdot X  
$$

$$  
J_2 = Q_1 + X  
$$

$$  
K_2 = \overline{Q_0}  
$$

### Paso 4: usar la regla del biestable para obtener (Q^+)

Si es D:

$$  
Q^+ = D  
$$

Si es T:

$$  
Q^+ = Q \oplus T  
$$

Si es JK:

Se usa la tabla JK.

Si es RS:

Se usa la tabla RS.

### Paso 5: construir una tabla con todos los estados posibles y entradas posibles

La tabla tendrá:

- Estado actual
    
- Entrada
    
- Estado siguiente
    
- Salida
    

### Paso 6: dibujar el diagrama de estados

A partir de la tabla de transición.

### Paso 7: interpretar qué función implementa

Por ejemplo:

- Contador
    
- Detector de secuencia
    
- Divisor
    
- Generador de secuencia
    
- Máquina de control
    

---

## 40. Tabla de excitación de biestables

Esta parte hay que tenerla muy a mano.

### Biestable D

|Q|Q+|D|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|0|
|1|1|1|

Regla:

$$  
D = Q^+  
$$

---

### Biestable T

|Q|Q+|T|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

Regla:

$$  
T = Q \oplus Q^+  
$$

---

### Biestable JK

|Q|Q+|J|K|
|---|---|---|---|
|0|0|0|X|
|0|1|1|X|
|1|0|X|1|
|1|1|X|0|

---

### Biestable RS

|Q|Q+|S|R|
|---|---|---|---|
|0|0|0|X|
|0|1|1|0|
|1|0|0|1|
|1|1|X|0|

---

## 41. Don’t care

Un don’t care es una situación que no importa o que nunca debería ocurrir.

Se escribe como:

$$  
X  
$$

o:

$$  
d  
$$

En Karnaugh, puedes usarlo como 0 o como 1, según te ayude a simplificar.

Ejemplo:

En un contador BCD, los estados 10 a 15 no se usan.

A veces puedes tratarlos como don’t care.

Pero cuidado:

Si el enunciado dice que esos estados deben ir a un estado seguro, entonces ya no son don’t care. Hay que definirlos.

---

# Plantillas de resolución

## 42. Plantilla para problemas combinacionales

Cuando te den un problema combinacional, sigue siempre este orden:

1. Identifica las entradas y salidas.
    
2. Interpreta el enunciado.
    
3. Construye la tabla de verdad.
    
4. Escribe la función como minitérminos o maxitérminos.
    
5. Simplifica con Karnaugh.
    
6. Implementa según lo que pidan.
    

Ejemplo de entradas y salida:

$$  
A,B,C,D \rightarrow F  
$$

Implementaciones posibles:

- Con puertas básicas
    
- Con NAND
    
- Con NOR
    
- Con MUX
    
- Con decodificador
    
- Con display de 7 segmentos
    

Nunca empieces dibujando puertas directamente.

Primero tabla, luego función, luego simplificación, luego circuito.

---

## 43. Plantilla para problemas con MUX

Si te piden implementar una función con MUX:

1. Mira cuántas variables tiene la función.
    
2. Mira qué tamaño de MUX te dan.
    
3. Decide qué variables van a selección.
    
4. Haz una tabla reducida.
    
5. Rellena las entradas del MUX con:
    
    - 0
        
    - 1
        
    - variable
        
    - variable negada
        

Caso fácil:

Función de 3 variables con MUX8a1:

$$  
S_2,S_1,S_0 = A,B,C  
$$

Cada entrada del MUX será 0 o 1.

Caso medio:

Función de 4 variables con MUX8a1:

$$  
S_2,S_1,S_0 = A,B,C  
$$

La variable restante (D) queda en las entradas.

Por tanto, cada entrada puede ser:

$$  
0,\ 1,\ D,\ \overline{D}  
$$

Caso con MUX4a1 y función de 4 variables:

Usas dos variables como selección y las otras dos quedan dentro de las entradas.

Por tanto, las entradas pueden ser funciones pequeñas de esas dos variables.

---

## 44. Plantilla para problemas con decodificador

Si te piden usar un decodificador:

1. Escribe la función como suma de minitérminos o identifica en qué filas vale 1.
    
2. Conecta las salidas correspondientes del decodificador.
    
3. Usa la puerta final adecuada.
    

Si el decodificador es activo alto:

$$  
F=\sum m(1,4,7)  
$$

entonces usas salidas:

$$  
O_1,O_4,O_7  
$$

y normalmente una OR.

Si el decodificador es activo bajo:

Las salidas seleccionadas valen 0, así que normalmente se usa NAND para combinar.

Si además la salida final debe ser activa a bajo, puede convenir implementar directamente la negada.

---

## 45. Plantilla para problemas de 7 segmentos

Para un problema de 7 segmentos:

1. Dibuja o mira qué segmentos se encienden para cada símbolo.
    
2. Recuerda la polaridad.
    
3. Construye la tabla de verdad para A, B, C, D, E, F, G.
    
4. Resuelve cada segmento como una función distinta.
    
5. Implementa cada segmento según lo que pidan.
    

Ejemplo de funciones:

$$  
A(x_2,x_1,x_0)  
$$

$$  
B(x_2,x_1,x_0)  
$$

$$  
C(x_2,x_1,x_0)  
$$

Cada segmento es una función independiente.

No se resuelve “el display entero” de golpe.

Se resuelve segmento por segmento.

---

## 46. Plantilla para máquinas de estados

Para diseñar una FSM:

1. Decide qué debe recordar cada estado.
    
2. Dibuja los estados.
    
3. Dibuja las transiciones.
    
4. Decide si es Moore o Mealy.
    
5. Haz la tabla de transición.
    
6. Codifica los estados.
    
7. Calcula entradas de biestables.
    
8. Simplifica.
    
9. Implementa.
    

Para analizar una FSM ya dada:

1. Identifica biestables.
    
2. Saca ecuaciones de sus entradas.
    
3. Calcula estado siguiente.
    
4. Haz tabla.
    
5. Dibuja grafo.
    
6. Interpreta qué detecta o qué secuencia genera.
    

---

# Errores típicos

## 47. Error 1: olvidar la polaridad

Si el display es activo a bajo:

$$  
0 = encendido  
$$

$$  
1 = apagado  
$$

No hacerlo al revés.

---

## 48. Error 2: confundir minitérminos con maxitérminos

Minitérminos:

- Se usan para filas donde la función vale 1.
    
- Forman suma de productos.
    

Maxitérminos:

- Se usan para filas donde la función vale 0.
    
- Forman producto de sumas.
    

---

## 49. Error 3: agrupar mal en Karnaugh

En Karnaugh solo se pueden hacer grupos de tamaño:

$$  
1,\ 2,\ 4,\ 8,\ 16  
$$

No valen grupos de 3, 5, 6, etc.

---

## 50. Error 4: olvidar que los bordes del mapa de Karnaugh son adyacentes

Los extremos del mapa se tocan.

Esto permite hacer grupos más grandes rodeando los bordes.

---

## 51. Error 5: diseñar una Mealy como si fuera Moore

En Moore:

$$  
Z=f(Q)  
$$

La salida depende solo del estado.

En Mealy:

$$  
Z=f(Q,X)  
$$

La salida depende del estado y de la entrada.

---

## 52. Error 6: usar mal la tabla de excitación del biestable

Cada biestable tiene su propia tabla:

- D
    
- T
    
- JK
    
- RS
    

No se calculan igual.

---

## 53. Error 7: tratar reset/preset asíncronos como si esperaran al reloj

Si son asíncronos, actúan inmediatamente.

No esperan al flanco de reloj.

---

## 54. Error 8: reiniciar mal un detector con solapamiento

Si el detector es con solapamiento, después de detectar no siempre se vuelve al estado inicial.

Hay que conservar el mayor sufijo útil.

---

## 55. Error 9: no respetar restricciones del enunciado

Si el enunciado dice:

- “Solo NOR”
    
- “Solo NAND”
    
- “Exclusivamente MUX8a1”
    
- “DEC4a16 activo alto”
    
- “Display activo a bajo”
    

hay que cumplirlo exactamente.

Aunque tengas una solución lógica correcta, si no respetas la restricción, el ejercicio está mal.

---

# Resumen mínimo para memorizar

## 56. Combinacional

$$  
\text{Tabla} \rightarrow \text{minitérminos/maxitérminos} \rightarrow \text{Karnaugh} \rightarrow \text{implementación}  
$$

---

## 57. NAND

Para NAND conviene trabajar con:

$$  
\text{suma de productos}  
$$

---

## 58. NOR

Para NOR conviene trabajar con:

$$  
\text{producto de sumas}  
$$

---

## 59. MUX

Para MUX:

$$  
\text{selecciones} \rightarrow \text{rellenar entradas con } 0,1,x,\overline{x}  
$$

---

## 60. Decodificador

Las salidas de un decodificador representan minitérminos.

Si es activo alto:

$$  
O_i = m_i  
$$

Si es activo bajo:

$$  
O_i = \overline{m_i}  
$$

---

## 61. Display activo a bajo

En un display activo a bajo:

$$  
0 = encendido  
$$

$$  
1 = apagado  
$$

---

## 62. Biestable D

$$  
D=Q^+  
$$

---

## 63. Biestable T

$$  
T=Q\oplus Q^+  
$$

---

## 64. Biestable JK

|Q|Q+|J|K|
|---|---|---|---|
|0|0|0|X|
|0|1|1|X|
|1|0|X|1|
|1|1|X|0|

---

## 65. Moore

$$  
Z=f(Q)  
$$

La salida depende solo del estado.

---

## 66. Mealy

$$  
Z=f(Q,X)  
$$

La salida depende del estado y de la entrada.

---

## 67. Detectores con solapamiento

Después de detectar, conserva el mayor sufijo útil.

No siempre se vuelve al estado inicial.

---

# Orden recomendado para estudiar

Primero conviene dominar la parte combinacional:

1. Tablas de verdad
    
2. Minitérminos y maxitérminos
    
3. Karnaugh
    
4. NAND y NOR
    
5. MUX
    
6. Decodificadores
    
7. Displays de 7 segmentos
    

Después conviene pasar a la parte secuencial:

1. Biestables
    
2. Tablas de excitación
    
3. Contadores
    
4. Máquinas Moore y Mealy
    
5. Detectores de trama
    
6. Cronogramas
    
7. Análisis de circuitos secuenciales dados
    

La idea no es memorizar ejercicios, sino dominar plantillas de resolución.