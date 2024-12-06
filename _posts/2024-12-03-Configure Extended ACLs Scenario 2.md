---
layout: post
title: Packet Tracer - Configure Extended ACLs Scenario 2
date: 2024-12-03 22:20:00
description: Configuración de ACLs extendidos
tags: SOC, Packet Tracer, Configuración redes, ciberseguridad, Network Defense
categories: Seguridad Informática
thumbnail: assets/img/logo-cisco.svg
featured: true
---

# **Datos Generales**
- **Software**: Cisco - Packet Tracer
- **Dificultad**: Media
- **Duracion**: 30 minutos
- **Observaciones**: Configuración básica para denegación y acceso a una red.

## **Tabla de direccionamiento**
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/SOC_ACL2-04.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/SOC_ACL2-05.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Objetivos**
- Parte 1: Configurar una ACL Named Extended ACL
- Parte 2: Aplicar y verificar la ACL

### **Escenario**
Permitir a dispositivos especificos de la LAN acceder a servidores y servicios ubicados en la red.

### **Instrucciones**
#### **Parte 1 - Configurar una ACL Named Extended ACL**
Configurar la ACL para implementar las siguientes politicas:
- Bloquear el acceso HTTP y HTTPS al Server1 y Server2 desde la PC1. Los servidores están en la nube y solo se conoce sus direcciones IP. 
- Bloquear el acceso FTP al Server1 y Server2 desde la PC2.
- Bloquear el acceso ICMP al Server1 y Server2 desde la PC3.

**Paso 1: Denegar el acceso a los servicios HTTP Y HTTPS de Server1 y Server2 a la PC1**
- **a.** Crear una ACL para IP en el router RT1 que denegara el acceso a la PC1 a los servicios HTTP y HTTPS del Server1 y Server2. 

**Pregunta:**
¿Cuál es el comando para iniciar la configuración de una lista de acceso extendida con el nombre ACL?
- ```ip access-list extended ACL```

- **b.** Denegar el acceso de PC1 a Server1, solo para HTTP (puerto 80). Usar la tabla de direcciones para obtener la dirección IP de PC1 y Server1. <br>
    ```RT1(config-ext-nacl)# deny tcp host 172.31.1.101 host 64.101.255.254 eq 80```
- **c.** Denegar el acceso HTTPS (port 443) de PC1 a Server1. <br>
    ```RT1(config-ext-nacl)# deny tcp host 172.31.1.101 host 64.101.255.254 eq 443```
- **d.** Denegar el acceso de PC1 a Server2, solo para HTTP (puerto 80). Usar la tabla de direcciones para obtener la dirección IP de PC1 y Server2.<br>
    ```RT1(config-ext-nacl)# deny tcp host 172.31.1.101 host 64.103.255.254 eq 80```
- **e.** Denegar el acceso HTTPS (port 443) de PC1 a Server2. <br>
    ```RT1(config-ext-nacl)# deny tcp host 172.31.1.101 host 64.103.255.254 eq 443```

**Comandos implementados**
```
RT1#conf ter
RT1(config)#ip access-list extended ACL
RT1(config-ext-nacl)#deny tcp host 172.31.1.101 host 64.101.255.254 eq 80
RT1(config-ext-nacl)#deny tcp host 172.31.1.101 host 64.101.255.254 eq 443
RT1(config-ext-nacl)#deny tcp host 172.31.1.101 host 64.103.255.254 eq 80
RT1(config-ext-nacl)#deny tcp host 172.31.1.101 host 64.103.255.254 eq 443
```
**Paso 2: Denegar el acceso a los servicios FTP de Server1 y Server2 a la PC1**

- **a.** Denegar el acceso de PC1 a Server1, solo para FTP (puerto 21)<br>
    `RT1(config-ext-nacl)# deny tcp host 172.31.1.102 host 64.101.255.254 eq 21`
- **b.** Denegar el acceso de PC1 a Server2, solo para FTP (puerto 21)<br>
    `RT1(config-ext-nacl)# deny tcp host 172.31.1.102 host 64.103.255.254 eq 21`

**Comandos implementados**
```
RT1(config-ext-nacl)#deny tcp host 172.31.1.102 host 64.101.255.254 eq 21
RT1(config-ext-nacl)#deny tcp host 172.31.1.102 host 64.103.255.254 eq 21
```
**Paso 3: Denegar el acceso de peticiones ping a Server1 y Server2 desde PC3**
- **a.** Denegar el acceso ICMP A Server1, desde la PC3<br>
    `RT1(config-ext-nacl)# deny icmp host 172.31.1.103 host 64.101.255.254`
- **b.** Denegar el acceso ICMP A Server2, desde la PC3<br>
    `RT1(config-ext-nacl)# deny icmp host 172.31.1.103 host 64.103.255.254`

**Comandos implementados**

```
RT1(config-ext-nacl)#deny icmp host 172.31.1.103 host 64.101.255.254
RT1(config-ext-nacl)#deny icmp host 172.31.1.103 host 64.103.255.254
```
**Paso 4: Permitir todo el tráfico ip**
- **a.** `permit ip any any`

**Paso 5: Verificar la configuración**

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/SOC_ACL2-01.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

#### **Parte 2 - Aplicar y verificar Extended ACL**

El tráfico que se debe filtrar proviene de la red 172.31.1.96/27 y está destinado a redes remotas. Las listas de acceso extendidas se deben colocar en la interfaz más cercana a la fuente del tráfico.

**Paso 1: Aplicar la ACL a la interfaz y direccióin correcta**

**Comandos implementados**
```
RT1#conf ter
RT1(config)#int g0/0
RT1(config-if)#ip access-group ACL in
RT1(config-if)#exit
```
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/SOC_ACL2-02.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

**Paso 2: Verficar la correcta implmentación de la ACL**

**Nota:**
Este laboratorio es parte del curso **Network Defense** de Cisco Network Academy