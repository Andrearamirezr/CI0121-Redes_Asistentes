## Indice

- [BGP](#bgp)
- [TCP-UDP](#tcp-udp)
- [QoS](#qos)

# Solución Packet Tracer 5

## BGP

Para solucionar este ejercicio se deben correr el siguiente script en el router ACME1:

```sh
router bgp 65001
 neighbor 1.1.1.1 remote-as 65003
 network 192.168.0.0 mask 255.255.255.0
```

Y este en el router OtherCo1:

```sh
router bgp 65002
 neighbor 1.1.1.9 remote-as 65003
 network 172.16.10.0 mask 255.255.255.0
```

# Solución Packet Tracer 6

## TCP-UDP

Solo se deben realizar los pasos y resolver las preguntas:

#### 1. What is this called? A variety of PDUs appears in the event list in the Simulation Panel. What is the meaning of the different colors?

Ya que solo un paquete puede viajar a la vez por el calble de red, a esto se le llama **multiplexion de conversación**. Y los diferentes colores de los PDU es porque **representan diferentes protocolos**.

### TCP y UDP

#### A. Why did it take so long for the HTTP PDU to appear?

En la simulación de entrar a una página web, se tarda bastante en ver el HTTTP PDU por que primero se necesita establecer la conexión TCP.

#### B. What is the section labeled? Are these communications considered to be reliable? Record the SRC PORT, DEST PORT, SEQUENCE NUM, and ACK NUM values.

La sección del PDU está etiquetada como **TCP**, y en efecto son conexiones confiables, el SRC PORT: 1026 pero puede variar segun la simulación, el DST PORT: 80, SEQ NUM: 1 y ACK NUM: 1.

#### C. Which TCP flags are set in this PDU?

Los flags que hay el PDU son: **ACK** y **PSH**.

#### D. How are the port and sequence numbers different than before?

La diferencia que hay entre el Inbound y el Outbound es los puertos están invertidos, y el SEQ NUM es 1.

#### E. What information is now listed in the TCP section? How are the port and sequence numbers different from the previous two PDUs?

El paquete que el MultiServer prepara para enviar inverte los puertos, cambia el ACK y activa los flags PSH y ACK.

### FTP

#### A. Are these communications considered to be reliable? Record the SRC PORT, DEST PORT, SEQUENCE NUM, and ACK NUM values. What is the value in the flag field?

Esta comunicación es confiable y el SRC PORT: 1027 y el DST PORT: 21, y se activa el flag SYN. El ACK y el SEQ son 0.

#### B. How are the port and sequence numbers different than before?

Ahora los puertos se invierten, y el ACK esta en 1. Adeás se activan los flags SYN y ACK.

#### C. What is the message from the server?

El mensaje del servidor FTP es "Welcome to PT Ftp server".

### DNS

#### A. What is the Layer 4 protocol? Are these communications considered to be reliable?

El protocolo es UDP, por lo que la comounication es no confiable.

#### B. Record the SRC PORT and DEST PORT values. Why are there no sequence and acknowledgement numbers?

El puerto origen es 1026, pero puede cambiar. El de destino es 53, y no hay nigun ACK o SEQ porque UDP no estable conexiones de manera confiable.

#### C. How are the port and sequence numbers different than before?

Los puesrtos estan invertidos.

#### D. What is the last section of the PDU called? What is the IP address for the name multiserver.pt.ptu?

Se llama "DNS ANSWER" y la IP al dominio es `192.168.1.254`

### Email

#### A. What transport layer protocol does email traffic use? Are these communications considered to be reliable?

Usa el protocolo TCP por lo tanto es confiable.

#### B. Record the SRC PORT, DEST PORT, SEQUENCE NUM, and ACK NUM values. What is the flag field value?

El puerto origen es 1027 (puede cambiar), el de destino es 25 y el ACK y SEQ son 0. Activa el flag SYN.

#### C. How are the port and sequence numbers different than before?

Los puerto se invierten y el ACK es 1. Además activa el flag SYN y ACK.

#### D. How are the port and sequence numbers different from the previous two results?

Los puertos se vuelve a invertir y el ACK y SEQ es 1. Además de activar el flag ACK.

#### E. How are the port and sequence numbers different from the previous two PDUs?

Tiene puerto de origen 1027 y de destino 25, ACK y SEQ son 1, y el flag ACK y PSH.

#### F. What email protocol is associated with TCP port 25? What protocol is associated with TCP port 110?

Se asocia con SMTP y el protocolo POP3

# Solución Packet Tracer 7

## QoS

Primero se configura el router ECCIR:

```sh
enable
config terminal
interface g0/0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
interface g0/0/1
ip address 192.168.1.1 255.255.255.0
no shutdown
end
```

Luego se configuran las IPs para las PCs:

| Nombre | IP          | Subnet Mask   | Gateway     |
| ------ | ----------- | ------------- | ----------- |
| PC1    | 192.168.1.5 | 255.255.255.0 | 192.168.1.1 |
| PC2    | 192.168.1.6 | 255.255.255.0 | 192.168.1.1 |
| PC3    | 192.168.2.5 | 255.255.255.0 | 192.168.2.1 |

Hay que asegurarse de activar las interfaces.

Ahora se hace un configuración ECCIR para crear una clasificación de tráfico:

```sh
enable
config terminal
ip access-list extended WWW_BROWSING_ACL
permit tcp any any eq 80
class-map WWW_BROWSING_CLASS
match access-group name WWW_BROWSING_ACL
policy-map CLASSIFY_WWW
class WWW_BROWSING_CLASS
interface GigabitEthernet0/0/1
service-policy input CLASSIFY_WWW
end
```

#### How many packets show up in www class?

Con esa configuración se puede ver que para WWW hay 0 paquetes.

#### How many packets show up in www class?

Si se genera trafico con PC2 entonces ahroa hay 2 paquetes.

Se configura ahora un clasiicación más alta al trafico de PC2 que los de PC1:

```sh
enable
config terminal
access-list 110 permit ip host 192.168.1.6 any
class-map match-all IMPORTANT
match access-group 110
policy-map SETDSCP
class IMPORTANT
set ip dscp ef
interface g0/0/1
service-policy input SETDSCP
end
```

Pued ser necesrio reiniciar la politica anterior:

```sh
configure terminal
interface g0/0/1
no service-policy input CLASSIFY_WWW
exit
end
```

#### How many packets are marked with dscp ef?

Aparecen por el momento 0 paquetes.

#### Did the number of packets marked "ef" increase?

Al hacer ping de PC1 a PC3(192.168.2.5)

#### Now run the command `show policy-map interface g0/0/1`. Did the number of packets marked "ef" increase?:w

Al hacer ping de PC2 a PC3(192.168.2.5), ahora aperecen 4 paquetes marcados como ef.
