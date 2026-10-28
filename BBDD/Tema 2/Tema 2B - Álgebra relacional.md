# Base de Datos - Tema 2B: Álgebra relacional

Apuntes elaborados a partir de las 38 diapositivas de `Tema 2 - Álgebra relacional.pdf`. Incluyen operadores, propiedades, vistas y ejercicios resueltos.

---

# 3. Tema 2. Álgebra relacional

*Origen principal: páginas 2–38 de «Tema 2 - Álgebra relacional».*

## 3.1 Qué es el álgebra relacional

> [!definition]
> El **álgebra relacional** es un lenguaje de consultas procedimental formado por operaciones sobre relaciones.

Es un sistema **cerrado**:

```text
relación ──operador──→ relación
```

Como el resultado vuelve a ser una relación, puede convertirse en operando de otra operación.

### Clasificación

| Clase | Operadores |
|---|---|
| Fundamentales | Selección, proyección, producto cartesiano, unión y diferencia. |
| Derivados | Intersección, yunción, yunción natural y cociente. |

Los derivados pueden expresarse utilizando los fundamentales. Eliminarlos complica la escritura, pero no reduce la potencia expresiva. Eliminar un operador fundamental sí la reduce dentro del conjunto presentado.

Otra clasificación:

- de conjuntos: unión, intersección, diferencia y producto cartesiano;
- específicamente relacionales: selección y proyección;
- mixtos: yunción, yunción natural y cociente.

### Notación común de estos apuntes

| Operación | Notación del curso | Notación frecuente |
|---|---|---|
| Selección | `S(F)(R)` | `σ_F(R)` |
| Proyección | `P(L)(R)` | `π_L(R)` |
| Producto | `R × S` | `R × S` |
| Unión | `R ∪ S` | `R ∪ S` |
| Diferencia | `R - S` | `R - S` |
| Intersección | `R ∩ S` | `R ∩ S` |
| Yunción | `R Y(F) S` | `R ⋈_F S` |
| Yunción natural | `R * S` | `R ⋈ S` |
| Cociente | `R / S` | `R ÷ S` |

---

## 3.2 Selección

```text
S(F)(R)
```

Es un operador unario que conserva las tuplas de `R` que satisfacen el predicado `F`.

- conserva todos los atributos;
- reduce o mantiene la cardinalidad;
- `|S(F)(R)| ≤ |R|`;
- se dice que reduce en **profundidad**.

El predicado puede combinar constantes, atributos, operaciones aritméticas, comparaciones y conectores lógicos.

### Ejemplos

Todas las filas de préstamos de la sucursal 1:

```text
S(CS = 1)(PRESTAMO)
```

Préstamos de esa sucursal con importe superior a 100000:

```text
S(CS = 1 ∧ I > 100000)(PRESTAMO)
```

> [!tip]
> Selección significa «qué filas». Imagina un filtro vertical que atraviesa todas las columnas y decide qué filas sobreviven.

---

## 3.3 Proyección

```text
P(L)(R)
```

Es un operador unario que conserva únicamente los atributos enumerados en `L`.

- reduce en **anchura**;
- puede reducir también la profundidad porque elimina duplicados;
- `|P(L)(R)| ≤ |R|`.

### Ejemplos

DNI de todos los clientes:

```text
P(DNI)(CLIENTE)
```

DNI de clientes con préstamos y códigos de las sucursales:

```text
P(DNI, CS)(PRESTAMO)
```

DNI de clientes con un préstamo superior a 100000:

```text
P(DNI)(S(I > 100000)(PRESTAMO))
```

> [!important]
> En álgebra relacional se trabaja con conjuntos. Si varias filas proyectadas quedan iguales, solo permanece una.

---

## 3.4 Producto cartesiano

```text
R × S
```

Combina cada tupla de `R` con cada tupla de `S`.

- es binario;
- el esquema contiene primero los atributos de `R` y después los de `S`;
- si hay atributos homónimos, se califican con la relación de origen;
- `|R × S| = |R| · |S|`.

