# Teórica 4 (LRC) - 28/7/2025

Evaluación de los temas:

* **Por qué es necesario el Routing**.
* **Configuración básica del dispositivo**.
* **Conceptos de conmutación**.

## Primera Evaluación de LR - 25% (resuelto)

### **Parte I - 50% - Opción Múltiple**

1. ¿Cuál de los siguientes elementos es esencial para realizar el proceso de routing?

* a) switch
* b) router
* c) repetidor
* d) hub

Mi respuesta: b)<br>
**Respuesta correcta:** b)

2. ¿Cuál es una ventaja principal del routing dinámico sobre el estático?

* a) switch
* b) router
* c) repetidor
* d) hub

Mi respuesta: b)<br>
**Respuesta correcta:** b)

3. ¿Qué protocolo de routing utiliza como métrica principal el conteo de saltos?

* a) ospf
* b) bgp
* c) rip
* d) is-is

Mi respuesta: c)<br>
**Respuesta correcta:** c)

4. ¿Cuál de estos beneficios está directamente asociado al uso de routing eficiente?

* a) mayores requerimientos de hardware
* b) reducción de latencia
* c) incremento en la congestión
* d) aumento del tráfico broadcast

Mi respuesta: b)<br>
**Respuesta correcta:** b)

5. ¿Qué tipo de routing es más recomendable para redes grandes y complejas?

* a) routing manual
* b) routing por dhcp
* c) routing estático
* d) routing dinámico

Mi respuesta: d)<br>
**Respuesta correcta:** d)

6. ¿Cuál es el propósito principal de la VLAN de administración en un switch Cisco?

* a) Enrutar tráfico entre VLANs
* b) Acceder al switch de forma remota
* c) Asignar direcciones MAC
* d) Habilitar PoE

Mi respuesta: d)<br>
**Respuesta correcta:** b)

7. ¿Qué archivo contiene la configuración de inicio del switch?

* a) startup-config.txt
* b) ios-config.bin
* c) config.text
* d) boot.bin

Mi respuesta: a)<br>
**Respuesta correcta:** c)

8. ¿Cuál es una ventaja principal del routing dinámico sobre el estático?

* a) show vlan
* b) show mac-address-table
* c) show interface vlan
* d) show arp

Mi respuesta: d)<br>
**Respuesta correcta:** b)

9. ¿Qué sucede si se configuran velocidades distintas en los extremos de una conexión?

* a) Se incrementa el rendimiento
* b) Se activa el modo Auto-MDIX
* c) Puede haber fallos de conectividad
* d) Se crea un dominio de broadcast

Mi respuesta: b)<br>
**Respuesta correcta:** c)

10. ¿Qué comando permite establecer manualmente el dúplex de una interfaz?

* a) duplex-mode full
* b) interface duplex full
* c) duplex full
* d) speed full

Mi respuesta: a)<br>
**Respuesta correcta:** c)

### **Parte II - Complete correctamente cada una de las respuestas de las preguntas - 50%**

1. El comando que permite ver el archivo de configuración de inicio actual del IOS es _________________________________________.

Mi respuesta: `show ios-config`<br>
**Respuesta correcta:** `show boot`

2. El modo dúplex que permite transmisión y recepción simultánea se llama _________________________________________.

Mi respuesta: Full dúplex<br>
**Respuesta correcta:** Full dúplex

3. Para ingresar al modo de configuración global en un switch se usa el comando _________________________________________.

Mi respuesta: `configure terminal`<br>
**Respuesta correcta:** `configure terminal`

4. El nombre del archivo que contiene la configuración de inicio en un switch Cisco es _________________________________________.

Mi respuesta: `startup-config.txt`<br>
**Respuesta correcta:** `config.text`

5. La dirección IP de administración se configura en la interfaz virtual conocida como _________________________________________.

Mi respuesta: Id de red<br>
**Respuesta correcta:** SVI -> Switched Virtual Interface

6. El algoritmo _______________________ calcula rutas con base en la distancia en saltos y es usado por RIP.

Mi respuesta: vector-distancia<br>
**Respuesta correcta:** Bellman-Ford

7. En el routing _______________________, los paquetes se envían a todos los dispositivos de una red.

Mi respuesta: dinámico<br>
**Respuesta correcta:** Broadcast

8. El routing puede reducir hasta un _______________________% el consumo de ancho de banda si se optimizan las rutas.

Mi respuesta: 60<br>
**Respuesta correcta:** 40

9. El protocolo _______________________ conecta sistemas autónomos en Internet y maneja políticas complejas.

Mi respuesta: BGP<br>
**Respuesta correcta:** BGP

1.  Las listas de control de acceso (ACL) se usan en routing para _________________________________________.

Mi respuesta: " "<br>
**Respuesta correcta:** Filtrar Paquetes