# Solución Packet Tracer VLAN

## Práctica básica de VLAN

Primero se necesita cambiar el nombre, desactivar la busqueda por DNS y las contraseñas

#### Configuración S1

```sh
enable
config terminal
hostname S1
no ip domain-lookup
enable secret class
line console 0
password cisco
login
exit
line vty 0 15
password cisco
login
exit
end
write memory
```

Para las demás solo hay que cambiar el nombre del host en el script anterior. Ahora se configuran las IPs para cada una da las máquinas (PC1, PC2, PC3, PC4, PC5, PC6).

Se creean las VLAN para cada switch (S1, S2, S3):

```sh
enable
config terminal
vlan 99
name Management&Native
exit
vlan 10
name Faculty/Staff
exit
vlan 20
name Students
exit
vlan 30
name Guest(Default)
exit
```

Ahora se asignan los puertos a las VLANs:

Para el switch S2:

```sh
interface fastEthernet0/6
switchport mode access
switchport access vlan 30
interface fastEthernet0/11
switchport mode access
switchport access vlan 10
interface fastEthernet0/18
switchport mode access
switchport access vlan 20
end
copy running-config startup-config
```

Para el switch S3:

```sh
interface fastEthernet0/10
switchport mode access
switchport access vlan 30
interface fastEthernet0/17
switchport mode access
switchport access vlan 10
interface fastEthernet0/24
switchport mode access
switchport access vlan 20
end
copy running-config startup-config
```

Por lo tanto para el switch S2 la VLAN 10 quedó con el puerto `Fa0/11`.

Se deben asignar las IPs para la administración:

#### Switch S1

```sh
interface vlan 99
ip address 172.17.99.11 255.255.255.0
no shutdown
```

#### Switch S2

```sh
interface vlan 99
ip address 172.17.99.12 255.255.255.0
no shutdown
```

#### Switch S3

```sh
interface vlan 99
ip address 172.17.99.13 255.255.255.0
no shutdown
```

Ahora se configura el trunking para cada switch:

#### Switch S1

```sh
interface fa0/1
switchport mode trunk
switchport trunk native vlan 99
interface fa0/2
switchport mode trunk
switchport trunk native vlan 99
end
```

#### Switch S2

```sh
interface fa0/1
switchport mode trunk
switchport trunk native vlan 99
end
```

#### Switch S3

```sh
interface fa0/2
switchport mode trunk
switchport trunk native vlan 99
end
```

Entonces ahora PC2, no puede hacer ping a PC1 ni a la IP de la VLAN 99. Pero sí a PC5.

Ahora se asigna la VLAN 20 a el puerto Fa0/11 en S2, para permitir conexión entre PC2 y PC1:

```sh
interface fastethernet 0/11
switchport access vlan 20
end
```

Si se hace ping de PC2 a PC1 no funciona, porque primero hay que cambiar el IP de PC1 a 172.17.20.21, para que ambas estén en la misma VLAN.
