# Base de Datos - Tema 2C: Cálculo relacional

Apuntes elaborados a partir de las 32 diapositivas de `Tema 2 - Cálculo relacional.pdf`. Se amplía la teoría con ejemplos resueltos para poder seguir la asignatura sin haber asistido a las clases anteriores.

## 0. Idea general

El álgebra y el cálculo relacional permiten formular las mismas consultas básicas, pero las plantean de forma distinta:

```text
Álgebra relacional       → indica una secuencia de operaciones
Cálculo relacional       → describe la condición que debe cumplir el resultado
```

> [!important]
> El álgebra responde a «¿cómo construyo el resultado?».
>
> El cálculo responde a «¿qué propiedades deben cumplir las tuplas del resultado?».

El cálculo relacional se basa en la **lógica de predicados** y tiene dos variantes:

- **CRT - cálculo relacional de tuplas:** las variables representan tuplas completas.
- **CRD - cálculo relacional de dominios:** las variables representan valores individuales de atributos.

### Índice

- [[#1. Lógica proposicional y lógica de predicados]]
- [[#2. Operadores y equivalencias lógicas]]
- [[#3. Reglas de inferencia]]
- [[#4. Cuantificadores]]
- [[#5. Cálculo relacional de tuplas - CRT]]
- [[#6. Ejemplos resueltos en CRT]]
- [[#7. Seguridad y cálculo restringido]]
- [[#8. Cálculo relacional de dominios - CRD]]
- [[#9. Ejemplos resueltos en CRD]]
- [[#10. Comparación entre álgebra, CRT y CRD]]
- [[#11. Repaso y autoevaluación]]

---

# 1. Lógica proposicional y lógica de predicados

## 1.1 Proposiciones

> [!definition]
> Una **proposición lógica** es una oración declarativa que puede ser verdadera o falsa, pero no ambas cosas simultáneamente.

Ejemplos:

- «Está lloviendo» puede ser verdadera o falsa.
- «La cuenta 7 tiene saldo superior a 1000» puede evaluarse si conocemos la cuenta.
- «Cierra la ventana» no es una proposición: es una orden.
- «¿Qué saldo tiene la cuenta?» no es una proposición: es una pregunta.

La lógica proposicional trata cada proposición como una unidad. Si:

```text
P = «Ana trabaja en C1»
Q = «Ana vive en La Laguna»
```

podemos construir `P ∧ Q`, `P ∨ Q` o `P → Q`.

## 1.2 Predicados

> [!definition]
> Un **predicado** es una expresión que contiene variables y se convierte en proposición cuando estas reciben valores o quedan cuantificadas.

```text
TRABAJA_EN(x, 'C1')
SALDO(c) > 1000
VIVE_EN(x, ciudad)
```

`TRABAJA_EN(x, 'C1')` no tiene todavía un valor de verdad mientras `x` sea libre. Al sustituir `x` por una persona o cuantificarla, obtenemos una afirmación evaluable.

La lógica de predicados distingue:

- **qué se afirma:** el predicado;
- **de quién o de qué se afirma:** los objetos representados por las variables.

En los predicados pueden aparecer:

- constantes;
- variables;
- operadores aritméticos;
- comparaciones;
- conectores lógicos;
- cuantificadores.

---

# 2. Operadores y equivalencias lógicas

## 2.1 Operadores fundamentales

| Operador | Lectura | Cuándo es verdadero |
|---|---|---|
| `¬P` | no P | Cuando P es falsa. |
| `P ∧ Q` | P y Q | Cuando ambas son verdaderas. |
| `P ∨ Q` | P o Q | Cuando al menos una es verdadera. |
| `P → Q` | si P, entonces Q | Siempre salvo cuando P es verdadera y Q falsa. |
| `P ↔ Q` | P si y solo si Q | Cuando P y Q tienen el mismo valor. |

### Tabla de verdad

| P | Q | `¬P` | `P ∧ Q` | `P ∨ Q` | `P → Q` | `P ↔ Q` |
|---|---|---|---|---|---|---|
| V | V | F | V | V | V | V |
| V | F | F | F | V | F | F |
| F | V | V | F | V | V | F |
| F | F | V | F | F | V | V |

> [!important] Cómo entender la implicación
> `P → Q` solo promete que, si ocurre P, también ocurrirá Q. Cuando P es falsa, la implicación no queda incumplida y se considera verdadera.

## 2.2 Partes de una implicación

En `P → Q`:

- `P` es el **antecedente**, premisa o hipótesis;
- `Q` es el **consecuente**, consecuencia o conclusión.

Expresiones relacionadas:

| Nombre | Fórmula |
|---|---|
| Implicación original | `P → Q` |
| Recíproca | `Q → P` |
| Contrarrecíproca | `¬Q → ¬P` |
| Inversa | `¬P → ¬Q` |

La original equivale a su contrarrecíproca. La recíproca equivale a la inversa. En general, la original no equivale a su recíproca.

> [!example]
> «Si una fila tiene clave ajena no nula, existe la fila padre» no implica que toda fila padre tenga una fila hija.

## 2.3 Precedencia

Si no hay paréntesis, el orden usado en las diapositivas es:

1. `¬`
2. `∧`
3. `∨`
4. `→`
5. `↔`

> [!tip]
> Aunque conozcas la precedencia, utiliza paréntesis en expresiones largas. Facilitan la lectura y evitan errores al cuantificar o negar.

## 2.4 Tautología, contradicción y contingencia

- **Tautología:** siempre verdadera, como `P ∨ ¬P`.
- **Contradicción:** siempre falsa, como `P ∧ ¬P`.
- **Contingencia:** unas veces verdadera y otras falsa.

## 2.5 Equivalencias básicas

Dos fórmulas son equivalentes, `P ⇔ Q`, cuando producen la misma tabla de verdad.

### Identidad y dominación

```text
P ∧ V ⇔ P             P ∨ F ⇔ P
P ∧ F ⇔ F             P ∨ V ⇔ V
```

### Idempotencia y doble negación

```text
P ∨ P ⇔ P             P ∧ P ⇔ P
¬¬P ⇔ P
```

### Conmutatividad y asociatividad

```text
P ∨ Q ⇔ Q ∨ P
P ∧ Q ⇔ Q ∧ P

(P ∨ Q) ∨ R ⇔ P ∨ (Q ∨ R)
(P ∧ Q) ∧ R ⇔ P ∧ (Q ∧ R)
```

### Distributividad

```text
(P ∨ Q) ∧ R ⇔ (P ∧ R) ∨ (Q ∧ R)
(P ∧ Q) ∨ R ⇔ (P ∨ R) ∧ (Q ∨ R)
```

### Leyes de De Morgan

```text
¬(P ∧ Q) ⇔ ¬P ∨ ¬Q
¬(P ∨ Q) ⇔ ¬P ∧ ¬Q
```

Estas leyes son esenciales para traducir «no existen X que cumplan P» y para transformar consultas con negaciones.

### Absorción y negación

```text
P ∨ (P ∧ Q) ⇔ P
P ∧ (P ∨ Q) ⇔ P

P ∨ ¬P ⇔ V
P ∧ ¬P ⇔ F
```

## 2.6 Equivalencias con implicaciones

Las más útiles son:

```text
P → Q ⇔ ¬P ∨ Q
¬(P → Q) ⇔ P ∧ ¬Q
P → Q ⇔ ¬Q → ¬P
P ↔ Q ⇔ (P → Q) ∧ (Q → P)
```

Otras equivalencias incluidas en las diapositivas:

```text
P ∨ Q ⇔ ¬P → Q
P ∧ Q ⇔ ¬(P → ¬Q)

(P → Q) ∧ (P → R) ⇔ P → (Q ∧ R)
(P → R) ∧ (Q → R) ⇔ (P ∨ Q) → R
(P → Q) ∨ (P → R) ⇔ P → (Q ∨ R)
(P → R) ∨ (Q → R) ⇔ (P ∧ Q) → R
```

> [!tip]
> Para demostrar que alguien cumple una condición «para todos», la implicación resulta natural: «si una sucursal está en La Laguna, entonces existe una cuenta suya allí».

---

# 3. Reglas de inferencia

Una equivalencia permite sustituir una fórmula por otra con igual valor de verdad. Una **regla de inferencia** permite obtener una conclusión a partir de premisas.

| Regla | Esquema | Lectura |
|---|---|---|
| Adición | `P ⟹ P ∨ Q` | Si P es cierta, P o Q también. |
| Simplificación | `P ∧ Q ⟹ P` | De una conjunción puede extraerse un componente. |
| Conjunción | `P, Q ⟹ P ∧ Q` | Dos premisas verdaderas pueden unirse. |
| Modus ponens | `P, P → Q ⟹ Q` | Se cumple la condición y su consecuencia. |
| Modus tollens | `¬Q, P → Q ⟹ ¬P` | Si no ocurre Q, no pudo ocurrir P. |
| Silogismo hipotético | `P → Q, Q → R ⟹ P → R` | Encadena implicaciones. |
| Silogismo disyuntivo | `P ∨ Q, ¬P ⟹ Q` | Descarta una alternativa. |
| Resolución | `P ∨ Q, ¬P ∨ R ⟹ Q ∨ R` | Elimina literales opuestos. |

Estas reglas explican cómo pueden simplificarse o justificarse razonamientos, aunque para escribir consultas se emplean sobre todo conectores, cuantificadores y equivalencias.

---

# 4. Cuantificadores

## 4.1 Cuantificador existencial

```text
(∃x)(P(x))
```

Significa que existe **al menos un** valor de `x` para el que `P(x)` es verdadero.

> [!example]
> «Existe una cuenta de Ana con saldo superior a 1000» requiere encontrar una sola cuenta que cumpla ambas condiciones.

## 4.2 Cuantificador universal

```text
(∀x)(P(x))
```

Significa que `P(x)` es verdadero para todos los valores del dominio considerado.

> [!example]
> «Ana tiene cuenta en todas las sucursales de La Laguna» exige comprobar cada sucursal lagunera.

## 4.3 Negación de cuantificadores

```text
(∀x)P(x) ⇔ ¬(∃x)¬P(x)
(∃x)P(x) ⇔ ¬(∀x)¬P(x)

¬(∀x)P(x) ⇔ (∃x)¬P(x)
¬(∃x)P(x) ⇔ (∀x)¬P(x)
```

La idea práctica es muy importante:

```text
«todos cumplen P» ⇔ «no existe ninguno que incumpla P»
«ninguno cumple P» ⇔ «todos incumplen P»
```

## 4.4 Varias variables

Si `P(x,y)` depende de dos variables:

```text
(∃x,y)P(x,y) ⇔ (∃x)(∃y)P(x,y)
(∀x,y)P(x,y) ⇔ (∀x)(∀y)P(x,y)
```

Cuantificadores del mismo tipo pueden permutarse. Mezclar tipos cambia normalmente el significado:

```text
(∀x)(∃y)P(x,y)   cada x puede tener su propio y
(∃y)(∀x)P(x,y)   existe un único y que sirve para todos los x
```

> [!warning]
> «Cada cliente tiene alguna cuenta» no significa que exista una misma cuenta para todos los clientes.

---

# 5. Cálculo relacional de tuplas - CRT

## 5.1 Forma de una consulta

```text
{ t / P(t) }
```

Se lee: «conjunto de todas las tuplas `t` que satisfacen el predicado `P(t)`».

- `t` es la variable **libre** y determina el resultado.
- Las demás variables deben quedar **ligadas** por `∃` o `∀`.
- El dominio de cada variable ligada debe indicarse mediante su pertenencia a una relación.

> [!definition]
> Una variable está **libre** si no se encuentra bajo el alcance de un cuantificador. Está **ligada** si un cuantificador determina los valores que puede tomar.

En ejemplos donde el resultado tiene un solo atributo usaremos una notación cómoda:

```text
{ <d> / P(d) }
```

que representa una relación unaria cuyo atributo es el valor `d`.

## 5.2 Átomos permitidos

Un predicado se construye a partir de átomos como:

```text
s ∈ R
s[A] Θ u[B]
s[A] Θ C
```

donde:

- `s` y `u` son variables de tupla;
- `R` es una relación;
- `A` y `B` son atributos válidos;
- `C` es una constante compatible;
- `Θ` es un operador comparacional como `=`, `≠`, `<` o `>`.

Ejemplos:

```text
p ∈ PRESTAMO
p[I] > 100000
p[DNI] = c[DNI]
```

## 5.3 Construcción de predicados

Según la definición formal de las diapositivas:

1. Un átomo es un predicado.
2. Si `P` y `Q` son predicados, también lo son `¬P`, `(P)`, `P ∨ Q` y `P ∧ Q`.
3. Si `P(x)` es un predicado, también lo son `(∀x)P(x)` y `(∃x)P(x)`.
4. Todas las variables excepto la libre deben estar cuantificadas.

La implicación puede escribirse directamente o sustituirse por `¬P ∨ Q`.

## 5.4 Método para formular una consulta

1. Decide qué atributos debe devolver la variable libre.
2. Introduce una variable para cada relación necesaria.
3. Especifica la pertenencia de cada variable: `r ∈ R`.
4. Conecta las relaciones comparando atributos comunes.
5. Añade filtros constantes o comparaciones.
6. Cuantifica todas las variables que no formen parte del resultado.
7. Comprueba que el resultado está limitado por valores procedentes de la base de datos.

---

# 6. Ejemplos resueltos en CRT

Se utiliza el esquema de las diapositivas:

```text
CLIENTE(DNI, NBC, CDC)
CUENTA(CS, NC, DNI, SLD)
PRESTAMO(CS, NP, DNI, I)
SUCURSAL(CS, NS, CDS)
```

## 6.1 Clientes con préstamo superior a 100000

```text
{ <d> /
  (∃c,p)(
    c ∈ CLIENTE
    ∧ p ∈ PRESTAMO
    ∧ d = c[DNI]
    ∧ p[DNI] = c[DNI]
    ∧ p[I] > 100000
  )
}
```

La variable libre es `d`. `c` y `p` están ligadas y conectadas por el DNI.

## 6.2 En una sucursal concreta

```text
{ <d> /
  (∃p)(
    p ∈ PRESTAMO
    ∧ d = p[DNI]
    ∧ p[I] > 100000
    ∧ p[CS] = 1
  )
}
```

La clave ajena de `PRESTAMO` garantiza que el DNI corresponde a un cliente válido si la base cumple integridad referencial.

## 6.3 En alguna sucursal de La Laguna

```text
{ <d> /
  (∃p,s)(
    p ∈ PRESTAMO
    ∧ s ∈ SUCURSAL
    ∧ d = p[DNI]
    ∧ p[CS] = s[CS]
    ∧ p[I] > 100000
    ∧ s[CDS] = 'La Laguna'
  )
}
```

`p[CS] = s[CS]` realiza en lógica el mismo emparejamiento que una yunción.

## 6.4 Cuentas en al menos dos sucursales distintas

```text
{ <d> /
  (∃q1,q2)(
    q1 ∈ CUENTA
    ∧ q2 ∈ CUENTA
    ∧ d = q1[DNI]
    ∧ q1[DNI] = q2[DNI]
    ∧ q1[CS] ≠ q2[CS]
  )
}
```

Las dos variables de tupla cumplen el mismo papel que dos copias renombradas de `CUENTA` en álgebra.

## 6.5 Cuenta en una sucursal de la ciudad donde vive

```text
{ <d> /
  (∃c,q,s)(
    c ∈ CLIENTE
    ∧ q ∈ CUENTA
    ∧ s ∈ SUCURSAL
    ∧ d = c[DNI]
    ∧ c[DNI] = q[DNI]
    ∧ q[CS] = s[CS]
    ∧ c[CDC] = s[CDS]
  )
}
```

## 6.6 Préstamo o cuenta en la sucursal 1

```text
{ <d> /
  (∃p)(p ∈ PRESTAMO ∧ d = p[DNI] ∧ p[CS] = 1)
  ∨
  (∃q)(q ∈ CUENTA ∧ d = q[DNI] ∧ q[CS] = 1)
}
```

Cada cuantificador abarca únicamente su rama. Los paréntesis hacen visible ese alcance.

## 6.7 Préstamo y cuenta en la sucursal 1

```text
{ <d> /
  (∃p,q)(
    p ∈ PRESTAMO
    ∧ q ∈ CUENTA
    ∧ d = p[DNI]
    ∧ d = q[DNI]
    ∧ p[CS] = 1
    ∧ q[CS] = 1
  )
}
```

## 6.8 Préstamo pero no cuenta en la sucursal 1

```text
{ <d> /
  (∃p)(p ∈ PRESTAMO ∧ d = p[DNI] ∧ p[CS] = 1)
  ∧
  ¬(∃q)(q ∈ CUENTA ∧ d = q[DNI] ∧ q[CS] = 1)
}
```

> [!tip]
> «Pero no» se traduce normalmente como una condición positiva y la negación de otra existencia.

## 6.9 Cuenta en todas las sucursales de La Laguna

```text
{ <d> /
  (∃c)(c ∈ CLIENTE ∧ d = c[DNI])
  ∧
  (∀s)(
    s ∈ SUCURSAL ∧ s[CDS] = 'La Laguna'
    →
    (∃q)(q ∈ CUENTA ∧ q[DNI] = d ∧ q[CS] = s[CS])
  )
}
```

Lectura: para toda sucursal `s`, si `s` está en La Laguna, existe una cuenta `q` del cliente en esa sucursal.

Una forma equivalente usa ausencia de contraejemplos:

```text
{ <d> /
  (∃c)(c ∈ CLIENTE ∧ d = c[DNI])
  ∧
  ¬(∃s)(
    s ∈ SUCURSAL
    ∧ s[CDS] = 'La Laguna'
    ∧ ¬(∃q)(q ∈ CUENTA ∧ q[DNI] = d ∧ q[CS] = s[CS])
  )
}
```

## 6.10 Cliente con la cuenta de menor saldo

```text
{ <d> /
  (∃q)(
    q ∈ CUENTA
    ∧ d = q[DNI]
    ∧ ¬(∃q2)(q2 ∈ CUENTA ∧ q2[SLD] < q[SLD])
  )
}
```

La consulta no «calcula» un mínimo mediante una función. Escoge una cuenta para la que no existe otra con saldo menor. Si hay empate, devuelve los titulares de todas las cuentas mínimas.

Para limitarlo a la sucursal 1:

```text
{ <d> /
  (∃q)(
    q ∈ CUENTA
    ∧ q[CS] = 1
    ∧ d = q[DNI]
    ∧ ¬(∃q2)(
      q2 ∈ CUENTA
      ∧ q2[CS] = 1
      ∧ q2[SLD] < q[SLD]
    )
  )
}
```

---

# 7. Seguridad y cálculo restringido

## 7.1 El problema de los resultados infinitos

Una expresión como:

```text
{ t / t ∉ PRESTAMO }
```

pretende devolver todas las tuplas del universo que no pertenecen a `PRESTAMO`. Como los dominios pueden ser infinitos, el resultado también puede serlo.

> [!definition]
> Una expresión es **segura o sana** si puede evaluarse mediante un proceso finito y produce un resultado finito basado en los valores relevantes de la base de datos.

Todas las expresiones del álgebra relacional básica son seguras.

## 7.2 Cálculo restringido de tuplas

El **cálculo restringido de tuplas** conserva solo los predicados seguros que tienen una expresión equivalente en álgebra relacional.

El álgebra relacional y el CRT restringido tienen la misma potencia expresiva:

- toda expresión algebraica puede escribirse en CRT restringido;
- toda consulta de CRT restringido puede expresarse mediante álgebra.

> [!important]
> «Declarativo» no significa que cualquier fórmula lógica sea una consulta válida. Hay que restringir el cálculo para asegurar resultados finitos y evaluables.

---

# 8. Cálculo relacional de dominios - CRD

## 8.1 Diferencia esencial

En CRT, una variable representa una fila completa. En CRD, cada variable representa un valor de atributo.

```text
CRT: p ∈ PRESTAMO y se accede con p[DNI], p[I], ...
CRD: <cs, np, dni, importe> ∈ PRESTAMO
```

## 8.2 Forma de una consulta

```text
{ <x1, x2, ..., xn> / P(x1, x2, ..., xn) }
```

`x1, ..., xn` son las variables libres y forman la tupla resultado. Las demás variables deben estar cuantificadas.

## 8.3 Átomos permitidos

```text
<x1, x2, ..., xn> ∈ R
x Θ y
x Θ C
```

- La primera forma afirma que una combinación de valores pertenece a una relación.
- La segunda compara dos variables de dominio.
- La tercera compara una variable con una constante.

Los predicados se construyen con negación, conjunción, disyunción, paréntesis y cuantificadores, igual que en CRT.

> [!note] Errata de las diapositivas
> Las páginas de definición de CRD dicen en dos ocasiones «consulta en CRT». Por la forma de la expresión y el título, debe leerse **CRD**.

---

# 9. Ejemplos resueltos en CRD

## 9.1 Préstamo superior a 100000

El esquema de `PRESTAMO` es `<CS, NP, DNI, I>`:

```text
{ <d> /
  (∃cs,np,i)(
    <cs, np, d, i> ∈ PRESTAMO
    ∧ i > 100000
  )
}
```

## 9.2 En una sucursal de La Laguna

`SUCURSAL` tiene esquema `<CS, NS, CDS>`:

```text
{ <d> /
  (∃cs,np,i,ns,ciudad)(
    <cs, np, d, i> ∈ PRESTAMO
    ∧ <cs, ns, ciudad> ∈ SUCURSAL
    ∧ i > 100000
    ∧ ciudad = 'La Laguna'
  )
}
```

La variable compartida `cs` expresa directamente la igualdad entre los códigos de sucursal.

## 9.3 Cuentas en dos sucursales distintas

```text
{ <d> /
  (∃cs1,nc1,saldo1,cs2,nc2,saldo2)(
    <cs1, nc1, d, saldo1> ∈ CUENTA
    ∧ <cs2, nc2, d, saldo2> ∈ CUENTA
    ∧ cs1 ≠ cs2
  )
}
```

## 9.4 Cuenta en la ciudad donde vive

```text
{ <d> /
  (∃nombre,ciudad,cs,nc,saldo,ns)(
    <d, nombre, ciudad> ∈ CLIENTE
    ∧ <cs, nc, d, saldo> ∈ CUENTA
    ∧ <cs, ns, ciudad> ∈ SUCURSAL
  )
}
```

La misma variable `d` enlaza cliente y cuenta; `cs` enlaza cuenta y sucursal; `ciudad` obliga a que domicilio y sucursal coincidan.

## 9.5 Cuenta en todas las sucursales de La Laguna

```text
{ <d> /
  (∃nombre,ciudad)(<d, nombre, ciudad> ∈ CLIENTE)
  ∧
  (∀cs,ns,cds)(
    <cs, ns, cds> ∈ SUCURSAL ∧ cds = 'La Laguna'
    →
    (∃nc,saldo)(<cs, nc, d, saldo> ∈ CUENTA)
  )
}
```

---

# 10. Comparación entre álgebra, CRT y CRD

| Aspecto | Álgebra relacional | CRT | CRD |
|---|---|---|---|
| Estilo | Procedimental | Declarativo | Declarativo |
| Variable principal | Relaciones intermedias | Tuplas | Valores de atributos |
| Unión de tablas | Producto/yunción | Comparación entre atributos de tuplas | Variables compartidas o igualdades |
| «Existe» | Aparece mediante una combinación no vacía | `∃` sobre tuplas | `∃` sobre valores |
| «Todos» | Cociente o diferencia de contraejemplos | `∀` o `¬∃¬` | `∀` o `¬∃¬` |
| Seguridad | Incorporada en las operaciones básicas | Debe restringirse | Debe restringirse |

### La misma consulta en tres lenguajes

**DNI con préstamo superior a 100000:**

Álgebra:

```text
P(DNI)(S(I > 100000)(PRESTAMO))
```

CRT:

```text
{ <d> / (∃p)(p ∈ PRESTAMO ∧ d = p[DNI] ∧ p[I] > 100000) }
```

CRD:

```text
{ <d> / (∃cs,np,i)(<cs,np,d,i> ∈ PRESTAMO ∧ i > 100000) }
```

> [!tip]
> Si te atascas en cálculo, resuelve primero la consulta mentalmente en álgebra. Después sustituye cada relación usada por variables y condiciones de pertenencia.

---

# 11. Repaso y autoevaluación

## 11.1 Conceptos que conviene distinguir

| No confundir | Diferencia |
|---|---|
| Proposición / predicado | La proposición ya tiene valor; el predicado depende de variables. |
| Variable libre / ligada | La libre forma el resultado; la ligada está cuantificada. |
| `∃` / `∀` | Al menos uno frente a todos. |
| Recíproca / contrarrecíproca | `Q→P` frente a `¬Q→¬P`; solo la segunda equivale a la original. |
| CRT / CRD | Variables de tupla frente a variables de valor. |
| Cálculo general / restringido | Fórmulas lógicas cualesquiera frente a consultas seguras. |
| `¬∃P` / `∃¬P` | Ninguno cumple P frente a alguno incumple P. |

## 11.2 Traducción rápida

| Expresión verbal | Patrón lógico |
|---|---|
| «algún», «al menos uno» | `(∃x)P(x)` |
| «todos» | `(∀x)P(x)` |
| «ninguno» | `¬(∃x)P(x)` |
| «no todos» | `(∃x)¬P(x)` |
| «solo si» | Implicación. |
| «si y solo si» | Bicondicional o dos implicaciones. |
| «pero no» | `P ∧ ¬Q` |
| «mínimo» | Existe candidato y no existe otro menor. |

## 11.3 Preguntas de autoevaluación

1. ¿Por qué el cálculo relacional es declarativo?
2. ¿Cuándo es falsa una implicación?
3. ¿A qué fórmula equivale `P → Q` sin usar implicación?
4. ¿Cómo se niega `(∀x)P(x)`?
5. ¿Qué diferencia existe entre una variable libre y una ligada?
6. ¿Qué átomos pueden aparecer en CRT?
7. ¿Cómo se expresa una yunción en CRT?
8. ¿Por qué `{t / t ∉ R}` puede ser insegura?
9. ¿Qué representa una variable en CRD?
10. ¿Cómo se expresa «la cuenta de saldo mínimo» sin una función de mínimo?

<details>
<summary>Respuestas breves</summary>

1. Porque describe propiedades del resultado sin ordenar una secuencia de operaciones.
2. Solo cuando el antecedente es verdadero y el consecuente falso.
3. `¬P ∨ Q`.
4. `(∃x)¬P(x)`.
5. La libre aparece en el resultado; la ligada está bajo un cuantificador.
6. Pertenencia de tupla, comparación entre atributos y comparación con constantes.
7. Con variables de las dos relaciones y una igualdad entre sus atributos de enlace.
8. Porque el universo exterior a `R` puede ser infinito.
9. Un valor de dominio, no una tupla completa.
10. Escogiendo una cuenta para la que no exista otra con saldo menor.

</details>

## 11.4 Resumen del tema

> [!summary]
> - El cálculo relacional describe condiciones y se basa en lógica de predicados.
> - CRT usa variables de tupla; CRD usa variables de dominio.
> - Las variables que no forman el resultado deben quedar cuantificadas.
> - `∃` expresa existencia y `∀` universalidad.
> - Las leyes de De Morgan y las equivalencias de cuantificadores permiten trabajar con negaciones.
> - «Todos» puede escribirse como «no existe un contraejemplo».
> - El cálculo restringido evita resultados infinitos y tiene la misma potencia expresiva que el álgebra relacional básica.
