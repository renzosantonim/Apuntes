# Base de Datos - Tema 1: Introducción

Apuntes elaborados a partir de las 23 diapositivas de `Tema 1 - Introducción bases de datos.pdf`. Se reorganiza y amplía el material para poder estudiarlo desde cero.

---

# 1. Tema 1. Introducción a las bases de datos

*Origen principal: páginas 2–23 de «Tema 1 - Introducción bases de datos».*

## 1.1 Procesamiento tradicional mediante ficheros

Antes de los SGBD, era habitual que cada aplicación mantuviera sus propios ficheros de datos.

```text
Aplicación de ventas  ──→ fichero_clientes_ventas
Aplicación de cobros  ──→ fichero_clientes_cobros
Aplicación de envíos  ──→ fichero_clientes_envíos
```

Este enfoque se conoce como **sistema de ficheros** o procesamiento tradicional de datos. Sus características son:

- proliferan ficheros específicos para cada aplicación;
- proliferan programas creados para necesidades concretas;
- los programas pueden haberse desarrollado independientemente, con lenguajes y herramientas diferentes;
- el énfasis se pone en el proceso que realiza cada programa, no en una gestión común de la información.

### Redundancia e inconsistencia

La misma información puede aparecer repetida en varios ficheros.

> [!example]
> Si la dirección de Ana figura en ventas, cobros y envíos, hay **redundancia**. Si solo se actualiza en dos de los tres ficheros, aparece una **inconsistencia**: el sistema mantiene varias versiones incompatibles del mismo dato.

La redundancia también aumenta el almacenamiento y el coste de acceso.

### Dificultad de acceso y aislamiento

Cada fichero puede tener un formato diferente. Una consulta nueva, no prevista cuando se creó la aplicación, puede exigir escribir otro programa específico.

Los datos quedan **aislados** por sus formatos y por las aplicaciones que saben interpretarlos. Integrar información procedente de varios ficheros se vuelve costoso.

### Concurrencia

Si dos programas actualizan simultáneamente el mismo dato, pueden sobrescribirse entre sí.

> [!example] Actualización perdida
> Una cuenta tiene saldo 100.
>
> 1. El proceso A lee 100 y calcula un ingreso de 20.
> 2. El proceso B lee 100 y calcula un cargo de 10.
> 3. A escribe 120.
> 4. B escribe 90.
>
> El resultado correcto era 110, pero la escritura de B ha perdido la actualización de A.

### Confidencialidad e integridad

En un sistema de ficheros, cada aplicación debe implementar por su cuenta:

- quién puede acceder a qué información;
- qué valores son válidos;
- qué relaciones deben conservarse entre los datos.

Repetir estas comprobaciones en muchos programas aumenta la complejidad y facilita que las reglas se apliquen de manera desigual.

### Atomicidad y recuperación

Una operación lógica puede requerir varios cambios. Si el sistema falla a mitad, la información no debe quedar en un estado intermedio.

> [!definition]
> Una operación es **atómica** cuando se ejecuta por completo o no produce ningún efecto. No debe quedar «a medias».

En una transferencia bancaria, retirar dinero de una cuenta e ingresarlo en otra debe constituir una unidad. Si falla el segundo paso, hay que deshacer el primero.

### Difícil reestructuración

Los programas dependen directamente del formato de los ficheros. Cambiar ese formato obliga a modificar las aplicaciones que los usan.

| Problema | Consecuencia |
|---|---|
| Redundancia | Más espacio y varias copias que mantener. |
| Inconsistencia | Copias del mismo dato con valores distintos. |
| Consultas no previstas | Hay que crear programas adicionales. |
| Aislamiento | Es difícil combinar ficheros heterogéneos. |
| Concurrencia | Las actualizaciones pueden interferir. |
| Seguridad dispersa | Cada programa protege los datos por separado. |
| Integridad dispersa | Las mismas reglas se repiten en varias aplicaciones. |
| Falta de atomicidad | Un fallo puede dejar cambios incompletos. |
| Dependencia física | Cambiar los ficheros rompe los programas. |

---

## 1.2 Sistemas de bases de datos y SGBD

Los sistemas de bases de datos surgen para centralizar los problemas anteriores y orientar el sistema hacia los **datos**.

> [!definition]
> Una **base de datos** es una colección organizada de datos relacionados, diseñada para ser compartida y consultada de forma controlada.

> [!definition]
> Un **sistema gestor de bases de datos (SGBD)** es el software encargado de definir, almacenar, consultar, actualizar y controlar una base de datos.

Los ficheros físicos siguen existiendo, pero quedan ocultos tras el SGBD. El usuario trabaja con una representación abstracta y el gestor decide cómo localizar o modificar los datos.

### Funciones del SGBD

