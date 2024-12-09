# Solución de la tarea 6

Primero se necesitan organizar los rangos, agregando `dirección` y `broadcast` a los rangos:

- B: 127 + 2 = **129**
- E: 63 + 2 = **65**
- C: 30 + 2 = **32**
- A: 16 + 2 = **18**
- D: 15 + 2 = **17**
- F: 7 + 2 = **9**

Como las IPs de una red solo se puede subdividir con una máscara que sea $2^n$. Se justan los rangos a valores validos que incluyan la `dirección`, su `broadcast` y las IPs asignables.

- B: 129 -> **256**
- E: 65 -> **128**
- C: 32 -> **32**
- A: 18 -> **32**
- D: 17 -> **32**
- F: 9 -> **16**

Se comienzan a asignar las IPs apartir de los rangos más pequeños, tomando en cuenta que la red asisgnada es `192.168.24.0`:

| Rango |    Red (CIDR)     |   Dirección    |   Broadcast    |           Asignables            | Total |
| :---: | :---------------: | :------------: | :------------: | :-----------------------------: | :---: |
|   B   |  192.168.24.0/24  |  192.168.24.0  | 192.168.24.255 |  192.168.24.1 - 192.168.24.254  |  256  |
|   E   |  192.168.25.0/25  |  192.168.25.0  | 192.168.25.127 |  192.168.25.1 - 192.168.25.126  |  128  |
|   C   | 192.168.25.128/27 | 192.168.25.128 | 192.168.25.159 | 192.168.25.129 - 192.168.25.158 |  32   |
|   A   | 192.168.25.160/27 | 192.168.25.160 | 192.168.25.191 | 192.168.25.161 - 192.168.25.190 |  32   |
|   D   | 192.168.25.192/27 | 192.168.25.192 | 192.168.25.223 | 192.168.25.193 - 192.168.25.222 |  32   |
|   F   | 192.168.25.224/28 | 192.168.25.224 | 192.168.25.240 | 192.168.25.225 - 192.168.25.239 |  16   |
