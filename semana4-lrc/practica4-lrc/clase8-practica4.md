# Práctica 4 (LRC) - 30/7/2025

Mismo ejercicio y configuración de la **Práctica 3**.

## Configuración Básica - Enrutamiento estático - Ruta por defecto

### lunes

```bash
lunes>enable
lunes#conf t
lunes(config)#ip route 0.0.0.0 0.0.0.0 1.1.1.2
lunes(config)#ip route 0.0.0.0 0.0.0.0 3.3.3.2
lunes(config)#ip route 0.0.0.0 0.0.0.0 6.6.6.2
lunes(config)#do write memory
```

### Miercoles

```bash
Miercoles>ena
Miercoles#conf t
Miercoles(config)#ip route 0.0.0.0 0.0.0.0 1.1.1.1
Miercoles(config)#ip route 0.0.0.0 0.0.0.0 2.2.2.2
Miercoles(config)#ip route 0.0.0.0 0.0.0.0 7.7.7.2
Miercoles(config)#do write memory
```

### Redes

```bash
Redes>ena
Redes#conf t
Redes(config)#ip route 0.0.0.0 0.0.0.0 2.2.2.1
Redes(config)#ip route 0.0.0.0 0.0.0.0 5.5.5.2
Redes(config)#ip route 0.0.0.0 0.0.0.0 8.8.8.2
Redes(config)#do write memory
```

### unicaes

```bash
unicaes>ena
unicaes#conf t
unicaes(config)#ip route 0.0.0.0 0.0.0.0 5.5.5.1
unicaes(config)#ip route 0.0.0.0 0.0.0.0 3.3.3.1
unicaes(config)#ip route 0.0.0.0 0.0.0.0 4.4.4.2
unicaes(config)#do write memory
```

### central

```bash
central>ena
central#conf t
central(config)#ip route 0.0.0.0 0.0.0.0 6.6.6.1
central(config)#ip route 0.0.0.0 0.0.0.0 7.7.7.1
central(config)#ip route 0.0.0.0 0.0.0.0 8.8.8.1
central(config)#ip route 0.0.0.0 0.0.0.0 4.4.4.1
central(config)#do write memory
```

## Tabla de Asignación

| Dispo       | Red desco | Mask    | Ip del Sig. Salto |
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
| unicaes     |           |         | U - R<br>5.5.5.1  |
|             | 0.0.0.0   | 0.0.0.0 | U - L<br>3.3.3.1  |
|             |           |         | U - C<br>4.4.4.2  |
| central     |           |         | C - L<br>6.6.6.1  |
|             | 0.0.0.0   | 0.0.0.0 | C - M<br>7.7.7.1  |
|             |           |         | C - R<br>8.8.8.1  |
|             |           |         | C - U<br>4.4.4.1  |

## Práctica

Eliminar 4 enlaces enttre routers, y enviar paquetes de extremo a extremo.

## Configuración hecha por el docente

En la carpeta `Enrutamiento Estático Utilizando Ruta por Defecto con Ip del Siguiente Salto-20250810/`, se encuentra el paso a paso de la configuración desarrollada en la práctica.

## Cisco Packet Tracer

* Archivo con el ejercicio realizado: `clase8-practica4.pkt`