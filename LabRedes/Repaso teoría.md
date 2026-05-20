## **1. Redes y VLANs**

- **Dominio de colisión:** Zona donde los dispositivos compiten por transmitir datos en un mismo canal físico. Los switches eliminan colisiones usando full-duplex. Importante para diseñar VLANs y separar dominios de broadcast.
- **Dominio de broadcast:** Área donde se propagan paquetes de difusión (broadcast/multicast). VLANs permiten limitar el alcance de broadcast, aumentando rendimiento y seguridad.
- **Puertos de switch:**
    - **Acceso (access):** Conecta PCs; pertenece a una VLAN; envía tramas sin etiquetar.
    - **Troncal (trunk):** Conecta switches/routers; transporta varias VLANs usando IEEE 802.1Q; la VLAN nativa no se etiqueta.
    - **General:** Puede comportarse como troncal o acceso según reglas; configurable con PVID.
- **PVID (Port VLAN ID):** VLAN por defecto del puerto; define cómo se tratan las tramas no etiquetadas.
- **Routing entre VLANs:** Se realiza en routers con subinterfaces, cada una con IP correspondiente a la VLAN. Permite la comunicación entre VLANs separadas.

**Extra para examen:**

- Conocer diferencias entre VLAN nativa y PVID.
- Saber identificar qué puertos de un switch son access/trunk/general en una topología.

---

## **2. Enrutamiento**

### **OSPF (IGP)**

- Protocolo de estado de enlace que calcula rutas de coste mínimo usando Dijkstra.
- **Áreas OSPF:**
    - **Standard:** predeterminado; permite toda la información de rutas externas y otras áreas.
    - **Stub:** bloquea rutas externas (LSA tipo 4 y 5); inyecta ruta por defecto.
    - **Totally Stub:** bloquea rutas externas y de otras áreas; solo ruta por defecto.
    - **NSSA:** similar a Stub pero permite un ASBR interno.
- **Routers OSPF:** Interno, ABR (frontera de área), ASBR (conexión con otros AS), DR (designado), Troncal (interfaz en área 0).
- Comandos: `routing ospf instance/area/network`, `show ospf route`, `show ospf neighbor`, sumarización de rutas con `area range`.

### **BGP (EGP)**

- Gestiona rutas entre sistemas autónomos.
- **Tipos de AS:** Stub, Transit, Multihomed, IXP.
- **Mensajes:** OPEN (inicia sesión), UPDATE (anuncia prefijos), KEEPALIVE, NOTIFICATIONS.
- **Atributos:** ORIGIN, AS_PATH, NEXT-HOP, LOCAL-PREF.
- Comandos: `router bgp`, `neighbor <IP> remote-as`, `network <prefix>`, `aggregate-address`, `show bgp neighbors`.

### **RIP y redistribución**

- Redistribuye rutas entre protocolos IGP dentro del AS.
- **Distancia administrativa (DA):** Prioridad de rutas redistribuidas; más baja = más preferida.

---

## **3. STP / RSTP / MSTP - Protocolos de Arbol de Expansión**

### **Objetivo**

- Evitar **bucles L2** en redes con **enlaces redundantes**.
- Asegurar que la red funcione aunque existan caminos alternativos entre switches.
- Mantener conectividad sin inundaciones de broadcast.

### **Cómo funciona**

1. Cada switch intercambia **BPDUs (Bridge Protocol Data Units)** con sus vecinos.
2. Se calcula un **árbol de expansión** (sin bucles):
    - Se elige un **switch raíz (Root Bridge)**, con la prioridad más baja (valor numérico menor).
    - Todos los switches determinan su **Root Port** (camino al root) y **Designated Ports**.
    - Puertos alternativos se bloquean para evitar bucles.
