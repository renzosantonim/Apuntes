### 1. Bloque de Test (2 puntos)

- **Formato:** 10 preguntas tipo test.
    
- **Puntuación:** $+0.2$ por acierto, $-0.1$ por fallo.
    
- **Patrón:** Mezclan pura teoría de C++ (qué hace `private`, `noexcept`, `virtual` o el polimorfismo) con propiedades teóricas de algoritmos (complejidades, de qué tamaño son las particiones en QuickSort o MergeSort, reglas de los ABB).

### 2. Bloque de Preguntas Cortas (4 puntos)

- **Formato:** 4 ejercicios a desarrollar en hojas separadas (1 punto cada uno).
    
- **El Patrón de Oro (Siempre caen estos 4):**
    
    1. **Traza de Tabla Hash:** Te dan una función de dispersión matemática (módulo, suma de dígitos) y un método de exploración (lineal, cuadrática, doble). Tienes que insertar datos paso a paso mostrando las colisiones.
        
    2. **Traza de Polimorfismo en C++:** Un bloque de código con clases heredadas (A, B, C), llamadas virtuales, ocultamiento con `const` y punteros en el Heap. Tienes que deducir exactamente qué números imprime el `main`.
        
    3. **Traza de Ordenación:** Aplicar paso a paso un algoritmo sobre un vector (ShakeSort, RadixSort, etc.), mostrando qué elementos se mueven en cada iteración.
        
    4. **Traza de Árboles AVL:** Insertar y eliminar una serie de números, identificar dónde se rompe el balance y dibujar el árbol antes y después de aplicar las rotaciones (II, DD, ID, DI).

### 3. Bloque de Desarrollo / Programación (4 puntos)

- **Formato:** 2 problemas de escribir código puro (2 puntos cada uno).
    
- **Patrón:**
    
    1. **El Algoritmo Frankenstein:** Te pedirán escribir una función C++ que mezcle varios algoritmos de ordenación (por ejemplo, ordenar la primera mitad con Selección descendente, la segunda con Inserción por la derecha, y aplicar un Merge).
        
    2. **Arquitectura OOP y Excepciones:** Diseñar una jerarquía de clases (Piezas de Ajedrez, N-Trees genéricos con plantillas) usando herencia, clases abstractas, métodos virtuales y un bloque `try-catch` robusto lanzando excepciones personalizadas.