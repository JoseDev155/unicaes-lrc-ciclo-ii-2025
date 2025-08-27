# Práctica 6 (LRC) - 13/8/2025

## Enrutamiento estático ip del siguiente salto

* Router 1941
* Sw C.2960

### Configuración Básica - R1

```bash
Router>enable
Router#conf t
Router(config)#hostname R1
R1(config)#int g0/0
R1(config-if)#ip add 192.168.1.1 255.255.255.0
R1(config-if)#no shutdown
R1(config-if)#int S0/0/0
R1(config-if)#ip add 1.1.1.1 255.255.255.252
R1(config-if)#no shutdown
R1(config-if)#int S0/0/1
R1(config-if)#ip add 3.3.3.1 255.255.255.252
R1(config-if)#no shut
R1(config-if)#int S0/1/0
R1(config-if)#ip add 2.2.2.1 255.255.255.252
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#ip dhcp excluded-address 192.168.1.1
R1(config)#ip dhcp pool R1-DHCP
R1(dhcp-config)#network 192.168.1.0 255.255.255.0
R1(dhcp-config)#default-router 192.168.1.1
R1(dhcp-config)#do write memory
```

### Tabla de Asignación

| Dispo. | Redes desconocidas | Mask de Redes Desconocidas | Ips del Sig. Salto    | Cantidad de líneas |
| ------ | ------------------ | -------------------------- | --------------------- | ------------------ |
| R1     | 192.168.2.0        | 255.255.255.0              | R1 - R3<br>1.1.1.2    |                    |
|        | 192.168.3.0        |                            | R1 - R2<br>2.2.2.2    |                    |
|        | 192.168.4.0        |                            | R1 - R5<br>3.3.3.2    |                    |
|        | 5.5.5.0            | 255.255.255.252            |                       |                    |
|        | 7.7.7.0            |                            |                       | 27 líneas          |
|        | 6.6.6.0            |                            |                       |                    |
|        | 4.4.4.0            |                            |                       |                    |
|        | 8.8.8.0            |                            |                       |                    |
|        | 10.10.10.0         |                            |                       |                    |
| R2     | 1.1.1.0            | 255.255.255.252            | R2 - R1<br>2.2.2.1    |                    |
|        | 3.3.3.0            |                            | R2 - R4<br>10.10.10.2 |                    |
|        | 5.5.5.0            |                            | R2 - R5<br>6.6.6.2    | 30 líneas          |
|        | 7.7.7.0            |                            |                       |                    |
|        | 4.4.4.0            |                            |                       |                    |
|        | 8.8.8.0            |                            |                       |                    |
|        | 192.168.1.0        | 255.255.255.0              |                       |                    |
|        | 192.168.2.0        |                            |                       |                    |
|        | 192.168.3.0        |                            |                       |                    |
|        | 192.168.4.0        |                            |                       |                    |
| R3     | 192.168.1.0        | 255.255.255.0              | R3 - R1<br>1.1.1.1    |                    |
|        | 192.168.3.0        |                            | R3 - R4<br>4.4.4.2    |                    |
|        | 192.168.4.0        |                            | R3 - R6<br>5.5.5.2    | 27 líneas          |
|        | 3.3.3.0            | 255.255.255.252            |                       |                    |
|        | 7.7.7.0            |                            |                       |                    |
|        | 2.2.2.0            |                            |                       |                    |
|        | 6.6.6.0            |                            |                       |                    |
|        | 8.8.8.0            |                            |                       |                    |
|        | 10.10.10.0         |                            |                       |                    |
| R4     | 192.168.1.0        | 255.255.255.0              | R4 - R2<br>10.10.10.1 |                    |
|        | 192.168.2.0        |                            | R4 - R3<br>4.4.4.1    | 30 líneas          |
|        | 192.168.3.0        |                            | R4 - R6<br>8.8.8.1    |                    |
|        | 192.168.4.0        |                            |                       |                    |
|        | 1.1.1.0            | 255.255.255.252            |                       |                    |
|        | 2.2.2.0            |                            |                       |                    |
|        | 6.6.6.0            |                            |                       |                    |
|        | 5.5.5.0            |                            |                       |                    |
|        | 7.7.7.0            |                            |                       |                    |
|        | 3.3.3.0            |                            |                       |                    |
| R5     | 192.168.1.0        | 255.255.255.0              | R5 - R1<br>3.3.3.1    |                    |
|        | 192.168.2.0        |                            | R5 - R2<br>6.6.6.1    | 27 líneas          |
|        | 192.168.4.0        |                            | R5 - R6<br>7.7.7.2    |                    |
|        | 1.1.1.0            | 255.255.255.252            |                       |                    |
|        | 2.2.2.0            |                            |                       |                    |
|        | 4.4.4.0            |                            |                       |                    |
|        | 5.5.5.0            |                            |                       |                    |
|        | 8.8.8.0            |                            |                       |                    |
|        | 10.10.10.0         |                            |                       |                    |
| R6     | 192.168.1.0        | 255.255.255.0              | R6 - R3<br>5.5.5.1    |                    |
|        | 192.168.2.0        |                            | R6 - R5<br>7.7.7.1    |                    |
|        | 192.168.3.0        |                            | R6 - R4<br>8.8.8.2    | 27 líneas          |
|        | 1.1.1.0            | 255.255.255.252            |                       |                    |
|        | 3.3.3.0            |                            |                       |                    |
|        | 2.2.2.0            |                            |                       |                    |
|        | 6.6.6.0            |                            |                       |                    |
|        | 10.10.10.0         |                            |                       |                    |
|        | 4.4.4.0            |                            |                       |                    |