3. El árbol se **recalcula automáticamente** ante cambios en la topología:
    - **STP (Spanning Tree Protocol):** Protocolo original que calcula un árbol de expansión evitando bucles. Convergencia lenta (~50 s).
	- **RSTP (Rapid STP):** Versión rápida de STP, reduce tiempo de parada de la red a pocos segundos.
	- **MSTP (Multiple STP):** Permite varios árboles de expansión dentro de la misma red, cada uno asociado a un grupo de VLANs, optimizando el uso de puertos y ancho de banda.

### **Roles de puertos**

- **Root Port (RP):** Puerto que apunta al switch raíz.
- **Designated Port (DP):** Puerto encargado de enviar tramas hacia la LAN.
- **Alternate / Backup:** Puertos de respaldo que se activan si falla el Designated Port.
- **Estado de puerto:**
    - **Fwd (Forwarding):** Puerto activo que envía/recibe tramas.
    - **Blk (Blocked):** Puerto bloqueado para prevenir bucles.

### **BID – Bridge Identifier**

- Compuesto por:
    - **Prioridad:** configurable, valor menor → mayor prioridad.
    - **MAC:** identifica de manera única el switch.
- Determina cuál switch será **raíz del spanning tree**.

### **STP/RSTP/MSTP**

- **STP:** estándar original, convergencia lenta (~50 s).
- **RSTP:** rápido, se ajusta a cambios inmediatos en la topología.
- **MSTP:** mantiene múltiples árboles para distintas VLANs, reduce enlaces bloqueados y mejora eficiencia.

### **Comandos típicos en Switch TP-Link**
```shell
spanning-tree                      # Activa STP en el switch
spanning-tree mode stp             # Configura STP estándar
spanning-tree mode rstp            # Activa RSTP
spanning-tree mode mstp            # Activa MSTP
spanning-tree mst configuration    # Configuración MSTP (región)
name <nombre-region>               # Nombre de la región MSTP
revision <numero>                  # Número de revisión MSTP
instance 1 vlan <id>               # Asocia VLAN a instancia MSTP 1
instance 2 vlan <id1,id2>          # Asocia VLAN a instancia MSTP 2
interface range gi 1/0/1-4         # Selecciona rango de puertos
spanning-tree                      # Aplica STP/RSTP/MSTP a los puertos
spanning-tree priority <valor>     # Forzar switch raíz
show spanning-tree active          # Estado activo del árbol
show spanning-tree interface       # Estado de los puertos
show spanning-tree mst instance 2  # Estado MSTP instancia 2
```

### **Consejos clave de examen**

- Saber **identificar el root bridge** y roles de puertos en la topología.
- Comprender cómo cambiar la **prioridad** para elegir la raíz.
- Entender diferencias entre **STP, RSTP y MSTP** y cuándo usar cada uno.
- Revisar estado de puertos: bloqueado → no envía tramas; forwarding → envía y recibe.


---

## **4. VRRP**

- **Objetivo:** Evitar que la caída de un router haga perder la conectividad de la LAN con la puerta de enlace.
- **Cómo funciona:**
    - Se define un **router virtual** con una IP que actúa como puerta de enlace para todos los hosts.
    - Varios routers físicos forman un **grupo VRRP**:
        - **Maestro:** envía anuncios periódicos indicando que está activo.
        - **Backup(s):** escuchan y toman control si el maestro falla.
- **Ventajas:**
    - Redundancia real para la puerta de enlace.
    - Evita la necesidad de cambiar manualmente la configuración de los PCs en caso de fallo.
- **Configuración básica:**
    
    - Crear interfaz VRRP:  
        `interface vrrp add interface=ether1 vrid=51` → activa VRRP sobre ether1 con ID 51.
    - Asignar prioridad al maestro:  
        `interface vrrp set vrrp1 priority=150` → mayor prioridad significa que será maestro.
    - Ver estado del grupo:  
        `interface vrrp print detail` → indica qué router es maestro y qué backups hay.
