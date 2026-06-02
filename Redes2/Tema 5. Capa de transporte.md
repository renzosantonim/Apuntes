## **1. Función de la capa de transporte**

La **capa de transporte** se encarga de la comunicación lógica entre **procesos** que se ejecutan en hosts distintos.

**Idea clave:**  
La capa de red comunica **hosts**, pero la capa de transporte comunica **procesos**.

Ejemplo:

Un ordenador puede tener abiertas varias aplicaciones a la vez:

- navegador web,
- Discord,
- correo,
- juego online.

Todas usan la red, pero los datos tienen que llegar al proceso correcto. De eso se encarga la capa de transporte mediante los **puertos**.

---

## **2. Protocolos principales de transporte**

Los dos protocolos más importantes son:

### **TCP**

TCP es un protocolo:

- orientado a conexión,
- fiable,
- entrega los datos en orden,
- tiene control de flujo,
- tiene control de congestión,
- usa puertos,
- trabaja como un flujo de bytes.

Se usa cuando importa que los datos lleguen completos y ordenados.

Ejemplos:

- web HTTP/HTTPS,
- correo,
- transferencia de archivos,
- SSH.

### **UDP**

UDP es un protocolo:

- no orientado a conexión,
- no fiable,
- no garantiza entrega,
- no garantiza orden,
- tiene menos sobrecarga que TCP,
- usa puertos,
- trabaja con datagramas independientes.

Se usa cuando se prefiere rapidez, baja latencia o simplicidad.

Ejemplos:

- DNS normalmente,
- DHCP,
- streaming,
- VoIP,
- juegos online.

---

## **3. Puertos**

Un **puerto** identifica una aplicación o proceso dentro de un host.

Las direcciones IP identifican máquinas.  
Los puertos identifican procesos dentro de esas máquinas.

**Idea clave:**

- IP destino: a qué máquina va el paquete.
- Puerto destino: a qué proceso de esa máquina va el segmento o datagrama.

Los puertos tienen **16 bits**, por tanto van de:

**0 a 65535**

Ejemplos importantes:

- HTTP: puerto 80 TCP.
- HTTPS: puerto 443 TCP.
- DNS: puerto 53 UDP/TCP.
- DHCP: puertos 67 y 68 UDP.
- SMTP: puerto 25 TCP.
- BGP: puerto 179 TCP.

---

## **4. Multiplexación y demultiplexación**

### **Multiplexación**

La **multiplexación** ocurre en el emisor.

Consiste en recoger datos de varios procesos y enviarlos usando la capa de red.

Ejemplo:

Tu ordenador puede estar enviando datos de Chrome, Discord y Spotify al mismo tiempo.  
La capa de transporte multiplexa esos datos.

### **Demultiplexación**

La **demultiplexación** ocurre en el receptor.

Consiste en mirar el puerto de destino y entregar los datos al proceso correcto.

Ejemplo:

Si llega un segmento con puerto destino 80, se entrega al proceso que esté escuchando en el puerto 80.

**Idea clave:**  
Los puertos permiten que varios procesos usen la red al mismo tiempo.

---

## **5. Qué identifica una comunicación**

En UDP, normalmente se usa:

- IP destino,
- puerto destino.

En TCP, una conexión queda identificada por cuatro valores:

- IP origen,
- puerto origen,
- IP destino,
- puerto destino.

Esto permite que un servidor atienda muchas conexiones a la vez, aunque todas vayan al mismo puerto del servidor.

Ejemplo:

Un servidor web escucha en el puerto 80, pero puede tener muchos clientes conectados porque cada conexión tiene distinto puerto origen y/o IP origen.

---

## **6. Checksum**

Tanto TCP como UDP tienen **checksum**.

El checksum sirve para detectar errores en los datos recibidos.

Diferencia importante:

- UDP puede detectar errores, pero no retransmite.
- TCP puede detectar errores y pedir/retransmitir datos porque ofrece fiabilidad.