### Enrutamiento estático - R2

```bash
R2>enable
R2#conf t
R2(config)#ip route 1.1.1.0 255.255.255.252 2.2.2.1
R2(config)#ip route 1.1.1.0 255.255.255.252 10.10.10.2
R2(config)#ip route 1.1.1.0 255.255.255.252 6.6.6.2
R2(config)#ip route 3.3.3.0 255.255.255.252 2.2.2.1
R2(config)#ip route 3.3.3.0 255.255.255.252 10.10.10.2
R2(config)#ip route 3.3.3.0 255.255.255.252 6.6.6.2
R2(config)#ip route 5.5.5.0 255.255.255.252 2.2.2.1
R2(config)#ip route 5.5.5.0 255.255.255.252 10.10.10.2
R2(config)#ip route 5.5.5.0 255.255.255.252 6.6.6.2
R2(config)#ip route 7.7.7.0 255.255.255.252 2.2.2.1
R2(config)#ip route 7.7.7.0 255.255.255.252 10.10.10.2
R2(config)#ip route 7.7.7.0 255.255.255.252 6.6.6.2
R2(config)#ip route 4.4.4.0 255.255.255.252 2.2.2.1
R2(config)#ip route 4.4.4.0 255.255.255.252 10.10.10.2
R2(config)#ip route 4.4.4.0 255.255.255.252 6.6.6.2
R2(config)#ip route 8.8.8.0 255.255.255.252 2.2.2.1
R2(config)#ip route 8.8.8.0 255.255.255.252 10.10.10.2
R2(config)#ip route 8.8.8.0 255.255.255.252 6.6.6.2
R2(config)#ip route 192.168.1.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.1.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.1.0 255.255.255.0 6.6.6.2
R2(config)#ip route 192.168.2.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.2.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.2.0 255.255.255.0 6.6.6.2
R2(config)#ip route 192.168.3.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.3.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.3.0 255.255.255.0 6.6.6.2
R2(config)#ip route 192.168.4.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.4.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.4.0 255.255.255.0 6.6.6.2
R2(config)#do write memory
```

### Configuración Básica - R1

