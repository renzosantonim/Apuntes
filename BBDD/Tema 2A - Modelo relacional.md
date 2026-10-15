# Base de Datos - Tema 2A: El modelo relacional

Apuntes elaborados a partir de las 26 diapositivas de `Tema 2 - El modelo relacional.pdf`. Incluyen estructura, claves, valores nulos e integridad.

---

# 2. Tema 2. El modelo relacional

*Origen principal: páginas 2–26 de «Tema 2 - El modelo relacional».*

## 2.1 Origen e idea central

El modelo relacional fue propuesto por **Edgar F. Codd** en 1970. Durante esa década aparecieron prototipos como System R de IBM y, desde los años ochenta, el modelo pasó a dominar el mercado de bases de datos.

> [!definition]
> Una **base de datos relacional** es un conjunto de relaciones, cada una con un nombre único.

Una relación se suele representar como tabla, aunque «relación» es el concepto matemático y «tabla» su representación visual.

---

## 2.2 Relación, atributo, dominio y tupla

| Concepto | Significado | Ejemplo |
|---|---|---|
| Relación | Conjunto finito de tuplas con el mismo esquema. | `EMPLEADO` |
| Atributo | Propiedad nombrada de la relación. | `DNI`, `NOMBRE` |
| Dominio | Conjunto de valores permitidos para un atributo. | Fechas válidas |
| Tupla | Asociación de un valor por atributo. | `<123, Ana, 2026-09-01>` |
| Grado | Número de atributos. | `EMPLEADO` tiene grado 3. |
| Cardinalidad | Número de tuplas de una relación. | 250 empleados. |

Cada atributo posee un dominio. Las diapositivas suponen valores **atómicos**, es decir, tratados como indivisibles por el modelo.

### Definición formal

Si una relación tiene dominios $D_1, D_2, \ldots, D_n$, su contenido es un subconjunto finito de:

$$
D_1 \times D_2 \times \cdots \times D_n
$$

El producto cartesiano contiene todas las combinaciones posibles; la relación conserva solo las que pertenecen a su estado actual.

### Dominios cualitativos y cuantitativos

- **Cualitativos:** no tienen carácter numérico intrínseco, aunque puedan codificarse con números. Ejemplos: nombre, estado civil.
- **Cuantitativos:** representan magnitudes numéricas. Ejemplos: salario, edad, estatura.

> [!warning]
> Que un dato se escriba con dígitos no significa que sea cuantitativo. Un número de teléfono o un código postal es normalmente cualitativo: sumarlo o calcular su media no tiene sentido.

---

## 2.3 Esquema y extensión

Una relación tiene dos partes:

- **Esquema o intensión:** nombre de la relación y definición de sus atributos.
- **Extensión o contenido:** conjunto de tuplas existente en un momento concreto.

```text
EMPLEADO(DNI, NOMBRE, FECHA_ALTA)   ← esquema

12345678A | Ana  | 2026-09-01       ← extensión
87654321B | Luis | 2025-02-10
```

El esquema suele ser relativamente estable; la extensión cambia con inserciones, modificaciones y borrados.

El esquema global de la base de datos reúne los esquemas de todas sus relaciones.

### Esquema bancario usado en los ejercicios

```text
CLIENTE(DNI, NBC, CDC)
CUENTA(CS, NC, DNI, SLD)
PRESTAMO(CS, NP, DNI, I)
SUCURSAL(CS, NBS, CDS)
```

Interpretación empleada en estos apuntes:

| Atributo | Significado |
|---|---|
| `DNI` | Identificador del cliente. |
| `NBC` | Nombre del cliente. |
| `CDC` | Ciudad de domicilio del cliente. |
| `CS` | Código de sucursal. |
| `NC` | Número de cuenta. |
| `SLD` | Saldo. |
| `NP` | Número de préstamo. |
| `I` | Importe del préstamo. |
| `NBS` | Nombre de la sucursal. |
| `CDS` | Ciudad de la sucursal. |

Los atributos comunes, como `DNI` o `CS`, permiten asociar tuplas de relaciones diferentes.

> [!note] Orden de filas y columnas
> Las filas no tienen un orden significativo. Las diapositivas consideran importante el orden de las columnas porque utilizan tuplas posicionales como `<t1, ..., tn>`.
>
> En la formulación relacional basada en atributos nombrados, el nombre evita depender de la posición. En cualquier caso, al aplicar unión o diferencia hay que hacer corresponder correctamente atributos y dominios.