**Trampa típica:**  
UDP no es “sin control de errores” del todo. Tiene checksum, pero no garantiza recuperación.

---

## **7. Transferencia fiable**

La red puede provocar varios problemas:

- pérdida de paquetes,
- errores en los datos,
- paquetes duplicados,
- paquetes desordenados.

Para conseguir una transferencia fiable se usan mecanismos como:

- ACKs,
- números de secuencia,
- temporizadores,
- retransmisiones.

TCP incorpora estos mecanismos.  
UDP no los incorpora por defecto.

---

## **8. ACKs, temporizadores y números de secuencia**

### **ACK**

Un **ACK** es una confirmación.

Sirve para que el receptor diga:

“he recibido correctamente este dato”.

### **Temporizador**

El emisor activa un temporizador cuando envía datos.

Si pasa demasiado tiempo sin recibir ACK, supone que hubo pérdida y retransmite.

### **Número de secuencia**

Permite identificar los datos enviados.

Sirve para:

- detectar duplicados,
- ordenar datos,
- saber qué se ha recibido y qué falta.

---

## **9. Protocolos ARQ**

ARQ significa **Automatic Repeat Request**.

Son mecanismos de retransmisión automática para conseguir fiabilidad.

Los principales son:

- Parada y Espera.
- Go-Back-N.
- Repetición Selectiva.

---

## **10. Parada y Espera**

En **Parada y Espera**, el emisor envía un paquete y espera su ACK antes de enviar el siguiente.

Funcionamiento:

1. El emisor envía un paquete.
2. Activa un temporizador.
3. El receptor recibe el paquete y responde con ACK.
4. El emisor recibe el ACK y envía el siguiente paquete.

Si el ACK no llega antes de que expire el temporizador, el emisor retransmite.

### **Ventajas**

- Es simple.
- Fácil de implementar.

### **Inconvenientes**

- Es poco eficiente.
- Solo hay un paquete en tránsito.
- Desaprovecha enlaces con mucho retardo.

**Idea clave:**  
Parada y Espera es fiable pero muy lento en enlaces con alta latencia.

---

## **11. Bit alternante**

En Parada y Espera se puede usar un número de secuencia de 1 bit:

- 0,
- 1. 1.

El emisor alterna entre 0 y 1.

Esto permite detectar duplicados.

Ejemplo:

Si el receptor ya recibió el paquete 0 y vuelve a recibir otro paquete 0, sabe que probablemente es una retransmisión duplicada.

---

## **12. Go-Back-N**

En **Go-Back-N**, el emisor puede enviar varios paquetes sin esperar ACK de cada uno inmediatamente.

Usa una **ventana deslizante**.

Características:

- permite tener varios paquetes en tránsito,
- usa ACKs acumulativos,
- si se pierde un paquete, se retransmite desde ese paquete en adelante,
- normalmente usa un único temporizador para el paquete más antiguo no confirmado.

### **Ventaja**

Es más eficiente que Parada y Espera porque permite enviar varios paquetes seguidos.

### **Inconveniente**

Puede retransmitir paquetes que ya habían llegado correctamente.

**Idea clave:**  
Go-Back-N retrocede hasta el paquete perdido y retransmite desde ahí.

---

## **13. ACK acumulativo**

En Go-Back-N se usan ACKs acumulativos.

Esto significa que un ACK confirma todos los paquetes anteriores hasta cierto punto.

Ejemplo:

Si llega ACK 5, significa que se han recibido correctamente todos los paquetes hasta el 5, según la numeración usada.

---

## **14. Repetición Selectiva**

En **Repetición Selectiva**, el emisor también puede enviar varios paquetes sin esperar, pero solo retransmite los paquetes que se pierden o llegan con error.

Características:

- usa ventana deslizante,
- usa ACKs individuales,
- retransmite solo los paquetes perdidos,
- necesita más memoria,
- necesita más control,
- suele usar temporizadores por paquete.