| Categoría | Qué permite hacer | Ejemplos |
|---|---|---|
| **Definición** | Crear o cambiar las estructuras y reglas. | Tablas, atributos, relaciones, restricciones. |
| **Manipulación** | Consultar o actualizar los datos. | Insertar, borrar, modificar, recuperar. |
| **Control** | Regular el uso correcto y seguro. | Autorización, transacciones, concurrencia. |

> [!important]
> El SGBD no elimina por arte de magia la redundancia o los errores. Proporciona mecanismos centralizados para diseñar bien la información, imponer restricciones y coordinar accesos.

---

## 1.3 Abstracción e independencia de datos

Un SGBD ofrece distintas perspectivas de la misma base de datos.

### Tres niveles de abstracción

| Nivel | Pregunta que responde | Contenido |
|---|---|---|
| **Físico o interno** | ¿Cómo se guardan realmente los datos? | Ficheros, páginas, índices, organización del almacenamiento. |
| **Conceptual** | ¿Qué datos existen y cómo se relacionan? | Entidades, atributos, tablas, relaciones y restricciones globales. |
| **Externo o de visión** | ¿Qué parte ve cada usuario o aplicación? | Vistas o subesquemas adaptados a cada necesidad. |

```text
Usuarios y aplicaciones
   ↓  vistas externas
Esquema conceptual global
   ↓  implementación
Esquema físico o interno
```

> [!example]
> Recursos Humanos puede ver nombre, puesto y salario. El directorio interno solo muestra nombre, departamento y extensión. Ambas vistas proceden de la misma base de datos, pero exponen información diferente.

### Independencia física

Es la capacidad de cambiar el esquema físico sin modificar el conceptual ni las aplicaciones.

Ejemplos:

- añadir un índice;
- cambiar la organización de un fichero;
- mover datos a otro dispositivo.

### Independencia lógica

Es la capacidad de cambiar el esquema conceptual sin obligar a cambiar las vistas externas o los programas que no necesitan verse afectados.

Ejemplos:

- añadir un atributo;
- dividir una tabla en dos y reconstruir su aspecto anterior mediante una vista;
- incorporar una nueva relación.

> [!tip]
> La independencia física separa la estructura lógica del almacenamiento. La independencia lógica separa las aplicaciones de ciertos cambios del esquema conceptual.

---

## 1.4 Modelos de datos

> [!definition]
> Un **modelo de datos** es un conjunto de herramientas conceptuales para describir los datos, sus relaciones, su significado y sus condiciones de integridad.

La descripción de una realidad mediante un modelo recibe el nombre de **esquema conceptual**.

### Componentes de un modelo

1. **Estructuras de datos:** objetos abstractos formados por datos.
2. **Operadores:** reglas para consultar o modificar las estructuras.
3. **Reglas de integridad:** condiciones que determinan qué estados son válidos.

El modelo relacional, por ejemplo, utiliza relaciones y tuplas como estructuras; selección, proyección o unión como operadores; y claves o restricciones referenciales como reglas de integridad.

### Categorías presentadas en las diapositivas

```text
Modelos lógicos
├── Basados en objetos
│   └── Modelo entidad-relación
└── Basados en registros
    └── Modelo relacional

Modelos físicos
└── Describen detalles de almacenamiento
```

### Modelo entidad-relación

El modelo E-R representa la realidad mediante **entidades**, **atributos** y **relaciones**.

| Elemento gráfico | Significado |
|---|---|
| Rectángulo simple | Entidad fuerte. |
| Rectángulo doble | Entidad débil. |
| Elipse simple continua | Atributo univaluado. |
| Elipse doble | Atributo multivaluado. |
| Elipse discontinua | Atributo derivado. |
| Rombo simple | Relación normal. |
| Rombo doble | Relación de dependencia. |
| Línea o liga | Conexión entre elementos. |

La cardinalidad de una relación puede ser 1:1, 1:N, N:1 o N:M.

### Modelo relacional

Representa datos y asociaciones mediante **tablas o relaciones**:

- una columna corresponde a un atributo;
- una fila o **tupla** asocia valores con un significado;
- cada tabla tiene un nombre único;
- los atributos de una tabla tienen nombres únicos.

Este modelo se desarrolla con detalle en el tema 2.

---

## 1.5 Lenguajes de bases de datos

### DDL: Data Definition Language

El **lenguaje de definición de datos** especifica el esquema:

- crea, borra o modifica estructuras;
- asigna nombres y tipos a los atributos;
- define relaciones;
- establece restricciones de integridad.

Las definiciones se registran en el **diccionario de datos**, que contiene metadatos: datos acerca de la propia base de datos.

### DML: Data Manipulation Language

El **lenguaje de manipulación de datos** permite:

- consultar o recuperar;
- insertar;
- modificar;
- borrar.