> [!example]
> Si `R` tiene 3 filas y `S` tiene 4, `R × S` contiene 12 combinaciones, antes de aplicar ningún filtro.

El producto por sí solo suele crear muchas combinaciones sin significado. Se usa junto con una selección que conserva las parejas relacionadas.

### Ejemplo desarrollado

DNI de clientes con un préstamo superior a 100000 en una sucursal de La Laguna:

```text
P(PRESTAMO.DNI)(
  S(PRESTAMO.CS = SUCURSAL.CS
    ∧ PRESTAMO.I > 100000
    ∧ SUCURSAL.CDS = 'La Laguna')(
      PRESTAMO × SUCURSAL
  )
)
```

> [!tip]
> Producto + selección por igualdad de claves es la forma fundamental de construir una yunción.

---

## 3.5 Unión

```text
R ∪ S
```

Incluye todas las tuplas que estén en `R`, en `S` o en ambas. Las repetidas se cuentan una vez.

Para aplicarla, `R` y `S` deben ser compatibles para la unión:

- mismo grado;
- dominios compatibles en atributos correspondientes.

Se cumple:

$$
|R \cup S| \leq |R| + |S|
$$

### Ejemplo

DNI de clientes que tienen un préstamo o una cuenta, o ambas cosas, en la sucursal 1:

```text
P(DNI)(S(CS = 1)(PRESTAMO))
∪
P(DNI)(S(CS = 1)(CUENTA))
```

---

## 3.6 Diferencia

```text
R - S
```

Conserva las tuplas de `R` que no están en `S`.

- es binaria;
- exige compatibilidad para la unión;
- `|R - S| ≤ |R|`;
- no es conmutativa: normalmente `R - S ≠ S - R`.

### Ejemplos

Clientes con préstamo en la sucursal 1 pero sin cuenta allí:

```text
P(DNI)(S(CS = 1)(PRESTAMO))
-
P(DNI)(S(CS = 1)(CUENTA))
```

Clientes con cuenta en la sucursal 1 pero sin préstamo allí:

```text
P(DNI)(S(CS = 1)(CUENTA))
-
P(DNI)(S(CS = 1)(PRESTAMO))
```

> [!warning]
> «Clientes sin préstamos» no se obtiene proyectando directamente los clientes que no aparecen en una fila concreta. Se formula como conjunto de todos los clientes menos el conjunto de clientes con préstamo.

---

## 3.7 Intersección

```text
R ∩ S
```

Conserva las tuplas que pertenecen simultáneamente a `R` y `S`. También exige compatibilidad para la unión.

$$
|R \cap S| \leq \min(|R|, |S|)
$$

Es derivada porque:

```text
R ∩ S = R - (R - S)
      = S - (S - R)
```

### Ejemplo

DNI de clientes que tienen préstamo y cuenta en la sucursal 1:

```text
P(DNI)(S(CS = 1)(PRESTAMO))
∩
P(DNI)(S(CS = 1)(CUENTA))
```

Sucursales que tienen alguna cuenta con titulares de Santa Cruz y también alguna con titulares de La Laguna:

```text
P(CS)(
  S(CLIENTE.DNI = CUENTA.DNI ∧ CLIENTE.CDC = 'Santa Cruz')(
    CLIENTE × CUENTA
  )
)
∩
P(CS)(
  S(CLIENTE.DNI = CUENTA.DNI ∧ CLIENTE.CDC = 'La Laguna')(
    CLIENTE × CUENTA
  )
)
```

---

## 3.8 Yunción

```text
R Y(F) S
```

La yunción o **join** combina las tuplas del producto cartesiano que satisfacen `F`.

```text
R Y(F) S = S(F)(R × S)
```

### Ejemplo

Combinar cada cuenta con su cliente:

```text
CLIENTE Y(CLIENTE.DNI = CUENTA.DNI) CUENTA
```

El resultado incluye atributos de ambas relaciones y solo parejas cuyo DNI coincide.

