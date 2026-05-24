## **1. Conversión rápida CIDR ↔ máscara**

Valores importantes de un octeto de máscara:

**0 bits:** 0**1 bit:** 128**2 bits:** 192**3 bits:** 224**4 bits:** 240**5 bits:** 248**6 bits:** 252**7 bits:** 254**8 bits:** 255

Ejemplos:

- `/24` → 255.255.255.0
- `/25` → 255.255.255.128
- `/26` → 255.255.255.192
- `/27` → 255.255.255.224
- `/28` → 255.255.255.240
- `/29` → 255.255.255.248
- `/30` → 255.255.255.252

**Truco:**  
Si el prefijo no acaba justo en octeto, el octeto “raro” se saca con la lista anterior.

Ejemplo:

`/19` = 8 + 8 + 3 + 0  
Máscara: `255.255.224.0`

---

## **2. Tamaño de bloque**

El tamaño de bloque depende de cuántos bits quedan para host.

**Bits de host = 32 - prefijo**

**Tamaño de bloque = 2^(bits de host)**

**Hosts útiles = 2^(bits de host) - 2**

Ejemplos:

- `/24`: 8 bits host → bloque 256 → 254 hosts útiles.
- `/25`: 7 bits host → bloque 128 → 126 hosts útiles.
- `/26`: 6 bits host → bloque 64 → 62 hosts útiles.
- `/27`: 5 bits host → bloque 32 → 30 hosts útiles.
- `/28`: 4 bits host → bloque 16 → 14 hosts útiles.
- `/29`: 3 bits host → bloque 8 → 6 hosts útiles.
- `/30`: 2 bits host → bloque 4 → 2 hosts útiles.

---

## **3. Calcular red, broadcast y rango de hosts**

Dada una IP y máscara, el objetivo es encontrar:

- dirección de red,
- dirección de broadcast,
- primer host,
- último host,
- número de hosts útiles.

### **Método rápido**

1. Mira el prefijo.
2. Calcula el tamaño del bloque.
3. Busca en qué bloque cae la IP.
4. La primera dirección del bloque es la red.
5. La última dirección del bloque es el broadcast.
6. Los hosts van desde red + 1 hasta broadcast - 1.

### **Ejemplo**

IP: `192.168.1.70/26`

`/26` deja 6 bits de host.

Tamaño de bloque:

`2^6 = 64`

Bloques en el último octeto:

- 0–63
- 64–127
- 128–191
- 192–255

La IP `192.168.1.70` cae en el bloque `64–127`.

Resultado:

- Red: `192.168.1.64`
- Broadcast: `192.168.1.127`
- Primer host: `192.168.1.65`
- Último host: `192.168.1.126`
- Hosts útiles: `62`

---

## **4. Saber si dos IPs están en la misma subred**

Para saber si dos IPs están en la misma subred:

1. Calculas la dirección de red de la primera IP.
2. Calculas la dirección de red de la segunda IP.
3. Si la dirección de red coincide, están en la misma subred.
4. Si no coincide, no están en la misma subred.

### **Ejemplo**

IP1: `192.168.25.23/27`IP2: `192.168.25.62/27`

`/27` → bloques de 32.

Bloques:

- 0–31
- 32–63
- 64–95
- …

`23` cae en `0–31`.  
Red IP1: `192.168.25.0`

`62` cae en `32–63`.  
Red IP2: `192.168.25.32`

No coinciden.

**Resultado:** no están en la misma subred.

---

## **5. VLSM: repartir una red en subredes**

Este es el método importante del PDF.

### **Pasos**

1. Contar cuántas redes o segmentos físicos hay.
2. Para cada red, mirar cuántos hosts necesita.
3. Ordenar las redes de mayor a menor número de hosts.
4. A cada red se le suman 2 direcciones:
    - una para red,
    - una para broadcast.
5. Redondear a la potencia de 2 superior.
6. Calcular la máscara:
    - si el bloque tiene tamaño `2^h`,
    - entonces la máscara es `/32-h`.
7. Asignar los bloques desde el inicio del prefijo global.
8. Cada nueva red empieza justo después del bloque anterior.
9. Broadcast = dirección de red + tamaño de bloque - 1.

### **Ejemplo rápido**

Prefijo global: `172.16.0.0/16`

Necesidades:

- Red B: 300 hosts.
- Red A: 128 hosts.
- Red C: 35 hosts.
- Red D: 2 hosts.
- Red E: 2 hosts.