```bash
Router>enable
Router#conf t
Router(config)#hostname R1
R1(config)#int g0/0
R1(config-if)#ip add 192.168.1.1 255.255.255.0
R1(config-if)#no shutdown
R1(config-if)#int S0/0/0
R1(config-if)#ip add 1.1.1.1 255.255.255.252
R1(config-if)#no shutdown
R1(config-if)#int S0/0/1
R1(config-if)#ip add 3.3.3.1 255.255.255.252
R1(config-if)#no shutdown
R1(config-if)#int S0/1/0
R1(config-if)#ip add 2.2.2.1 255.255.255.252
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#ip dhcp excluded-address 192.168.1.1
R1(config)#ip dhcp pool R1-DHCP
R1(dhcp-config)#network 192.168.1.0 255.255.255.0
R1(dhcp-config)#default-router 192.168.1.1
R1(dhcp-config)#do write memory
R1(dhcp-config)#exit
R1(config)#ip route 192.168.2.0 255.255.255.0 1.1.1.2
R1(config)#ip route 192.168.2.0 255.255.255.0 2.2.2.2
R1(config)#ip route 192.168.2.0 255.255.255.0 3.3.3.2
R1(config)#ip route 192.168.3.0 255.255.255.0 1.1.1.2
R1(config)#ip route 192.168.3.0 255.255.255.0 2.2.2.2
R1(config)#ip route 192.168.3.0 255.255.255.0 3.3.3.2
R1(config)#ip route 192.168.4.0 255.255.255.0 1.1.1.2
R1(config)#ip route 192.168.4.0 255.255.255.0 2.2.2.2
R1(config)#ip route 192.168.4.0 255.255.255.0 3.3.3.2
R1(config)#ip route 5.5.5.0 255.255.255.252 1.1.1.2
R1(config)#ip route 5.5.5.0 255.255.255.252 2.2.2.2
R1(config)#ip route 5.5.5.0 255.255.255.252 3.3.3.2
R1(config)#ip route 7.7.7.0 255.255.255.252 1.1.1.2
R1(config)#ip route 7.7.7.0 255.255.255.252 2.2.2.2
R1(config)#ip route 7.7.7.0 255.255.255.252 3.3.3.2
R1(config)#ip route 6.6.6.0 255.255.255.252 1.1.1.2
R1(config)#ip route 6.6.6.0 255.255.255.252 2.2.2.2
R1(config)#ip route 6.6.6.0 255.255.255.252 3.3.3.2
R1(config)#ip route 4.4.4.0 255.255.255.252 1.1.1.2
R1(config)#ip route 4.4.4.0 255.255.255.252 2.2.2.2
R1(config)#ip route 4.4.4.0 255.255.255.252 3.3.3.2
R1(config)#ip route 8.8.8.0 255.255.255.252 1.1.1.2
R1(config)#ip route 8.8.8.0 255.255.255.252 2.2.2.2
R1(config)#ip route 8.8.8.0 255.255.255.252 3.3.3.2
R1(config)#ip route 10.10.10.0 255.255.255.252 1.1.1.2
R1(config)#ip route 10.10.10.0 255.255.255.252 2.2.2.2
R1(config)#ip route 10.10.10.0 255.255.255.252 3.3.3.2
R1(config)#do write memory
```

### Configuración Básica - R2

```bash
Router>enable
Router#conf t
Router(config)#hostname R2
R2(config)#int S0/0/0
R2(config-if)#ip add 2.2.2.2 255.255.255.252
R2(config-if)#no shut
R2(config-if)#int S0/0/1
R2(config-if)#ip add 10.10.10.1 255.255.255.252
R2(config-if)#no shut
R2(config-if)#int S0/1/0
R2(config-if)#ip add 6.6.6.1 255.255.255.252
R2(config-if)#no shut
R2(config-if)#exit
R2(config)#ip route 1.1.1.0 255.255.255.252 2.2.2.1
R2(config)#ip route 1.1.1.0 255.255.255.252 10.10.10.2
R2(config)#ip route 1.1.1.0 255.255.255.252 6.6.6.2
R2(config)#ip route 3.3.3.0 255.255.255.252 2.2.2.1
R2(config)#ip route 3.3.3.0 255.255.255.252 10.10.10.2
R2(config)#ip route 3.3.3.0 255.255.255.252 6.6.6.2
R2(config)#ip route 5.5.5.0 255.255.255.252 2.2.2.1
R2(config)#ip route 5.5.5.0 255.255.255.252 10.10.10.2
R2(config)#ip route 5.5.5.0 255.255.255.252 6.6.6.2
R2(config)#ip route 7.7.7.0 255.255.255.252 2.2.2.1
R2(config)#ip route 7.7.7.0 255.255.255.252 10.10.10.2
R2(config)#ip route 7.7.7.0 255.255.255.252 6.6.6.2
R2(config)#ip route 4.4.4.0 255.255.255.252 2.2.2.1
R2(config)#ip route 4.4.4.0 255.255.255.252 10.10.10.2
R2(config)#ip route 4.4.4.0 255.255.255.252 6.6.6.2
R2(config)#ip route 8.8.8.0 255.255.255.252 2.2.2.1
R2(config)#ip route 8.8.8.0 255.255.255.252 10.10.10.2
R2(config)#ip route 8.8.8.0 255.255.255.252 6.6.6.2
R2(config)#ip route 192.168.1.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.1.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.1.0 255.255.255.0 6.6.6.2
R2(config)#ip route 192.168.2.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.2.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.2.0 255.255.255.0 6.6.6.2
R2(config)#ip route 192.168.3.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.3.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.3.0 255.255.255.0 6.6.6.2
R2(config)#ip route 192.168.4.0 255.255.255.0 2.2.2.1
R2(config)#ip route 192.168.4.0 255.255.255.0 10.10.10.2
R2(config)#ip route 192.168.4.0 255.255.255.0 6.6.6.2
R2(config)#do write memory
```

