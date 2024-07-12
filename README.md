<div align="center"> 
<h2>Proyecto de Red Empresarial para LinkLabs S.A.</h2>
</div>

<p align="center"> 
<img src="https://i.postimg.cc/1tbmF9DW/logo.png" alt="LinkLabs Logo" width="450"/> </p>

## Introducción

LinkLabs S.A, una empresa de TI con múltiples sedes e infraestructura de red que ha crecido rápidamente durante los últimos años, necesita una solución para sus problemas de integración y conectividad. Este proyecto tiene como objetivo diseñar y implementar una red empresarial escalable y segura que permita una comunicación fluida entre todas las sedes de la empresa.

## Objetivos de la Solución Propuesta

-   Diseñar una red empresarial escalable y segura que permita una comunicación fluida entre todas las sedes de la empresa.
-   Implementar VLAN y Inter-VLAN Routing para mejorar la seguridad y la escalabilidad de la red.
-   Utilizar Subnetting con VLSM para optimizar el uso de direcciones IP.
-   Configurar Access Lists para controlar el tráfico de red y mejorar la seguridad.


## Imágenes del diseño de la nueva red

### Topología WAN
<img src="https://i.postimg.cc/SxVmrLWY/topologia-wan.png" alt="Topología WAN" width="800"/>

### Topología sede Lima
<img src="https://i.postimg.cc/bwqzkV2j/topologia-sede-lima.png" alt="Topología Sede Lima" width="800"/>


### Topología sede Piura
<img src="https://i.postimg.cc/SKsktXrT/topologia-sede-piura.png" alt="Topología Sede Piura" width="800"/>

### Topología sede Arequipa
<img src="https://i.postimg.cc/65J65pWq/topologia-sede-arequipa.png" alt="Topología Sede Arequipa" width="800"/>

### Topología sede Cajamarca
<img src="https://i.postimg.cc/7PTYk2yj/topologia-sede-cajamarca.png" alt="Topología Sede Cajamarca" width="800"/>

### Topología sede Cusco
<img src="https://i.postimg.cc/KvPGKhjN/topologia-sede-cusco.png" alt="Topología Sede Cusco" width="800"/>

### Configuración DNS
<img src="https://i.postimg.cc/SR8y7wrm/dns-configured.png" alt="DNS" width="500"/>

### Página web de la empresa desde Cisco Packet Tracer
<img src="https://i.postimg.cc/PxvhTB01/web-packet-tracer.png" alt="Web Page" width="800"/>

### Página web de la empresa LinkLabs (vista del navegador)
<img src="https://i.postimg.cc/Y2gkVB6H/webpage.png" alt="Web Page LinkLabs" width="800"/>

## Configuración de la Red

### Creación de VLAN

-   Crear VLAN para la sede de Lima:
    -   `vlan 10`  (Administración)
    -   `vlan 20`  (Finanzas)
    -   `vlan 30`  (Logística)
    -   `vlan 40`  (Marketing)
    -   `vlan 50`  (Ventas)
    -   `vlan 80`  (Wifi Clientes)
    -   `vlan 90`  (Wifi Ejecutivos)
    -   `vlan 100`  (Servidores)

### Configuración de Access Lists

-   Crear ACL para la VLAN 80 (Wifi Clientes):
    
    -   `access-list 100 permit udp 10.6.80.64 0.0.0.31 host 10.6.81.3 eq 53`  (permitir tráfico DNS)
    -   `access-list 100 permit tcp 10.6.80.64 0.0.0.31 host 10.6.81.3 eq 53`  (permitir tráfico DNS)
    -   `access-list 100 permit tcp 10.6.80.64 0.0.0.31 host 10.6.81.5 eq 80`  (permitir tráfico HTTP)
    -   `access-list 100 deny ip 10.6.80.64 0.0.0.31 any`  (denegar tráfico no permitido)
    -   Esta ACL permite que los dispositivos en la VLAN 80 accedan a recursos DNS y web en la red, mientras que deniega cualquier otro tráfico no autorizado.
-   Crear ACL para la VLAN 50 (Ventas):
    
    -   `access-list 101 deny udp 10.6.16.192 0.0.0.63 any eq 67`  (denegar tráfico DHCP)
    -   `access-list 101 permit udp 10.6.16.192 0.0.0.63 any`  (permitir tráfico por defecto)
    -   `access-list 101 permit tcp 10.6.16.192 0.0.0.63 any`  (permitir tráfico por defecto)
    -   `access-list 101 permit ip 10.6.16.192 0.0.0.63 10.6.17.0 0.0.0.31`  (permitir tráfico entre VLANs)
    -   Esta ACL deniega que los dispositivos en la VLAN 50 accedan a recursos DHCP en la red, mientras que permite cualquier otro tráfico autorizado.

### Enrutamiento Dinámico RIP

-   Configurar enrutamiento dinámico RIP en el router de la sede de Lima:
    -   `router rip`  (habilitar RIP en el router)
    -   `version 2`  (versión de RIP)
    -   `network 10.6.17.64`  (red de la VLAN 10)
    -   `network 10.6.17.32`  (red de la VLAN 20)
    -   `network 10.6.16.0`  (red de la VLAN 30)
    -   `network 10.6.16.128`  (red de la VLAN 40)
    -   `no auto-summary`  (no resumir rutas)

## Conclusiones

Este proyecto del curso de redes y comunicación de datos ha demostrado que es posible diseñar y implementar una red empresarial escalable y segura que permita una comunicación fluida entre todas las sedes de la empresa. 