> [!tip]
> Una yunción responde a «combina información relacionada». Una intersección responde a «qué tuplas completas aparecen en ambos conjuntos». No son lo mismo.

---

## 3.9 Yunción natural

```text
R * S
```

Es una yunción que impone de forma implícita la igualdad de todos los atributos con el mismo nombre. En el resultado aparece una sola copia de cada columna homónima.

Casos extremos:

- si no hay atributos comunes, `R * S = R × S`;
- si tienen exactamente los mismos atributos, `R * S = R ∩ S`.

### Ejemplos

DNI de clientes con préstamo superior a 100000 en una sucursal de La Laguna:

```text
P(DNI)(
  S(I > 100000 ∧ CDS = 'La Laguna')(
    PRESTAMO * SUCURSAL
  )
)
```

Ciudades de residencia de clientes con alguna cuenta cuyo saldo supera 100000:

```text
P(CDC)(
  S(SLD > 100000)(
    CLIENTE * CUENTA
  )
)
```

Clientes con una cuenta en una sucursal situada en la ciudad donde viven:

```text
P(DNI)(
  S(CDC = CDS)(
    CLIENTE * CUENTA * SUCURSAL
  )
)
```

> [!warning]
> La yunción natural empareja **todos** los atributos homónimos. Si dos columnas comparten nombre por casualidad pero no significado, el resultado será incorrecto. En ese caso conviene renombrar o usar una yunción con condición explícita.

---

## 3.10 Cociente o división

```text
R / S
```

Se utiliza para consultas que contienen «para todos».

Si los atributos de `S` están contenidos estrictamente en los de `R`, el resultado conserva los valores de los atributos restantes que están relacionados con **todas** las tuplas de `S`.

### Intuición

Supongamos:

```text
TIENE_CUENTA(DNI, CS)
SUCURSALES_LAGUNA(CS)
```

Entonces:

```text
TIENE_CUENTA / SUCURSALES_LAGUNA
```

devuelve los DNI que aparecen emparejados con cada código de sucursal de `SUCURSALES_LAGUNA`.

### Definición mediante operaciones fundamentales

Sea `LR` la lista de atributos de `R` y `LS` la de `S`:

```text
R / S =
P(LR - LS)(R)
-
P(LR - LS)(
  (P(LR - LS)(R) × S) - R
)
```

Interpretación:

1. Se obtienen todos los candidatos.
2. Se generan las combinaciones que cada candidato debería tener con `S`.
3. Se detectan las combinaciones ausentes en `R`.
4. Se eliminan los candidatos a los que les falta alguna.

### Ejercicio de las diapositivas

DNI de clientes con al menos una cuenta en **todas** las sucursales de La Laguna:

```text
R = P(DNI, CS)(CUENTA)
S = P(CS)(S(CDS = 'La Laguna')(SUCURSAL))

Resultado = R / S
```

> [!important]
> Unión expresa «alguno». Intersección expresa «ambos conjuntos concretos». División expresa «todos los elementos de un conjunto variable».

---

## 3.11 Operaciones de actualización

Las diapositivas expresan actualizaciones como operaciones de conjuntos:

```text
Inserción de una tupla:       R ∪ {t}
Inserción de una relación:    R ∪ E

Borrado de una tupla:         R - {t}
Borrado de una relación:      R - E

Modificación t1 → t2:         (R - {t1}) ∪ {t2}
```

Una modificación se entiende como borrar la versión anterior e insertar la nueva.

Estas operaciones solo son válidas si el resultado respeta dominios, claves e integridad referencial.

---

## 3.12 Por qué no hay un complemento general

Un posible complemento sería:

$$
\overline{R} = (D_1 \times D_2 \times \cdots \times D_n) - R
$$

Pero alguno de los dominios puede ser infinito. El complemento contendría potencialmente infinitas tuplas y dejaría de ser una relación finita manejable por el álgebra presentada.

> [!note]
> Sí puede calcularse una diferencia respecto de una relación finita concreta. Lo que no se define es un complemento absoluto universal sin acotar el universo.

