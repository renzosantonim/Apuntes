## **1. Función de la capa de aplicación**

La **capa de aplicación** es la capa más cercana al usuario.

Se encarga de definir los protocolos que usan las aplicaciones para comunicarse por red.

Ejemplos de aplicaciones de red:

- navegador web,
- correo electrónico,
- mensajería,
- juegos online,
- streaming,
- aplicaciones P2P.

**Idea clave:**  
La capa de aplicación no transmite bits directamente. Usa los servicios de la capa de transporte, normalmente **TCP** o **UDP**.

---

## **2. Aplicación, proceso y socket**

Una **aplicación** es un programa que realiza una tarea.

Un **proceso** es una aplicación en ejecución.

Una **aplicación distribuida** está formada por procesos que se ejecutan en máquinas distintas y se comunican por red.

Ejemplo:

- navegador web en tu ordenador,
- servidor web en otra máquina.

Ambos son procesos que se comunican a través de la red.

El **socket** es la interfaz que usa un proceso para enviar y recibir datos por la red.

**Idea clave:**  
El socket es la “puerta” entre la aplicación y la capa de transporte.

---

## **3. Arquitecturas de aplicación**

### **Cliente-servidor**

En la arquitectura cliente-servidor hay dos roles:

**Cliente**

- Solicita servicios.
- Normalmente inicia la comunicación.
- Ejemplo: navegador web.

**Servidor**

- Ofrece servicios.
- Espera peticiones.
- Suele estar siempre disponible.
- Ejemplo: servidor web.

Ejemplo típico:

Cuando entras en una página web, tu navegador actúa como cliente y el servidor de la página responde.

---

### **P2P**

En una arquitectura **P2P**, los nodos pueden actuar como clientes y servidores.

Los nodos se llaman **peers**.

Características:

- No depende necesariamente de un servidor central.
- Cada peer puede pedir y ofrecer recursos.
- Suele escalar bien porque cuantos más peers hay, más recursos pueden aportar.

Ejemplo típico:

- BitTorrent.
- Compartición de archivos entre usuarios.

**Idea clave:**  
Cliente-servidor separa roles. P2P mezcla roles.

---

## **4. Comunicación entre procesos**

Dos procesos en máquinas distintas se comunican enviando mensajes a través de sockets.

Para que un proceso pueda enviar datos a otro necesita saber:

- dirección IP del host destino,
- puerto del proceso destino.

Ejemplo:

Una aplicación cliente quiere conectarse a un servidor web:

- IP: identifica la máquina del servidor.
- Puerto 80 o 443: identifica el servicio web dentro de esa máquina.

**Idea clave:**  
IP identifica el host. Puerto identifica el proceso o servicio.

---

## **5. HTTP**

**HTTP**, HyperText Transfer Protocol, es el protocolo principal de la Web.

Características:

- Es un protocolo de capa de aplicación.
- Sigue modelo cliente-servidor.
- El cliente suele ser un navegador.
- El servidor responde con recursos web.
- Usa TCP.
- HTTP usa normalmente el puerto 80.
- HTTPS usa normalmente el puerto 443.

**Idea clave:**  
HTTP no es lo mismo que Internet. HTTP es un protocolo de aplicación usado en la Web.

---

## **6. Mensajes HTTP**

HTTP funciona mediante mensajes de petición y respuesta.

### **Petición HTTP**

La envía el cliente al servidor.

Puede pedir una página, imagen, archivo, etc.

Métodos importantes:

**GET**

- Solicita un recurso.
- Ejemplo: pedir una página web.

**POST**

- Envía datos al servidor.
- Ejemplo: enviar un formulario.

**PUT**

- Actualiza o reemplaza un recurso.

**DELETE**

- Elimina un recurso.

---

### **Respuesta HTTP**

La envía el servidor al cliente.

Incluye un código de estado.

Códigos importantes:

**200 OK**

- La petición fue correcta.

**301 / 302**

- Redirección.

**400 Bad Request**

- La petición está mal formada.

**403 Forbidden**

- El acceso está prohibido.

**404 Not Found**

- Recurso no encontrado.

**500 Internal Server Error**

- Error interno del servidor.

---

## **7. HTTP persistente y no persistente**

### **HTTP no persistente**

Se abre una conexión TCP para cada objeto solicitado.

Ejemplo:

Si una página tiene HTML, imágenes y CSS, podrían abrirse varias conexiones.