### **Ventaja**

Es más eficiente que Go-Back-N cuando hay pérdidas.

### **Inconveniente**

Es más complejo.

**Idea clave:**  
Repetición Selectiva retransmite solo lo que falta.

---

## **15. Comparación rápida de ARQ**

**Parada y Espera**

- Solo envía un paquete cada vez.
- Espera ACK antes de continuar.
- Muy simple.
- Poco eficiente.

**Go-Back-N**

- Envía varios paquetes.
- Usa ACK acumulativos.
- Si falla uno, retransmite desde ese en adelante.
- Eficiencia media.

**Repetición Selectiva**

- Envía varios paquetes.
- Usa ACKs individuales.
- Retransmite solo los perdidos.
- Más eficiente, pero más complejo.

---

## **16. UDP**

UDP es un protocolo de transporte sencillo.

Características principales:

- no establece conexión,
- no garantiza entrega,
- no garantiza orden,
- no garantiza que no haya duplicados,
- tiene checksum,
- usa puertos,
- tiene poca sobrecarga.

UDP es útil cuando la aplicación puede tolerar pérdidas o cuando prefiere rapidez.

Ejemplos:

- DNS,
- DHCP,
- VoIP,
- streaming,
- juegos online.

**Idea clave:**  
UDP no es fiable, pero es ligero y rápido.

---

## **17. Cabecera UDP**

La cabecera UDP es sencilla.

Campos principales:

- puerto origen,
- puerto destino,
- longitud,
- checksum.

No tiene campos para controlar conexión, ventana, números de secuencia o ACKs como TCP.

Por eso tiene menos sobrecarga.

---

## **18. TCP**

TCP es un protocolo de transporte fiable y orientado a conexión.

Características principales:

- establece conexión antes de transmitir,
- entrega datos en orden,
- detecta errores,
- retransmite si hace falta,
- elimina duplicados,
- usa control de flujo,
- usa control de congestión,
- usa puertos,
- trabaja como flujo de bytes.

**Idea clave:**  
TCP da fiabilidad sobre una red IP que no es fiable.

---

## **19. TCP como flujo de bytes**

TCP no conserva necesariamente los límites de los mensajes de la aplicación.

Esto significa que si una aplicación hace dos envíos separados, el receptor podría recibirlos:

- juntos,
- separados,
- partidos en varios trozos.

TCP garantiza el orden de los bytes, pero no separa “mensajes” como tal.

Esto es importante para sockets.

**Idea clave:**  
TCP es flujo de bytes, no mensajes independientes.

---

## **20. Establecimiento de conexión TCP**

TCP usa el **three-way handshake** para establecer conexión.

Pasos:

1. Cliente envía SYN.
2. Servidor responde SYN-ACK.
3. Cliente responde ACK.

Después de esto, la conexión queda establecida.

**Idea clave:**  
TCP necesita conexión previa; UDP no.

---

## **21. Cierre de conexión TCP**

Para cerrar una conexión TCP se usan segmentos con FIN y ACK.

La idea básica es que cada extremo cierra su sentido de la comunicación.

No hace falta memorizar todos los estados salvo que el profesor haya insistido, pero sí saber que TCP tiene un cierre ordenado de conexión.

---

## **22. Control de flujo**

El **control de flujo** evita que el emisor envíe más datos de los que el receptor puede procesar.

Protege al receptor.

TCP usa una ventana de recepción.

**Idea clave:**  
Control de flujo = no saturar al receptor.

---

## **23. Control de congestión**

El **control de congestión** evita saturar la red.

Protege a la red.

TCP reduce su ritmo de envío cuando detecta congestión, por ejemplo mediante pérdidas o timeouts.

**Idea clave:**  
Control de congestión = no saturar la red.

---

## **24. Control de flujo vs control de congestión**

Esta diferencia es muy preguntable.

**Control de flujo**