### Configuración Básica - R3

```bash
Router>enable
Router#conf t
Router(config)#hostname R3
R3(config)#int S0/0/0
R3(config-if)#ip add 1.1.1.2 255.255.255.252
R3(config-if)#no shut
R3(config-if)#int S0/0/1
R3(config-if)#ip add 4.4.4.1 255.255.255.252
R3(config-if)#no shut
R3(config-if)#int S0/1/0
R3(config-if)#ip add 5.5.5.1 255.255.255.252
R3(config-if)#no shut
R3(config-if)#int g0/0
R3(config-if)#ip add 192.168.2.1 255.255.255.0
R3(config-if)#no shut
R3(config-if)#exit
R3(config)#ip dhcp excluded-address 192.168.2.1
R3(config)#ip dhcp pool R3-DHCP
R3(dhcp-config)#network 192.168.2.0 255.255.255.0
R3(dhcp-config)#default-router 192.168.2.1
R3(dhcp-config)#do write memory
R3(dhcp-config)#exit
R3(config)#ip route 192.168.1.0 255.255.255.0 1.1.1.1
R3(config)#ip route 192.168.1.0 255.255.255.0 4.4.4.2
R3(config)#ip route 192.168.1.0 255.255.255.0 5.5.5.2
R3(config)#ip route 192.168.3.0 255.255.255.0 1.1.1.1
R3(config)#ip route 192.168.3.0 255.255.255.0 4.4.4.2
R3(config)#ip route 192.168.3.0 255.255.255.0 5.5.5.2
R3(config)#ip route 192.168.4.0 255.255.255.0 1.1.1.1
R3(config)#ip route 192.168.4.0 255.255.255.0 4.4.4.2
R3(config)#ip route 192.168.4.0 255.255.255.0 5.5.5.2
R3(config)#ip route 3.3.3.0 255.255.255.252 1.1.1.1
R3(config)#ip route 3.3.3.0 255.255.255.252 4.4.4.2
R3(config)#ip route 3.3.3.0 255.255.255.252 5.5.5.2
R3(config)#ip route 7.7.7.0 255.255.255.252 1.1.1.1
R3(config)#ip route 7.7.7.0 255.255.255.252 4.4.4.2
R3(config)#ip route 7.7.7.0 255.255.255.252 5.5.5.2
R3(config)#ip route 2.2.2.0 255.255.255.252 1.1.1.1
R3(config)#ip route 2.2.2.0 255.255.255.252 4.4.4.2
R3(config)#ip route 2.2.2.0 255.255.255.252 5.5.5.2
R3(config)#ip route 6.6.6.0 255.255.255.252 1.1.1.1
R3(config)#ip route 6.6.6.0 255.255.255.252 4.4.4.2
R3(config)#ip route 6.6.6.0 255.255.255.252 5.5.5.2
R3(config)#ip route 8.8.8.0 255.255.255.252 1.1.1.1
R3(config)#ip route 8.8.8.0 255.255.255.252 4.4.4.2
R3(config)#ip route 8.8.8.0 255.255.255.252 5.5.5.2
R3(config)#ip route 10.10.10.0 255.255.255.252 1.1.1.1
R3(config)#ip route 10.10.10.0 255.255.255.252 4.4.4.2
R3(config)#ip route 10.10.10.0 255.255.255.252 5.5.5.2
R3(config)#do write memory
```

### Configuración Básica - R4