Inconveniente:

- Más sobrecarga.
- Más retardos por abrir y cerrar conexiones.

### **HTTP persistente**

Se reutiliza la misma conexión TCP para varios objetos.

Ventaja:

- Menos sobrecarga.
- Mejor rendimiento.

**Idea clave:**  
HTTP persistente reutiliza conexiones TCP.

---

## **8. DNS**

**DNS**, Domain Name System, traduce nombres de dominio a direcciones IP.

Ejemplo:

`www.ull.es` → dirección IP del servidor.

Sin DNS tendríamos que recordar direcciones IP en lugar de nombres.

Características:

- Es un sistema distribuido.
- Es jerárquico.
- Usa normalmente UDP puerto 53.
- Puede usar TCP puerto 53 en algunos casos.

**Idea clave:**  
DNS resuelve nombres a IPs.

---

## **9. Jerarquía DNS**

DNS está organizado jerárquicamente.

Niveles típicos:

**Servidores raíz**

- Nivel superior.
- Indican qué servidores gestionan dominios de primer nivel.

**TLD**

- Top Level Domain.
- Ejemplos: `.com`, `.org`, `.es`, `.net`.

**Servidores autoritativos**

- Tienen la información real de un dominio concreto.
- Por ejemplo, los registros de `ull.es`.

**Servidor DNS local**

- Es el que suele consultar primero tu equipo.
- Puede pertenecer al ISP, universidad, empresa, router, etc.

---

## **10. Tipos de consultas DNS**

### **Consulta recursiva**

El servidor consultado se encarga de obtener la respuesta completa para el cliente.

El cliente pregunta y espera la respuesta final.

### **Consulta iterativa**

El servidor no da necesariamente la respuesta final, sino que indica a qué otro servidor preguntar.

**Idea clave:**  
Recursiva = “búscamelo tú”.  
Iterativa = “pregunta a este otro”.

---

## **11. Registros DNS**

Registros importantes:

**A**

- Asocia nombre con dirección IPv4.

**AAAA**

- Asocia nombre con dirección IPv6.

**CNAME**

- Alias de otro nombre.

**MX**

- Servidor de correo de un dominio.

**NS**

- Servidor de nombres autorizado para un dominio.

---

## **12. Caché DNS**

DNS usa caché para mejorar el rendimiento.

Cuando un servidor o equipo resuelve un nombre, puede guardar la respuesta durante un tiempo.

Ese tiempo se llama **TTL**, Time To Live.

Ventajas:

- Menos consultas.
- Menos retardo.
- Menos carga en servidores DNS.

Inconveniente:

- Si cambia una IP, puede tardar en propagarse por las cachés.

---

## **13. Correo electrónico**

El correo electrónico usa varios protocolos.

### **SMTP**

SMTP se usa para enviar correo.

Características:

- Protocolo de aplicación.
- Usa TCP.
- Puerto típico: 25.
- Sirve para enviar mensajes entre servidores o desde cliente a servidor.

**Idea clave:**  
SMTP = envío de correo.

---

### **POP3**

POP3 se usa para recoger correo desde un servidor.

Características:

- Descarga los mensajes al cliente.
- Modelo más simple.
- Puede borrar los mensajes del servidor tras descargarlos.

**Idea clave:**  
POP3 = descargar correo.

---

### **IMAP**

IMAP también se usa para acceder al correo, pero mantiene los mensajes en el servidor.

Características:

- Permite sincronización entre varios dispositivos.
- El correo permanece en el servidor.
- Más flexible que POP3.

**Idea clave:**  
IMAP = correo sincronizado en servidor.

---

## **14. FTP**

**FTP**, File Transfer Protocol, sirve para transferir archivos.

Características:

- Protocolo de aplicación.
- Usa TCP.
- Usa una conexión de control.
- Usa otra conexión para datos.

Puertos típicos:

- 21 para control.
- 20 para datos en modo activo.

No creo que sea lo más importante, pero puede caer una pregunta conceptual.

---

## **15. DHCP como protocolo de aplicación**

Aunque DHCP está muy relacionado con direccionamiento IP, se considera protocolo de aplicación porque funciona sobre UDP.

Sirve para asignar configuración de red automáticamente.

Puede proporcionar:

- dirección IP,
- máscara,
- puerta de enlace,
- servidores DNS.

Usa UDP.

Secuencia típica:

**DORA**

1. Discover.
2. Offer.
3. Request.
4. ACK.

---

## **16. Sockets**

Este bloque es especialmente importante porque el profesor avisó de prestar atención a la práctica de sockets.

Un **socket** es un punto final de comunicación.

Desde el punto de vista de programación, permite que una aplicación envíe y reciba datos por red.

Hay sockets TCP y UDP.

---

## **17. Socket TCP**

TCP es orientado a conexión, así que antes de enviar datos hay que establecer conexión.

### **Servidor TCP**

Pasos típicos:

1. `socket()`: crea el socket.
2. `bind()`: asocia el socket a una IP y puerto local.
3. `listen()`: pone el socket a escuchar conexiones.
4. `accept()`: acepta una conexión entrante.
5. `recv()` / `send()`: recibe y envía datos.
6. `close()`: cierra el socket.

**Idea clave:**En TCP servidor aparecen `bind`, `listen` y `accept`.

---

### **Cliente TCP**

Pasos típicos:

1. `socket()`: crea el socket.
2. `connect()`: se conecta al servidor.
3. `send()` / `recv()`: envía y recibe datos.
4. `close()`: cierra el socket.

**Idea clave:**  
El cliente TCP usa `connect()` para iniciar la conexión.

---

## **18. Socket UDP**

UDP no es orientado a conexión.

No necesita establecer conexión previa como TCP.

### **Servidor UDP**

Pasos típicos:

1. `socket()`: crea el socket UDP.
2. `bind()`: asocia el socket a un puerto local.
3. `recvfrom()`: recibe un datagrama.
4. `sendto()`: envía una respuesta.
5. `close()`: cierra el socket.

### **Cliente UDP**

Pasos típicos:

1. `socket()`: crea el socket UDP.
2. `sendto()`: envía un datagrama al servidor.
3. `recvfrom()`: recibe respuesta, si la hay.
4. `close()`: cierra el socket.

**Idea clave:**UDP normalmente usa `sendto()` y `recvfrom()`, no `listen()` ni `accept()`.

---

## **19. Diferencias entre sockets TCP y UDP**

**TCP**

- Orientado a conexión.
- Usa `connect()` en cliente.
- Usa `listen()` y `accept()` en servidor.
- Usa normalmente `send()` y `recv()`.
- Es fiable y ordenado.
- Es flujo de bytes.

**UDP**

- No orientado a conexión.
- No usa `listen()` ni `accept()`.
- Usa normalmente `sendto()` y `recvfrom()`.
- No garantiza entrega ni orden.
- Trabaja con datagramas independientes.

---

## **20. Funciones importantes de sockets**

**socket()**

- Crea un socket.

**bind()**

- Asocia un socket a una IP y puerto local.
- Muy típico en servidores.

**listen()**

- Solo en TCP servidor.
- Deja el socket escuchando conexiones.

**accept()**

- Solo en TCP servidor.
- Espera una conexión entrante.
- Devuelve un nuevo socket para comunicarse con ese cliente.

**connect()**

- Usado por el cliente TCP para conectarse al servidor.

**send()**

- Envía datos por un socket conectado, normalmente TCP.

**recv()**

- Recibe datos por un socket conectado, normalmente TCP.

**sendto()**

- Envía un datagrama indicando destino, normalmente UDP.

**recvfrom()**

- Recibe un datagrama y permite saber de quién vino, normalmente UDP.

**close()**

- Cierra el socket.

---

## **21. TCP como flujo y UDP como datagramas**

Esto puede caer perfectamente en test o en sockets.

### **TCP**

TCP es un flujo de bytes.

Eso significa que no conserva necesariamente los límites de los mensajes.

Si el emisor hace:

- `send("hola")`
- `send("adios")`

El receptor podría recibir:

- `"holaadios"` junto,
- `"hola"` y luego `"adios"`,
- o fragmentos en varias llamadas.

La aplicación debe saber separar los mensajes.

### **UDP**

UDP trabaja con datagramas.

Cada `sendto()` genera un datagrama independiente.

El receptor recibe datagramas completos, si llegan.

**Idea clave:**  
TCP = flujo de bytes.  
UDP = datagramas independientes.

---

## **22. Aplicaciones y transporte**

Cada protocolo de aplicación suele usar TCP o UDP según sus necesidades.

HTTP usa TCP porque necesita fiabilidad.

