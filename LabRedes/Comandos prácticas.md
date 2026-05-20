### **Práctica 1 – Manejo básico de routers y switches**

**Objetivos:** Acceso a consola, configuración básica, asignación IP y reset de dispositivos.

**Router MikroTik (RouterOS)**

- Acceso consola: `screen /dev/ttyUSB0 115200`
- Reset de fábrica: `system reset-configuration no-defaults=yes keep-users=no`
- Asignar IP a interfaz: `ip address add address=<IP>/<mask> interface=<interfaz>`
- Añadir rutas estáticas:  
    `ip route add dst-address=<red> gateway=<gateway>`  
    `ip route add gateway=<gateway>` (default route)
- Hostname: `system identity set name=<nombre>`
- Comandos útiles: `ip route print`, `interface print` 

**Switch TP-Link**

- Consola: `screen /dev/ttyUSB0 38400` (usuario `admin`)
- Reset: `reset`
- Modo privilegiado: `enable` → `configure`
- Guardar configuración: `copy running-config startup-config`
- Configuración VLAN de gestión:
```shell
interface vlan 1      # Selecciona la interfaz VLAN 1 para configurarla
ip address <IP> <mask>  # Asigna la dirección IP y máscara de red a esa VLAN
```
- Mostrar estado interfaces: `show interface status`

---

### **Práctica 2 – VLANs y enrutamiento entre VLANs**

**Conceptos:**

- Puertos de acceso: tramas no etiquetadas, asignados a una VLAN
- Puertos troncales: tramas etiquetadas para varias VLANs, VLAN nativa no etiquetada
- Puertos generales: combinan acceso y troncal, configurable PVID

**Comandos Switch (TP-Link)**

- Crear VLAN:
```shell
vlan <id>              # Crear VLAN
name <nombre>          # Asignar nombre a VLAN
```

- Asignar puerto acceso:
```shell
switchport mode access  # Configura puerto como acceso
switchport access vlan <id>  # Asocia puerto a VLAN
switchport mode trunk    # Configura puerto como troncal
no shutdown
```

- Asignar puerto troncal:
```shell
interface Gi1/0/<puerto>        # Selecciona el puerto del switch para configurar
switchport mode trunk           # Configura el puerto como troncal (varias VLANs)
switchport trunk allowed vlan <lista>  # Permite únicamente las VLANs listadas
switchport pvid <id>            # Define la VLAN nativa (sin etiquetar)
no shutdown                     # Activa el puerto si estaba apagado
```

- Configuración PVID y VLAN general:
```shell
interface Gi1/0/<puerto>     # Selecciona el puerto del switch a configurar
switchport general allowed vlan <lista> tagged/untagged  # Define qué VLANs se permiten y si salen etiquetadas o no
switchport pvid <id>.  # Establece la VLAN por defecto para tramas no etiquetadas
```

- Ver configuración VLAN: `show vlan`

- Configurar interfaces virtuales en router para inter-VLAN routing:
```shell
interface vlan add interface=ether1 name=ether1.10 vlan-id=10  # Crea subinterfaz VLAN 10 sobre ether1
ip address add address=<IP>/<mask> interface=ether1.10  # Asigna IP a la subinterfaz VLAN 10
```

---

### **Práctica 3 – Spanning Tree (STP/RSTP/MSTP)**

**Objetivos:** Evitar bucles, configurar árbol raíz, activar variantes de STP.

**Conceptos:**

- BID = Bridge Identifier (Prioridad + MAC)
- Roles puertos: Root Port, Designated Port, Alternate Port, Backup Port
- Estados enlaces: Fwd (activo), Blk (bloqueado)

**Comandos Switch:**

- STP:
```shell
spanning-tree                   # Activa el protocolo STP en el switch
spanning-tree mode stp          # Configura STP en modo estándar
interface range gi 1/0/1-4      # Selecciona un rango de puertos físicos
spanning-tree                   # Aplica STP a los puertos seleccionados
show spanning-tree active       # Muestra el estado activo del árbol STP
show spanning-tree interface    # Muestra el estado STP por puerto
spanning-tree priority <valor>  # Establece prioridad para forzar switch raíz
```

- RSTP: `spanning-tree mode rstp`

- MSTP:
```shell
spanning-tree mode mstp                 # Activa MSTP en el switch
spanning-tree mst configuration         # Entra en modo configuración MSTP
name <nombre-region>                     # Asigna un nombre a la región MSTP
revision <numero>                        # Número de revisión de la                                                         configuración MSTP
instance 1 vlan <id>                     # Asocia VLAN <id> a la instancia 1
instance 2 vlan <id1,id2>                # Asocia VLAN <id1,id2> a la instancia 2
spanning-tree mst instance 2 priority <valor>  # Establece prioridad para raíz MSTP instancia 2
show spanning-tree mst instance 2       # Muestra el estado de la instancia MSTP 2
```

---

### **Práctica 4 – OSPF (IGP)**

**Conceptos:**