---

## 3.13 Potencia expresiva y completitud relacional

> [!definition]
> La **potencia expresiva** de un lenguaje es el conjunto de consultas que permite formular.

El álgebra relacional y el cálculo relacional clásico tienen la misma potencia expresiva: una consulta formulada en uno puede traducirse al otro.

Un lenguaje es **relacionalmente completo** si puede expresar al menos todas las consultas del álgebra relacional básica.

Esto no significa que pueda resolver cualquier problema imaginable. Hay consultas, como ciertos cierres recursivos, que requieren extensiones.

---

## 3.14 Consultas equivalentes y optimización

Dos consultas son equivalentes si producen el mismo resultado para cualquier estado válido de las relaciones.

Cuando existen varias expresiones equivalentes interesa escoger una que:

- use menos recursos;
- sea más legible;
- reduzca pronto el volumen de datos intermedios.

### Propiedades de conjuntos

Unión e intersección son conmutativas y asociativas:

```text
R ∪ S = S ∪ R
(R ∪ S) ∪ T = R ∪ (S ∪ T)

R ∩ S = S ∩ R
(R ∩ S) ∩ T = R ∩ (S ∩ T)
```

Distribución:

```text
(R ∪ S) ∩ T = (R ∩ T) ∪ (S ∩ T)
(R ∩ S) ∪ T = (R ∪ T) ∩ (S ∪ T)
```

### Producto y yunción natural

Son asociativos. Pueden considerarse conmutativos si se ignora el orden de presentación de los atributos:

```text
(R × S) × T = R × (S × T)
(R * S) * T = R * (S * T)
```

### Cascada de selecciones

```text
S(F1)(S(F2)(R)) = S(F1 ∧ F2)(R)
```

El orden de filtros conjuntivos puede cambiarse.

### Cascada de proyecciones

Si `L1 ⊆ L2`:

```text
P(L1)(P(L2)(R)) = P(L1)(R)
```

La proyección exterior solo puede pedir atributos conservados por la interior.

### Selección y proyección

```text
P(L)(S(F)(R)) = S(F)(P(L)(R))
```

solo si todos los atributos usados por `F` pertenecen a `L`.

> [!warning]
> Si se proyecta y se elimina un atributo necesario para el filtro, ya no se puede intercambiar el orden.

### Empujar selecciones hacia los operandos

Si `F1` solo usa atributos de `R` y `F2` solo de `S`:

```text
S(F1 ∧ F2)(R × S)
=
S(F1)(R) × S(F2)(S)
```

La misma idea se aplica a la yunción natural. Filtrar antes suele reducir mucho los resultados intermedios.

### Proyección y producto

Si `LR` y `LS` son las listas de atributos:

```text
P(L)(R × S)
=
P(L ∩ LR)(R) × P(L ∩ LS)(S)
```

Esta transformación presupone que se conservan todos los atributos necesarios para operaciones posteriores.

### Selección y operadores de conjuntos

Para `Θ ∈ {∪, ∩, -}`:

```text
S(F)(R Θ S) = S(F)(R) Θ S(F)(S)
```

### Proyección y unión

```text
P(L)(R ∪ S) = P(L)(R) ∪ P(L)(S)
```

> [!tip] Regla práctica de optimización
> Filtra pronto y conserva solo las columnas necesarias, pero no elimines atributos que se necesiten después para una condición, una yunción o el resultado final.

---

## 3.15 Vistas

> [!definition]
> Una **vista** es una expresión de consulta a la que se asigna un nombre.

```text
V1 = S(F1 ∧ F2)(R × S)
```

La vista puede reutilizarse para construir consultas más complejas.

### Vista ordinaria

- se almacena su definición, no el resultado;
- funciona como relación virtual;
- se recalcula cuando se consulta;
- no puede definirse recursivamente en el marco presentado por las diapositivas;
- en general, solo vistas suficientemente simples pueden actualizarse sin ambigüedad.

Las vistas también permiten crear sinónimos y renombrar atributos:

```text
V1 = R       conserva los nombres de R
V1(L) = R    usa los nombres indicados en L
```

### Usos

1. **Simplificar consultas:** encapsulan expresiones complejas.
2. **Proteger confidencialidad:** ocultan filas o columnas mediante selección y proyección.
3. **Aportar independencia lógica:** recrean una interfaz anterior aunque cambie el diseño subyacente.

### Vista materializada

Almacena tanto la definición como el contenido.

| Vista ordinaria | Vista materializada |
|---|---|
| Poco espacio adicional. | Necesita espacio para el resultado. |
| Recalcula al consultar. | Lee un resultado ya calculado. |
| Consulta potencialmente más lenta. | Consulta más rápida. |
| No requiere mantener contenido propio. | Debe refrescarse cuando cambian las tablas base. |

> [!note]
> Decir que una vista ordinaria «es lenta» es una simplificación. El coste real depende de la consulta, los índices y el optimizador. La idea esencial es que no conserva de forma permanente un resultado precalculado.

---

## 3.16 Álgebra extendida con nulos

Las diapositivas añaden operadores para trabajar con esquemas distintos y valores nulos.

### Unión externa

```text
R ∪E S
```

Generaliza la unión:

- los atributos homónimos deben tener dominios compatibles;
- el esquema resultado reúne los atributos de ambas relaciones;
- las tuplas se completan con nulos en los atributos que no existen en su relación de origen;
- los duplicados se eliminan.

### Yunción natural externa

```text
R YE S
```

Incluye las coincidencias de la yunción natural y también las tuplas sin pareja, completándolas con nulos.

- **izquierda:** conserva todas las tuplas del operando izquierdo;
- **derecha:** conserva todas las del derecho;
- **completa:** conserva las no emparejadas de ambos.

### Yunción posibilista

```text
R YP S
```

Compara atributos homónimos considerando que `?` puede coincidir con otro `?` o con cualquier valor. Si no hay atributos comunes, coincide con el producto cartesiano.

> [!warning]
> La yunción posibilista es una convención específica del material. No debe confundirse con la igualdad ordinaria de SQL, donde `NULL = valor` no es verdadero, sino desconocido.

---

## 3.17 Renombrado y comparación de una relación consigo misma

La hoja de problemas utiliza consultas en las que hay que comparar dos filas de una misma relación: personas que trabajan en más de una compañía, cuentas de un cliente en sucursales distintas o personas supervisadas por el mismo supervisor.

Para distinguir las dos copias se usa el **operador de renombrado**, que suele escribirse con la letra griega rho:

```text
ρ(NUEVO_NOMBRE)(R)
ρ(NUEVO_NOMBRE(nuevo1, nuevo2, ...))(R)
```

- La primera forma cambia el nombre de la relación.
- La segunda cambia también los nombres de sus atributos.

> [!example] Personas que trabajan en más de una compañía
> Partimos de `TRABAJA(nombre-persona, nombre-compañía, salario)` y creamos dos copias:
>
> ```text
> T1(persona1, compañía1, salario1) = TRABAJA
> T2(persona2, compañía2, salario2) = TRABAJA
>
> P(persona1)(
>   S(persona1 = persona2 ∧ compañía1 ≠ compañía2)(T1 × T2)
> )
> ```
>
> La igualdad asegura que ambas filas pertenecen a la misma persona y la desigualdad exige dos compañías diferentes.

### Cuándo hace falta renombrar

- al comparar dos filas de una misma tabla;
- cuando un producto contiene atributos con nombres ambiguos;
- cuando una yunción natural uniría columnas homónimas que no representan lo mismo;
- cuando hay que alinear nombres antes de una unión, diferencia o intersección.

> [!warning]
> Escribir simplemente `R × R` deja dos copias de los mismos nombres de atributo. Aunque se puedan calificar como `R1.A` y `R2.A`, hay que declarar esas copias o renombrarlas para que la expresión sea inequívoca.

---

## 3.18 Patrones lingüísticos frecuentes en problemas

