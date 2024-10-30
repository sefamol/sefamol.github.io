---
layout: post
title: Tony The Tiger - Java serialisation attack
date: 2024-10-29 18:00:00
description: CTF guiado que explota el la vulnerabilidad serialización de Java
tags: ctf, pentesting, ciberseguridad, Java Web App, criptografía
categories: Seguridad Informática
thumbnail: assets/img/tony.png
---

# **Datos Generales**
- **URL**: https://tryhackme.com/r/room/tonythetiger 
- **Dificultad**: Fácil
- **Flags**: Usuario y Root
- **Aprendizaje**: Explotación con metasploit, criptografía y esteganografía   


# **Conocimientos iniciales**
### Serialización
La serialización, en sentido abstracto, es el proceso de convertir **objetos en bytes**, para luego transmitirlos por la red. Posteriormente este flujo de **bytes se convierten nuevamente en objeto**. Esta conversión final se conoce como **desserialización**.
Información ampliada en el siguiente enlace:
<a href=" https://chuidiang.org/index.php?title=Serializaci%C3%B3n_de_objetos_en_java" target="_blank">Serialización de objetos en java</a>

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/serialization.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Serialización de objetos en Java.
</div>

# **El CTF** 
### Reconocimiento
Al iniciar el proceso de **reconocimiento** es común realizar la enumeración de puertos, el scaneo de directorios y de subdominios, entre otras pruebas según presente la aplicación web obejtivo.
En el caso de este ctf se obtuvo resultados de ínteres mediante el scaneo de puertos. La herramienta utilizada para ello fue  nmap. El resultado muestra que el puerto 8080 se encuentra habilitado para desplegar un servicio http. El mismo funciona utilizando la tecnología **Apache / Coyote JSP**.  

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT09.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    nmap -Pn -sC -sV ip.
</div>

Ingresando por el puerto se reconoce que se utiliza la aplicación **JBoss** para el front-end.

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT10.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Posible vulnerabilidad, aplicación JBoss para el front end.
</div>
