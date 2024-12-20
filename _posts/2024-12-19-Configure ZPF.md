---
layout: post
title: Packet Tracer - Configure ZPF
date: 2024-12-19 21:30:00
description: Configuración de un ZPF
tags: SOC, Packet Tracer, Configuración redes, ciberseguridad, Network Defense, ipv6, ZPF
categories: Seguridad Informática
thumbnail: assets/img/logo-cisco.svg
featured: true
---

# **Datos Generales**
- **Software**: Cisco - Packet Tracer
- **Dificultad**: Media
- **Duracion**: 30 minutos
- **Observaciones**: Configuración básica de una ZPF.

## **Tabla de direccionamiento**
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ZPF-01.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ZPF-08.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Objetivos**
- Verificar la conectividad entre dispositivos antes de la configuración del Firewall.
- Configurar una zone-based policy firewall (ZPF) en el router R3.
- Verficar la funcionalidad del ZPF.

### **Instrucciones**
#### **Parte 1 - Verificar la conectividad entre dispositivos previo a la configuración del Firewall**

**Desde PC-C**
`ping 192.168.3.3`

**Desde PC-A**

`ping 192.168.1.3`

**Desde PC-C**

`http://192.168.3.3`

**Desde PC-A**

`http://192.168.1.3`

**Estableciendo sesión SSH por la interface S/0/0/1 en R2 desde ambas Pcs**

Desde pc-a y pc-c

`C:\>ssh -l Admin 10.2.2.2`


#### **Parte 2 - Creación de 2 zonas seguras en R3 - estas deben ser interna y externa**

- **a.** Creando las zonas IN-ZONE Y OUT-ZONE<br>
**Comandos implementados**
    ```
    R3#conf ter
    R3(config)#zone security IN-ZONE
    R3(config-sec-zone)#exit
    R3(config)#zone security OUT-ZONE
    R3(config-sec-zone)#
    ```


<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ZPF-02.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>


#### **Parte 3: Configuración de un class map**

configurar un class map que coincida con todas las direcciones IP de la red interna. Primero, crear una ACL que defina la red interna en R3. También crear un map-class para inspeccionar el tráfico interno.

- **a.** Creación de la class map<br>

**Comandos implementados**
```
R3(config)#access-list 101 permit ip 192.168.3.0 0.0.0.255 any
R3(config)#class-map type inspect match-all IN-NET-CLASS-MAP
R3(config-cmap)#match access-group 101
R3(config-cmap)#exit
```
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ZPF-03.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

#### **Parte 4: Configurar y aplicar las póliticas de Firewall**

Crear un policy map para inspeccionar el tráfico

**Comandos implementados**

```
R3(config)#policy-map type inspect IN-2-OUT-PMAP
R3(config-pmap)#class type inspect IN-NET-CLASS-MAP
R3(config-pmap-c)#inspect
R3(config-pmap-c)#
```
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ZPF-04.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

Definir las zonas de origen y destino especificadas en el inciso anterior

```
R3(config)#zone-pair security IN-2-OUT-ZPAIR source IN-ZONE destination OUT-ZONE
R3(config-sec-zone-pair)#service-policy type inspect IN-2-OUT-PMAP
R3(config-sec-zone-pair)#
```
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ZPF-05.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

#### **Parte 5: Asignación de la interfaz a las zonas de seguridad creadas**

Asignamos la interfaz correcta a la zona de seguridad interna en R3

**Comandos implementados**
```
R3(config)#interface g0/1
R3(config-if)#zone-member security IN-ZONE
R3(config-if)#
```
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ZPF-06.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>


Asignamos la interfaz correcta a la zona de seguridad externa en R3

**Comandos implementados**
```
R3(config)#interface s0/0/1
R3(config-if)#zone-member security OUT-ZONE
R3(config-if)#
```
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ZPF-07.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

**Nota:**
Este laboratorio es parte del curso **Network Defense** de Cisco Network Academy