---

## 2.4 Variables de tupla y de dominio

Una variable de tipo tupla representa una fila de una relación.

```text
t ∈ CUENTA
t[SLD]       valor del atributo SLD en t
t[1]         valor del primer atributo, si se usa notación posicional
```

También puede escribirse una tupla como `<t1, ..., tn>`, donde cada componente es una variable de dominio.

Estas variables pueden cuantificarse:

- Existencial: `∃t` significa «existe al menos una tupla t».
- Universal: `∀t` significa «para toda tupla t».

Ejemplos conceptuales:

```text
Existe alguna cuenta con saldo mayor que 100000:
(∃t ∈ CUENTA)(t[SLD] > 100000)

Todas las cuentas tienen saldo mayor que 100:
(∀t ∈ CUENTA)(t[SLD] > 100)
```

---

## 2.5 Superclaves y claves

### Superclave

> [!definition]
> Una **superclave** es un conjunto de atributos cuyos valores identifican de forma única cada tupla de una relación.

Si `DNI` ya identifica a cada cliente, entonces `{DNI}` es superclave, pero también lo son `{DNI, NBC}` y `{DNI, NBC, CDC}`. Añadir atributos conserva la unicidad, aunque resulte innecesario.

Toda relación tiene al menos una superclave: en el peor caso, el conjunto de todos sus atributos, ya que no puede haber tuplas duplicadas.

### Clave candidata

> [!definition]
> Una **clave** o clave candidata es una superclave **minimal**: si se elimina cualquiera de sus atributos, deja de identificar unívocamente.

Minimal no significa «con el menor número de atributos entre todas las claves». Significa que ninguno de sus atributos sobra.

> [!example]
> En `MATRICULA(DNI, EMAIL, NUM_EXPEDIENTE)`, los tres atributos podrían ser únicos por separado. Entonces existen tres claves candidatas de un solo atributo.
>
> En otra relación, `{TIPO_DOCUMENTO, NUMERO}` podría ser clave compuesta aunque exista también una clave diferente de un solo atributo.

Los atributos que forman parte de alguna clave candidata se denominan **atributos principales**.

### Clave primaria y alternativas

- La **clave primaria** es la clave candidata escogida para identificar habitualmente las tuplas.
- Las demás son **claves alternativas**.

Factores para escoger la primaria:

| Criterio | Preferencia |
|---|---|
| Estabilidad | Que el valor no cambie con el tiempo. |
| Simplicidad | Pocos atributos y valores manejables. |
| Fiabilidad | Que pueda validarse y dificulte errores. |
| Universalidad | Que su uso sea ampliamente conocido. |

> [!important]
> La clave primaria no es «más única» que las alternativas. Todas las claves candidatas garantizan unicidad; una se elige como principal por motivos de diseño.

---

## 2.6 Claves ajenas y jerarquía referencial

> [!definition]
> Una **clave ajena o externa** es un conjunto de atributos de una relación hija que hace referencia a una clave de una relación padre.

Los dominios de los atributos que se corresponden deben ser compatibles.

Ejemplo:

```text
SUCURSAL(CS, NBS, CDS)        clave: CS
CUENTA(CS, NC, DNI, SLD)      clave ajena: CUENTA.CS → SUCURSAL.CS
```

- `CUENTA` es la tabla hija o referenciante.
- `SUCURSAL` es la tabla padre o referenciada.

La tabla padre y la hija pueden ser la misma. Por ejemplo:

```text
EMPLEADO(ID, NOMBRE, ID_JEFE)
ID_JEFE → EMPLEADO.ID
```

Esto es una **autorreferencia**.

### Jerarquía referencial

Las referencias forman un grafo de dependencias. En el caso más sencillo:

```text
SUCURSAL
   ├── CUENTA
   └── PRESTAMO

CLIENTE
   ├── CUENTA
   └── PRESTAMO
```

Para crear tablas se suelen crear primero las referenciadas y después las dependientes. Para eliminarlas, se sigue el orden contrario.

> [!note]
> Aunque las diapositivas hablan de «jerarquía», las referencias pueden formar un grafo, contener autorreferencias y no siempre constituir un árbol estricto.

---

## 2.7 Valores nulos y lógica ternaria

El valor nulo `?` representa información desconocida o incompleta.

Ejemplos:

- se desconoce el teléfono de un cliente;
- una nota aún no ha sido generada;
- una persona recién incorporada no tiene fecha de vacaciones anteriores.

