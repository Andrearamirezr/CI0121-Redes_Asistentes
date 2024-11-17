# Solución de la tarea 6

Primero se necesitan organizar los rangos:

- B: 127 + 2 = **129**
- E: 63 + 2 = **65**
- C: 30 + 2 = **32**
- A: 16 + 2 = **18**
- D: 15 + 2 = **17**
- F: 7 + 2 = **9**

Se comienzan a asignar las IPs apartir de los rangos más pequeños, tomando en cuenta que la red asisgnada es `192.168.24.0`:

| Rango |        Red        |   Dirección    |   Broadcast    |           Asignables            | Total |
| :---: | :---------------: | :------------: | :------------: | :-----------------------------: | :---: |
|   F   |  192.168.24.0/28  |  192.168.24.0  | 192.168.24.15  |  192.168.24.1 - 192.168.24.15   |  16   |
|   D   | 192.168.24.16/27  | 192.168.24.16  | 192.168.24.47  |  192.168.24.17 - 192.168.24.46  |  32   |
|   A   | 192.168.24.48/27  | 192.168.24.48  | 192.168.24.79  |  192.168.24.49 - 192.168.24.78  |  32   |
|   C   | 192.168.24.80/27  | 192.168.24.80  | 192.168.24.111 | 192.168.24.81 - 192.168.24.110  |  32   |
|   E   | 192.168.24.112/25 | 192.168.24.112 | 192.168.24.239 | 192.168.24.113 - 192.168.24.238 |  128  |
|   B   | 192.168.24.240/24 |      ---       |      ---       |               ---               |  ---  |

Hay que tomar en cuenta que apesar de que se solicitan en total 255 IPs, para el rango 'B' no quedan suficientes IPs esto porque una red solo se puede subdividir con una máscara que sea $2^n$. Además de que cada rango de red tiene su `dirección` y su `broadcast`.