### «Alguno» o «al menos uno»

Se obtiene una relación con las coincidencias necesarias y se proyecta el identificador buscado.

```text
Personas que trabajan en alguna compañía de La Laguna
=
P(nombre-persona)(
  TRABAJA * S(ciudad-compañía = 'La Laguna')(LOCALIZACIÓN)
)
```

### «Ninguno» o «no existe»

Se parte del universo finito de candidatos y se restan los que sí cumplen la propiedad.

```text
Personas que no trabajan en ninguna compañía
=
P(nombre-persona)(VIVE)
-
P(nombre-persona)(TRABAJA)
```

> [!tip]
> Para resolver «ninguno», formula primero el conjunto positivo «al menos uno» y réstalo del conjunto de candidatos válidos.

### «Solo» o «solamente»

Normalmente significa que **no existe un contraejemplo**. El patrón es:

```text
candidatos con alguna relación válida
-
candidatos con alguna relación prohibida
```

Por ejemplo, «hombres a quienes solo caen simpáticas mujeres casadas» se resuelve quitando de los hombres con alguna simpatía aquellos relacionados con alguna mujer no casada.

> [!warning]
> En lenguaje natural, «solo» puede exigir o no la existencia de al menos un caso. En estos ejercicios conviene construir primero el conjunto de candidatos que sí participan en la relación para evitar incluir personas sin ninguna relación por verdad vacía.

### «Todos»

Suele indicar un cociente o una formulación por ausencia de contraejemplos:

```text
R / S
```

devuelve los valores relacionados con todos los elementos de `S`.

También puede razonarse así:

```text
candidatos
-
candidatos a los que les falta al menos un elemento obligatorio
```

### «Al menos dos distintos»

Requiere dos copias renombradas, igualdad en el propietario y desigualdad en el elemento que debe variar.

### «El mínimo» o «el máximo»

Sin agregados, se elimina a quien tiene un competidor mejor:

```text
cuentas
-
cuentas para las que existe otra con saldo menor
```

Para hallar el máximo se invierte la comparación.

### Construcción por etapas

En expresiones largas es preferible nombrar resultados intermedios:

```text
LAGUNA = S(ciudad-compañía = 'La Laguna')(LOCALIZACIÓN)
TRABAJAN_LAGUNA = TRABAJA * LAGUNA
RESULTADO = P(nombre-persona)(TRABAJAN_LAGUNA)
```

Esto no cambia el significado y reduce errores de paréntesis, atributos y precedencia.

---

## 3.19 Resumen del álgebra

> [!summary]
> - Selección filtra filas; proyección elige columnas.
> - El producto crea todas las combinaciones.
> - Unión, diferencia e intersección requieren relaciones compatibles.
> - La yunción filtra un producto; la natural usa atributos homónimos.
> - El cociente resuelve consultas con «para todos».
> - Las actualizaciones pueden expresarse mediante unión y diferencia.
> - Las equivalencias permiten reescribir y optimizar consultas.
> - Una vista nombra una consulta; una materializada conserva además su resultado.
> - Los operadores externos incorporan tuplas no emparejadas mediante nulos.
> - El renombrado permite comparar una relación consigo misma sin ambigüedad.
> - «Ninguno» suele resolverse con diferencia, «todos» con cociente y «solo» eliminando contraejemplos.

---

# 4. Ejercicios integradores resueltos

Se utiliza el esquema:

```text
CLIENTE(DNI, NBC, CDC)
CUENTA(CS, NC, DNI, SLD)
PRESTAMO(CS, NP, DNI, I)
SUCURSAL(CS, NBS, CDS)
```

## 4.1 Ciudades de clientes con cuentas de saldo alto

**Enunciado:** ciudades donde residen los clientes que tienen alguna cuenta con saldo superior a 100000.

### Con yunción natural

```text
P(CDC)(S(SLD > 100000)(CLIENTE * CUENTA))
```

### Razonamiento