Las tres últimas son operaciones de **actualización**.

### DCL: Data Control Language

El **lenguaje de control de datos** gestiona permisos y autorizaciones.

> [!note]
> En SQL estas categorías sirven para clasificar sentencias. No necesariamente son tres programas distintos.

### Clasificaciones de los DML

#### Procedimentales y declarativos

| Tipo | El usuario indica | Ejemplo de las diapositivas |
|---|---|---|
| **Procedimental** | Qué datos quiere y qué secuencia de operaciones seguir. | Álgebra relacional. |
| **Declarativo** | Qué datos quiere, sin fijar el procedimiento. | Cálculo relacional. |

#### Conversacionales y diferidos

- **Conversacional:** las sentencias se ejecutan interactivamente y el resultado aparece tras cada una.
- **Diferido:** las sentencias forman parte de un programa o procedimiento que después se ejecuta.

#### Huéspedes e independientes

- Un DML **huésped** se integra en un lenguaje anfitrión de propósito general, como Java o C.
- Puede integrarse ampliando la sintaxis mediante un precompilador o mediante una API.
- **ODBC** y **JDBC** son tecnologías de conexión mencionadas en las diapositivas.
- Un DML **independiente** puede formar procedimientos sin apoyarse en otro lenguaje.

---

## 1.6 OLTP y OLAP

| Aspecto | OLTP | OLAP |
|---|---|---|
| Nombre | Online Transaction Processing | Online Analytical Processing |
| Objetivo | Operación diaria | Análisis y apoyo a decisiones |
| Carga predominante | Inserciones, modificaciones y borrados | Consultas complejas sobre gran volumen |
| Actualización | Continua | Escasa o mediante cargas periódicas/incrementales |
| Diseño habitual | Relacional y normalizado | Analítico, frecuentemente multidimensional |
| Ejemplo | Registrar una compra | Analizar ventas por región y trimestre |

> [!tip]
> OLTP pregunta «¿qué acaba de ocurrir?». OLAP pregunta «¿qué patrones aparecen en todo lo ocurrido?».

---

## 1.7 Usuarios de un sistema de bases de datos

| Perfil | Función principal |
|---|---|
| Operadores o usuarios de aplicaciones | Realizan el trabajo cotidiano, normalmente OLTP. |
| Desarrolladores | Construyen aplicaciones y utilizan el DML. |
| Administrador de bases de datos — DBA | Diseña, mantiene, controla permisos e integridad; usa sobre todo DDL y DCL. |
| Analistas de datos | Explotan la información, normalmente con orientación OLAP. |

---

## 1.8 Estructura interna de un SGBD

### Gestor de almacenamiento

Sirve de interfaz entre los datos de bajo nivel y los programas.

- **Gestor de archivos:** organiza el espacio y las estructuras físicas.
- **Gestor de memoria intermedia:** mueve y conserva temporalmente páginas entre disco y memoria.
- **Gestor de transacciones:** mantiene atomicidad y coordina operaciones concurrentes.
- **Gestor de autorizaciones e integridad:** comprueba permisos y restricciones.

### Procesador de consultas

- **Intérprete DDL/DCL:** procesa definiciones y las registra en el diccionario.
- **Compilador DML:** traduce la consulta a un plan de evaluación de bajo nivel.
- **Motor de evaluación:** ejecuta ese plan.

```text
Sentencia del usuario
        ↓
Procesador de consultas → plan de evaluación
        ↓
Gestor de almacenamiento
        ↓
Datos físicos
```

> [!important]
> Una consulta indica el resultado deseado. El SGBD puede estudiar varias formas de obtenerlo y escoger un plan más eficiente.

---

## 1.9 Arquitecturas de aplicaciones

### Dos capas

```text
Cliente con la aplicación ↔ Servidor de base de datos
```

La aplicación cliente se comunica directamente con el SGBD.

### Tres capas

```text
Cliente / interfaz
        ↕
Servidor de aplicaciones
        ↕
Servidor de base de datos
```

La capa intermedia contiene la lógica de negocio, valida operaciones y centraliza el acceso a los datos.

### Resumen del tema 1

> [!summary]
> - Los sistemas de ficheros dispersan datos y reglas entre aplicaciones.
> - Un SGBD centraliza definición, manipulación y control.
> - Los niveles físico, conceptual y externo aportan abstracción.
> - La independencia permite modificar un nivel sin afectar innecesariamente a los superiores.
> - Un modelo define estructuras, operadores y restricciones.
> - DDL define, DML consulta o actualiza y DCL controla permisos.
> - OLTP soporta la operación diaria; OLAP analiza grandes volúmenes.
> - El procesador de consultas y el gestor de almacenamiento cooperan para ejecutar las peticiones.

---