```bash
Router>enable
Router#conf t
Router(config)#hostname R4
R4(config)#int S0/0/0
R4(config-if)#ip add 4.4.4.2 255.255.255.252
R4(config-if)#no shut
R4(config-if)#int S0/0/1
R4(config-if)#ip add 10.10.10.2 255.255.255.252
R4(config-if)#no shut
R4(config-if)#int S0/1/0
R4(config-if)#ip add 8.8.8.2 255.255.255.252
R4(config-if)#no shut
R4(config-if)#exit
R4(config)#ip route 192.168.1.0 255.255.255.0 10.10.10.1
R4(config)#ip route 192.168.1.0 255.255.255.0 4.4.4.1
R4(config)#ip route 192.168.1.0 255.255.255.0 8.8.8.1
R4(config)#ip route 192.168.2.0 255.255.255.0 10.10.10.1
R4(config)#ip route 192.168.2.0 255.255.255.0 4.4.4.1
R4(config)#ip route 192.168.2.0 255.255.255.0 8.8.8.1
R4(config)#ip route 192.168.3.0 255.255.255.0 10.10.10.1
R4(config)#ip route 192.168.3.0 255.255.255.0 4.4.4.1
R4(config)#ip route 192.168.3.0 255.255.255.0 8.8.8.1
R4(config)#ip route 192.168.4.0 255.255.255.0 10.10.10.1
R4(config)#ip route 192.168.4.0 255.255.255.0 4.4.4.1
R4(config)#ip route 192.168.4.0 255.255.255.0 8.8.8.1
R4(config)#ip route 1.1.1.0 255.255.255.252 10.10.10.1
R4(config)#ip route 1.1.1.0 255.255.255.252 4.4.4.1
R4(config)#ip route 1.1.1.0 255.255.255.252 8.8.8.1
R4(config)#ip route 2.2.2.0 255.255.255.252 10.10.10.1
R4(config)#ip route 2.2.2.0 255.255.255.252 4.4.4.1
R4(config)#ip route 2.2.2.0 255.255.255.252 8.8.8.1
R4(config)#ip route 6.6.6.0 255.255.255.252 10.10.10.1
R4(config)#ip route 6.6.6.0 255.255.255.252 4.4.4.1
R4(config)#ip route 6.6.6.0 255.255.255.252 8.8.8.1
R4(config)#ip route 5.5.5.0 255.255.255.252 10.10.10.1
R4(config)#ip route 5.5.5.0 255.255.255.252 4.4.4.1
R4(config)#ip route 5.5.5.0 255.255.255.252 8.8.8.1
R4(config)#ip route 7.7.7.0 255.255.255.252 10.10.10.1
R4(config)#ip route 7.7.7.0 255.255.255.252 4.4.4.1
R4(config)#ip route 7.7.7.0 255.255.255.252 8.8.8.1
R4(config)#ip route 3.3.3.0 255.255.255.252 10.10.10.1
R4(config)#ip route 3.3.3.0 255.255.255.252 4.4.4.1
R4(config)#ip route 3.3.3.0 255.255.255.252 8.8.8.1
R4(config)#do write memory
```

### Configuración Básica - R5

```bash
Router>enable
Router#conf t
Router(config)#hostname R5
R5(config)#int S0/0/0
R5(config-if)#ip add 3.3.3.2 255.255.255.252
R5(config-if)#no shut
R5(config-if)#int S0/0/1
R5(config-if)#ip add 6.6.6.2 255.255.255.252
R5(config-if)#no shut
R5(config-if)#int S0/1/0
R5(config-if)#ip add 7.7.7.1 255.255.255.252
R5(config-if)#no shut
R5(config-if)#int g0/0
R5(config-if)#ip add 192.168.3.1 255.255.255.0
R5(config-if)#no shut
R5(config-if)#exit
R5(config)#ip dhcp excluded-address 192.168.3.1
R5(config)#ip dhcp pool R5-DHCP
R5(dhcp-config)#network 192.168.3.0 255.255.255.0
R5(dhcp-config)#default-router 192.168.3.1
R5(dhcp-config)#do write memory
R5(dhcp-config)#exit
R5(config)#ip route 192.168.1.0 255.255.255.0 3.3.3.1
R5(config)#ip route 192.168.1.0 255.255.255.0 6.6.6.1
R5(config)#ip route 192.168.1.0 255.255.255.0 7.7.7.2
R5(config)#ip route 192.168.2.0 255.255.255.0 3.3.3.1
R5(config)#ip route 192.168.2.0 255.255.255.0 6.6.6.1
R5(config)#ip route 192.168.2.0 255.255.255.0 7.7.7.2
R5(config)#ip route 192.168.4.0 255.255.255.0 3.3.3.1
R5(config)#ip route 192.168.4.0 255.255.255.0 6.6.6.1
R5(config)#ip route 192.168.4.0 255.255.255.0 7.7.7.2
R5(config)#ip route 1.1.1.0 255.255.255.252 3.3.3.1
R5(config)#ip route 1.1.1.0 255.255.255.252 6.6.6.1
R5(config)#ip route 1.1.1.0 255.255.255.252 7.7.7.2
R5(config)#ip route 2.2.2.0 255.255.255.252 3.3.3.1
R5(config)#ip route 2.2.2.0 255.255.255.252 6.6.6.1
R5(config)#ip route 2.2.2.0 255.255.255.252 7.7.7.2
R5(config)#ip route 4.4.4.0 255.255.255.252 3.3.3.1
R5(config)#ip route 4.4.4.0 255.255.255.252 6.6.6.1
R5(config)#ip route 4.4.4.0 255.255.255.252 7.7.7.2
R5(config)#ip route 5.5.5.0 255.255.255.252 3.3.3.1
R5(config)#ip route 5.5.5.0 255.255.255.252 6.6.6.1
R5(config)#ip route 5.5.5.0 255.255.255.252 7.7.7.2
R5(config)#ip route 8.8.8.0 255.255.255.252 3.3.3.1
R5(config)#ip route 8.8.8.0 255.255.255.252 6.6.6.1
R5(config)#ip route 8.8.8.0 255.255.255.252 7.7.7.2
R5(config)#ip route 10.10.10.0 255.255.255.252 3.3.3.1
R5(config)#ip route 10.10.10.0 255.255.255.252 6.6.6.1
R5(config)#ip route 10.10.10.0 255.255.255.252 7.7.7.2
R5(config)#do write memory
```