> [!important]
> Nulo no significa cero, cadena vacía ni «no». Significa que no se dispone de un valor ordinario.

Para esta asignatura se adopta una única clase de nulo y se considera que una tupla duplica a otra si todas sus componentes coinciden, incluido nulo con nulo.

### Propagación del nulo

- Operación aritmética con nulo: `5 + ? = ?`.
- Comparación con nulo: `3 < ? = ?`.

Las comparaciones dejan de producir solo verdadero o falso y aparece una lógica de tres valores: `V`, `F`, `?`.

### Tablas de verdad

| `A ∧ B` | V | F | ? |
|---|---:|---:|---:|
| **V** | V | F | ? |
| **F** | F | F | F |
| **?** | ? | F | ? |

| `A ∨ B` | V | F | ? |
|---|---:|---:|---:|
| **V** | V | V | V |
| **F** | V | F | ? |
| **?** | V | ? | ? |

| A | `¬A` |
|---|---|
| V | F |
| F | V |
| ? | ? |

El operador `ISNULL(atributo)` devuelve verdadero si el valor es nulo y falso en caso contrario.

> [!warning]
> No se comprueba un nulo con `atributo = ?`, porque esa comparación vuelve a producir desconocido. Se necesita un operador específico como `ISNULL`.

---

## 2.8 Condiciones de integridad

> [!definition]
> Una **restricción de integridad** es una condición que deben satisfacer los datos para que el estado de la base sea formalmente válido.

### Integridad de dominio

Limita los valores permitidos:

- enteros entre 1 y 10;
- fechas posteriores a una fecha dada;
- municipios de una provincia;
- prohibición de nulos.

### Restricciones de unicidad

Impiden que dos tuplas compartan los mismos valores en un conjunto de atributos.

### Integridad de entidad

> [!definition]
> Ningún atributo de la clave primaria puede contener un valor nulo.

La clave primaria requiere unicidad y `NOT NULL`, porque no podría identificar sin ambigüedad si parte de su valor fuera desconocida.

### Integridad referencial

> [!definition]
> Todo valor no nulo de una clave ajena debe aparecer en la clave referenciada.

Si `CUENTA.CS = 7`, debe existir una sucursal con `SUCURSAL.CS = 7`, salvo que la clave ajena admita nulo y tome ese valor.

---

## 2.9 Actualizaciones e integridad referencial

### Operaciones sobre la tabla padre

| Operación | Comprobación y respuesta |
|---|---|
| Insertar padre | No rompe referencias existentes. |
| Borrar padre | Si hay hijas dependientes: rechazar, borrar en cascada o poner nulos cuando sea válido. |
| Modificar clave del padre | Si hay hijas: rechazar o propagar el nuevo valor en cascada. |

### Operaciones sobre la tabla hija

| Operación | Comprobación y respuesta |
|---|---|
| Borrar hija | No rompe la referencia desde otras filas por esta clave ajena. |
| Insertar hija | Su clave ajena no nula debe existir en el padre. |
| Modificar clave ajena | El nuevo valor no nulo debe existir en el padre. |

> [!example]
> No se puede insertar una cuenta de la sucursal 99 si no existe la sucursal 99. Tampoco se puede borrar una sucursal que aún tiene cuentas, salvo que la regla definida rechace, propague el borrado o transforme las referencias de una forma admitida.

> [!warning]
> Poner la clave ajena a nulo solo es posible si sus atributos admiten nulos. En una clave ajena compuesta también hay que respetar la convención exacta del SGBD y las restricciones declaradas.

---

## 2.10 Componentes del modelo relacional

| Componente del modelo | En el modelo relacional |
|---|---|
| Estructuras | Relaciones, atributos, dominios y tuplas. |
| Operadores | Selección, proyección, unión, diferencia, producto cartesiano, etc. |
| Integridad | Dominios, claves, nulos, entidad y referencia. |

### Resumen del modelo relacional

> [!summary]
> - Una relación posee esquema y extensión.
> - El grado cuenta atributos; la cardinalidad cuenta tuplas.
> - Una superclave identifica; una clave además es minimal.
> - La primaria es una clave candidata elegida; las demás son alternativas.
> - Una clave ajena conecta una hija con una clave de su padre.
> - Los nulos introducen un tercer valor lógico: desconocido.
> - La integridad de entidad prohíbe nulos en la primaria.
> - La integridad referencial exige que toda referencia no nula encuentre su fila padre.

---

