
## **1. Función de la capa física**

La **capa física** se encarga de transmitir **bits** entre un emisor y un receptor usando un medio físico.

No trabaja con IPs, puertos, paquetes ni tramas. Eso pertenece a capas superiores.

La capa física define cosas como:

- cómo se representan los bits mediante señales,
- qué medio se utiliza,
- qué conectores se usan,
- qué velocidad de transmisión puede alcanzarse,
- cómo se codifica o modula la información.

La unidad de datos de esta capa son los **bits**.

---

## **2. Señales analógicas y digitales**

Una **señal analógica** varía de forma continua en el tiempo.

Ejemplos:

- voz,
- radio,
- señales eléctricas continuas.

Una **señal digital** toma valores discretos, normalmente asociados a 0 y 1.

Ejemplo:

- pulsos eléctricos que representan bits.

---

## **3. Conceptos básicos de señales**
| **Concepto**   | **Significado**                                   |
| -------------- | ------------------------------------------------- |
| Amplitud       | Intensidad o valor máximo de la señal             |
| Frecuencia     | Número de ciclos por segundo                      |
| Periodo        | Tiempo que tarda un ciclo                         |
| Fase           | Desplazamiento respecto a una referencia          |
| Espectro       | Conjunto de frecuencias de una señal              |
| Ancho de banda | Rango de frecuencias que ocupa o permite un medio |
Relación importante:

**frecuencia = 1 / periodo**

La frecuencia se mide en **hercios, Hz**.

---

## **4. Medios de transmisión**

Los medios pueden ser **guiados** o **no guiados**.

### **Medios guiados**

La señal viaja por un soporte físico.

Ejemplos:

- par trenzado,
- cable coaxial,
- fibra óptica.

### **Medios no guiados**

La señal se propaga por el aire o el espacio.

Ejemplos:

- radio,
- microondas,
- satélite,
- WiFi.

---

## **5. Par trenzado**

El **par trenzado** está formado por pares de hilos de cobre enrollados entre sí.

El trenzado ayuda a reducir interferencias.

Tipos importantes:

| **Tipo** | **Significado**         | **Característica**  |
| -------- | ----------------------- | ------------------- |
| UTP      | Unshielded Twisted Pair | Sin apantallamiento |
| STP      | Shielded Twisted Pair   | Apantallado         |
| FTP      | Foiled Twisted Pair     | Pantalla global     |
Ideas importantes:

- UTP es barato y común.
- STP/FTP protegen mejor frente a interferencias.
- El par trenzado se usa mucho en redes Ethernet.

### **Cable directo y cruzado**

- **Cable directo:** ambos extremos usan la misma norma.
- **Cable cruzado:** un extremo usa T568A y el otro T568B.

Hoy en día muchos dispositivos detectan automáticamente el tipo de cable, pero conceptualmente sigue siendo preguntable.

---

## **6. Cable coaxial**

El **cable coaxial** tiene dos conductores principales:

- conductor central o **vivo**,
- conductor exterior o **malla**.

La malla sirve como protección frente a interferencias.

Fue muy usado en redes antiguas y sigue usándose en otros contextos, como televisión por cable.

---

## **7. Fibra óptica**

La **fibra óptica** transmite información mediante luz.

Ventajas:

- permite grandes velocidades,
- permite largas distancias,
- es inmune a interferencias electromagnéticas,
- tiene menor atenuación que otros medios.

Inconvenientes:

- suele ser más cara,
- es más delicada,
- requiere equipamiento específico.

Tipos básicos:

| **Tipo**  | **Característica**                                   |
| --------- | ---------------------------------------------------- |
| Monomodo  | Más distancia y más velocidad                        |
| Multimodo | Menos distancia, más barata y común en redes locales |

## **8. Transmisión simplex, half-duplex y full-duplex**
| **Tipo**    | **Significado**                                        |
| ----------- | ------------------------------------------------------ |
| Simplex     | La comunicación va solo en un sentido                  |
| Half-duplex | La comunicación va en ambos sentidos, pero no a la vez |
| Full-duplex | La comunicación va en ambos sentidos simultáneamente   |

Ejemplos típicos:

- Simplex: emisión de televisión tradicional.
- Half-duplex: walkie-talkie.
- Full-duplex: llamada telefónica.

---

## **9. Codificación**

La **codificación** consiste en representar datos digitales mediante señales digitales.

Ejemplos de codificación:

- NRZ,
- NRZI,
- Manchester,
- Manchester diferencial.

No creo que tengas que aprenderte los dibujos perfectos, pero sí la idea general.

