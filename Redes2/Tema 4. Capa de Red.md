## **1. Función de la capa de red**

La capa de red se encarga de llevar paquetes desde un host origen hasta un host destino, aunque estén en redes diferentes.

Su unidad de datos es el paquete o datagrama IP.

Diferencia importante:

- Capa de enlace: comunica nodos vecinos usando tramas.
- Capa de red: comunica hosts de redes distintas usando paquetes.

## **2. Router**

Un router trabaja principalmente en capa 3.

Su función es reenviar paquetes entre redes distintas.

Para decidir por dónde enviar un paquete, mira la dirección IP destino y consulta su tabla de encaminamiento.

Ideas clave:

- Switch: capa 2, usa direcciones MAC.
- Router: capa 3, usa direcciones IP.
- Las MAC cambian salto a salto.
- Las IP origen y destino se mantienen de extremo a extremo, salvo casos como NAT.

## **3. Forwarding y routing**

Forwarding significa reenviar un paquete usando una tabla.

Routing significa calcular o aprender las rutas que forman esa tabla.

Diferencia clave:

- Forwarding: acción local del router, paquete a paquete.
- Routing: proceso de cálculo de rutas.

## **4. IP y servicio best effort**

IP ofrece un servicio best effort.

Esto significa que IP intenta entregar los paquetes, pero no garantiza:

- entrega,
- orden,
- ausencia de duplicados,
- retardo máximo,
- ancho de banda.

Si se necesita fiabilidad, normalmente la aporta TCP en la capa de transporte.

## **5. Datagrama IP**

Un datagrama IP contiene cabecera y datos.

Campos importantes:

- IP origen: dirección del emisor.
- IP destino: dirección del receptor.
- TTL: evita que un paquete circule indefinidamente.
- Protocolo: indica si dentro va TCP, UDP, ICMP, etc.

El TTL disminuye en cada router.  
Si llega a 0, el paquete se descarta.

## **6. Direccionamiento IPv4**

Una dirección IPv4 tiene 32 bits.

Se escribe con cuatro octetos en decimal, por ejemplo:

192.168.1.10

La máscara indica qué parte de la IP pertenece a la red y qué parte pertenece al host.

Ejemplo:

192.168.1.10/24

Significa:

- 24 bits para red.
- 8 bits para host.

Esto lo estudiaremos aparte porque será la parte práctica del examen.

## **7. Dirección de red, broadcast y hosts**

En una red IPv4:

La dirección de red identifica la red.  
No se asigna a un equipo.

La dirección de broadcast sirve para enviar a todos los hosts de la red.  
Tampoco se asigna a un equipo.

Los hosts válidos van desde:

- red + 1,
- hasta broadcast - 1.

Número de hosts útiles:

2^h - 2

donde h es el número de bits de host.

## **8. Direcciones privadas**

Los rangos privados más importantes son:

- 10.0.0.0/8
- 172.16.0.0/12
- 192.168.0.0/16

Estas direcciones se usan en redes privadas y no se enrutan directamente por Internet.

Para salir a Internet normalmente se usa NAT.

## **9. NAT**

NAT significa Network Address Translation.

Sirve para traducir direcciones IP.

Uso típico:

- dentro de la red se usan IPs privadas,
- al salir a Internet se usa una IP pública,
- el router cambia la IP privada por la IP pública.

Con PAT o NAPT también se traducen puertos.

Esto permite que muchos dispositivos compartan una sola IP pública.

Ventaja:

- ahorra direcciones IPv4 públicas.

Inconveniente:

- dificulta conexiones entrantes directas,
- puede complicar P2P, juegos online o VoIP.

## **10. ICMP**

ICMP es un protocolo de control asociado a IP.

Sirve para mensajes de error o información.

Ejemplos:

- destino inalcanzable,
- tiempo excedido,
- echo request,
- echo reply.

Herramientas relacionadas:

- ping usa ICMP echo request y echo reply.
- traceroute se basa en mensajes de tiempo excedido u otros mecanismos parecidos.

Importante:

ICMP no usa TCP ni UDP.  
Va directamente sobre IP.

## **11. DHCP**

DHCP permite asignar automáticamente configuración IP a un host.

Puede entregar:

- dirección IP,
- máscara,
- puerta de enlace,
- servidor DNS.

Usa UDP.

Secuencia típica:

DORA:

1. Discover.
2. Offer.
3. Request.
4. ACK.

## **12. Protocolos de routing**

RIP:

- protocolo interior,
- vector de distancia,
- métrica: número de saltos,
- máximo 15 saltos,
- 16 se considera infinito,
- simple pero poco escalable.

OSPF:

- protocolo interior,
- estado de enlace,
- usa Dijkstra,
- calcula caminos de menor coste,
- más escalable que RIP.

BGP:

- protocolo exterior,
- usado entre sistemas autónomos,
- basado en políticas,
- usa TCP puerto 179,
- no elige simplemente el camino más corto.

Tipos de BGP:

- eBGP: entre sistemas autónomos distintos.
- iBGP: dentro del mismo sistema autónomo.

## **13. Congestión**

Hay congestión cuando la red recibe más tráfico del que puede manejar.

Consecuencias:

- aumentan las colas,
- aumenta el retardo,
- se pierden paquetes,
- baja el rendimiento efectivo.

## **14. QoS**

QoS significa Quality of Service.

Busca ofrecer cierta calidad o prioridad a algunos tipos de tráfico.

Parámetros importantes:

- ancho de banda,
- retardo,
- jitter,
- pérdida de paquetes.

El jitter es la variación del retardo.

Es importante en:

- VoIP,
- videollamadas,
- streaming en directo,
- juegos online.

## **15. Lo importante de verdad**

Para este tema, lo más importante es:

- Router = capa 3.
- Forwarding no es lo mismo que routing.
- IP es best effort.
- TTL evita bucles infinitos.
- IPv4 tiene 32 bits.
- La máscara separa parte de red y parte de host.
- Dirección de red y broadcast no se asignan a hosts.
- Hosts útiles = 2^h - 2.
- Rangos privados: 10/8, 172.16/12 y 192.168/16.
- NAT traduce direcciones privadas a públicas.
- ICMP no usa TCP ni UDP.
- DHCP usa UDP y sigue DORA.
- RIP = vector distancia.
- OSPF = estado de enlace.
- BGP = entre sistemas autónomos, usa TCP 179.
- QoS se relaciona con retardo, jitter, ancho de banda y pérdidas.

## **16. Trampas típicas**

IP garantiza entrega fiable.

Falso. IP es best effort.

Forwarding y routing son lo mismo.

Falso. Forwarding es reenviar paquetes; routing es calcular rutas.

ICMP usa TCP.

Falso. ICMP va directamente sobre IP.

DHCP usa TCP.

Falso. DHCP usa UDP.

RIP usa estado de enlace.

Falso. RIP usa vector distancia.

OSPF usa vector distancia.

Falso. OSPF usa estado de enlace.

BGP se usa para enrutar dentro de una LAN doméstica.

Falso. BGP se usa entre sistemas autónomos.

Una IP privada se enruta directamente por Internet.

Falso. Las IP privadas no se enrutan directamente por Internet.