- Protege al receptor.
- Evita enviar más de lo que el receptor puede aceptar.
- Depende de la capacidad/buffer del receptor.

**Control de congestión**

- Protege a la red.
- Evita meter demasiado tráfico en la red.
- Depende de pérdidas, retardos o señales de congestión.

---

# **Lo importante de verdad**

Para este tema, lo más importante es:

- La capa de transporte comunica procesos.
- IP identifica hosts; los puertos identifican procesos.
- TCP y UDP son los protocolos principales.
- TCP es fiable, orientado a conexión y ordenado.
- UDP no es fiable, no orientado a conexión y tiene poca sobrecarga.
- UDP también usa puertos y checksum.
- TCP establece conexión con SYN, SYN-ACK, ACK.
- TCP trabaja como flujo de bytes.
- UDP trabaja con datagramas independientes.
- Multiplexación: varios procesos envían usando transporte.
- Demultiplexación: se entrega al proceso correcto usando puertos.
- ACKs, temporizadores y números de secuencia permiten fiabilidad.
- Parada y Espera: uno a uno.
- Go-Back-N: retransmite desde el perdido.
- Repetición Selectiva: retransmite solo el perdido.
- Control de flujo protege al receptor.
- Control de congestión protege a la red.

---

# **Trampas típicas**

**“La capa de transporte comunica máquinas.”**  
Impreciso. La capa de red comunica hosts; la capa de transporte comunica procesos.

**“UDP no usa puertos.”**  
Falso. UDP sí usa puertos.

**“UDP garantiza entrega pero no orden.”**  
Falso. UDP no garantiza ni entrega ni orden.

**“TCP no necesita establecer conexión.”**  
Falso. TCP es orientado a conexión.

**“TCP conserva los límites de los mensajes.”**  
Falso. TCP es un flujo de bytes.

**“UDP es un flujo de bytes.”**  
Falso. UDP trabaja con datagramas independientes.

**“El control de flujo evita congestionar la red.”**  
Falso. El control de flujo protege al receptor.

**“El control de congestión protege al receptor.”**  
Falso. Protege a la red.

**“Go-Back-N retransmite solo el paquete perdido.”**  
Falso. Retransmite desde el perdido en adelante.

**“Repetición Selectiva retransmite desde el perdido en adelante.”**  
Falso. Retransmite solo los paquetes perdidos o erróneos.

**“UDP no tiene checksum.”**  
Falso. UDP sí tiene checksum.

---

# **Mini test**

## **Pregunta 1**

Marca las correctas:

A. La capa de transporte comunica procesos.  
B. TCP y UDP son protocolos de transporte.  
C. Los puertos permiten identificar procesos dentro de un host.  
D. La capa de transporte usa direcciones MAC para entregar datos.

Correctas: **A, B y C**.

---

## **Pregunta 2**

Marca las correctas:

A. TCP es orientado a conexión.  
B. TCP entrega los datos en orden.  
C. TCP tiene control de flujo.  
D. TCP tiene control de congestión.

Correctas: **A, B, C y D**.

---

## **Pregunta 3**

Marca las correctas:

A. UDP no garantiza entrega.  
B. UDP no garantiza orden.  
C. UDP tiene menos sobrecarga que TCP.  
D. UDP usa puertos.

Correctas: **A, B, C y D**.

---

## **Pregunta 4**

Marca las correctas:

A. Parada y Espera envía un paquete y espera ACK.  
B. Go-Back-N usa ACKs acumulativos.  
C. Repetición Selectiva retransmite solo los paquetes perdidos.  
D. Go-Back-N retransmite solo el paquete perdido.

Correctas: **A, B y C**.

---

## **Pregunta 5**

Marca las correctas:

A. El control de flujo protege al receptor.  
B. El control de congestión protege a la red.  
C. TCP establece conexión con SYN, SYN-ACK y ACK.  
D. UDP necesita three-way handshake.

Correctas: **A, B y C**.