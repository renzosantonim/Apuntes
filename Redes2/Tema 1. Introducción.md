
## **1. Idea general de Internet**

Internet es una **red de redes** que conecta dispositivos de todo el mundo.

También puede verse como una infraestructura que permite ejecutar **aplicaciones distribuidas**, es decir, aplicaciones cuyos procesos están en máquinas distintas y se comunican por red.

Ejemplos:

- Web.
- Correo electrónico.
- Mensajería.
- Streaming.
- Juegos online.
- Aplicaciones P2P.

Importante:

- **Internet no es lo mismo que la Web**.
- Internet es la infraestructura.
- La Web es una aplicación que funciona sobre Internet.

---

## **2. Elementos básicos de Internet**

Internet está formada por:

- **Hosts o sistemas terminales**: ordenadores, móviles, servidores, etc.
- **Enlaces de comunicación**: cable, fibra, radio, satélite, etc.
- **Dispositivos intermedios**: routers, switches, puntos de acceso, etc.
- **ISP**: proveedores de acceso a Internet.
- **Protocolos**: reglas que permiten la comunicación.

Los estándares de Internet suelen publicarse como **RFC** y son desarrollados por organismos como la **IETF**.

---

## **3. Qué es un protocolo**

Un protocolo define:

- El formato de los mensajes.
- El orden en que se intercambian.
- Las acciones al enviar y recibir mensajes.
- Las acciones ante ciertos eventos.

Definición útil:

Un protocolo es un conjunto de reglas que define cómo se comunican dos o más entidades en una red.

Ejemplos:

- IP.
- TCP.
- UDP.
- HTTP.
- DNS.
- Ethernet.

---

## **4. Aplicaciones distribuidas**

Una aplicación distribuida está formada por programas que se ejecutan en distintos equipos y se comunican por red.

### **Cliente-servidor**

- El **cliente** solicita un servicio.
- El **servidor** ofrece el servicio.
- El cliente suele iniciar la comunicación.

Ejemplo:

- Navegador web y servidor web.

### **P2P**

- Los nodos pueden actuar como clientes y servidores.
- No depende necesariamente de un servidor central.
- Los nodos se llaman **peers**.

Ejemplo:

- Compartición de archivos P2P.

---

## **5. Tipos de redes según alcance**

|**Tipo**|**Significado**|**Alcance típico**|
|---|---|---|
|LAN|Local Area Network|Casa, aula, edificio|
|WLAN|Wireless LAN|LAN inalámbrica, WiFi|
|MAN|Metropolitan Area Network|Ciudad o zona metropolitana|
|WAN|Wide Area Network|Grandes distancias|

---

## **6. Organización por capas**

Las redes se organizan en capas para reducir la complejidad.

Cada capa:

- Usa servicios de la capa inferior.
- Ofrece servicios a la capa superior.
- Se encarga de una función concreta.

### **Modelo TCP/IP usado en clase**

|**Capa**|**Unidad de datos**|**Ejemplos**|
|---|---|---|
|Aplicación|Mensaje|HTTP, DNS, SMTP|
|Transporte|Segmento / datagrama UDP|TCP, UDP|
|Red|Datagrama / paquete|IP|
|Enlace|Trama|Ethernet, WiFi|
|Física|Bits|Cable, fibra, radio|

### **Modelo OSI**

Capas OSI, de abajo arriba:

1. Física.
2. Enlace.
3. Red.
4. Transporte.
5. Sesión.
6. Presentación.
7. Aplicación.

En TCP/IP, las funciones de **sesión** y **presentación** suelen integrarse en **aplicación**.

---

## **7. Encapsulación**

Al enviar datos, cada capa añade su propia cabecera.

Orden típico:

**Mensaje → Segmento → Datagrama/paquete → Trama → Bits**

Al recibir, se hace el proceso inverso: cada capa elimina su cabecera y entrega los datos a la capa superior.

Eso se llama **desencapsulación**.

---

## **8. Dispositivos básicos**

|**Dispositivo**|**Capa principal**|**Función básica**|
|---|---|---|
|Switch|Enlace|Reenvía tramas usando direcciones MAC|
|Router|Red|Reenvía paquetes usando direcciones IP|

Idea importante:

- Un switch clásico trabaja en capa 2.
- Un router trabaja en capa 3.

---

## **9. Lo más probable de test**

- Internet no es lo mismo que la Web.
- Un protocolo define reglas de comunicación.
- Cliente-servidor: cliente pide, servidor responde.
- P2P: los nodos pueden actuar como cliente y servidor.
- LAN/WLAN/MAN/WAN según alcance.
- Capas TCP/IP en orden.
- Capas OSI en orden.
- Unidad de datos por capa.
- Switch = capa 2.
- Router = capa 3.
- Encapsulación: mensaje, segmento, datagrama, trama, bits.

---

## **10. Mini test**

### **Pregunta 1**

Marca las correctas:

A. Internet es una red de redes.  
B. La Web e Internet son exactamente lo mismo.  
C. Una aplicación distribuida puede tener procesos en máquinas distintas.  
D. Los protocolos definen reglas de comunicación.

Correctas: **A, C y D**.

### **Pregunta 2**

Marca las correctas:

A. En cliente-servidor, el cliente solicita servicios.  
B. En P2P, los nodos pueden actuar como clientes y servidores.  
C. En P2P siempre existe un único servidor central obligatorio.  
D. Un navegador web puede actuar como cliente.

Correctas: **A, B y D**.

### **Pregunta 3**

Marca las correctas:

A. La capa física transmite bits.  
B. La capa de enlace trabaja con tramas.  
C. La capa de red trabaja con datagramas o paquetes.  
D. La capa de aplicación trabaja con mensajes.

Correctas: **A, B, C y D**.

### **Pregunta 4**

Marca las correctas:

A. Un switch clásico trabaja principalmente en capa de enlace.  
B. Un router trabaja principalmente en capa de red.  
C. Un switch clásico enruta paquetes IP entre redes diferentes.  
D. Un router usa direcciones IP para tomar decisiones de reenvío.

Correctas: **A, B y D**.