### Configuración Básica - R6

```bash
Router>enable
Router#conf t
Router(config)#hostname R6
R6(config)#int S0/0/0
R6(config-if)#ip add 5.5.5.2 255.255.255.252
R6(config-if)#no shut
R6(config-if)#int S0/0/1
R6(config-if)#ip add 8.8.8.1 255.255.255.252
R6(config-if)#no shut
R6(config-if)#int S0/1/0
R6(config-if)#ip add 7.7.7.2 255.255.255.252
R6(config-if)#no shut
R6(config-if)#int g0/0
R6(config-if)#ip add 192.168.4.1 255.255.255.0
R6(config-if)#no shut
R6(config-if)#exit
R6(config)#ip dhcp excluded-address 192.168.4.1
R6(config)#ip dhcp pool R6-DHCP
R6(dhcp-config)#network 192.168.4.0 255.255.255.0
R6(dhcp-config)#default-router 192.168.4.1
R6(dhcp-config)#do write memory
R6(dhcp-config)#exit
R6(config)#ip route 192.168.1.0 255.255.255.0 5.5.5.1
R6(config)#ip route 192.168.1.0 255.255.255.0 7.7.7.1
R6(config)#ip route 192.168.1.0 255.255.255.0 8.8.8.2
R6(config)#ip route 192.168.2.0 255.255.255.0 5.5.5.1
R6(config)#ip route 192.168.2.0 255.255.255.0 7.7.7.1
R6(config)#ip route 192.168.2.0 255.255.255.0 8.8.8.2
R6(config)#ip route 192.168.3.0 255.255.255.0 5.5.5.1
R6(config)#ip route 192.168.3.0 255.255.255.0 7.7.7.1
R6(config)#ip route 192.168.3.0 255.255.255.0 8.8.8.2
R6(config)#ip route 1.1.1.0 255.255.255.252 5.5.5.1
R6(config)#ip route 1.1.1.0 255.255.255.252 7.7.7.1
R6(config)#ip route 1.1.1.0 255.255.255.252 8.8.8.2
R6(config)#ip route 3.3.3.0 255.255.255.252 5.5.5.1
R6(config)#ip route 3.3.3.0 255.255.255.252 7.7.7.1
R6(config)#ip route 3.3.3.0 255.255.255.252 8.8.8.2
R6(config)#ip route 2.2.2.0 255.255.255.252 5.5.5.1
R6(config)#ip route 2.2.2.0 255.255.255.252 7.7.7.1
R6(config)#ip route 2.2.2.0 255.255.255.252 8.8.8.2
R6(config)#ip route 6.6.6.0 255.255.255.252 5.5.5.1
R6(config)#ip route 6.6.6.0 255.255.255.252 7.7.7.1
R6(config)#ip route 6.6.6.0 255.255.255.252 8.8.8.2
R6(config)#ip route 10.10.10.0 255.255.255.252 5.5.5.1
R6(config)#ip route 10.10.10.0 255.255.255.252 7.7.7.1
R6(config)#ip route 10.10.10.0 255.255.255.252 8.8.8.2
R6(config)#ip route 4.4.4.0 255.255.255.252 5.5.5.1
R6(config)#ip route 4.4.4.0 255.255.255.252 7.7.7.1
R6(config)#ip route 4.4.4.0 255.255.255.252 8.8.8.2
R6(config)#do write memory
```

## Cisco Packet Tracer

* Archivo con el ejercicio realizado: `clase12-practica6.pkt`