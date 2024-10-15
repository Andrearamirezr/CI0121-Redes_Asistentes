# Solución Wireshark 1

## Ejercicio 1

### A. What is the IP address of the client that initiates the conversation?

La IP del cliente es `131.247.95.216`

### B. Use the first two packets to identify the server that is going to be contacted. List the common name, and three IP addresses that can be used for the server.

El servidor es `www.google.com`, y las IPs que se dan como respuesta son:

- `64.233.161.99`
- `64.233.161.104`
- `64.233.161.147`

### C. What is happening in frames 3, 4, and 5?

Estos 3 frames son el **three-way handshake**, que se utiliza el protocolo TCP.

### D. What is happening in frames 6 and 7?

El cliente (`131.247.95.216`) envia una solicitud **get** al servidor (`www.google.com`) para obtener el contenido de la página web. El servidor responde con un **ack** para confirmar que recibió la solicitud.

### E. Ignore frame eight. However, for your information, frame eight is used to manage flow control.

No es necesario responder, pero básicamente el servidor esta informando que ha cambiado el tamaño de la ventana de 16384 a 6432.

### F. What is happening in frames nine and ten? How are these two frames related?

El frame 9 esta respondiendo a la solicitud en el frame 6 y en el frame 10 está confirmando que se envio correctamente la respuesta.

### G. What happens in packet 11?

Este paquete es la confirmación del cliente de recibir el paquete del frame 9 correctamente.

### H. After the initial set of packets is received, the client sends out a new request in packet 12. This occurs automatically without any action by the user. Why does this occur? See the first “hint” to the left.

