# Práctica 3 (LRC) - 23/7/2025

## Dispositivos a utilizar

* Router 2911
* Sw 2960

## Tabla de Asignación

| Dispo       | Interfaz     | Ip           | Mask             |
| ----------- | ------------ | ------------ | ---------------- |
| Lunes       | S0/0/0       | 1.1.1.1      | 255.255.255.252  |
|             | S0/1/0       | 3.3.3.1      |                  |
|             | S0/0/1       | 6.6.6.1      |                  |
|             | g0/0         | 192.168.1.1  | 255.255.255.0    |
|             | g0/1         | 192.168.2.1  |                  |
|             | g0/2         | 192.168.3.1  |                  |
| Miercoles   | S0/0/0       | 1.1.1.2      | 255.255.255.252  |
|             | S0/1/0       | 2.2.2.1      |                  |
|             | S0/0/1       | 7.7.7.1      |                  |
|             | g0/0         | 192.168.4.1  | 255.255.255.0    |
|             | g0/1         | 192.168.5.1  |                  |
|             | g0/2         | 192.168.6.1  |                  |
| Redes       | S0/0/0       | 2.2.2.2      | 255.255.255.252  |
|             | S0/0/1       | 8.8.8.1      |                  |
|             | g0/0         | 5.5.5.1      |                  |
|             | g0/1         | 192.168.7.1  | 255.255.255.0    |
|             | g0/2         | 192.168.8.1  |                  |
| unicaes     | S0/0/0       | 3.3.3.2      | 255.255.255.252  |
|             | g0/0         | 5.5.5.2      |                  |
|             | g0/1         | 4.4.4.1      |                  |
|             | g0/2         | 192.168.10.1 | 255.255.255.0    |
| central     | S0/0/0       | 6.6.6.2      | 255.255.255.252  |
|             | S0/1/0       | 7.7.7.2      |                  |
|             | S0/0/1       | 8.8.8.2      |                  |
|             | g0/0         | 4.4.4.2      |                  |

## Conf. Básica - DHCP - Lunes

### Configuración Básica

```bash
Router>enable
Router#configure terminal
Router(config)#hostname lunes
lunes(config)#int Se0/0/0
lunes(config-if)#ip add 1.1.1.1 255.255.255.252
lunes(config-if)#no shut
lunes(config-if)#int Se0/1/0
lunes(config-if)#ip add 3.3.3.1 255.255.255.252
lunes(config-if)#no shut
lunes(config-if)#int Se0/0/1
lunes(config-if)#ip add 6.6.6.1 255.255.255.252
lunes(config-if)#no shut
lunes(config-if)#int g0/0
lunes(config-if)#ip add 192.168.1.1 255.255.255.0
lunes(config-if)#no shut
lunes(config-if)#int g0/1
lunes(config-if)#ip add 192.168.2.1 255.255.255.0
lunes(config-if)#no shut
lunes(config-if)#int g0/2
lunes(config-if)#ip add 192.168.3.1 255.255.255.0
lunes(config-if)#no shut
```

### DHCP

```bash
lunes(config-if)#exit
lunes(config)#ip dhcp excluded-address 192.168.1.1 192.168.1.20
lunes(config)#ip dhcp pool L1
lunes(dhcp-config)#network 192.168.1.0 255.255.255.0
lunes(dhcp-config)#default-router 192.168.1.1
lunes(dhcp-config)#exit
lunes(config)#ip dhcp excluded-address 192.168.2.1
lunes(config)#ip dhcp pool L2
lunes(dhcp-config)#network 192.168.2.0 255.255.255.0
lunes(dhcp-config)#default-router 192.168.2.1
lunes(dhcp-config)#exit
lunes(config)#ip dhcp excluded-address 192.168.3.1 192.168.3.200
lunes(config)#ip dhcp pool L3
lunes(dhcp-config)#network 192.168.3.0 255.255.255.0
lunes(dhcp-config)#default-router 192.168.3.1
```

### Enrutamiento estático utilizando **ruta por defecto** e **ip del sig. salto**

* **Red**: `0.0.0.0`
* **Mask**: `0.0.0.0`

