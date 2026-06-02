## **1. Función de la capa de enlace**

La **capa de enlace** se encarga de transmitir datos entre nodos conectados directamente por un mismo enlace.

Su unidad de datos es la **trama**.

No se encarga de llevar paquetes de extremo a extremo por Internet. Eso es tarea de la capa de red.

Idea clave:

- **Capa física:** transmite bits.
- **Capa de enlace:** transmite tramas entre nodos vecinos.
- **Capa de red:** transmite paquetes entre origen y destino atravesando redes.

---

## **2. Funciones principales de la capa de enlace**

La capa de enlace puede encargarse de:

- formar tramas,
- controlar el acceso al medio,
- detectar errores,
- usar direcciones físicas,
- entregar datos entre nodos vecinos.

No todas las tecnologías de enlace implementan exactamente las mismas funciones, pero esas son las más típicas.

---

## **3. Tramas**

Una **trama** es la unidad de datos de la capa de enlace.

Normalmente contiene:

- cabecera de enlace,
- datos,
- cola o tráiler.

Dentro de la parte de datos suele ir encapsulado un paquete de capa de red, por ejemplo un datagrama IP.

Estructura simplificada:

| **Parte**    | **Función**                                         |
| ------------ | --------------------------------------------------- |
| Cabecera     | Información de control, direcciones MAC, tipo, etc. |
| Datos        | Información procedente de la capa superior          |
| Cola/tráiler | Detección de errores, como CRC                      |

---

## **4. Direcciones MAC**

Las direcciones **MAC** son direcciones de capa de enlace.

Características:

- identifican interfaces de red,
- normalmente tienen 48 bits,
- se escriben en hexadecimal,
- se usan en redes locales,
- son distintas de las direcciones IP.

Ejemplo de MAC:

`00:1A:2B:3C:4D:5E`

Diferencia importante:

| **Dirección** | **Capa** | **Uso**                        |
| ------------- | -------- | ------------------------------ |
| MAC           | Enlace   | Entrega dentro de la red local |
| IP            | Red      | Entrega entre redes            |
## **5. Control de errores**

La capa de enlace puede detectar errores en las tramas.

Un mecanismo típico es el **CRC**, Cyclic Redundancy Check.

Idea:

- El emisor calcula un valor de comprobación.
- Lo añade a la trama.
- El receptor recalcula y compara.
- Si no coincide, la trama se considera errónea.

Importante:

Detectar errores no significa necesariamente corregirlos. Muchas veces, si una trama llega mal, se descarta.

---

## **6. Control de acceso al medio**

Cuando varios dispositivos comparten el mismo medio, hace falta decidir quién puede transmitir.

Esto se llama **control de acceso al medio** o **MAC**, Medium Access Control.

No confundir:

- **MAC dirección:** identificador de interfaz.
- **MAC como subcapa:** control de acceso al medio.

Ejemplos de problemas:

- dos dispositivos transmiten a la vez,
- se produce una colisión,
- hay que organizar el acceso al canal.

---

## **7. Protocolos de acceso múltiple**

Cuando varios nodos comparten un canal, pueden usarse distintos métodos de acceso.

### **División del canal**

El canal se reparte entre los usuarios.

Ejemplos:

| **Técnica** | **Reparto**              |
| ----------- | ------------------------ |
| TDMA        | Por turnos de tiempo     |
| FDMA        | Por bandas de frecuencia |
| CDMA        | Por códigos              |

### **Acceso aleatorio**

Los nodos transmiten cuando tienen datos.

Puede haber colisiones.

Ejemplos:

- ALOHA,
- CSMA,
- CSMA/CD,
- CSMA/CA.

### **Toma de turnos**

Los nodos se organizan para transmitir por turnos.

Ejemplos:

- polling,
- token passing.

---

## **8. CSMA/CD**

**CSMA/CD** significa Carrier Sense Multiple Access with Collision Detection.

Se usaba en Ethernet compartida antigua.

Funcionamiento básico:

1. El nodo escucha el canal.
2. Si está libre, transmite.
3. Si detecta una colisión, deja de transmitir.
4. Espera un tiempo aleatorio.
5. Intenta transmitir de nuevo.