1. `CLIENTE * CUENTA` asocia clientes y cuentas por `DNI`.
2. `S(SLD > 100000)` conserva cuentas con saldo alto.
3. `P(CDC)` devuelve únicamente las ciudades y elimina duplicados.

---

## 4.2 Clientes con cuentas en al menos dos sucursales

**Enunciado:** DNI de clientes con cuentas en al menos dos sucursales distintas.

Se necesitan dos copias renombradas de `CUENTA`:

```text
C1(CS1, NC1, DNI1, SLD1) = CUENTA
C2(CS2, NC2, DNI2, SLD2) = CUENTA

P(DNI1)(
  S(DNI1 = DNI2 ∧ CS1 ≠ CS2)(C1 × C2)
)
```

### Razonamiento

1. El autorrenombrado permite comparar dos filas de la misma relación.
2. `DNI1 = DNI2` exige que ambas cuentas pertenezcan al mismo cliente.
3. `CS1 ≠ CS2` exige sucursales diferentes.
4. La proyección devuelve el DNI sin repeticiones.

> [!important]
> Para expresar «al menos dos» suele compararse la relación consigo misma mediante copias renombradas.

---

## 4.3 Clientes con cuenta en su ciudad

**Enunciado:** DNI de clientes con al menos una cuenta en una sucursal de la ciudad en la que viven.

```text
P(DNI)(
  S(CDC = CDS)(
    CLIENTE * CUENTA * SUCURSAL
  )
)
```

### Razonamiento

- La primera yunción natural conecta `CLIENTE` y `CUENTA` mediante `DNI`.
- La siguiente conecta la cuenta con `SUCURSAL` mediante `CS`.
- La selección compara la ciudad del cliente con la de la sucursal.
- La proyección elimina todos los atributos salvo `DNI`.

---

## 4.4 Sucursales con clientes de dos ciudades

**Enunciado:** códigos de sucursales que tienen alguna cuenta con titulares de Santa Cruz y alguna cuenta con titulares de La Laguna.

```text
SC = P(CS)(S(CDC = 'Santa Cruz')(CLIENTE * CUENTA))
LL = P(CS)(S(CDC = 'La Laguna')(CLIENTE * CUENTA))

Resultado = SC ∩ LL
```

La intersección exige que el código aparezca en ambos conjuntos.

---

## 4.5 Clientes con cuenta en todas las sucursales laguneras

**Enunciado:** DNI de clientes que tienen al menos una cuenta en todas las sucursales de La Laguna.

```text
PARES = P(DNI, CS)(CUENTA)
LAGUNA = P(CS)(S(CDS = 'La Laguna')(SUCURSAL))

Resultado = PARES / LAGUNA
```

La división descarta cualquier DNI al que le falte al menos uno de los códigos contenidos en `LAGUNA`.

### Caso límite

Si no hay sucursales en La Laguna, la condición universal es vacuamente verdadera en la formulación matemática: todo candidato de `P(DNI)(PARES)` satisface «para todas las sucursales del conjunto vacío». En ejercicios habituales se presupone que existe al menos una.

---

## 4.6 Clientes sin préstamos

**Enunciado adicional de repaso:** DNI de clientes que no tienen ningún préstamo.

```text
P(DNI)(CLIENTE) - P(DNI)(PRESTAMO)
```

Primero se obtiene el universo finito de clientes y después se restan los que aparecen en préstamos.

---

## 4.7 Optimización de una consulta

Consulta original para clientes de La Laguna con cuentas de saldo alto:

```text
P(CLIENTE.DNI)(
  S(CLIENTE.DNI = CUENTA.DNI
    ∧ CLIENTE.CDC = 'La Laguna'
    ∧ CUENTA.SLD > 100000)(
      CLIENTE × CUENTA
  )
)
```

Una expresión equivalente que filtra antes:

```text
P(DNI)(
  S(CDC = 'La Laguna')(CLIENTE)
  *
  S(SLD > 100000)(CUENTA)
)
```

La segunda suele crear resultados intermedios menores porque no construye primero todo el producto.

---