El archivo HTML solicitado, tiene una imagen incluida, por lo que se produce otro **hit** haciendo la solicitud de la imagen al servidor. Se puede ver la imagen visitando el enlace https://www.google.com/intl/en/images/logo.gif
![la imagen solicitada](https://www.google.com/intl/en/images/logo.gif)

Esta solicitud la hace el navegador de forma automática.

### I. What is occurring in packets 13 through 22?

Se produce la trasnmisión de la imagen solicitada, hasta recibir el ok de la respuesta por parte del servidor.

### J. Explain what happens in packets 23 through 26. See the second “hint” to the left.

Similar al proceso anterior, las páingas web suelen tener un icono que se utiliza para mostrar en las pestañas del navegador, en este caso se solicita el icono de google:

![favicon de google](https://www.google.com/favicon.ico)

### K. In one sentence describe what the user was doing (Reading email? Accessing a web page? FTP? Other?).

EL usuario estaba accediendo a una pagina web. En concreto `www.google.com`, una versión antigua claro que solo tenía html y un imagen.

## Ejercicio 2

### A. In the first few packets, the client machine is looking up the common name (cname) of a web site to find its IP address. What is the cname of this web site? Give two IP addresses for this web site.

El CNAME del sitio web es `yahoo.com`, que apunta a `yahoo.akadns.net` que tiene las siguientes IP's:

1. `216.209.117.106`
2. `216.209.117.109`
3. `216.209.117.104`
4. `216.209.117.204`
5. `216.209.117.206`
6. `216.209.118.70`
7. `216.209.118.76`
8. `216.209.118.79`

### B. How many packets/frames does it take to receive the web page (the answer to the first http get request only)?

Toma desde el frame 6 hasta el frame 22, es decir 17 frames.

### C. Does this web site use gzip to compress its data for sending? Does it write cookies? In order to answer these questions, look under the payload for the reassembled packet that represents the web page. This will be the last packet from question b above. Look to see if it has “Content-Encoding” set to gzip, and to see if it has a “Set-Cookie” to write a cookie.

Sí usa GZIP y además escribe varias COOCKIES.

### D. What is happening in packets 26 and 27? Does every component of a web page have to come from the same server? See the Hint to the left.

En el frame 16 se hace una solicitud DNS para encontrar la IP de `us.js2.yimg.com`, el frame 27 responde con las IP's, entre ellas `64.21.46.150`.
No ncesariamente todos los componentes de una página web deben venir del mismo servidor, en el caso del ejemplo se esta solicitando un archivo de javascript a otro servidor.

### E. In packet 37 we see another DNS query, this time for us.i1.yimg.com. Why does the client need to ask for this IP address? Didn’t we just get this address in packet 26? (This is a trick question; carefully compare the two common names in packet 26 and 37).

No, puesto que la IP que se solicito fue al CNAME `us.js2.yimg.com`, que es diferente al que se pide en el frame 37 (`us.i1.yimg.com`).

### F. In packet 42 we see a HTTP “Get” statement, and in packet 48 a new HTTP “Get” statement. Why didn’t the system need another DNS request before the second get statement? Click on packet 42 and look in the middle window. Expand the line titled “Hypertext Transfer Protocol” and read the “Host:” line. Compare that line to the “Host:” line for packet 48.

Como se puede observar en ambos paquetes, estos se dirigen al host `us.i1.yimg.com` del cuál anteriormente ya se habia solicitado su IP, por lo que esta quedó almacenada en el DNS cache. Evitando así la necesidad de otra consulta DNS.

### G. Examine packet 139. It is one segment of a PDU that is reassembled with several other segments in packet 160. Look at packets 141, 142, and 143. Are these three packets also part of packet 160? What happens if a set of packets that are supposed to be reassembled do not arrive in a continuous stream or do not arrive in the proper order?

Solo el frame 143 es parte del frame 160. El orden en el que llegan los paquetes en TCP es indiferente, puesto que los paquetes se reordenan utilizando los números de secuencia para reensamblar todos los datos correctamente.

### H. Return to examine frames 141 and 142. Both of these are graphics (GIF files) from the same source IP address. How does the client know which graphic to match up to each get statement? Hint: Click on each and look in the middle window for the heading line that starts with “Transmission Control Protocol”. What difference do you see in the heading lines for the two files? Return to the original “Get” statements. Can you see the same difference in the “Get” statements?

El cliente al hacer una solicitud a un servidor utiliza un puerto efimero, en el caso de la solicitud para las dos imágenes GIF utiliza `1226` y `1225`. Entonces para saber que imagen va con que solicitud utiliza cada puerto efimero respectivo.

## Ejercicio 3

### A. Compare the destination port in the TCP packet in frame 3 with the destination port in the TCP packet in frame 12. What difference do you see? What does this tell you about the difference in the two requests?

La solicitud que se hace en el frame 3 es una solicitud al puerto `80` que es un **puerto bien conocido (well know port)** para las conexiones HTTP. En cambio, el frame 12 hace la solicitud al puerto `443` que es el puerto utilizado para las conexiones HTTPS que utiliza conexiones cifradas.

| Row  | Yahoo Frame | My.Usf Frame | Brief Explanation                                             |
| ---- | ----------- | ------------ | ------------------------------------------------------------- |
| i)   | 1-2         | 8-9          | DNS Request to find IP address for common name & DNS Response |
| ii)  | 2-5         | 10-12        | Three-way handshake                                           |
| iii) | \*\*\*\*    | 13-20        |                                                               |
| Iv)  | 6           | 21           | "Get"request for web page                                     |
| v)   | 7           | 22           | First packet from web server with web page content.           |

### B. Explain what is happening in row “iii” above. Why are there no frames listed for yahoo in row “iii"?

La conexión a Yahoo se hace mediante el protocolo HTTP, lo que significa que no tiene ningún tipo de cifrado. En cambio la conexión a My.Usf está utilizando el protocolo HTTPS, por lo que en el frame 13 a 20 hace el proceso de **TSL handshake**, donde se envian diferentes datos para poder generara la clave simétrica de la sesión.

### C. Look at the “Info” column on frame 6. It says: “GET / HTTP / 1.1. What is the corresponding Info field for the my.usf.com web request (frame 21)? Why doesn’t it read the same as in frame 6?

Como en la conexión a www.my.usf.com se utiliza el protocolo HTTPS, no se puede ver el contenido de los paquetes que se envian (pues estan cifrados), por eso solo se puede ver como "Application Data".

## Ejercicio 4

Pueden ver un ejemplo de como se veria la consulta a [os.ecci.ucr.ac.cr/ci0121](https://os.ecci.ucr.ac.cr/ci0121) en WireShark, [haciendo click aquí](./data/consulta_pregunta4.pcap). Se ve similar a la consulta a my.usf.com, pero como es una web frecuentada (esperamos) entonces no hay consulta a DNS. La IP del servidor `os.ecci.ucr.ac.cr/ci01211` es `163.178.104.62`
