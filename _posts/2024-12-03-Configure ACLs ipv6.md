---
layout: post
title: Packet Tracer - Configure ACLs ipv6
date: 2024-12-09 22:20:00
description: Configuración de ACLs en ipv6
tags: SOC, Packet Tracer, Configuración redes, ciberseguridad, Network Defense, ipv6
categories: Seguridad Informática
thumbnail: assets/img/logo-cisco.svg
featured: false
---

# **Datos Generales**
- **Software**: Cisco - Packet Tracer
- **Dificultad**: Media
- **Duracion**: 30 minutos
- **Observaciones**: Configuración básica para denegación y acceso a una red ipv6.

## **Tabla de direccionamiento**
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv610.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv609.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Objetivos**
- Parte 1: Configurar, aplicar y verificar una ACL ipv6
- Parte 2: Configurar, aplicar y verificar una segunda ACL ipv6

### **Instrucciones**
#### **Parte 1 - Configurar una ACL Named Extended ACL**
Los logs muestran que una computadora en la red 2001:db8:1:11::0/64 está actualizando repetidamente una página web. Esto está provocando un ataque (DoS) a Server3. Hasta que se pueda identificar y limpiar el cliente, se debe bloquear el acceso HTTP y HTTPS a esa red.

**Paso 1: Configurar una ACL que bloquee el acceso HTTP y HTTPS**

- **a.** Bloquear el acceso HTTP y HTTPS a Server3 <br>
    ```
    R1(config)# deny tcp any host 2001:db8:1:30::30 eq www
    R1(config)# deny tcp any host 2001:db8:1:30::30 eq 443
    ```
- **b.** Permitir todo otro tráfico ipv6 <br>

**Comandos implementados**
```
R1#configure terminal
R1(config)#IPv6 access list BLOCK_HTTP
R1(config-ipv6-acl)#deny tcp any host 2001:DB8:1:30::30 eq www
R1(config-ipv6-acl)#deny tcp any host 2001:DB8:1:30::30 eq 443
R1(config-ipv6-acl)#permit ipv6 any any
R1(config-ipv6-acl)#exit
```
**Paso 2: Aplicar la ACL a la interfaz correcta**

- **a.** Aplicar la ACL en la interfaz más cercana a la fuente del tráfico que se bloqueará.<br>

**Comandos implementados**
```
R1(config)#interface gigabitEthernet0/1
R1(config-if)#ipv6 traffic-filter BLOCK_HTTP in
```
**Paso 3: Verificar la implementación de la ACL**
- desde el navegador de la PC1 la ip http://2001:db8:1:30::30 o https://2001:db8:1:30::30 deberia desplegarse<br>
- desde el navegador de la PC2 la ip http://2001:db8:1:30::30 o https://2001:db8:1:30::30 no deberia desplegarse<br>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv602.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### **Parte 2 - Configurar aplicar y verificar una segunda ACL ipv6**

Los logs ahora indican que el servidor esta recibiendo pings desde diferentes direccioens ipv6 en un ataque DDoS. Se debe filtrar las peticiones ping ICMO del servidor.

**Paso 1: Crear una lista de acesso para bloquear ICMP**

Configuramos una ACL llamada BLOCK_ICMP en R3 con las siguientes cracteristicas:

- **a.** Bloquear todo el tráfico ICMP desde cualquier host a cualquier destino <br>
- **b.** Permitir todo el tráfico ipv6 restante <br>

**Comandos implementados**
```
R3>en
R3#configure terminal
R3(config)#ipv6 access-list BLOCK_ICMP
R3(config-ipv6-acl)#deny icmp any any
R3(config-ipv6-acl)#permit ipv6 any any
```
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv604.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

**Paso 2: Aplicar la ACL a la interfaz correcta**
En este caso, el tráfico ICMP puede venir desde cualquier fuente. Para asegurar que el tráfico sea bloqueado independientemente de su origen, aplicar la ACL más cercana al destino.

**Verificamos la interfaz mas cercana**
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv605.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

**Comandos implementados**

```
R3#show ip interface brief
R3#configure terminal
R3(config)#interface gigabitEthernet0/0
R3(config-if)#ipv6 traffic-filter BLOCK_ICMP OUT
```
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv606.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

**Paso 3: Verificamos**
- El ping desde PC2 a 2001:db8:1:30::30 debería fallar <br>
- El ping desde PC1 a 2001:db8:1:30::30 debería fallar <br>
- La navegación desde PC1 a 2001:db8:1:30::30 debería desplegarse <br>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv607.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ACLS_ipv608.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

**Nota:**
Este laboratorio es parte del curso **Network Defense** de Cisco Network Academy