Ideas importantes:

- Detecta colisiones.
- Se asocia a Ethernet clásica.
- Tiene sentido en medios compartidos half-duplex.
- En Ethernet con switches full-duplex prácticamente no hay colisiones.

---

## **9. CSMA/CA**

**CSMA/CA** significa Carrier Sense Multiple Access with Collision Avoidance.

Se usa en redes inalámbricas como WiFi.

A diferencia de CSMA/CD, intenta **evitar** colisiones en vez de detectarlas.

¿Por qué?

Porque en redes inalámbricas es difícil detectar colisiones mientras se transmite.

Ideas importantes:

- Se usa en WiFi.
- Intenta evitar colisiones.
- Puede usar ACKs.
- Está relacionado con el problema del nodo oculto.

---

## **10. Ethernet**

Ethernet es la tecnología más habitual en redes LAN cableadas.

Estándar:

**IEEE 802.3**

Características:

- usa tramas,
- usa direcciones MAC,
- tradicionalmente usaba CSMA/CD,
- hoy suele funcionar con switches,
- en full-duplex no hay colisiones.

Velocidades típicas:

- 10 Mbps,
- 100 Mbps,
- 1 Gbps,
- 10 Gbps.

Nomenclatura típica:

| **Nombre** | **Significado aproximado**          |
| ---------- | ----------------------------------- |
| 10BASE-T   | Ethernet 10 Mbps sobre par trenzado |
| 100BASE-TX | Fast Ethernet 100 Mbps              |
| 1000BASE-T | Gigabit Ethernet sobre par trenzado |

---

## **11. Switch**

Un **switch** es un dispositivo de capa de enlace.

Funciona principalmente usando direcciones MAC.

Qué hace:

- recibe tramas,
- aprende qué MAC está en cada puerto,
- guarda esa información en una tabla MAC,
- reenvía la trama por el puerto adecuado.

Si no conoce la MAC destino, puede inundar la trama por varios puertos, excepto por el puerto por el que llegó.

---

## **12. Tabla MAC**

La tabla MAC relaciona:

**dirección MAC → puerto del switch**

Ejemplo:

| **MAC**           | **Puerto** |
| ----------------- | ---------- |
| AA:AA:AA:AA:AA:AA | 1          |
| BB:BB:BB:BB:BB:BB | 2          |
El switch aprende mirando la **MAC origen** de las tramas que recibe.

Luego reenvía usando la **MAC destino**.

Esto es muy preguntable:

- aprende con la MAC origen,
- reenvía buscando la MAC destino.

---

## **13. Hub vs switch**
| **Dispositivo** | **Capa** | **Funcionamiento**                |
| --------------- | -------- | --------------------------------- |
| Hub             | Física   | Repite bits por todos los puertos |
| Switch          | Enlace   | Reenvía tramas según MAC          |

El hub no entiende direcciones MAC ni tramas. Solo repite señales.

El switch es más inteligente y reduce colisiones.

---

## **14. Dominios de colisión y broadcast**

### **Dominio de colisión**

Conjunto de dispositivos que pueden colisionar si transmiten a la vez.

- Con hub: todos los equipos comparten el mismo dominio de colisión.
- Con switch: cada puerto suele ser su propio dominio de colisión.

### **Dominio de broadcast**

Conjunto de dispositivos que reciben una trama broadcast.

Un switch, por defecto, propaga broadcasts dentro de la misma LAN.

Para separar dominios de broadcast se usan routers o VLANs.

---

## **15. WiFi**

WiFi pertenece a la capa de enlace y física.

Estándar:

**IEEE 802.11**

Características:

- red inalámbrica,
- usa puntos de acceso,
- usa CSMA/CA,
- comparte el medio radio,
- es más propensa a interferencias que una red cableada.

---

## **16. Punto de acceso**

Un **punto de acceso**, AP, conecta dispositivos inalámbricos a la red.

En una red WiFi típica:

- los clientes se conectan al AP,
- el AP actúa como intermediario,
- el AP puede estar conectado a una red cableada.

---

## **17. BSS y ESS**

### **BSS**

**Basic Service Set**

Es el conjunto de estaciones inalámbricas asociadas a un punto de acceso.

