# Solución Quiz 2

### El esquema de comunicación Bluetooth pertenece a la famila de protocolos:

Polling (slave y master)

### Escriba una ventaja de un protocolo de _canalización_

1. No hay colisiones.
2. Es justo.

### Si tenemos la siguiente dirección IPv4 $c_3$ $c_4$.194.188.97/16, donde $c_1$ $c_2$ $c_3$ $c_4$ $c_5$ $c_6$ representa su número de carnet (si el carnet fuera A12345, el número sería 23), indique lo [siguiente:](siguiente:.md)

Asumiendo el carnet de ejemplo:

**Dirección IP de la red:** 23.194.0.0
**Dirección IP para el primer host:** 23.194.0.1
**Dirección IP para el último host:** 23.194.255.254
**Dirección IP para el broadcast:** 23.194.255.255

### Tenemos las siguientes solicitudes:

- Rango A 64 direcciones utilizables
- Rango B 30 direcciones utilizables
- Rango C 32 direcciones utilizables

### Si nos dan la siguiente dirección IPv4 base 192.168.64.0 indique como quedarían las asignaciones de cada rango, debe escribir dirección IPv4 y máscara.

| Rango |    Red (CIDR)     |   Dirección    |   Broadcast    |            IPs Asignables            | IPs Totales |
| :---: | :---------------: | :------------: | :------------: | :----------------------------------: | :---------: |
|   A   |  192.168.64.0/25  |  192.168.64.0  | 192.168.64.127 | 192.168.64.1 - 192.168.64.126 (126)  |     128     |
|   B   | 192.168.64.128/27 | 192.168.64.128 | 192.168.64.159 | 192.168.64.129 - 192.168.64.158 (30) |     32      |
|   C   | 192.168.64.160/26 | 192.168.64.160 | 192.168.64.223 | 192.168.64.161 - 192.168.64.222 (62) |     64      |

Recordar que la dirección y el broadcast no son direcciones utilizables.
