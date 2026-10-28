# Base de Datos - Repaso global

Material común para consolidar los cuatro bloques teóricos: comparaciones, método de resolución, autoevaluación y correspondencia con las diapositivas.

---

# 5. Repaso global

## 5.1 Conceptos que conviene distinguir

| No confundir | Diferencia esencial |
|---|---|
| Base de datos / SGBD | Los datos organizados frente al software que los gestiona. |
| Esquema / extensión | Estructura relativamente estable frente al contenido actual. |
| Grado / cardinalidad | Número de atributos frente a número de tuplas. |
| Superclave / clave | Identifica frente a identifica y además es minimal. |
| Clave primaria / alternativa | Ambas son candidatas; una se escoge como principal. |
| Clave primaria / clave ajena | Identifica una fila frente a referenciar una clave. |
| Integridad de entidad / referencial | Primaria sin nulos frente a referencias válidas. |
| Selección / proyección | Filas frente a columnas. |
| Unión / yunción | Suma tuplas compatibles frente a combinar atributos de filas relacionadas. |
| Intersección / yunción | Tuplas completas comunes frente a combinación mediante condición. |
| Diferencia / complemento | Resta entre relaciones finitas frente a universo absoluto. |
| Vista / materializada | Definición virtual frente a resultado almacenado. |
| OLTP / OLAP | Operación cotidiana frente a análisis. |
| Álgebra / cálculo relacional | Secuencia de operaciones frente a descripción lógica del resultado. |
| CRT / CRD | Variables de tupla frente a variables de dominio. |
| Variable libre / ligada | Forma el resultado frente a quedar bajo un cuantificador. |
| Existencial / universal | Al menos uno frente a todos. |

## 5.2 Cómo traducir un enunciado al álgebra

| Expresión del enunciado | Operación probable |
|---|---|
| «cuyos», «con», «mayor que» | Selección. |
| «mostrar solo DNI y nombre» | Proyección. |
| «o cualquiera de los dos» | Unión. |
| «en ambos» | Intersección. |
| «pero no» o «sin» | Diferencia. |
| «relacionar clientes con sus cuentas» | Yunción. |
| «para todas las sucursales» | Cociente. |
| «al menos dos distintos» | Autoproducto o autojoin con renombrado. |
| «ninguno» | Universo de candidatos menos los que sí cumplen. |
| «solamente» | Candidatos válidos menos quienes tienen un contraejemplo. |

### Método de trabajo

1. Identifica qué atributos debe tener el resultado.
2. Localiza las relaciones que contienen esos atributos y las condiciones.
3. Conecta las relaciones necesarias mediante claves.
4. Aplica selecciones para filtrar.
5. Proyecta al final los atributos pedidos.
6. Si aparece «todos», comprueba si corresponde división.
7. Verifica compatibilidad antes de unión, diferencia o intersección.

## 5.3 Preguntas de autoevaluación

1. ¿Por qué la redundancia puede provocar inconsistencia?
2. ¿Qué diferencia hay entre independencia lógica y física?
3. ¿Cuáles son los tres componentes de un modelo de datos?
4. ¿Qué función cumplen DDL, DML y DCL?
5. ¿Por qué OLTP y OLAP suelen requerir diseños diferentes?
6. ¿Qué diferencia hay entre esquema y extensión?
7. ¿Por qué toda clave es superclave pero no toda superclave es clave?
8. ¿Puede una relación tener varias claves candidatas?
9. ¿Qué exige la integridad referencial al insertar una fila hija?
10. ¿Por qué `? = ?` no se utiliza para comprobar nulos?
11. ¿Qué operaciones reducen profundidad y anchura?
12. ¿Qué requisito comparten unión, diferencia e intersección?
13. ¿Cómo se expresa una yunción mediante operadores fundamentales?
14. ¿Qué palabra del enunciado suele indicar un cociente?
15. ¿Por qué conviene aplicar selecciones antes de productos o yunciones?
16. ¿Cuándo una yunción natural se convierte en producto cartesiano?
17. ¿Qué coste intercambia una vista materializada por consultas más rápidas?
18. ¿Por qué no existe un complemento general en el álgebra presentada?
19. ¿Qué diferencia existe entre CRT y CRD?
20. ¿Cómo se niega una condición universal?
21. ¿Por qué se restringe el cálculo relacional?

<details>
<summary>Respuestas breves</summary>

