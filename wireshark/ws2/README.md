# Solución Wireshark 2

## Ejercicio 1

Archivo: telnet.pcap

### Tarea: reconstruct the telnet session

Para poder ver mejor los datos se puede hacer click derecho en el primer paquete y darle formato a Follow TCP Stream.

1. Who logged into 192.168.0.1?
   Username: fake
   Password: user
2. After logged what the user do?
   Hizo ping a www.yahoo.com

## Ejercicio 2

Archivos: massivesyn1.pcap and massivesyn2.pcap

### Tarea: Find files differences

1. massivesyn1.pcap is a :
   Parece ser un intento de ataque SYN Flood (DDoS).
1. massivesyn2.pcap is a :
   Parece ser un ataque SYN Flood pero distribuido (DDoS).

## Ejercicio 3

Archivos: student1.pcap and student2.pcap
Scenario: You are an IT admin in UCR, you had reported that student1 (a new student) cannot browse or mail with its laptop. After some research, student2, sitting next to student1, can browse with any problems.

### Tarea: compare these two capture files and state why student1’s machine is not online

Solution

1. student1 must:
   Deberia hacer la solicitud ARP a la ip `192.168.0.10` en lugar de `192.168.0.11`

## Ejercicio 4

Archivo: chat.dmp

### Tare: compare these two capture files and state why student1’s machine is not online

1. What kind of protocol is used?
   Se utliza el protocolo MSNMS
2. Who are the chatters?
   Son Tomas y Brian
3. What do they say about you (sysadmin)?
   Parece que quieren "Hacker" el servidor, para molestar.
