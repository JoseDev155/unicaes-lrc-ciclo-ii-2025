# Teórica 2 (LRC) - 14/7/2025

No hubo clase :) pero se nos dejó la diapositiva en plataforma.

## **Diapositiva: Configuración básica del dispositivo**

### Objetivos del módulo

1. Configurar un swith con ajustes iniciales
2. Configurar puertos del switch
3. Acceso remoto seguro
4. Configuración básica de un router
5. Verificar redes conectadas directamente

### 1.1 Configurar un swith con ajustes iniciales

#### Secuencia de inicio del switch

* Paso 1: Autoprueba de encendido (POST)
* Paso 2: Carga del cargador de arranque
* Paso 3: Inicialización de CPU
* Paso 4: Inicialización del sistema de archivos
* Paso 5: Carga del IOS

#### El comando del sistema de arranque

```bash
S1(config)# boot system flash:/c2960-lambsek9-mz.150-2.SE/ c2960-lambsek9-mz.150-2.SE.bin
```

| Comando                          | Definición                       |
| -------------------------------- | -------------------------------- |
| `boot system`                    | El comando principal             |
| `flash:`                         | El dispositivo de almacenamiento |
| `c2960-lambsek9-mz.150-2.SE/`    | La ruta al sistema de archivos   |
| `c2960-lambsek9-mz.150-2.SE.bin` | El nombre del archivo IOS        |

#### Interruptor de indicadores LED

El botón Mode se usa para moverse entre los diferentes modos: STAT, DUPLX, SPEED y PoE.

#### Recuperación de un bloqueo del sistema

1. Conectar PC mediante cable de consola
2. Desenchufar el cable de alimentación
3. Reconectar ek cable y presionar el botón Mode
4. Mantener el botón Mode presionado
5. Acceder al modo de cargador de arranque

#### Acceso a la administración de conmutadores

Para preparar un switch para el acceso de administración remota, debe configurarse con una dirección IP y una máscara de subred.

La administración remota requiere configurar correctamente el SVI con una dirección IP única en la red y una puerta de enlace predeterminada
para acceder desde otras redes.

#### Configuración de Switch SVI

De forma predeterminada el switch está configurado para controlar su administración a través de la VLAN1. Todos los puertos están asignados a
la VLAN1 de forma predeterminada.

*Por motivos de seguridad, se considera una buena práctica utilizar una VLAN distinta a la VLAN1 para la VLAN de gestión*.

**Paso 1 Configure la interfaz de administración**

Desde el modo de configuración de la interfaz VLAN, se aplica una dirección IPv4 y una máscara de subred al SVI de administración del
switch.

#### Ejemplo de configuración de switch SVI

Configurar la interfaz de administración IPv4/IPv6

| Tarea                                                               | Comandos de IOS                                        |
| ------------------------------------------------------------------- | ------------------------------------------------------ |
| Ingrese al modo de configuración global.                            | `S1# configure terminal`                               |
| Ingrese al modo de configuración de interfaz para el SVI.           | `S1(config)# interface vlan 99`                        |
| Configure la dirección IPv4 de la interfaz de administración.       | `S1(config-if)# ip address 172.17.99.11 255.255.255.0` |
| Configurar la dirección IPv6 de la interfaz de administración.      | `S1(config-if)# ipv6 address 2001:db8:acad:99::1/64`   |
| Habilite la interfaz de administración.                             | `S1(config-if)# no shutdown`                           |
| Regrese al modo EXEC privilegiado.                                  | `S1(config-if)# end`                                   |
| Guarde la configuración en ejecución en la configuración de inicio. | `S1# copy running-config startup-config`               |

#### Configuración de la puerta de enlace predeterminada

**Paso 2: Configurar la puerta de enlace predeterminada**