1. Porque dos copias del mismo dato pueden actualizarse de forma distinta.
2. La física permite cambiar almacenamiento; la lógica permite cambiar el esquema conceptual sin afectar ciertas vistas.
3. Estructuras, operadores y reglas de integridad.
4. Definir, manipular y controlar, respectivamente.
5. OLTP prioriza muchas transacciones; OLAP, consultas analíticas grandes.
6. Estructura frente al conjunto actual de tuplas.
7. Una clave exige minimalidad y una superclave no.
8. Sí; una se elige primaria y las demás quedan como alternativas.
9. Que cada clave ajena no nula encuentre una clave referenciada.
10. Porque una comparación con nulo produce desconocido; se usa `ISNULL`.
11. Selección reduce profundidad; proyección reduce anchura y puede reducir profundidad.
12. Compatibilidad para la unión.
13. `R Y(F) S = S(F)(R × S)`.
14. «Todos» o «cada».
15. Para reducir el tamaño de resultados intermedios.
16. Cuando no hay atributos homónimos.
17. Más espacio y coste de mantenimiento o refresco.
18. Porque el producto de dominios puede ser infinito.
19. CRT usa variables que representan tuplas; CRD usa variables que representan valores de atributos.
20. `¬(∀x)P(x) ⇔ (∃x)¬P(x)`.
21. Para excluir expresiones que produzcan resultados infinitos o no evaluables mediante un proceso finito.

</details>

## 5.4 Hoja rápida de operadores

| Operador | Entrada | Resultado | Regla clave |
|---|---|---|---|
| `S(F)(R)` | Una relación | Filas que cumplen `F` | Mismo esquema. |
| `P(L)(R)` | Una relación | Columnas de `L` | Elimina duplicados. |
| `R × S` | Dos relaciones | Todas las parejas | Multiplica cardinalidades. |
| `R ∪ S` | Dos compatibles | Tuplas de cualquiera | Sin duplicados. |
| `R - S` | Dos compatibles | Tuplas solo de `R` | No conmutativa. |
| `R ∩ S` | Dos compatibles | Tuplas comunes | Derivada. |
| `R Y(F) S` | Dos relaciones | Parejas que cumplen `F` | Selección sobre producto. |
| `R * S` | Dos relaciones | Coincidencia de homónimos | Una copia de cada homónimo. |
| `R / S` | Atributos de S incluidos en R | Valores relacionados con todo S | Expresa universalidad. |
| `ρ(N)(R)` | Una relación | La misma relación renombrada | Permite copias inequívocas y autojoins. |

---

# 6. Correspondencia con las diapositivas y aclaraciones

## 6.1 Cobertura de «Introducción bases de datos»

| Páginas | Contenido integrado |
|---|---|
| 2–5 | Procesamiento tradicional y desventajas. |
| 6–7 | Sistemas de bases de datos y funciones del SGBD. |
| 8 | Abstracción e independencia. |
| 9–13 | Modelos de datos, E-R y relacional. |
| 14–19 | DDL, DML, DCL y clasificaciones del DML. |
| 20 | OLTP y OLAP. |
| 21 | Perfiles de usuario. |
| 22 | Estructura del SGBD. |
| 23 | Arquitecturas de dos y tres capas. |

## 6.2 Cobertura de «El modelo relacional»

| Páginas | Contenido integrado |
|---|---|
| 2 | Contexto histórico. |
| 3–8 | Relaciones, dominios, esquemas, tuplas y cuantificación. |
| 9–12 | Superclaves, claves, primaria y alternativas. |
| 13–14 | Claves ajenas y jerarquía referencial. |
| 15–20 | Nulos, lógica ternaria e `ISNULL`. |
| 21–25 | Restricciones e integridad referencial. |
| 26 | Componentes del modelo. |

## 6.3 Cobertura de «Álgebra relacional»

| Páginas | Contenido integrado |
|---|---|
| 2–4 | Definición y clasificación de operadores. |
| 5–13 | Operadores fundamentales y ejercicios. |
| 14–21 | Operadores derivados y ejercicios. |
| 22–23 | Actualización y ausencia de complemento. |
| 24–30 | Potencia, equivalencia y propiedades. |
| 31–34 | Vistas y vistas materializadas. |
| 35–38 | Álgebra extendida con nulos. |

## 6.4 Cobertura de «Cálculo relacional»

| Páginas | Contenido integrado |
|---|---|
| 2–4 | Definición, CRT/CRD y lógica de predicados. |
| 5–18 | Operadores, equivalencias, inferencia y cuantificadores. |
| 19–22 | CRT y consultas del esquema bancario. |
| 23–26 | Seguridad, potencia y definición formal de CRT. |
| 27–32 | CRD, definición formal y consultas. |

## 6.5 Aclaraciones importantes

> [!important]
> 1. Se mantiene la notación del curso para facilitar la correspondencia con exámenes y ejercicios.
> 2. Se distingue el concepto matemático de relación de su presentación como tabla.
> 3. El orden de columnas se matiza porque la notación posicional lo necesita, mientras que los atributos nombrados reducen esa dependencia.
> 4. La semántica de nulos descrita es la adoptada por las diapositivas; SQL real posee reglas concretas que pueden diferir en detalles.
> 5. La yunción natural debe usarse solo cuando los atributos homónimos representan realmente el mismo concepto.
> 6. Las expresiones resueltas se han añadido como apoyo didáctico; no son una transcripción literal de soluciones del profesor.

### Límites de estos apuntes

Las fuentes recibidas no desarrollan todavía SQL, diseño E-R completo, transformación de diagramas a tablas, normalización ni transacciones en detalle. Aquí solo se explican cuando son necesarios para entender las cuatro presentaciones, sin anticipar temario no proporcionado.