Tamaños:

- 300 + 2 = 302 → bloque 512 → `/23`
- 128 + 2 = 130 → bloque 256 → `/24`
- 35 + 2 = 37 → bloque 64 → `/26`
- 2 + 2 = 4 → bloque 4 → `/30`
- 2 + 2 = 4 → bloque 4 → `/30`

Asignación:

- Red B: `172.16.0.0/23`, broadcast `172.16.1.255`
- Red A: `172.16.2.0/24`, broadcast `172.16.2.255`
- Red C: `172.16.3.0/26`, broadcast `172.16.3.63`
- Red D: `172.16.3.64/30`, broadcast `172.16.3.67`
- Red E: `172.16.3.68/30`, broadcast `172.16.3.71`

---

## **6. Enlaces entre routers**

Un enlace punto a punto entre routers normalmente necesita 2 IPs útiles:

- una para un router,
- otra para el otro router.

Por eso se suele usar `/30`.

En `/30`:

- tamaño de bloque: 4 direcciones,
- hosts útiles: 2,
- una dirección de red,
- una dirección de broadcast.

Ejemplo:

`172.16.3.64/30`

- Red: `172.16.3.64`
- Hosts: `172.16.3.65` y `172.16.3.66`
- Broadcast: `172.16.3.67`

---

## **7. Tablas de enrutamiento**

Una tabla de enrutamiento indica por dónde mandar paquetes hacia cada red.

Cada entrada suele tener:

- red destino,
- máscara,
- interfaz de salida,
- gateway o siguiente salto.

### **Entrada directamente conectada**

Si el router tiene una interfaz dentro de esa red, no necesita gateway.

Ejemplo:

`172.16.2.0/24` por `eth1`, gateway `-`

### **Entrada indirecta**

Si para llegar a la red hay que pasar por otro router, se indica gateway.

Ejemplo:

`172.16.0.0/23` por `eth0`, gateway `172.16.3.66`

---

## **8. Cómo elegir una ruta en una tabla**

Para decidir qué entrada se aplica a una IP destino:

1. Se comprueba qué entradas coinciden con la IP destino.
2. Si coinciden varias, se elige la de prefijo más largo.
3. La ruta `0.0.0.0/0` siempre coincide.
4. Pero solo se usa si no hay otra ruta más específica.

**Idea clave:**  
Gana la ruta con el prefijo más largo.

Ejemplo:

Para destino `172.16.1.58`, si existen:

- `172.16.0.0/16`
- `172.16.1.0/24`
- `0.0.0.0/0`

Gana:

`172.16.1.0/24`

porque `/24` es más específico que `/16` y `/0`.

---

## **9. Ruta por defecto**

La ruta por defecto es:

`0.0.0.0/0`

Se usa cuando no hay ninguna ruta más específica.

Normalmente apunta hacia:

- el router de salida,
- Internet,
- la red principal.

---

## **10. Errores típicos**

**Error 1:** olvidar sumar 2 direcciones al calcular VLSM.  
Siempre se suma red + broadcast.

**Error 2:** asignar la dirección de red a un host.  
No se puede.

**Error 3:** asignar el broadcast a un host.  
No se puede.

**Error 4:** no ordenar las redes de mayor a menor en VLSM.  
Hay que empezar por las más grandes.

**Error 5:** usar `/24` para todo.  
VLSM ajusta el tamaño según los hosts necesarios.

**Error 6:** olvidar los enlaces entre routers.  
Cada enlace entre routers también es una red.

**Error 7:** elegir mal en la tabla de rutas.  
Siempre gana el prefijo más largo.

**Error 8:** pensar que la ruta por defecto gana siempre.  
Falso. Solo gana si no hay otra más específica.

---

## **11. Chuleta mínima para examen**

- IPv4 tiene 32 bits.
- CIDR `/n`: n bits de red.
- Bits de host = `32 - n`.
- Tamaño de bloque = `2^h`.
- Hosts útiles = `2^h - 2`.
- Red = primera dirección del bloque.
- Broadcast = última dirección del bloque.
- Primer host = red + 1.
- Último host = broadcast - 1.
- VLSM: ordenar redes de mayor a menor.
- Para VLSM: hosts + 2, redondear a potencia de 2.
- Máscara = `/32 - bits_host`.
- Enlaces punto a punto: normalmente `/30`.
- En tablas de rutas gana el prefijo más largo.
- Ruta por defecto = `0.0.0.0/0`.