| Dispo.      | Red Desco | Mask    | Ip del Sig. Salto |
| ----------- | --------- | ------- | ----------------- |
| Lunes       |           |         | L - M<br>1.1.1.2  |
|             | 0.0.0.0   | 0.0.0.0 | L - U<br>3.3.3.2  |
|             |           |         | L - C<br>6.6.6.2  |
| Miercoles   |           |         | M - L<br>1.1.1.1  |
|             | 0.0.0.0   | 0.0.0.0 | M - R<br>2.2.2.2  |
|             |           |         | M - C<br>7.7.7.2  |
| Redes       |           |         | R - M<br>2.2.2.1  |
|             | 0.0.0.0   | 0.0.0.0 | R - U<br>5.5.5.2  |
|             |           |         | R - C<br>8.8.8.2  |
| unicaes     |           |         | U - L<br>3.3.3.1  |
|             | 0.0.0.0   | 0.0.0.0 | U - R<br>5.5.5.1  |
|             |           |         | U - C<br>4.4.4.2  |
| central     |           |         | C - L<br>6.6.6.1  |
|             | 0.0.0.0   | 0.0.0.0 | C - M<br>7.7.7.1  |
|             |           |         | C - R<br>8.8.8.1  |
|             |           |         | C - U<br>4.4.4.1  |

```bash
lunes(dhcp-config)#exit
lunes(config)#ip route 0.0.0.0 0.0.0.0 1.1.1.2
lunes(config)#ip route 0.0.0.0 0.0.0.0 3.3.3.2
lunes(config)#ip route 0.0.0.0 0.0.0.0 6.6.6.2
lunes(config)#do write memory
```

## Conf. Básica - DHCP - Miercoles

### Configuración Básica

```bash
Router>enable
Router#configure terminal
Router(config)#hostname miercoles
miercoles(config)#int Se0/0/0
miercoles(config-if)#ip add 1.1.1.2 255.255.255.252
miercoles(config-if)#no shut
miercoles(config-if)#int Se0/1/0
miercoles(config-if)#ip add 2.2.2.1 255.255.255.252
miercoles(config-if)#no shut
miercoles(config-if)#int Se0/0/1
miercoles(config-if)#ip add 7.7.7.1 255.255.255.252
miercoles(config-if)#no shut
miercoles(config-if)#int g0/0
miercoles(config-if)#ip add 192.168.4.1 255.255.255.0
miercoles(config-if)#no shut
miercoles(config-if)#int g0/1
miercoles(config-if)#ip add 192.168.5.1 255.255.255.0
miercoles(config-if)#no shut
miercoles(config-if)#int g0/2
miercoles(config-if)#ip add 192.168.6.1 255.255.255.0
miercoles(config-if)#no shut
```

### DHCP

```bash
miercoles(config-if)#exit
miercoles(config)#ip dhcp excluded-address 192.168.4.1
miercoles(config)#ip dhcp pool M1
miercoles(dhcp-config)#network 192.168.4.0 255.255.255.0
miercoles(dhcp-config)#default-router 192.168.4.1
miercoles(dhcp-config)#exit
miercoles(config)#ip dhcp excluded-address 192.168.5.1
miercoles(config)#ip dhcp pool M2
miercoles(dhcp-config)#network 192.168.5.0 255.255.255.0
miercoles(dhcp-config)#default-router 192.168.5.1
miercoles(dhcp-config)#exit
miercoles(config)#ip dhcp excluded-address 192.168.6.1
miercoles(config)#ip dhcp pool M3
miercoles(dhcp-config)#network 192.168.6.0 255.255.255.0
miercoles(dhcp-config)#default-router 192.168.6.1
```

### Enrutamiento estático utilizando **ruta por defecto** e **ip del sig. salto**

```bash
miercoles(dhcp-config)#exit
miercoles(config)#ip route 0.0.0.0 0.0.0.0 1.1.1.1
miercoles(config)#ip route 0.0.0.0 0.0.0.0 2.2.2.2
miercoles(config)#ip route 0.0.0.0 0.0.0.0 7.7.7.2
miercoles(config)#do write memory
```

## Conf. Básica - DHCP - Redes

### Configuración Básica

