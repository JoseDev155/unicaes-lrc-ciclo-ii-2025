# Práctica 1 (LRC) - 9/7/2025

## Clasificación de redes

Cuarto octeto igual a `0`:

`/24` => 255.255.255.0

Cuarto octeto igual a `252`:

`/30` => 255.255.255.252

4 ip => 2 son utilizables

1er => Id de Red
4 => Broadcast

1.1.1.0 => 1.1.1.1, 1.1.1.2

AP = Punto de accedo

## Configuración de Routers

### Router0

Conf. básica de R. Lunes

```bash
Router>enable
# Modo exe privilegiado
Router#configure terminal
# Modo de configuración global
Router(config)#hostname lunes
lunes(config)#interface g0/0
lunes(config-if)#ip address 192.168.1.1 255.255.255.0
lunes(config-if)#no shutdown
lunes(config-if)#int g0/1
lunes(config-if)#ip add 192.168.2.1 255.255.255.0
lunes(config-if)#no shut
lunes(config-if)#int g0/2
lunes(config-if)#ip add 192.168.3.1 255.255.255.0
lunes(config-if)#no shut
lunes(config-if)#int Se0/0/0
lunes(config-if)#ip add 1.1.1.1 255.255.255.252
lunes(config-if)#no shutdown
```

Configuración del servidor DHCP

```bash
lunes(config-if)#exit
lunes(config)#ip dhcp excluded-address 192.168.1.1 192.168.1.105
lunes(config)#ip dhcp pool L1
lunes(dhcp-config)#network 192.168.1.0 255.255.255.0
lunes(dhcp-config)#default-router 192.168.1.1
lunes(dhcp-config)#exit
lunes(config)#ip dhcp excluded-address 192.168.2.1
lunes(config)#ip dhcp pool L2
lunes(dhcp-config)#network 192.168.2.0 255.255.255.0
lunes(dhcp-config)#default-router 192.168.2.1
lunes(dhcp-config)#exit
lunes(config)#ip dhcp excluded-address 192.168.3.1
lunes(config)#ip dhcp pool L3
lunes(dhcp-config)#network 192.168.3.0 255.255.255.0
lunes(dhcp-config)#default-router 192.168.3.1
lunes(dhcp-config)#exit
lunes(config)#do write memory
```

### Router1

Conf. básica de R. Miercoles

```bash
Router>enable
Router#configure terminal
Router(config)#hostname miercoles
miercoles(config)#int Se0/0/0
miercoles(config-if)#ip add 1.1.1.2 255.255.255.252
miercoles(config-if)#no shut
miercoles(config-if)#int gi0/0
miercoles(config-if)#ip add 192.168.4.1 255.255.255.0
miercoles(config-if)#no shut
miercoles(config-if)#int gi0/1
miercoles(config-if)#ip add 192.168.5.1 255.255.255.0
miercoles(config-if)#no shut
miercoles(config-if)#int gi0/2
miercoles(config-if)#ip add 192.168.6.1 255.255.255.0
miercoles(config-if)#no shut
```

Configuración del servidor DHCP

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
miercoles(dhcp-config)#exit
miercoles(config)#do write memory
```

## Activar DHCP en dispositivos

* Hacemos clic sobre el dispositivo
* Nos vamos a **Desktop** > **IP Configuration**
* Y cambiamos la opción **Static** por **DHCP**

## Cisco Packet Tracer

* Archivo con el ejercicio realizado: `clase2-practica1.pkt`