- Estado de enlace, costo por interfaz, cálculo rutas Dijkstra
- Tipos de routers: Interno, DR, ABR, ASBR
- Tipos de áreas: Standard, Stub, Totally Stub, NSSA

**Comandos MikroTik:**

- Crear interfaces de loopback: `interface bridge add name=lo0`
- Activar OSPF:
```shell
routing ospf instance add name=default           # Crea una instancia OSPF llamada 'default'
routing ospf area add name=area1 area-id=<id>   # Crea un área OSPF con ID <id>
routing ospf network add network=<red>/<mask> area=<area>  # Asocia la red al área OSPF especificada
```

- Comprobar:  `routing ospf route print`, `routing ospf neighbor print`
- Sumarización: `routing ospf area range add area=<area> range=<red>`

---
### **Práctica 5 – Redistribución de rutas y VRRP**

**Redistribución:**

- Distancia administrativa (DA) para compatibilidad entre protocolos
- Comandos FRR RIP/OSPF:
```shell
router rip                      # Activa el protocolo RIP
redistribute ospf metric 1      # Redistribuye rutas OSPF en RIP con métrica 1
router ospf                     # Activa el protocolo OSPF
area 1 stub                     # Configura el área 1 como stub (ruta por defecto hacia ABR)
area 2 nssa no-summary           # Configura el área 2 como NSSA sin resumen
area 1 range 10.1.0.0/23         # Sumariza las redes del área 1
```

**VRRP:**

- Crear interfaz virtual y asignar IP:
```shell
interface vrrp add interface=ether1 vrid=51    # Crea una interfaz virtual VRRP sobre ether1 con ID 51
interface vrrp set vrrp1 priority=150         # Asigna prioridad 150 para que este router sea maestro preferente
interface vrrp print detail                    # Muestra detalles y estado de la interfaz VRRP
```

- Probar redundancia desconectando maestro

---

### **Práctica 6 – BGP (EGP)**

- Tipos de AS: stub, tránsito, multihomed
- Mensajes BGP: OPEN, UPDATE, KEEPALIVE, NOTIFICATIONS
- Comandos FRR:
```shell
router bgp <AS>                       # Activa BGP en el router con número de AS <AS>
neighbor <IP> remote-as <AS>          # Define un vecino BGP con su AS remoto
neighbor <IP> next-hop-self           # Establece que este router será el NEXT-HOP para rutas anunciadas
network <prefix>                      # Anuncia un prefijo de red a BGP
aggregate-address <red> summary-only  # Crea un prefijo agregado/resumen
show bgp neighbors                     # Muestra información de los vecinos BGP
show bgp ipv4 unicast                  # Muestra la tabla de rutas BGP IPv4
clear ip bgp * soft                    # Reinicia la sesión BGP suavemente para aplicar cambios
```

- Política de tráfico: `route-map <nombre> permit <num>` + `set local-preference <valor>`

---

### **Práctica 7 – DHCP y DNS**

**DHCP**

- Configurar pool:
```shell
subnet <red> netmask <mask> {          # Define la subred para DHCP
    range <IP start> <IP end>;          # Rango de IPs asignables a clientes
    option routers <gateway>;           # Puerta de enlace por defecto para la   subred
    option broadcast-address <broadcast>; # Dirección de broadcast de la subred
}
```

- DHCP relay:
```shell
ip dhcp-relay add name=<nombre> dhcp-server=<IP> interface=<interfaz> local-address=<IP>  # Configura un agente DHCP relay que reenvía solicitudes a un servidor remoto
```

**DNS**

- Zonas directas e inversas:
```shell
zone "redes.local" { type master; file "/etc/bind/db.redes.local"; };        # Define la zona directa del dominio como master y asigna el archivo de configuración
zone "0.2.10.in-addr.arpa" { type master; file "/etc/bind/db.0.2.10"; };     # Define la zona inversa para resolución IP a nombre, como master
```

- Comandos útiles:  
```shell
systemctl restart isc-dhcp-server       # Reinicia el servicio DHCP en el servidor
journalctl -u isc-dhcp-server -f       # Muestra en tiempo real los logs del servicio DHCP
dig ns1.redes.local                     # Consulta DNS directa del servidor ns1.redes.local
dig -x <IP>                             # Consulta DNS inversa para la dirección IP indicada
```

---

### **Práctica 8 – Firewall y NAT**

**Firewall RouterOS**

- Cadenas por defecto: input, forward, output
- Regla = patrón + acción (accept/drop/jump)
- Ejemplo reglas:
```shell
add chain=forward src-address=127.0.0.0/8 action=drop           # Bloquea todo tráfico con origen loopback
add chain=forward action=accept                                  # Permite todo el resto del tráfico
add chain=forward protocol=tcp connection-state=invalid action=drop  # Bloquea paquetes TCP con estado de conexión inválido
add chain=forward connection-state=established action=accept        # Permite paquetes de conexiones ya establecidas
add chain=forward connection-state=related action=accept            # Permite paquetes relacionados con conexiones existentes
```

- Crear cadena personalizada: 
`add chain=trafico_tcp protocol=tcp dst-port=69 action=drop`
- Saltos: 
`jump jump-target=<cadena>`