- **Conceptos clave:**
    - **VRID (Virtual Router ID):** Identificador único del router virtual.
    - **Advert interval:** Frecuencia de anuncios del maestro.
    - **Failover:** Los routers backup toman el control inmediatamente si no reciben anuncios.


---

## **5. DHCP y DNS**

### **DHCP (Dynamic Host Configuration Protocol)**

- **Objetivo:** Asignar IPs dinámicas a los hosts automáticamente.
- **Componentes:**
    - **Pool:** Rango de direcciones disponibles.
    - **Lease time:** Duración de la IP asignada.
    - **Gateway y broadcast:** Opciones que se envían al host.
- **Proceso de comunicación:**
    1. **Discover:** El host busca un servidor DHCP.
    2. **Offer:** El servidor propone una IP.
    3. **Request:** El host solicita esa IP.
    4. **ACK:** El servidor confirma la asignación.
- **DHCP Relay:** Permite que un servidor DHCP centralizado atienda redes distintas.
- **DHCP Snooping:** Función de seguridad que evita que hosts maliciosos suplanten al servidor DHCP.
- **Comandos importantes:**
```
ip dhcp-relay add name=<nombre> dhcp-server=<IP> interface=<interfaz> local-address=<IP>
```

### **DNS (Domain Name System)**

- **Objetivo:** Resolver nombres de dominio a direcciones IP y viceversa.
- **Tipos de servidores:**
    - **Root:** dirigen a TLD.
    - **TLD:** gestionan dominios .com, .org, .net.
    - **Autoritativos:** contienen registros finales de la zona.
    - **Locales:** caché, sirven a los clientes.
- **Registros más comunes:**
    - **A:** Nombre → IPv4
    - **MX:** Servidores de correo
    - **CNAME:** Alias
    - **PTR:** IP → nombre (inversa)
- **Zonas:** Definen el espacio de nombres controlado por cada servidor.
- **Comandos útiles:**
```
dig ns1.redes.local       # Consulta directa
dig -x <IP>               # Consulta inversa
systemctl restart isc-dhcp-server
journalctl -u isc-dhcp-server -f
resolvectl flush-caches
```

- **Tips de examen:**
    - Comprender la diferencia entre zona directa e inversa.
    - Saber cuándo usar relay y snooping.
    - Entender cómo verificar que DHCP/DNS funcionan correctamente.


---

## **6️⃣ Firewall y NAT (explicado más a fondo)**

### **Firewall (RouterOS)**

- Filtra paquetes según reglas y cadenas: `input`, `forward`, `output`.
- **Regla:** Patrón + acción:
    - Patrón puede ser por:
        - Direcciones IP origen/destino.
        - Puertos TCP/UDP.
        - Protocolo.
        - Interfaz de entrada/salida.
        - Estado de la conexión (`new`, `established`, `related`, `invalid`).
    - Acción: `accept`, `drop`, `jump`.
- **Orden de reglas:** Se procesan de arriba hacia abajo; si un paquete coincide con una regla, se ejecuta la acción y no continúa.
- **Cadenas personalizadas:** Permiten organizar reglas complejas; se saltan desde la cadena principal usando `jump`.
- Ejemplos típicos:
    - Bloquear IP loopback: `add chain=forward src-address=127.0.0.0/8 action=drop`.
    - Permitir tráfico establecido: `connection-state=established action=accept`.
    - Bloquear paquetes inválidos: `connection-state=invalid action=drop`.

### **NAT**

- **Objetivo:** Traducir direcciones IP y/o puertos para conectividad y seguridad.
- **Tipos:**
    - **One-to-one (static NAT):** 1 IP privada ↔ 1 IP pública.
    - **Many-to-many (dynamic NAT):** varias IP privadas ↔ varias públicas.
    - **Many-to-one (PAT):** varias IP privadas comparten 1 IP pública con puertos distintos.
- **Sentido:**
    - **Source NAT:** tráfico saliente (Internet desde LAN).
    - **Destination NAT:** tráfico entrante (publicación de servicios internos).