### **NRZ**

Representa bits con niveles de señal.

Problema:

- si hay muchos bits iguales seguidos, puede ser difícil mantener la sincronización.

### **NRZI**

El bit se representa mediante cambios o ausencia de cambios en la señal.

### **Manchester**

Combina datos y reloj.

Cada bit tiene una transición en medio del intervalo, lo que ayuda a la sincronización.

Idea típica de test:

- Manchester facilita la sincronización, pero necesita más ancho de banda.

---

## **10. Modulación**

La **modulación** consiste en modificar una señal portadora para transmitir información.

Se usa especialmente cuando se transmiten datos digitales mediante señales analógicas.

Tipos importantes:

| **Modulación** | **Qué modifica** |
| -------------- | ---------------- |
| ASK            | Amplitud         |
| FSK            | Frecuencia       |
| PSK            | Fase             |
| QAM            | Amplitud y fase  |

### **ASK**

Modifica la amplitud de la señal.

### **FSK**

Modifica la frecuencia de la señal.

### **PSK**

Modifica la fase de la señal.

### **QAM**

Modifica amplitud y fase.

Permite representar más bits por símbolo.

---

## **11. Multiplexación**

La **multiplexación** permite que varias señales compartan un mismo medio de transmisión.

Tipos importantes:

| **Tipo** | **Idea**                                             |
| -------- | ---------------------------------------------------- |
| FDM      | Divide por frecuencias                               |
| TDM      | Divide por tiempo                                    |
| WDM      | Divide por longitudes de onda, usado en fibra óptica |

### **FDM**

Cada comunicación usa una banda de frecuencia distinta.

### **TDM**

Cada comunicación usa el medio durante intervalos de tiempo distintos.

### **WDM**

Se usa en fibra óptica. Varias señales viajan usando distintas longitudes de onda de luz.

---

## **12. Atenuación, ruido e interferencias**

Durante la transmisión, la señal puede degradarse.

### **Atenuación**

La señal pierde intensidad con la distancia.

### **Ruido**

Señales no deseadas que alteran la señal original.

### **Interferencia**

Perturbación causada por otras señales cercanas.

Esto puede provocar errores en los bits recibidos.

---

## **13. Lo más probable de test**

Lo más importante de este tema es saber:

- La capa física transmite **bits**.
- No trabaja con IPs, puertos ni tramas.
- Diferencia entre señal analógica y digital.
- Diferencia entre medio guiado y no guiado.
- Ejemplos de medios guiados: par trenzado, coaxial, fibra.
- Ejemplos de medios no guiados: radio, satélite, WiFi.
- UTP no está apantallado; STP sí.
- Fibra óptica usa luz y es inmune a interferencias electromagnéticas.
- Simplex, half-duplex y full-duplex.
- Codificación no es lo mismo que modulación.
- ASK cambia amplitud.
- FSK cambia frecuencia.
- PSK cambia fase.
- QAM cambia amplitud y fase.
- FDM divide por frecuencia.
- TDM divide por tiempo.
- WDM se usa en fibra óptica.

---

## **14. Mini test**

### **Pregunta 1**

Marca las correctas:

A. La capa física transmite bits.  
B. La capa física se encarga del direccionamiento IP.  
C. La capa física define cómo se representan los bits mediante señales.  
D. La capa física trabaja directamente con puertos TCP.

Correctas: **A y C**.

---

### **Pregunta 2**

Marca las correctas:

A. El par trenzado es un medio guiado.  
B. La fibra óptica es un medio no guiado.  
C. La radio es un medio no guiado.  
D. El cable coaxial es un medio guiado.

Correctas: **A, C y D**.

---

### **Pregunta 3**

Marca las correctas:

A. UTP no tiene apantallamiento.  
B. STP tiene apantallamiento.  
C. La fibra óptica transmite mediante luz.  
D. La fibra óptica es muy sensible a interferencias electromagnéticas.

Correctas: **A, B y C**.

---

### **Pregunta 4**

Marca las correctas:

A. ASK modifica la amplitud.  
B. FSK modifica la frecuencia.  
C. PSK modifica la fase.  
D. QAM combina amplitud y fase.

Correctas: **A, B, C y D**.

---

### **Pregunta 5**

Marca las correctas:

A. FDM reparte el medio por frecuencias.  
B. TDM reparte el medio por intervalos de tiempo.  
C. WDM se asocia a fibra óptica.  
D. Full-duplex permite comunicación en ambos sentidos simultáneamente.

Correctas: **A, B, C y D**.