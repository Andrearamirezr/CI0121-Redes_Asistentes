# Solución de la tarea 12

### Parte 1

La capacidad de la red es 1Mbps, el host A transmite $100 bytes \times 8bits/1 byte = 800 bits$ por lo tanto el trhoughput del host A seria:

$$
800 bits \times \frac{1}{0.001s} = 800.000 bps = 800 kbps
$$

Por lo tanto el host A tien mayor throughput.

### Parte 2

Both UDP and TCP use port numbers to identify the destination entity when delivering a message. Give two reasons why these protocols invented a new abstract ID (port numbers), instkkjead of using process IDs, which already existed when these protocols were designed.

1. Permite independencia entre el protocolo y el sistema operativo
2. Permite multiples conecciónes con currentes, varios PIDs pueden usar el mismo puerto.