| Tarea                                                               | Comandos de IOS                              |
| ------------------------------------------------------------------- | -------------------------------------------- |
| Ingrese al modo de configuración global.                            | `S1# configure terminal`                     |
| Configure la puerta de enlace predeterminada para el conmutador.    | `S1(config)# ip default-gateway 172.17.99.1` |
| Regrese al modo EXEC privilegiado.                                  | `S1(config-if)# end`                         |
| Guarde la configuración en ejecución en la configuración de inicio. | `S1# copy running-config startup-config`     |

#### Verificación de la configuración SVI

**Paso 3: Verificar configuración**

```bash
S1# show ip interface brief
Interface   IP-Address      OK? Method  Status  Protocol
Vlan99      172.17.99.11    YES Manual  down    down
(output omitted)
S1# show ipv6 interface brief
Vlan99                  [down/down]
    FE80::C27B:BCFF:FEC4:A9C1
    2001:DB8:ACAD:99::1
(output omitted)
```

Otros comandos útiles para verificar la configuración incluyen:
* `show runnin-config` - Muestra la configuración actual
* `show vlan` - Muestra información de las VLANs configuradas
* `ping` - Verifica la conectividad con otros dispositivos

### 1.2 Configurar puertos de conmutador

#### Comunicación dúplex

##### Full-Duplex

Permite transmisión y recepción simultánea de datos

##### Half-Duplex

Permite transmisión de datos en una sola dirección a la vez

#### Configuración de puertos de switch en la capa física

* Configuración automática
* Configuración manual

#### Configuración de puertos de switch en la capa física

| Tarea                                                               | Comandos de IOS                          |
| ------------------------------------------------------------------- | ---------------------------------------- |
| Ingrese al modo de configuración global.                            | `S1# configure terminal`                 |
| Ingrese al modo de configuración de la interfaz.                    | `S1(config)# interface FastEthernet 0/1` |
| Configure la interfaz dúplex.                                       | `S1(config-if)# duplex full`             |
| Configure la velocidad de la interfaz.                              | `S1(config-if)# speed 100`               |
| Regrese al modo EXEC privilegiado.                                  | `S1(config-if)# end`                     |
| Guarde la configuración en ejecución en la configuración de inicio. | `S1# copy running-config startup-config` |

**Opciones de configuración:**

* **Duplex**: auto, full, half
* **Speed**: auto, 10, 100, 1000

#### Auto-MDIX

Cuando se habilita el cruce automático de la interfaz dependiente del medio (auto-MDIX), la interfaz del switch detecta automáticamente el tipo
de conexión de cable requerido (directo o cruzado) y configura la conexión de manera adecuada.

La función auto-MDIX está habilitada de forma prefeterminada en los switches Catalyst 2960 y Catalyst 3560, pero no está disponible en los
switches Catalyst 2850 y Catalyst 3550 más antiguos.

Para examinar la configuración de auto-MDIX oara una interfaz específica, usa el comando `show controllers ethernet-controller` con la
variante `phy`. Para limitar la salida a las líneas que hacen referencia a auto-MDIX.

```bash
S1# show controllers ethernet-controller fa0/1 phy | include MDIX Auto-MDIX : On [AminState=1 Flags=0x00052248]
```

#### Comandos de verificación del switch

**Comados de estado de interfaces**

* `show interfaces [interface-id]` - Muestra el estado y la configuración de la interfaz.
* `show ip interface [interface-id]` - Muestra información de IP sobre una interfaz.
* `show ipv6 interface [interface-id]` - Muestra información IPv6 sobre una interfaz.

**Comandos de configuración**

* `show startup-config` - Muestra la configuración de inicio actual.
* `show running-config` - Muestra la configuración actual en ejecución.
* `show flash` - Muestra la información sobre el sistema de archivos flash.

**Comandos del sistema**

* `show version` - Muestra el estado del hardware y software del sistema.
* `show history` - Muestra el historial del comando ingresado.
* `show mac-address-table` o `show mac-address-table` - Muestra la tabla de direcciones MAC.