### **ESS**

**Extended Service Set**

Conjunto de varios BSS conectados entre sí, normalmente mediante una red de distribución.

Permite cubrir áreas más grandes con varios puntos de acceso.

---

## **18. ARP**

**ARP** significa Address Resolution Protocol.

Sirve para obtener la dirección MAC asociada a una dirección IP dentro de una red local.

Ejemplo:

Un equipo quiere enviar datos a `192.168.1.20`, pero necesita saber su MAC. Para eso usa ARP.

Funcionamiento básico:

1. El host envía una solicitud ARP en broadcast.
2. El equipo que tiene esa IP responde con su MAC.
3. El emisor guarda la correspondencia en su caché ARP.

Importante:

ARP se usa en IPv4.

---

## **19. Lo más probable de test**

De este tema conviene saberse muy bien:

- La capa de enlace usa **tramas**.
- La capa de enlace comunica nodos vecinos.
- Las direcciones MAC son de capa de enlace.
- Las MAC suelen tener 48 bits.
- CRC sirve para detección de errores.
- Ethernet es **IEEE 802.3**.
- WiFi es **IEEE 802.11**.
- Ethernet clásica usaba CSMA/CD.
- WiFi usa CSMA/CA.
- Un switch trabaja en capa 2.
- Un hub trabaja en capa 1.
- El switch aprende usando MAC origen.
- El switch reenvía usando MAC destino.
- ARP resuelve IP → MAC.
- Con switches se reducen dominios de colisión.
- El broadcast se propaga por la LAN salvo que haya routers/VLANs.

---

## **20. Trampas típicas**

### **Trampa 1**

“Un switch aprende mirando la MAC destino.”

Falso. Aprende mirando la **MAC origen**.

---

### **Trampa 2**

“ARP traduce nombres de dominio a direcciones IP.”

Falso. Eso lo hace DNS. ARP obtiene la **MAC asociada a una IP**.

---

### **Trampa 3**

“WiFi usa CSMA/CD.”

Falso. WiFi usa **CSMA/CA**.

---

### **Trampa 4**

“Ethernet es IEEE 802.11.”

Falso. Ethernet es **IEEE 802.3**. WiFi es **IEEE 802.11**.

---

### **Trampa 5**

“Un hub trabaja en capa de enlace.”

Falso. Un hub trabaja en **capa física**.

---

### **Trampa 6**

“Un switch clásico enruta entre redes IP distintas.”

Falso. Un switch clásico trabaja en capa 2. Para enrutar entre redes hace falta router o switch multicapa.

---

## **21. Mini test**

### **Pregunta 1**

Marca las correctas:

A. La capa de enlace trabaja con tramas.  
B. La capa de enlace se encarga de comunicar nodos vecinos.  
C. La capa de enlace usa direcciones MAC.  
D. La capa de enlace se encarga principalmente de enrutar paquetes entre redes lejanas.

Correctas: **A, B y C**.

---

### **Pregunta 2**

Marca las correctas:

A. Ethernet es IEEE 802.3.  
B. WiFi es IEEE 802.11.  
C. Ethernet clásica usaba CSMA/CD.  
D. WiFi usa CSMA/CD.

Correctas: **A, B y C**.

---

### **Pregunta 3**

Marca las correctas:

A. Un switch aprende direcciones mirando la MAC origen.  
B. Un switch reenvía tramas mirando la MAC destino.  
C. Un hub trabaja en capa física.  
D. Un switch clásico trabaja en capa de red.

Correctas: **A, B y C**.

---

### **Pregunta 4**

Marca las correctas:

A. ARP sirve para obtener la MAC asociada a una IP.  
B. DNS sirve para obtener la IP asociada a un nombre.  
C. ARP se usa dentro de la red local.  
D. ARP sustituye a TCP en redes Ethernet.

Correctas: **A, B y C**.

---

### **Pregunta 5**

Marca las correctas:

A. CRC permite detectar errores.  
B. Una dirección MAC suele tener 48 bits.  
C. Un switch reduce dominios de colisión.  
D. Un router o una VLAN pueden separar dominios de broadcast.

Correctas: **A, B, C y D**.