**NAT**

- Tipos: one-to-one, many-to-many, many-to-one (PAT)
- Sentido: source NAT (salida), destination NAT (entrada)

---

## Chuletario Laboratorio de Redes - Tabla de referencia rápida

| Práctica                  | Dispositivo / Sección   | Comandos Clave                                                                                                                                                                                                                                                                                             | Notas / Configuración                                                                                | Topología / VLANs                                                          |
| ------------------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| 1 - Manejo básico         | Router MikroTik         | `system reset-configuration`, `ip address add <IP>/<mask> interface=<int>`, `ip route add dst-address=<red> gateway=<gateway>`, `system identity set name=<nombre>`                                                                                                                                        | Asignar IP, hostname, rutas estáticas. Persistencia automática                                       | N/A (pruebas básicas)                                                      |
| 1 - Manejo básico         | Switch TP-Link          | `reset`, `enable`, `configure`, `copy running-config startup-config`, `interface vlan 1`, `ip address <IP> <mask>`, `show interface status`                                                                                                                                                                | VLAN de gestión y control de interfaces                                                              | N/A                                                                        |
| 2 - VLANs                 | Switch TP-Link          | `vlan <id>`, `name <nombre>`, `switchport mode access/trunk/general`, `switchport access vlan <id>`, `switchport trunk allowed vlan <lista>`, `switchport pvid <id>`                                                                                                                                       | Configurar PVID, puertos de acceso/troncal/general                                                   | VLAN 10,20,30,99; Troncales etiquetadas; acceso VLAN                       |
| 2 - VLANs                 | Router MikroTik         | `interface vlan add interface=ether1 name=ether1.<id> vlan-id=<id>`, `ip address add address=<IP>/<mask> interface=ether1.<id>`                                                                                                                                                                            | Subinterfaces para inter-VLAN routing                                                                | IP asignadas según VLANs, subredes diferenciadas                           |
| 3 - Spanning Tree         | Switch TP-Link          | `spanning-tree`, `spanning-tree mode stp/rstp/mstp`, `interface range gi 1/0/1-4`, `spanning-tree priority <valor>`, `show spanning-tree active/interface`, MSTP `spanning-tree mst configuration`                                                                                                         | Forzar raíz, verificar estado puertos y roles                                                        | Red con enlaces redundantes, Core/Distribución/Acceso                      |
| 4 - OSPF                  | Router MikroTik         | `interface bridge add name=lo0`, `routing ospf instance add name=default`, `routing ospf area add name=<area> area-id=<id>`, `routing ospf network add network=<red>/<mask> area=<area>`, `routing ospf route print`, `routing ospf neighbor print`, `routing ospf area range add area=<area> range=<red>` | Configurar loopback, OSPF en áreas, sumarización                                                     | Área 0 y áreas de prueba según topología                                   |
| 5 - Redistribución y VRRP | Router FRR              | `router rip`, `redistribute ospf metric 1`, `router ospf`, `area <n> stub/nssa no-summary`, `area <n> range <red>`                                                                                                                                                                                         | Redistribución entre protocolos con Distancia Administrativa                                         | Red multi-área con RIP/OSPF                                                |
| 5 - VRRP                  | Router MikroTik         | `interface vrrp add interface=<int> vrid=<id>`, `interface vrrp set vrrp1 priority=<valor>`, `interface vrrp print detail`                                                                                                                                                                                 | Redundancia primer salto, asignación IP virtual, maestro/backup                                      | LAN redundante, IP virtual para gateway                                    |
| 6 - BGP                   | Router FRR              | `router bgp <AS>`, `neighbor <IP> remote-as <AS>`, `neighbor <IP> next-hop-self`, `network <prefix>`, `aggregate-address <red> summary-only`, `show bgp neighbors`, `show bgp ipv4 unicast`, `clear ip bgp * soft`, `route-map`                                                                            | iBGP/eBGP, política de tráfico, tuneles GRE, distribución rutas                                      | AS multihomed, redundancia hacia Internet, NAT interna                     |
| 7 - DHCP / DNS            | Servidor Linux / Router | DHCP: pool con `subnet <red> netmask <mask> { range <IPstart> <IPend>; option routers <IP>; option broadcast-address <IP>; }`, `ip dhcp-relay add name=<nombre> dhcp-server=<IP> interface=<int> local-address=<IP>`. DNS: zonas directas/inversas en BIND                                                 | Configuración DHCP relay, registros DNS, forwarders                                                  | Red interna y subredes VLAN según topología, PCs y servidores configurados |
| 8 - Firewall / NAT        | Router MikroTik         | Firewall: `add chain=<chain> src-address=<IP> dst-port=<port> protocol=<proto> action=<accept/drop/jump>`, `print chain=<chain>`, `move <pos>`; NAT: `one-to-one`, `many-to-one`, `many-to-many`                                                                                                           | Reglas basadas en estado de conexión y direcciones IP, crear cadenas personalizadas, NAT source/dest | Acceso controlado desde/ hacia Internet, DMZ, redes internas               |