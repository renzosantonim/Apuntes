
## 1. La Jerarquía de los Lenguajes (De menor a mayor poder)
> **Regla de oro:** Todo lenguaje de un nivel inferior pertenece automáticamente a los niveles superiores.

| Nivel | Tipo de Lenguaje | Máquina que lo resuelve | Gramática | Memoria / Bombeo |
| :--- | :--- | :--- | :--- | :--- |
| **Tipo 3** (Más débil) | **Regular** | Autómata Finito (DFA / NFA) | Gramática Regular (Ej: A → aB \| a) | **Sin memoria.** Solo sabe su estado actual. Tiene su propio Lema de Bombeo. |
| **Tipo 2** | **Independiente del Contexto (CFL)** | Autómata a Pila (Pushdown) | Gramática Indep. del Contexto (Ej: S → 0S1) | **Memoria LIFO (Pila).** Cuenta balanceando, 1 cosa a la vez. Tiene su propio Lema de Bombeo. |
| **Extra** (El Decisor) | **Recursivo** (Decidible) | Máquina de Turing que **SIEMPRE SE PARA** | *(No tiene gramática propia)* | Memoria de cinta infinita. **Es el algoritmo perfecto**, nunca entra en bucle infinito. |
| **Tipo 0** (Más fuerte) | **Recursivamente Enumerable (RE)** | Máquina de Turing Estándar | Gramática sin restricciones | Memoria infinita. Si la palabra es falsa, **puede quedarse colgada en bucle infinito**. |

---

## 2. Propiedades de Cierre ("Cheat Sheet")
*Guía rápida para preguntas tipo test: "¿La unión de dos lenguajes X sigue siendo X?"*

| Operación | Regulares | Indep. Contexto (CFL) | Recursivos | Rec. Enumerables (RE) |
| :--- | :--- | :--- | :--- | :--- |
| **Unión** (L₁ ∪ L₂) | ✅ SÍ | ✅ SÍ | ✅ SÍ | ✅ SÍ |
| **Concatenación** (L₁ · L₂) | ✅ SÍ | ✅ SÍ | ✅ SÍ | ✅ SÍ |
| **Estrella Kleene** (L*) | ✅ SÍ | ✅ SÍ | ✅ SÍ | ✅ SÍ |
| **Intersección** (L₁ ∩ L₂) | ✅ SÍ | ❌ **NO** (¡Trampa!) | ✅ SÍ | ✅ SÍ |
| **Complemento** (~L) | ✅ SÍ | ❌ **NO** (¡Trampa!) | ✅ SÍ | ❌ **NO** (¡Trampa!) |

---

## 3. Las 5 "Trampas" clásicas de los exámenes

1. **"La intersección de dos lenguajes Independientes del Contexto es siempre Independiente del Contexto".**
   * **FALSO.** Es la única operación básica donde los CFL fallan. La intersección de dos CFL puede dar como resultado un lenguaje que necesite una Máquina de Turing.
2. **"El complemento de un lenguaje Recursivamente Enumerable siempre es Recursivamente Enumerable".**
   * **FALSO.** Si cruzas esa línea, te sales de la computabilidad garantizada.
3. **"La intersección de un lenguaje Regular con un Independiente del Contexto..."**
   * **RESULTADO:** Siempre da un lenguaje Independiente del Contexto. (El nivel fuerte absorbe al débil sin perder su categoría).
4. **"Si L es un lenguaje Independiente del Contexto, entonces es Recursivo."**
   * **VERDADERO.** Todo CFL se puede resolver con un Autómata a Pila, lo que significa que existe una Máquina de Turing que siempre se para.
5. **"Si L no cumple el lema del bombeo para regulares, entonces no es regular."**
   * **VERDADERO.** Es una condición matemática obligatoria. Si falla, está 100% demostrado por contradicción que no es regular.