DNS suele usar UDP porque las consultas son pequeñas y rápidas, aunque también puede usar TCP.

DHCP usa UDP porque se usa incluso antes de que el cliente tenga IP configurada.

VoIP, streaming y juegos pueden usar UDP porque prefieren baja latencia frente a retransmisiones lentas.

---

# **Lo importante de verdad**

Para este tema, lo más importante es:

- La capa de aplicación define protocolos usados por aplicaciones.
- Una aplicación distribuida tiene procesos en máquinas distintas.
- Un socket conecta aplicación y transporte.
- Cliente-servidor: cliente pide, servidor responde.
- P2P: los peers pueden pedir y ofrecer.
- HTTP usa TCP.
- HTTP puerto 80, HTTPS puerto 443.
- GET solicita recursos.
- POST envía datos.
- DNS traduce nombres a IPs.
- DNS usa normalmente UDP puerto 53.
- Registros: A, AAAA, CNAME, MX, NS.
- SMTP sirve para enviar correo.
- POP3 e IMAP sirven para recibir/acceder al correo.
- DHCP usa UDP y sigue DORA.
- TCP servidor: `socket`, `bind`, `listen`, `accept`, `recv/send`, `close`.
- TCP cliente: `socket`, `connect`, `send/recv`, `close`.
- UDP: `sendto` y `recvfrom`.
- TCP es flujo de bytes.
- UDP usa datagramas independientes.

---

# **Trampas típicas**

**“DNS traduce IPs a direcciones MAC.”**  
Falso. DNS traduce nombres de dominio a IPs. ARP traduce IP a MAC en IPv4.

**“HTTP y Web son lo mismo que Internet.”**  
Falso. Internet es la infraestructura. HTTP es un protocolo de aplicación usado en la Web.

**“HTTP usa UDP normalmente.”**  
Falso. HTTP usa TCP.

**“DNS solo puede usar TCP.”**  
Falso. DNS usa normalmente UDP, aunque puede usar TCP.

**“SMTP sirve para recibir correo del servidor al cliente.”**  
Falso. SMTP se usa para enviar correo. POP3/IMAP se usan para acceder o recibir correo.

**“Un servidor TCP usa connect().”**Falso. El cliente TCP usa `connect()`. El servidor usa `bind()`, `listen()` y `accept()`.

**“UDP usa listen() y accept().”**Falso. UDP no establece conexión, normalmente usa `sendto()` y `recvfrom()`.

**“TCP conserva los mensajes tal como los manda la aplicación.”**  
Falso. TCP es flujo de bytes, no conserva límites de mensajes.

**“UDP garantiza entrega porque usa datagramas.”**  
Falso. UDP usa datagramas, pero no garantiza entrega.

**“El socket pertenece solo a la capa física.”**  
Falso. El socket es la interfaz entre aplicación y transporte.

---

# **Mini test**

## **Pregunta 1**

Marca las correctas:

A. La capa de aplicación define protocolos usados por aplicaciones.  
B. HTTP es un protocolo de capa de aplicación.  
C. DNS traduce nombres de dominio a direcciones IP.  
D. Los sockets sirven para que los procesos usen la red.

Correctas: **A, B, C y D**.

---

## **Pregunta 2**

Marca las correctas:

A. HTTP usa normalmente TCP.  
B. HTTPS usa normalmente el puerto 443.  
C. GET se usa para solicitar recursos.  
D. POST puede usarse para enviar datos al servidor.

Correctas: **A, B, C y D**.

---

## **Pregunta 3**

Marca las correctas:

A. DNS usa normalmente UDP puerto 53.  
B. Un registro A asocia un nombre con una IPv4.  
C. Un registro MX está relacionado con correo.  
D. DNS sustituye a ARP.

Correctas: **A, B y C**.

---

## **Pregunta 4**

Marca las correctas:

A. Un servidor TCP usa `bind()`.  
B. Un servidor TCP usa `listen()`.  
C. Un servidor TCP usa `accept()`.  
D. Un cliente TCP usa `connect()`.

Correctas: **A, B, C y D**.

---

## **Pregunta 5**

Marca las correctas:

A. UDP normalmente usa `sendto()` y `recvfrom()`.  
B. UDP necesita `accept()` para aceptar conexiones.  
C. TCP es un flujo de bytes.  
D. UDP trabaja con datagramas independientes.

Correctas: **A, C y D**.