```bash
Router>enable
Router#configure terminal
Router(config)#hostname redes
redes(config)#int Se0/0/0
redes(config-if)#ip add 2.2.2.2 255.255.255.252
redes(config-if)#no shut
redes(config-if)#int Se0/0/1
redes(config-if)#ip add 8.8.8.1 255.255.255.252
redes(config-if)#no shut
redes(config-if)#int g0/0
redes(config-if)#ip add 5.5.5.1 255.255.255.252
redes(config-if)#no shut
redes(config-if)#int g0/1
redes(config-if)#ip add 192.168.7.1 255.255.255.0
redes(config-if)#no shut
redes(config-if)#int g0/2
redes(config-if)#ip add 192.168.8.1 255.255.255.0
redes(config-if)#no shut
```

### DHCP

```bash
redes(config-if)#exit
redes(config)#ip dhcp excluded-address 192.168.7.1
redes(config)#ip dhcp pool R1
redes(dhcp-config)#network 192.168.7.0 255.255.255.0
redes(dhcp-config)#default-router 192.168.7.1
redes(dhcp-config)#exit
redes(config)#ip dhcp excluded-address 192.168.8.1
redes(config)#ip dhcp pool R2
redes(dhcp-config)#network 192.168.8.0 255.255.255.0
redes(dhcp-config)#default-router 192.168.8.1
```

### Enrutamiento estático utilizando **ruta por defecto** e **ip del sig. salto**

```bash
redes(dhcp-config)#exit
redes(config)#ip route 0.0.0.0 0.0.0.0 2.2.2.1
redes(config)#ip route 0.0.0.0 0.0.0.0 5.5.5.2
redes(config)#ip route 0.0.0.0 0.0.0.0 8.8.8.2
redes(config)#do write memory
```

## Conf. Básica - DHCP - unicaes

### Configuración Básica

```bash
Router>enable
Router#configure terminal
Router(config)#hostname unicaes
unicaes(config)#int Se0/0/0
unicaes(config-if)#ip add 3.3.3.2 255.255.255.252
unicaes(config-if)#no shut
unicaes(config-if)#int g0/0
unicaes(config-if)#ip add 5.5.5.2 255.255.255.252
unicaes(config-if)#no shut
unicaes(config-if)#int g0/1
unicaes(config-if)#ip add 4.4.4.1 255.255.255.252
unicaes(config-if)#no shut
unicaes(config-if)#int g0/2
unicaes(config-if)#ip add 192.168.10.1 255.255.255.0
unicaes(config-if)#no shut
```

### DHCP

```bash
unicaes(config-if)#exit
unicaes(config)#ip dhcp excluded-address 192.168.10.1
unicaes(config)#ip dhcp pool U1
unicaes(dhcp-config)#network 192.168.10.0 255.255.255.0
unicaes(dhcp-config)#default-router 192.168.10.1
```

```bash
unicaes(dhcp-config)#exit
unicaes(config)#ip route 0.0.0.0 0.0.0.0 3.3.3.1
unicaes(config)#ip route 0.0.0.0 0.0.0.0 5.5.5.1
unicaes(config)#ip route 0.0.0.0 0.0.0.0 4.4.4.2
unicaes(config)#do write memory
```

## Conf. Básica - central

```bash
Router>enable
Router#configure terminal
Router(config)#hostname central
central(config)#int Se0/0/0
central(config-if)#ip add 6.6.6.2 255.255.255.252
central(config-if)#no shut
central(config-if)#int Se0/1/0
central(config-if)#ip add 7.7.7.2 255.255.255.252
central(config-if)#no shut
central(config-if)#int Se0/0/1
central(config-if)#ip add 8.8.8.2 255.255.255.252
central(config-if)#no shut
central(config-if)#int g0/0
central(config-if)#ip add 4.4.4.2 255.255.255.252
central(config-if)#no shut
```

### Enrutamiento estático utilizando **ruta por defecto** e **ip del sig. salto**

```bash
central(config-if)#exit
central(config)#ip route 0.0.0.0 0.0.0.0 6.6.6.1
central(config)#ip route 0.0.0.0 0.0.0.0 7.7.7.1
central(config)#ip route 0.0.0.0 0.0.0.0 8.8.8.1
central(config)#ip route 0.0.0.0 0.0.0.0 4.4.4.1
central(config)#do write memory
```

## Cisco Packet Tracer

* Archivo con el ejercicio realizado: `clase6-practica3.pkt`