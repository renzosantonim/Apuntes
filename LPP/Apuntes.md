# Lenguajes y Paradigmas de la Programación

## 0. Idea general de estos apuntes

En esta asignatura estudiamos diferentes formas de **expresar y organizar un programa**.

Un mismo problema puede resolverse describiendo instrucciones que cambian datos, organizando objetos que colaboran, componiendo funciones o coordinando tareas concurrentes.

> [!important]
> Un **lenguaje de programación** proporciona la notación.
>
> Un **paradigma de programación** proporciona una forma de pensar y estructurar la solución.
>
> Un lenguaje puede permitir varios paradigmas. En estos apuntes, Ruby sirve como hilo conductor de muchos ejemplos.


> [!note] Numeración del documento original
> El manuscrito contiene «Tema 1», «Tema 2», «Tema 4. Programación funcional» y «Tema 5. Programación concurrente», además de pruebas unitarias y TDD.
>
> No aparece un encabezado independiente de «Tema 3». Además, las hojas de programación funcional llevan numeración inferior `3.1` y `3.2`, aunque su título dice «Tema 4».
>
> Se mantienen los títulos visibles. Esto describe el PDF recibido; no confirma el temario del curso actual.

### Índice

- [[#1. Tema 1. Introducción a los lenguajes de programación]]
- [[#2. Tema 2. Programación imperativa]]
- [[#3. Orientación a objetos y Ruby — continuación del tema 2]]
- [[#4. Tema 4. Programación funcional]]
- [[#5. Tema 5. Programación concurrente]]
- [[#6. Pruebas unitarias y TDD]]
- [[#7. Repaso global]]
- [[#8. Correspondencia con el PDF y aclaraciones]]

---

# 1. Tema 1. Introducción a los lenguajes de programación

## 1.1 ¿Qué es un lenguaje de programación?

> [!definition]
> Un lenguaje de programación es una notación formal que permite expresar datos y operaciones para que un computador pueda realizar una tarea.

Partimos de un problema, lo describimos con precisión, diseñamos un algoritmo y lo expresamos en un lenguaje de programación.

```text
Problema
   ↓
Formalización del problema
   ↓
Algoritmo
   ↓
Programa escrito en un lenguaje
   ↓
Traducción o interpretación y ejecución
```

Por ejemplo, para calcular una media:

1. **Problema:** obtener la nota media de varios exámenes.
2. **Formalización:** sumar las notas y dividir por el número de exámenes.
3. **Algoritmo:** obtener la suma, contar los elementos y realizar la división.
4. **Programa:** expresar esas operaciones en un lenguaje concreto.

---

## 1.2 Primitivas, combinación y abstracción

Los apuntes distinguen tres elementos básicos:

| Elemento | Idea | Ejemplo orientativo |
|---|---|---|
| **Primitivas** | Elementos básicos con los que trabaja el lenguaje. | Valores y operaciones elementales. |
| **Combinación o agrupación** | Formas de unir elementos sencillos. | Expresiones, secuencias y bloques. |
| **Abstracción** | Dar una identidad a una operación o estructura y ocultar sus detalles. | Funciones, clases y módulos. |

> [!tip]
> Abstraer permite usar una operación sin repetir ni conocer todos sus pasos internos.
>
> Por ejemplo, llamar a `calcular_media(notas)` expresa la intención sin escribir de nuevo el cálculo.

Entre los factores que favorecen la adopción de un lenguaje, el manuscrito menciona:

- claridad;
- una curva de aprendizaje asumible;
- condiciones de licencia.

---

## 1.3 ¿Qué es un paradigma?

> [!definition]
> Un paradigma de programación es un modelo o enfoque para organizar un programa y expresar su cómputo.

### Programación imperativa

Expresa **cómo resolver el problema** mediante instrucciones que modifican el estado del programa.

```ruby
suma = 0
[2, 4, 6].each do |numero|
  suma = suma + numero
end
```

La variable `suma` cambia durante la ejecución.

### Programación declarativa

Pone el foco en **qué resultado o relación se quiere obtener**.

El esquema original distingue:

- **Programación funcional:** utiliza funciones y su composición.
- **Programación lógica:** utiliza hechos, reglas y relaciones lógicas.

### Esquema del manuscrito

```text
Mayor cercanía a la descripción del problema
│
├── Declarativa
│   ├── Funcional
│   └── Lógica
│
├── Imperativa
│   ├── Scripting
│   ├── Orientación a objetos
│   └── Modelo de Von Neumann
│
└── Ensamblador: cercanía a la máquina
```

> [!note] Cómo interpretar este esquema
> Es un mapa introductorio, no una clasificación excluyente. La orientación a objetos puede combinarse con otros estilos y el scripting describe una forma de uso de los lenguajes, sin imponer un único paradigma.
>
> El ensamblador es un lenguaje de bajo nivel; no es, por sí mismo, un paradigma.

---

## 1.4 Compilación e interpretación

### Compilación

Un compilador traduce un programa a otra representación. En el modelo clásico de compilación nativa, se obtiene código que acaba formando un ejecutable.

Una vez generado, ese ejecutable puede ejecutarse repetidamente. Si cambia el código fuente, normalmente hay que volver a compilar las partes afectadas.

### Interpretación

Un intérprete ejecuta el programa a partir de su código fuente o de una representación intermedia.

Para ejecutar el programa en otra plataforma se necesita una implementación compatible, además de las dependencias que utilice.

| Aspecto | Compilación nativa clásica | Interpretación |
|---|---|---|
| Traducción | Se realiza antes de ejecutar el resultado. | El intérprete procesa o ejecuta la representación del programa. |
| Repetición | Se reutiliza el ejecutable generado. | Se vuelve a utilizar el intérprete. |
| Portabilidad | El ejecutable depende de su plataforma de destino. | Depende de disponer de un intérprete y un entorno compatibles. |
| Rendimiento | Puede beneficiarse de optimizaciones previas. | Depende de la implementación y del programa. |

Para visualizar el coste de compilar una vez y ejecutar $n$ veces:

$$
T_{\text{total}} \approx T_{\text{compilación}} + n \cdot T_{\text{ejecución}}
$$

> [!warning] Aclaración del original
> Interpretar no significa necesariamente «compilar todo cada vez». Tampoco compilación e interpretación son categorías incompatibles: una implementación puede combinar ambas, por ejemplo compilando a una representación intermedia que después ejecuta una máquina virtual.
>
> «Compilado» tampoco garantiza por sí solo que cualquier programa sea más rápido.

---

## 1.5 Fases del procesamiento de un programa

### 1. Análisis léxico

Agrupa caracteres en **tokens**, como identificadores, números, operadores y palabras reservadas.

Por ejemplo:

```text
x = 3 + 2
```

contiene un identificador, una asignación, dos números y un operador de suma.

### 2. Análisis sintáctico

Comprueba si la secuencia de tokens respeta la **gramática** del lenguaje y construye su estructura sintáctica.

### 3. Análisis semántico

Comprueba restricciones de significado, como usos válidos de nombres y compatibilidad de tipos, según el lenguaje.

En un lenguaje con una declaración de entero, asignarle una cadena puede ser un error de tipos:

```text
entero r = "Hola"
```

Este es un ejemplo conceptual, no sintaxis de Ruby. En los lenguajes dinámicos algunas comprobaciones ocurren durante la ejecución.

### 4. Representación intermedia y optimización

El programa puede convertirse en una representación interna y transformarse para mejorar su ejecución sin cambiar su comportamiento observable.

### 5. Generación de código, ensamblado y enlazado

Una cadena clásica de herramientas nativas puede seguir este orden:

```text
Fuente → análisis léxico → análisis sintáctico → análisis semántico
       → representación intermedia → optimización
       → generación de código ensamblador → ensamblado
       → código objeto → enlazado → ejecutable
```

- El **ensamblador** transforma código ensamblador en código objeto.
- El **enlazador** une código objeto y bibliotecas, resolviendo referencias entre ellos.

> [!warning] Corrección del esquema original
> El manuscrito sitúa el enlazado antes del ensamblado. En la cadena clásica descrita aquí, el ensamblado precede al enlazado.
>
> Las implementaciones concretas pueden integrar u omitir fases; no todos los lenguajes recorren exactamente esta cadena.

---

## 1.6 Resumen del tema 1

> [!summary]
> - Un lenguaje permite expresar programas.
> - Un paradigma organiza la manera de plantearlos.
> - Las primitivas se combinan y se abstraen.
> - La programación imperativa describe pasos y cambios de estado.
> - La declarativa pone el foco en resultados y relaciones.
> - Léxico, sintaxis y semántica responden a preguntas diferentes.
> - Compilar, interpretar, ensamblar y enlazar no son sinónimos.

---

# 2. Tema 2. Programación imperativa

## 2.1 Relación con la arquitectura de Von Neumann

La programación imperativa refleja el modelo de una máquina que ejecuta instrucciones y modifica datos almacenados en memoria.

Sus elementos característicos son:

- variables y estado;
- asignaciones;
- secuencias de instrucciones;
- estructuras de control.

> [!definition]
> El **estado** del programa es la información que describe su situación en un momento de la ejecución, incluidos los valores de sus variables.

La CPU dispone de registros y accede a la memoria para obtener instrucciones y datos.

> [!note] Memoria de programa y memoria de datos
> El dibujo original separa ambas para explicar qué contienen. En el modelo clásico de Von Neumann, instrucciones y datos comparten memoria. La separación del dibujo debe entenderse como una distinción funcional.

---

## 2.2 Organización de la memoria

El manuscrito distingue tres zonas conceptuales:

| Zona | Qué almacena | Idea de duración |
|---|---|---|
| **Almacenamiento estático** | Datos con duración estática. | Pueden existir durante toda la ejecución. |
| **Pila — stack** | Información de llamadas activas a subprogramas. | Se incorpora y retira al entrar y salir de llamadas. |
| **Montículo — heap** | Datos reservados dinámicamente. | Su duración no tiene por qué coincidir con una llamada. |

```text
┌───────────────────────────┐
│ Almacenamiento estático   │
├───────────────────────────┤
│ Pila: llamadas activas    ↓│
├───────────────────────────┤
│ Espacio disponible        │
├───────────────────────────┤
│ Heap: datos dinámicos    ↑ │
└───────────────────────────┘
```

Las flechas reproducen la idea del dibujo: el sentido de crecimiento y la distribución real dependen de la implementación.

> [!important]
> La pila organiza las llamadas activas. El heap permite que ciertos datos sobrevivan al retorno de la función que los creó.
>
> No todos los objetos de todos los lenguajes deben almacenarse necesariamente en el heap.

---

## 2.3 Programación procedural

> [!definition]
> La programación procedural organiza el programa en subprogramas, procedimientos o funciones, cada uno con una responsabilidad.

En vez de escribir toda la solución seguida, se divide en operaciones reutilizables.

```text
Programa principal
├── leer_datos
├── procesar_datos
└── mostrar_resultado
```

Esta división facilita comprender, reutilizar y comprobar cada parte.

---

## 2.4 Pila y registros de activación

> [!definition]
> Un **registro de activación** almacena la información necesaria para gestionar una llamada concreta a un subprograma.

El esquema del original incluye:

| Parte | Función |
|---|---|
| Valor de retorno | Resultado que debe recibir quien hizo la llamada. |
| Parámetros | Información de entrada. |
| Zona de control | Datos para continuar la ejecución al terminar la llamada. |
| Variables locales | Datos propios de esa activación. |
| Temporales | Resultados intermedios de operaciones. |

Si `principal` llama a `f`, y `f` llama a `g`:

```text
Parte superior de la pila
┌──────────────────┐
│ Activación de g  │ ← llamada más reciente
├──────────────────┤
│ Activación de f  │
├──────────────────┤
│ principal        │
└──────────────────┘
```

Cuando `g` termina, se retira su activación y continúa `f`.

> [!tip]
> En una función recursiva puede haber varias activaciones de la misma función, cada una con sus parámetros y variables locales.

> [!note] Ámbito y duración
> El **ámbito** indica dónde puede utilizarse un nombre en el código.
>
> La **duración** indica durante qué parte de la ejecución existe un dato.
>
> La pila ayuda a gestionar activaciones, pero no define por sí sola las reglas de ámbito de un lenguaje. Además, algunos datos de la llamada pueden almacenarse en registros u otras estructuras.

---

## 2.5 Programación estructurada

La programación estructurada organiza el **flujo de control** mediante estructuras claras:

1. **Secuencia:** ejecutar instrucciones en orden.
2. **Selección:** elegir una alternativa según una condición.
3. **Iteración:** repetir instrucciones.

```ruby
suma = 0

[1, 2, 3, 4].each do |numero|
  if numero.even?
    suma = suma + numero
  end
end

suma # => 6
```

Aquí aparecen una secuencia, una selección (`if`), una iteración (`each`) y asignaciones.

> [!important]
> La idea central del principio de programación estructurada es poder construir programas mediante secuencia, selección e iteración, sin depender de saltos arbitrarios.

> [!note] Aclaración del original
> «Se basa en el manejo de datos» es demasiado general para definirla. Lo distintivo de la programación estructurada es la organización del control.
>
> Procedural y estructurada son compatibles: un programa puede dividirse en funciones y utilizar control estructurado dentro de cada una.

---

## 2.6 Resumen de programación imperativa

> [!summary]
> - Las instrucciones modifican el estado del programa.
> - La memoria puede explicarse mediante almacenamiento estático, pila y heap.
> - Las funciones permiten organizar el código.
> - Cada llamada necesita información de activación.
> - La programación estructurada usa secuencia, selección e iteración.

---

# 3. Orientación a objetos y Ruby — continuación del tema 2

*Origen: páginas 8–15 del PDF.*

## 3.1 Objetos y encapsulación

> [!definition]
> Un **objeto** reúne datos que representan su estado y métodos que definen su comportamiento.

Por ejemplo, un objeto que representa una cuenta puede contener:

- un saldo;
- un titular;
- operaciones para consultar o modificar el saldo.

La **encapsulación** agrupa esa información y permite controlar cómo se accede a ella.

```text
Objeto
├── Datos: características y estado
└── Métodos: comportamiento
```

---

## 3.2 Clases e instancias

> [!definition]
> Una **clase** define la estructura y el comportamiento de sus instancias.
>
> Una **instancia** es un objeto concreto creado a partir de esa clase.

Ejemplo desarrollado:

```ruby
class Persona
  attr_reader :nombre

  def initialize(nombre)
    @nombre = nombre
  end

  def to_s
    "Persona: #{@nombre}"
  end
end

ana = Persona.new("Ana")
luis = Persona.new("Luis")

ana.nombre # => "Ana"
luis.nombre # => "Luis"
ana.to_s # => "Persona: Ana"
```

`ana` y `luis` pertenecen a la misma clase, pero mantienen un estado independiente.

---

## 3.3 Variables y métodos de instancia y de clase

### Variables

| Tipo | Notación en Ruby | Significado |
|---|---|---|
| Variable de instancia | `@nombre` | Pertenece al objeto receptor. |
| Variable de clase | `@@contador` | Se comparte en la clase y su jerarquía de herencia. |

> [!note]
> En Ruby las clases también son objetos. Una variable `@x` utilizada sobre el objeto clase es una variable de instancia de ese objeto clase; no equivale a `@@x`.

### Métodos

| Tipo | Definición habitual dentro de una clase | Llamada |
|---|---|---|
| Método de instancia | `def nombre` | `objeto.nombre` |
| Método de clase | `def self.nombre` | `Clase.nombre` |

```ruby
class Saludo
  def mensaje
    "Hola desde una instancia"
  end

  def self.descripcion
    "Clase para producir saludos"
  end
end

Saludo.new.mensaje
Saludo.descripcion
```

---

## 3.4 `initialize`, `attr_reader` y `to_s`

El original destaca estos tres elementos al definir clases:

| Elemento | Utilidad |
|---|---|
| `initialize` | Establece el estado inicial de una instancia. |
| `attr_reader` | Genera métodos de lectura para atributos. |
| `to_s` | Produce una representación textual del objeto. |

> [!warning] No son requisitos obligatorios
> El manuscrito dice que una clase «completa» debe tenerlos. Son elementos útiles para sus ejercicios, pero Ruby no obliga a definir los tres en todas las clases.

---

## 3.5 Diferencia entre `new` e `initialize`

> [!important]
> `new` crea y devuelve la instancia.
>
> `initialize` prepara su estado inicial.

Conceptualmente, el comportamiento habitual de `Clase.new(argumentos)` es:

```text
1. Reservar y crear una instancia de Clase.
2. Invocar initialize sobre ella con los argumentos.
3. Devolver la instancia creada.
```

> [!warning] Corrección del pseudocódigo original
> La instancia devuelta por `new` no se sustituye por el resultado que devuelva `initialize`.
>
> Aunque la última expresión de `initialize` sea un número o una cadena, la llamada habitual a `Clase.new` devuelve el objeto recién creado.

---

## 3.6 Recolección de basura

Ruby utiliza un **recolector de basura** para recuperar memoria de objetos que dejan de ser alcanzables.

Por ello no hay que definir un destructor que libere manualmente la memoria de cada objeto.

> [!note]
> Recuperar memoria no equivale a gestionar todos los recursos externos. Por ejemplo, un fichero abierto debe cerrarse adecuadamente.

---

## 3.7 Clase, tipo y duck typing

Para conocer la clase de un objeto:

```ruby
"Hola".class # => String
```

Para saber si responde a una operación:

```ruby
"Hola".respond_to?(:upcase) # => true
```

En el enfoque de estos apuntes:

- la **clase** indica de qué clase es instancia el objeto;
- el **tipo**, entendido como protocolo de uso, se relaciona con las operaciones que admite.

> [!definition]
> El **duck typing** consiste en utilizar un objeto por el comportamiento que ofrece, sin exigir que pertenezca a una clase concreta.

La pregunta práctica es: «¿Puede realizar las operaciones que necesito?».

> [!note]
> Que un método exista no garantiza que haga lo esperado. También debe aceptar los argumentos y respetar el significado que requiere el programa.

---

## 3.8 Polimorfismo

> [!definition]
> El **polimorfismo** permite que una misma operación trabaje con objetos distintos, usando el comportamiento que ofrece cada uno.

El original usa la idea de una función que suma uno:

```ruby
def incrementar(algo)
  algo + 1
end

incrementar(3)   # => 4
incrementar(2.5) # => 3.5
```

También puede funcionar con una clase propia que implemente `+` de forma compatible.

```ruby
class NumeroEnvuelto
  attr_reader :valor

  def initialize(valor)
    @valor = valor
  end

  def +(otro)
    NumeroEnvuelto.new(@valor + otro)
  end
end

incrementar(NumeroEnvuelto.new(4)).valor # => 5
```

> [!important]
> El polimorfismo no significa que cualquier objeto sirva para cualquier operación. Debe cumplir el protocolo que se utiliza.

---

## 3.9 Herencia

La herencia permite definir una clase a partir de otra y reutilizar o especializar su comportamiento.

```ruby
class Animal
  def sonido
    "Sonido genérico"
  end
end

class Perro < Animal
  def sonido
    "Guau"
  end
end
```

- `Animal` es la superclase.
- `Perro` es la subclase.
- `Perro#sonido` redefine el comportamiento heredado.

La relación de superclases del ejemplo del manuscrito es:

```text
Array → Object → BasicObject
```

Las flechas significan «hereda de». No muestran todos los módulos incluidos.

### Uso de `super`

`super` invoca la siguiente implementación del **mismo método** en la cadena de búsqueda.

```ruby
class PersonaConEdad < Persona
  attr_reader :edad

  def initialize(nombre, edad)
    super(nombre)
    @edad = edad
  end
end
```

> [!warning] Corrección del original
> En Ruby no se utiliza `super.metodo` como sintaxis general para llamar a un método del padre.
>
> - `super`: reenvía los argumentos recibidos por el método actual.
> - `super()`: llama sin argumentos.
> - `super(x)`: pasa explícitamente `x`.
>
> No se limita a `initialize`.

---

## 3.10 Visibilidad

Ruby distingue métodos:

- **Públicos — `public`:** forman parte de la interfaz accesible desde fuera.
- **Protegidos — `protected`:** permiten acceso en contextos de objetos de la clase o su jerarquía, sujeto a las reglas de Ruby.
- **Privados — `private`:** se reservan para uso interno y normalmente se llaman sin receptor explícito.

> [!tip]
> Piensa en la visibilidad como una forma de separar las operaciones ofrecidas al usuario de una clase de los pasos internos necesarios para implementarlas.

---

## 3.11 Módulos: espacios de nombres y mixins

> [!definition]
> Un **módulo** agrupa constantes, clases y métodos relacionados.

El manuscrito destaca dos usos.

### A. Espacio de nombres

Evita confusiones entre elementos que tienen el mismo nombre.

```ruby
module Geometria
  VERSION = "1.0"

  class Punto
  end

  def self.descripcion
    "Operaciones geométricas"
  end
end

Geometria::VERSION
Geometria::Punto.new
Geometria.descripcion
```

- `::` permite acceder a clases y constantes del espacio de nombres.
- `.` permite invocar un método del módulo.

### B. Mixin

Permite incorporar comportamiento de un módulo a una clase.

```ruby
module Saludable
  def saludar
    "Hola"
  end
end

class Usuario
  include Saludable
end

Usuario.new.saludar # => "Hola"
```

Si el módulo está en otro fichero, primero se carga con `require` o `require_relative`, según cómo se localice el archivo, y después se incluye.

### Módulos destacados en los apuntes

| Módulo | Operación que debe aportar la clase | Qué permite |
|---|---|---|
| `Comparable` | `<=>` | Obtener operaciones de comparación. |
| `Enumerable` | `each` | Obtener operaciones de recorrido, transformación y filtrado. |

`<=>` devuelve un valor negativo, cero o positivo según el orden, o `nil` si los objetos no son comparables. Los casos habituales devuelven `-1`, `0` o `1`.

```ruby
class Nota
  include Comparable
  attr_reader :valor

  def initialize(valor)
    @valor = valor
  end

  def <=>(otra)
    @valor <=> otra.valor
  end
end

Nota.new(5) < Nota.new(8) # => true
```

---

## 3.12 Conversión de tipos y `coerce`

### Conversión explícita

El programador solicita la conversión:

```ruby
12.to_s    # => "12"
"3.5".to_f # => 3.5
```

### Conversión implícita y orden de los operandos

Una operación puede aplicar un protocolo de conversión para trabajar con otro objeto. No todas las conversiones se hacen automáticamente.

```ruby
"a" * 3 # => "aaa"
```

No equivale a:

```ruby
3 * "a" # Provoca un TypeError en Ruby estándar.
```

El receptor de `*` es distinto: en un caso una cadena y en el otro un entero.

### Papel de `coerce`

En operaciones numéricas, `coerce` permite obtener una pareja de operandos compatibles para reintentar la operación.

```ruby
2.coerce(3.0) # => [3.0, 2.0]
```

> [!warning] Corrección del original
> `coerce` no es simplemente «cambiar el orden de los operandos». Debe devolver una pareja compatible y respetar el significado de la operación original. Devolver siempre `[self, other]` no es una solución general, especialmente en operaciones no conmutativas.
>
> Véase la [documentación de Numeric#coerce](https://docs.ruby-lang.org/en/master/Numeric.html#method-i-coerce).

---

## 3.13 Comparación de objetos en Ruby

| Operación | Qué expresa |
|---|---|
| `a.equal?(b)` | Identidad: si son exactamente el mismo objeto. |
| `a == b` | Igualdad según la implementación de la clase. |
| `a.eql?(b)` | Igualdad usada, junto con `hash`, en claves de hashes; su criterio depende de la clase. |
| `a === b` | Comparación de caso o pertenencia, según el receptor. |

### Identidad frente a igualdad

```ruby
a = "hola"
b = "hola"
c = a

a == b      # => true
a.equal?(b) # => false
a.equal?(c) # => true
```

### Números: `==` frente a `eql?`

```ruby
1 == 1.0    # => true
1.eql?(1.0) # => false
```

En este ejemplo `eql?` distingue el tipo numérico. No debe transformarse en una regla universal sobre todas las clases, que pueden definir su propio criterio.

### Comparación de caso: `===`

```ruby
String === "hola" # => true
(1..5) === 3      # => true
```

Con una clase, `Clase === objeto` comprueba si el objeto es instancia de esa clase o de una subclase. Con un rango, tiene un significado de pertenencia al rango.

> [!important]
> `===` no significa «más igual que `==`». Su comportamiento depende del receptor.
>
> Los objetos ordinarios disponen de estos métodos por definición o herencia; no todos se definen originalmente en `Object`. Por ejemplo, `equal?` pertenece a `BasicObject`.

---

## 3.14 Métodos singleton y singleton class

> [!definition]
> Un **método singleton** es un método definido para un objeto concreto.

```ruby
especial = Object.new
normal = Object.new

def especial.saludar
  "Hola, soy especial"
end

especial.saludar              # => "Hola, soy especial"
normal.respond_to?(:saludar)   # => false
```

La **singleton class**, también llamada *eigenclass*, aloja métodos específicos de ese objeto.

```text
Búsqueda para el objeto especial
   ↓
Singleton class de especial
   ↓
Clase ordinaria del objeto
   ↓
Ancestros
```

> [!note]
> El esquema representa la búsqueda de métodos. Crear un método singleton no hace que `objeto.class` deje de devolver su clase ordinaria.
>
> Los métodos de clase también pueden entenderse como métodos singleton del objeto que representa a la clase.

---

## 3.15 Búsqueda de métodos

Para los casos básicos del manuscrito, sin `prepend` ni refinamientos:

1. Se busca en la singleton class del receptor, si tiene comportamiento específico.
2. Se busca en su clase.
3. Se revisan los módulos incluidos: en inclusiones sucesivas simples, los incorporados más recientemente tienen prioridad.
4. Se continúa por la superclase y sus ancestros.
5. Si no se encuentra el método, se recurre a `method_missing`.

> [!tip]
> `Clase.ancestors` permite inspeccionar la cadena de ancestros. `objeto.singleton_class.ancestors` ayuda a incluir la perspectiva del objeto concreto.

### `Kernel` y `method_missing`

`Kernel` es un módulo que aporta numerosas operaciones habituales y está incluido en `Object`.

> [!warning] Corrección del original
> El manuscrito presenta `method_missing` como una función de `Kernel`. Su definición básica está en `BasicObject`. Por defecto, una llamada a un método inexistente acaba produciendo `NoMethodError`.
>
> Véase [BasicObject#method_missing](https://docs.ruby-lang.org/en/master/BasicObject.html#method-i-method_missing).

---

## 3.16 Resumen de orientación a objetos

> [!summary]
> - Un objeto reúne estado y comportamiento.
> - Una clase define instancias; cada instancia puede mantener sus propios datos.
> - `new` crea la instancia e `initialize` la inicializa.
> - La herencia reutiliza y especializa comportamiento.
> - Los módulos sirven como espacios de nombres y mixins.
> - Duck typing y polimorfismo permiten trabajar con diferentes objetos compatibles.
> - Identidad, igualdad y comparación de caso son conceptos distintos.
> - Los métodos singleton pertenecen a un objeto concreto.
> - La búsqueda de métodos sigue una cadena de ancestros.

---
# 4. Tema 4. Programación funcional

*Origen: páginas 16–18 del PDF. El encabezado dice «Tema 4», aunque la numeración inferior utiliza `3.1` y `3.2`.*

## 4.1 Idea general

La programación funcional construye cálculos utilizando funciones y combinándolas entre sí.

En su versión pura, el resultado depende de las entradas, sin basarse en modificaciones de un estado externo.

> [!important]
> En el enfoque imperativo solemos describir cómo van cambiando los datos.
>
> En el funcional expresamos cómo se obtiene un resultado a partir de otros valores.

El manuscrito destaca:

- funciones como elementos básicos;
- menor dependencia explícita del estado de la máquina;
- funciones puras;
- funciones de orden superior;
- memoización;
- currying.

> [!warning] Cómo entender las «limitaciones» del original
> «No se usan variables» debe entenderse como evitar variables mutables y reasignaciones en el estilo puro. Sí existen parámetros y nombres asociados a valores.
>
> Tampoco es obligatorio que todas las funciones sean de orden superior o que todo programa utilice memoización y currying.
>
> Para repetir cálculos se emplean recursión y operaciones sobre colecciones. Ruby admite este estilo, pero también permite mutación y bucles.

---

## 4.2 Funciones puras

> [!definition]
> Una función es **pura** cuando:
>
> 1. Produce el mismo resultado para las mismas entradas.
> 2. No provoca efectos laterales observables.

Ejemplo:

```ruby
def cuadrado(x)
  x * x
end

cuadrado(4) # => 16
```

Son efectos laterales, por ejemplo:

- modificar una variable externa;
- cambiar un objeto compartido;
- escribir en un fichero;
- imprimir en pantalla.

> [!tip]
> Si una función depende solo de sus argumentos, resulta más fácil razonar sobre ella y comprobarla de forma aislada.

---

## 4.3 Funciones de orden superior

> [!definition]
> Una función es de **orden superior** si recibe funciones como argumentos, devuelve una función o ambas cosas.

No es necesario cumplir las dos condiciones a la vez. Ser de orden superior tampoco garantiza ser pura.

Ejemplo desarrollado en Ruby:

```ruby
def aplicar_dos_veces(funcion, valor)
  funcion.call(funcion.call(valor))
end

incremento = ->(x) { x + 1 }
aplicar_dos_veces(incremento, 3) # => 5
```

El cálculo es:

$$
f(f(3)) = f(4) = 5
$$

---

## 4.4 Memoización

> [!definition]
> La **memoización** guarda resultados ya calculados para reutilizarlos cuando se repite una llamada con las mismas entradas.

La idea es:

```text
Llamada f(x)
   ↓
¿Está guardado el resultado para x?
   ├── Sí → devolverlo
   └── No → calcularlo, guardarlo y devolverlo
```

Puede evitar trabajo repetido en algoritmos recursivos, aunque no se limita a ellos.

> [!important]
> La reutilización es correcta cuando el resultado sigue siendo válido para esas entradas. Las funciones puras facilitan esta condición.
>
> La memoización intercambia memoria por ahorro de cálculo; no siempre compensa.

---

## 4.5 Currying y aplicación parcial

> [!definition]
> El **currying** transforma una función de varios argumentos en una sucesión de funciones que reciben argumentos de uno en uno.

Por ejemplo:

$$
f(a,b)=a+b
$$

puede expresarse como:

$$
f_c(a)(b)=a+b
$$

En Ruby:

```ruby
sumar = ->(a, b) { a + b }
sumar_curried = sumar.curry

sumar_diez = sumar_curried.call(10)
sumar_diez.call(3) # => 13
```

1. `curry` obtiene la versión que permite suministrar los argumentos por etapas.
2. Al proporcionar `10`, queda una función pendiente del otro argumento.
3. Al proporcionar `3`, se obtiene `13`.

> [!note] Aclaración del original
> «Reducir el número de parámetros» describe mejor la **aplicación parcial**, que fija algunos argumentos. El currying es la transformación que permite expresar la función como llamadas sucesivas.

---

## 4.6 Bloques en Ruby

> [!definition]
> Un **bloque** es un fragmento de código que se pasa asociado a una llamada a un método.

Se escribe con llaves o con `do ... end`:

```ruby
[1, 2, 3].map { |x| x * 2 }
```

```ruby
[1, 2, 3].map do |x|
  x * 2
end
```

Ambos ejemplos producen:

```ruby
[2, 4, 6]
```

Un método puede ejecutar el bloque recibido mediante `yield`:

```ruby
def transformar(valor)
  yield(valor)
end

transformar(5) { |x| x * 3 } # => 15
```

---

## 4.7 `Enumerable`

`Enumerable` proporciona operaciones sobre colecciones que pueden recorrerse mediante `each`.

Para utilizarlo en una clase propia:

1. Incluir `Enumerable`.
2. Definir `each` para entregar los elementos al bloque.

```ruby
class Coleccion
  include Enumerable

  def initialize(elementos)
    @elementos = elementos
  end

  def each
    return enum_for(:each) unless block_given?

    @elementos.each { |elemento| yield elemento }
  end
end

Coleccion.new([1, 2, 3]).map { |x| x * 2 } # => [2, 4, 6]
```

### Operaciones mencionadas en el manuscrito

Con `datos = [1, 2, 3, 4]`:

| Método | Función | Ejemplo | Resultado |
|---|---|---|---|
| `collect` o `map` | Transformar cada elemento. | `datos.map { \|x\| x * 2 }` | `[2, 4, 6, 8]` |
| `sum` | Sumar elementos. | `datos.sum` | `10` |
| `inject` o `reduce` | Acumular un resultado. | `datos.inject(:+)` | `10` |
| `select` | Filtrar por una condición. | `datos.select { \|x\| x.even? }` | `[2, 4]` |
| `take(n)` | Obtener los primeros `n`. | `datos.take(2)` | `[1, 2]` |
| `drop(n)` | Omitir los primeros `n`. | `datos.drop(2)` | `[3, 4]` |

Filtrado utilizando el índice:

```ruby
datos = [10, 20, 30, 40]
datos.select.with_index { |valor, indice| indice.even? }
# => [10, 30]
```

El índice comienza en cero.

> [!important]
> `map` transforma, `select` filtra e `inject` acumula.
>
> Estas versiones no modifican por sí mismas el array original, aunque el código de un bloque sí podría tener efectos laterales.

### Ejemplo combinado

Sumar los cuadrados de los números pares:

```ruby
[1, 2, 3, 4]
  .select { |x| x.even? }
  .map { |x| x * x }
  .sum
# => 20
```

Paso a paso:

```text
[1, 2, 3, 4] → [2, 4] → [4, 16] → 20
```

---

## 4.8 `Proc` y lambda

Un objeto `Proc` permite guardar código y ejecutarlo después mediante `call`. Una lambda es una modalidad de `Proc`.

```ruby
doble_proc = Proc.new { |x| x * 2 }
doble_lambda = lambda { |x| x * 2 }
doble_flecha = ->(x) { x * 2 }

doble_proc.call(3)   # => 6
doble_lambda.call(3) # => 6
doble_flecha.call(3) # => 6
```

### Diferencia destacada en el original

Para parámetros posicionales ordinarios, una lambda exige la cantidad de argumentos esperada. Un `Proc` no lambda es más flexible.

```ruby
flexible = proc { |x, y| [x, y] }
flexible.call(1) # => [1, nil]

estricta = ->(x, y) { [x, y] }
# estricta.call(1) provoca ArgumentError.
```

> [!note] Aclaración
> «Comprueba parámetros» se refiere aquí a su cantidad y tratamiento, no a una comprobación automática de sus tipos.
>
> También cambia `return`: en una lambda retorna de la propia lambda; en un `Proc` no lambda intenta retornar del método donde se creó, lo que puede fallar si ese contexto ya terminó.
>
> Véase la [documentación de Proc](https://docs.ruby-lang.org/en/master/Proc.html).

---

## 4.9 Clausuras — closures

> [!definition]
> Una **clausura** combina código con acceso al entorno léxico en el que se definió.

Esto permite que una función conserve acceso a variables de su contexto de creación.

```ruby
def crear_sumador(incremento)
  ->(x) { x + incremento }
end

sumar_cinco = crear_sumador(5)
sumar_cinco.call(10) # => 15
```

Aunque `crear_sumador` ya haya terminado, la lambda conserva acceso a `incremento`.

> [!warning] No es necesariamente una fotografía de los valores
> En Ruby una clausura conserva acceso a las variables capturadas. Si esas variables cambian, el resultado puede reflejar el cambio.

```ruby
valor = 1
leer = -> { valor }
valor = 2

leer.call # => 2
```

---

## 4.10 Metaprogramación, reflexión y DSL

### Metaprogramación

> [!definition]
> La **metaprogramación** consiste en escribir programas que generan, inspeccionan o modifican código o estructuras de otros programas, incluido el propio.

Crear nuevos lenguajes es una aplicación posible, pero no su única finalidad.

### Reflexión

La **reflexión** permite que un programa inspeccione su propia estructura y, cuando el lenguaje lo permite, la modifique.

En Ruby, consultar la clase de un objeto o los métodos a los que responde son ejemplos sencillos de introspección.

### DSL

> [!definition]
> Un **DSL — Domain-Specific Language** es un lenguaje especializado en un dominio concreto.

El esquema del manuscrito es:

```text
Ruby, como lenguaje de implementación
            ↓
     Metaprogramación
            ↓
DSL para describir un dominio específico
```

Un DSL interno puede aprovechar la sintaxis del lenguaje anfitrión. Por ejemplo, las construcciones de RSpec permiten describir comportamientos esperados de un programa.

> [!note]
> En este contexto, «lenguaje objeto» significa el lenguaje que se describe o construye. No significa necesariamente «lenguaje orientado a objetos».

---

## 4.11 Resumen de programación funcional

> [!summary]
> - Las funciones permiten construir y combinar cálculos.
> - La pureza requiere determinismo y ausencia de efectos laterales.
> - Una función de orden superior recibe o devuelve funciones.
> - La memoización reutiliza resultados.
> - El currying permite suministrar argumentos por etapas.
> - `map`, `select` e `inject` expresan transformación, filtrado y acumulación.
> - `Proc` y lambda permiten tratar código como objetos invocables.
> - Una clausura conserva acceso a su entorno.
> - La metaprogramación puede facilitar la creación de DSL.

---

# 5. Tema 5. Programación concurrente

*Origen: páginas 19–22 del PDF.*

## 5.1 Idea general

> [!definition]
> La **programación concurrente** organiza un programa en varias tareas cuyo progreso puede solaparse en el tiempo.

Permite aprovechar recursos, atender varias actividades y separar responsabilidades.

> [!important]
> **Concurrencia:** varias tareas progresan durante un mismo periodo, aunque alternen su ejecución.
>
> **Paralelismo:** varias tareas se ejecutan simultáneamente.

Un único núcleo puede alternar tareas concurrentes. Para ejecutar varias instrucciones realmente a la vez hacen falta recursos de ejecución paralelos.

---

## 5.2 Procesos

> [!definition]
> Un **proceso** es una instancia de un programa en ejecución, junto con su estado y sus recursos asociados.

El original menciona:

- tiempo de CPU;
- código y datos;
- información de gestión, como PID y prioridad;
- registros;
- pila y heap;
- ficheros y otros recursos;
- posibles regiones de memoria compartida.

**PID** significa identificador del proceso.

> [!note]
> Los procesos suelen tener espacios de direcciones separados. Pueden compartir información mediante mecanismos explícitos de comunicación o memoria compartida.

---

## 5.3 Estados de un proceso

| Estado | Significado |
|---|---|
| **Creado** | Se está preparando su ejecución. |
| **Listo** | Puede ejecutarse, pero espera CPU. |
| **En ejecución** | Está utilizando la CPU. |
| **Bloqueado** | Espera un evento, un recurso o una operación. |
| **Terminado** | Ha finalizado. |

```text
Creado → Listo → En ejecución → Terminado
           ↑          │
           │          ├── fin del turno de CPU → Listo
           │          │
           │          └── espera de un evento → Bloqueado
           │                                      │
           └────────── evento completado ──────────┘
```

> [!important]
> **Listo** significa que solo falta disponer de CPU.
>
> **Bloqueado** significa que primero debe cumplirse otra condición.

> [!note] Aclaración del esquema original
> Una interrupción no implica siempre pasar a bloqueado. Por ejemplo, una interrupción de temporizador puede provocar que el proceso en ejecución vuelva a listo al terminar su turno.

---

## 5.4 Hilos — threads

> [!definition]
> Un **hilo** es un flujo de ejecución dentro de un proceso.

Un proceso puede tener varios hilos para atender diferentes tareas.

### Qué comparten y qué mantienen por separado

| Recurso | Hilos de un mismo proceso |
|---|---|
| Código | Compartido. |
| Datos globales | Compartidos. |
| Heap del proceso | Generalmente compartido. |
| Recursos como ficheros abiertos | Generalmente compartidos. |
| Registros y contador de programa | Estado propio de cada hilo. |
| Pila de ejecución | Propia de cada hilo. |

> [!warning] Corrección del original
> El manuscrito agrupa «pila y heap» como privados de cada hilo. En el modelo habitual, cada hilo tiene su pila, pero los hilos del proceso comparten el heap.
>
> Compartir datos facilita la comunicación, pero exige coordinar los accesos que puedan interferir.

---

## 5.5 Granularidad de las tareas

La **granularidad** indica cuánto trabajo se asigna a cada tarea.

| Enfoque | Trabajo por tarea | Consecuencias habituales |
|---|---|---|
| **Grano fino** | Pequeño. | Más tareas y, con frecuencia, mayor coste de coordinación. |
| **Grano grueso** | Grande. | Menos tareas y menor coordinación relativa, pero puede costar equilibrar la carga. |

No se puede deducir el tiempo total solo por la granularidad: influyen los recursos, el reparto del trabajo y la sincronización.

### Problemas vergonzosamente paralelos

Un problema es **vergonzosamente paralelo** cuando puede dividirse en tareas prácticamente independientes, con muy poca comunicación entre ellas.

Ejemplo: aplicar la misma transformación a miles de imágenes independientes.

> [!warning] Corrección importante
> El original dice «no tiene sentido hacer paralelo». Es al contrario: estos problemas suelen ser especialmente fáciles de paralelizar.
>
> No es un tercer tamaño de grano, sino una propiedad de la independencia entre tareas.

---

## 5.6 Crear hilos en Ruby

```ruby
require 'thread'

hilo = Thread.new do
  2 + 3
end

hilo.join
hilo.value # => 5
```

- `Thread.new` crea un hilo que ejecuta el bloque.
- `join` hace que quien lo llama espere a que termine ese hilo.
- `value` permite obtener el resultado del bloque; también espera si es necesario.

> [!important]
> Crear hilos permite expresar concurrencia. El paralelismo efectivo depende de la implementación de Ruby y del tipo de trabajo.

---

## 5.7 Programación paralela y distribuida

| Concepto | Idea central |
|---|---|
| **Paralela** | Ejecutar trabajo simultáneamente utilizando varios recursos de cómputo. |
| **Distribuida** | Repartir componentes entre varias máquinas que se comunican. |

El manuscrito asocia la programación paralela a una máquina y a buscar velocidad; la distribuida, a varias máquinas y al uso de middleware.

> [!note] Matiz del original
> Un sistema distribuido también puede buscar velocidad, escalabilidad o tolerancia a fallos. Además, un cálculo paralelo puede ejecutarse en varias máquinas. Las dos ideas pueden coexistir.

### Middleware

> [!definition]
> El **middleware** es software intermedio que facilita la comunicación y coordinación entre componentes o máquinas, ocultando parte de sus diferencias.

---

## 5.8 Condiciones de carrera

> [!definition]
> Hay una **condición de carrera** cuando la corrección del resultado depende del orden o del momento en que se intercalan operaciones concurrentes.

Imaginemos que dos hilos incrementan un contador inicialmente igual a cero:

```text
Hilo A lee 0
Hilo B lee 0
Hilo A calcula 1
Hilo B calcula 1
Hilo A escribe 1
Hilo B escribe 1
```

El resultado es `1`, aunque se pretendían dos incrementos.

> [!important]
> Una instrucción como `contador += 1` no debe suponerse una operación indivisible: conceptualmente lee, calcula y escribe.
>
> No hace falta simultaneidad física exacta para que exista un problema; basta una intercalación que produzca un resultado incorrecto.

---

## 5.9 Exclusión mutua: `Mutex`

> [!definition]
> Una **sección crítica** es una parte del programa que accede a un recurso compartido y necesita protección frente a accesos incompatibles.
>
> Un **mutex** permite que solo un hilo a la vez entre en una sección protegida por ese mismo mutex.

Ejemplo desarrollado:

```ruby
require 'thread'

contador = 0
mutex = Mutex.new

hilos = Array.new(2) do
  Thread.new do
    1000.times do
      mutex.synchronize do
        contador += 1
      end
    end
  end
end

hilos.each(&:join)
contador # => 2000
```

`synchronize` adquiere el mutex, ejecuta el bloque y lo libera incluso si el bloque lanza una excepción.

La forma manual del manuscrito utiliza `lock` y `unlock`. Si se escribe así, debe garantizarse la liberación:

```ruby
mutex.lock
begin
  # Acceso al recurso compartido.
ensure
  mutex.unlock
end
```

> [!important]
> La protección requiere que todos los accesos incompatibles respeten el mismo mecanismo. Proteger solo uno de los hilos no basta.

### Mutex, semáforo y barrera

| Mecanismo | Finalidad |
|---|---|
| **Mutex** | Exclusión mutua sobre una sección crítica. |
| **Semáforo** | Regular el acceso mediante un contador de permisos. |
| **Barrera** | Esperar hasta que todos los participantes alcancen un punto. |

No son nombres intercambiables de una misma herramienta.

---

## 5.10 Secuenciación y variables de condición

A veces un hilo necesita esperar a que otro haya preparado un dato o cumplido una condición.

Una **variable de condición** permite suspender la espera y avisar cuando puede haberse producido un cambio relevante.

### Ejemplo corregido del manuscrito

```ruby
require 'thread'

mutex = Mutex.new
condicion = ConditionVariable.new
preparado = false
resultado = nil

consumidor = Thread.new do
  mutex.synchronize do
    condicion.wait(mutex) until preparado
    resultado * 2
  end
end

productor = Thread.new do
  mutex.synchronize do
    resultado = 21
    preparado = true
    condicion.signal
  end
end

productor.join
consumidor.value # => 42
```

Funcionamiento:

1. El consumidor adquiere el mutex y comprueba `preparado`.
2. Si todavía es falso, `wait(mutex)` libera temporalmente el mutex y espera.
3. El productor adquiere el mutex, prepara el resultado y cambia la condición.
4. `signal` despierta a un hilo que esté esperando.
5. El consumidor vuelve a adquirir el mutex, comprueba la condición y continúa cuando es verdadera.

> [!warning] Corrección importante del ejemplo original
> `wait` debe ejecutarse con el mutex adquirido. Además, hay que comprobar una condición compartida en un bucle.
>
> La señal no queda guardada como un permiso para un hilo que empiece a esperar después. La variable `preparado` evita perder el hecho de que el trabajo ya terminó.
>
> Véase [Thread::ConditionVariable](https://docs.ruby-lang.org/en/master/Thread/ConditionVariable.html).

---

## 5.11 Interbloqueo — deadlock

> [!definition]
> Un **interbloqueo** aparece cuando varias tareas quedan esperando recursos o acciones entre sí y ninguna puede avanzar.

Ejemplo:

```text
Hilo A tiene el recurso 1 y espera el recurso 2.
Hilo B tiene el recurso 2 y espera el recurso 1.
```

Cada hilo espera una liberación que el otro no puede realizar mientras está bloqueado.

> [!note]
> No es necesario que se bloqueen todos los hilos del programa: basta con que un conjunto quede interbloqueado.
>
> Una medida habitual es adquirir varios recursos siempre en un orden consistente.

---

## 5.12 Resumen de concurrencia

> [!summary]
> - Concurrencia y paralelismo no son lo mismo.
> - Los procesos tienen estado y recursos; los hilos son flujos dentro de un proceso.
> - Los hilos comparten datos y heap, pero mantienen sus propias pilas y registros.
> - La granularidad afecta al reparto y al coste de coordinación.
> - `join` espera a la terminación de un hilo.
> - Un mutex protege una sección crítica.
> - Una variable de condición permite esperar cambios de estado.
> - Una carrera puede producir resultados incorrectos.
> - Un deadlock impide que ciertas tareas avancen.

---

# 6. Pruebas unitarias y TDD

*Origen: páginas 24–25 del PDF.*

## 6.1 Pruebas unitarias

> [!definition]
> Una **prueba unitaria** comprueba el comportamiento de una unidad pequeña del programa mediante entradas y resultados esperados.

Puede comprobar:

- un valor devuelto;
- una modificación de estado;
- una excepción esperada.

El manuscrito presenta un flujo de «escribir código y después pruebas», con commits para registrar los cambios.

> [!note]
> Ese orden es una metodología posible, no la definición de prueba unitaria. Una prueba unitaria también puede escribirse antes del código.

### Organización de archivos

```text
proyecto/
├── lib/
│   └── calculadora.rb
└── test/
    └── tc_calculadora.rb
```

- `lib/` contiene el código.
- `test/` contiene las pruebas.

---

## 6.2 Ejemplo con `Test::Unit`

Código de apoyo, en `lib/calculadora.rb`:

```ruby
class Calculadora
  def sumar(a, b)
    a + b
  end

  def dividir(a, b)
    raise ZeroDivisionError, "Divisor cero" if b == 0

    a.to_f / b
  end
end
```

Pruebas, en `test/tc_calculadora.rb`:

```ruby
require 'test/unit'
require_relative '../lib/calculadora'

class TestCalculadora < Test::Unit::TestCase
  def setup
    @calculadora = Calculadora.new
  end

  def teardown
    # Liberar recursos de la prueba si fuera necesario.
  end

  def test_suma
    assert_equal(5, @calculadora.sumar(2, 3))
  end

  def test_division_por_cero
    assert_raise(ZeroDivisionError) do
      @calculadora.dividir(4, 0)
    end
  end
end
```

### Elementos importantes

| Elemento | Papel |
|---|---|
| `Test::Unit::TestCase` | Clase base para las pruebas. |
| `setup` | Prepara el contexto antes de cada prueba. |
| `teardown` | Realiza limpieza después de cada prueba. |
| Métodos `test_...` | Identifican casos de prueba. |
| `assert_equal(esperado, obtenido)` | Comprueba igualdad. |
| `assert_raise(Excepcion) { ... }` | Comprueba que el bloque lanza esa excepción. |

Desde la raíz del proyecto:

```sh
ruby -I. test/tc_calculadora.rb
```

`-I.` añade el directorio actual a la ruta de búsqueda de bibliotecas. En este ejemplo, el archivo de la aplicación se carga con `require_relative`.

> [!warning] Correcciones de sintaxis del original
> - El nombre de la clase debe comenzar con mayúscula.
> - El método de limpieza se llama `teardown`, sin guion bajo intermedio.
> - Los métodos y la clase deben cerrar sus bloques con `end`.
> - El nombre convencional de un caso empieza por `test_`.

---

## 6.3 TDD: desarrollo dirigido por pruebas

> [!definition]
> **TDD — Test-Driven Development** es una metodología en la que se escribe primero una prueba que expresa el comportamiento deseado y después el código necesario para satisfacerla.

El ciclo de trabajo es:

```text
ROJO: escribir una prueba y comprobar que falla
   ↓
VERDE: implementar lo necesario para que pase
   ↓
REFACTORIZAR: mejorar el código manteniendo las pruebas correctas
   ↓
Repetir con el siguiente comportamiento
```

> [!important]
> TDD es una metodología. `Test::Unit` y RSpec son herramientas.
>
> Se puede practicar TDD con distintas herramientas. Utilizar RSpec no garantiza que se haya seguido TDD.

El original muestra primero una expectativa y después el código, registrando cada paso mediante commits. Los commits conservan el historial, pero no sustituyen comprobar el fallo inicial y el éxito posterior.

---

## 6.4 RSpec

RSpec permite describir comportamientos mediante ejemplos y expectativas. Se necesita tener disponible la gema `rspec`.

### Organización

```text
proyecto/
├── lib/
│   └── calculadora.rb
└── spec/
    └── calculadora_spec.rb
```

### Ejemplo

Usando la misma clase `Calculadora`:

```ruby
require_relative '../lib/calculadora'

RSpec.describe Calculadora do
  before(:each) do
    @calculadora = Calculadora.new
  end

  it 'suma dos números' do
    expect(@calculadora.sumar(2, 3)).to eq(5)
  end

  it 'no confunde suma con multiplicación' do
    expect(@calculadora.sumar(2, 3)).not_to eq(6)
  end

  it 'rechaza la división por cero' do
    expect { @calculadora.dividir(4, 0) }
      .to raise_error(ZeroDivisionError)
  end
end
```

### Construcciones principales

| Construcción | Significado |
|---|---|
| `describe` | Agrupa ejemplos sobre un comportamiento o componente. |
| `it` | Define un ejemplo concreto. |
| `before(:each)` | Prepara el contexto antes de cada ejemplo. |
| `before(:all)` | Se ejecuta una vez antes de los ejemplos del grupo. |
| `expect(valor).to eq(esperado)` | Espera que ambos valores sean iguales. |
| `expect(valor).not_to eq(otro)` | Espera que no sean iguales. |
| `expect { codigo }.to raise_error(Error)` | Espera una excepción al ejecutar el bloque. |

> [!tip]
> Para comprobar un valor se usa `expect(valor)`.
>
> Para comprobar que una operación lanza una excepción se pasa un bloque: `expect { operacion }`.

> [!note]
> `before(:each)` ayuda a preparar un contexto independiente por ejemplo. Con `before(:all)`, compartir estado mutable puede hacer que una prueba afecte a otra.
>
> Véase la [documentación de hooks de RSpec](https://rspec.info/features/3-13/rspec-core/hooks/before-and-after-hooks/).

Ejecución desde la raíz del proyecto, con RSpec disponible:

```sh
rspec spec/calculadora_spec.rb
```

---

## 6.5 Resumen de pruebas

> [!summary]
> - Una prueba compara un comportamiento observado con uno esperado.
> - `setup` y `teardown` preparan y limpian el contexto de cada prueba de `Test::Unit`.
> - `assert_equal` comprueba valores; `assert_raise` comprueba excepciones.
> - TDD sigue el ciclo rojo, verde y refactorización.
> - RSpec permite expresar ejemplos con `describe`, `it` y `expect`.
> - La metodología no depende exclusivamente de una biblioteca de pruebas.

---

# 7. Repaso global

## 7.1 Conceptos que conviene distinguir

| Conceptos | Diferencia esencial |
|---|---|
| Lenguaje / paradigma | Notación / forma de organizar el cómputo. |
| Léxico / sintaxis / semántica | Tokens / estructura / restricciones de significado. |
| Pila / heap | Activaciones de llamadas / almacenamiento dinámico. |
| Ámbito / duración | Dónde puede usarse un nombre / cuánto tiempo existe el dato. |
| Clase / objeto | Definición / instancia concreta. |
| `new` / `initialize` | Creación y devolución / preparación del estado. |
| Identidad / igualdad | Mismo objeto / equivalencia según un criterio. |
| Función pura / de orden superior | Sin efectos laterales y determinista / recibe o devuelve funciones. |
| `map` / `select` / `inject` | Transformar / filtrar / acumular. |
| Concurrencia / paralelismo | Progreso solapado / ejecución simultánea. |
| Proceso / hilo | Contexto de ejecución y recursos / flujo dentro de él. |
| Mutex / variable de condición | Proteger acceso / esperar que se cumpla una condición. |
| Carrera / deadlock | Resultado sensible al orden / imposibilidad de avanzar. |
| Prueba unitaria / TDD | Tipo de comprobación / metodología de desarrollo. |

---

## 7.2 Preguntas de autoevaluación

*Preguntas de repaso añadidas para estudiar; no proceden de una hoja oficial de ejercicios.*

1. ¿Qué diferencia hay entre un lenguaje y un paradigma?
2. ¿Qué comprueban los análisis léxico, sintáctico y semántico?
3. ¿Por qué una función recursiva puede tener varias activaciones?
4. ¿Qué diferencia hay entre `@dato` y `@@dato`?
5. ¿Por qué `initialize` no es lo mismo que `new`?
6. ¿Cómo permite el duck typing trabajar con clases distintas?
7. ¿Qué hace `super` dentro de un método redefinido?
8. ¿Qué operación debes implementar para usar `Comparable`? ¿Y `Enumerable`?
9. ¿Cuándo puede ser verdadero `a == b` y falso `a.equal?(b)`?
10. ¿Qué diferencia a un método singleton de uno de instancia ordinario?
11. ¿Puede una función ser de orden superior y tener efectos laterales?
12. ¿Qué conserva una clausura?
13. ¿Qué diferencia hay entre `map`, `select` e `inject`?
14. ¿Qué comparten los hilos de un proceso?
15. ¿Por qué un mutex y una variable de condición resuelven necesidades diferentes?
16. ¿Qué problema evita comprobar un predicado antes de esperar una señal?
17. ¿Qué diferencia hay entre condición de carrera e interbloqueo?
18. ¿Cuáles son las tres fases del ciclo TDD?

> [!tip] Forma de repasar
> Intenta responder sin mirar. Si dudas, vuelve al apartado correspondiente y explica su ejemplo paso a paso con tus propias palabras.

---

# 8. Correspondencia con el PDF y aclaraciones

## 8.1 Cobertura del documento recibido

Las páginas de esta tabla se cuentan desde la portada del PDF, no desde la numeración manuscrita.

| Páginas del PDF | Contenido | Apartado de estos apuntes |
|---|---|---|
| 1 | Portada y atribución. | Procedencia. |
| 2 | Lenguajes, primitivas, abstracción y formas de ejecución. | 1.1–1.4 |
| 3 | Mapa de paradigmas. | 1.3 |
| 4 | Compilación, interpretación y fases. | 1.4–1.5 |
| 5 | Modelo imperativo y memoria. | 2.1–2.2 |
| 6 | Procedural, activaciones y programación estructurada. | 2.3–2.5 |
| 7 | Publicidad. | Excluida. |
| 8 | Objetos, clases, variables y métodos. | 3.1–3.3 |
| 9 | `initialize`, acceso, `to_s`, recolección y duck typing. | 3.4–3.7 |
| 10 | Herencia, `super` y visibilidad. | 3.9–3.10 |
| 11 | Módulos, namespaces, mixins, `Comparable` y `Enumerable`. | 3.11 |
| 12 | Clase, tipo, polimorfismo y conversiones. | 3.7–3.8 y 3.12 |
| 13 | Comparaciones. | 3.13 |
| 14 | Métodos singleton y eigenclass. | 3.14 |
| 15 | Búsqueda de métodos y `Kernel`. | 3.15 |
| 16 | Bases de programación funcional. | 4.1–4.5 |
| 17 | Bloques, `Enumerable`, `Proc` y lambda. | 4.6–4.8 |
| 18 | Clausuras, metaprogramación y DSL. | 4.9–4.10 |
| 19 | Concurrencia, procesos y estados. | 5.1–5.3 |
| 20 | Hilos, granularidad y memoria. | 5.4–5.5 |
| 21 | Hilos en Ruby, paralela, distribuida y sincronización. | 5.6–5.9 |
| 22 | Variables de condición, deadlock y carreras. | 5.8 y 5.10–5.11 |
| 23 | Publicidad. | Excluida. |
| 24 | Pruebas unitarias. | 6.1–6.2 |
| 25 | TDD y RSpec. | 6.3–6.4 |

---

## 8.2 Aclaraciones importantes respecto al manuscrito

> [!important]
> Estas correcciones forman parte de la edición para estudio. No deben confundirse con frases transcritas literalmente del alumno.

| Formulación del manuscrito | Aclaración aplicada |
|---|---|
| Interpretar equivale a compilar cada vez. | Hay distintas estrategias y combinaciones de traducción y ejecución. |
| Enlazado antes de ensamblado. | En la cadena nativa clásica, el ensamblado produce código objeto y después se enlaza. |
| Pila como requisito absoluto de los subprogramas. | Es el mecanismo habitual presentado; no la única implementación posible. |
| Programación estructurada definida por manejo de datos. | Su rasgo central es el control mediante secuencia, selección e iteración. |
| Toda clase debe definir `initialize`, `attr_reader` y `to_s`. | Son recursos útiles, no obligaciones del lenguaje. |
| La instancia se sustituye por el retorno de `initialize`. | `new` devuelve la instancia creada. |
| `super.metodo`. | `super` invoca la siguiente implementación del método actual. |
| `coerce` invierte operandos. | Produce operandos compatibles conservando el sentido de la operación. |
| `eql?` siempre compara tipo y valor; `===` siempre es `is_a?`. | Son métodos cuyo comportamiento depende de la clase receptora. |
| Todos los métodos de comparación se definen en `Object`. | Algunos proceden de `BasicObject` y otros se redefinen. |
| `method_missing` pertenece a `Kernel`. | Su definición básica está en `BasicObject`. |
| En funcional no existen variables y todas las funciones son de orden superior. | Se distingue inmutabilidad de ausencia de nombres, y orden superior de pureza. |
| Currying consiste solo en reducir parámetros. | Se distingue la transformación de la aplicación parcial. |
| Lambda comprueba parámetros. | La diferencia destacada es el tratamiento de argumentos, no el chequeo de tipos. |
| Clausura como copia fija de valores. | En Ruby conserva acceso a las variables capturadas. |
| Cada hilo tiene su heap independiente. | El heap suele compartirse dentro del proceso. |
| Un problema vergonzosamente paralelo no debe paralelizarse. | Sus tareas independientes facilitan paralelizarlo. |
| La programación distribuida no busca velocidad. | También puede perseguir rendimiento; no es su único objetivo. |
| Esperar una señal basta para coordinar hilos. | Se requiere mutex adquirido y comprobación de un predicado compartido. |
| Deadlock bloquea necesariamente todos los hilos. | Puede afectar solo a un conjunto de tareas. |
| `tear_down` y nombres de clase en minúscula. | Se normalizan a `teardown` y nombres de clase válidos. |
| TDD se identifica con RSpec. | Se distingue la metodología de la herramienta. |

### Límites de la reconstrucción

La mayor parte de la escritura es legible. El identificador de la clase del pequeño ejemplo de sobrecarga de `+` de la página 12 no se lee con suficiente seguridad; se ha sustituido por `NumeroEnvuelto`, manteniendo la idea de construir un nuevo objeto con el resultado. Los ejemplos ampliados y los nombres descriptivos se han añadido para facilitar el estudio.

Los recortes de los bordes afectan principalmente a anotaciones laterales. No se han reconstruido frases no legibles como si fueran texto confirmado. El contenido del índice corresponde a lo visible en este PDF; no presupone temas adicionales.
