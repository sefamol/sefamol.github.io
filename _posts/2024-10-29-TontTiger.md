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

Ingresando por el puerto 8080 se reconoce que la aplicación **JBoss** se utiliza para el front-end.

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

## Primera Flag

Además, se pudo identificar que existe una imagen en la web, la misma se encuentra almacenada en imgur y se puede observar que contiene un mensaje oculto utilizando la herramienta **strings**.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/tonyTT11.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/tonyTT12.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Imagen de la web y hallazgo del mensaje oculto.
</div>

## Segunda Flag

Luego de obtener la primera flag, realizamos la explotación de la vulnerabilidad jboss reconocida anteriormente. Para ello descargamos el exploit desde github: https://github.com/joaomatosf/jexboss. fijamos la **ip atacante (nuestra ip)** y el **puerto** por el cual nos conectaremos.

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT01.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Ejecución del exploit.
</div>

Para mantener funcional el exploit utilizaremos **netcat** escuchando por el **puerto 4444**

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT02.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Ejecución del puerto en escucha.
</div>

### Hallando la flag del usuario jboss

Una vez realizado la conexión con el servidor, es posible navegar en los ficheros del usuario cmnatic. Mediante una inspección simple de los ficheros se observo la carpeta **jboss**. utilizando el comando **ls -la** se puede observar el archivo .jboss.txt el mismo que es posible desplegar utilizando el comando cat.

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT03.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Visualización de la flag del usuario jboss.
</div>

### Escalamiento

Además, en el mismo fichero encontramos el archivo note, que contiene información útil para el escalamiento

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT04.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Contenido del archivo note.
</div>

Posteriormente hacemos más amigable la terminal y logeamos con el usuario jboss

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT05.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Estabilización de la tty y acceso a la cuenta jboss.
</div>

### Obteniendo la flag de root

Dentro la cuenta de jboss podemos intentar acceder a la carpeta root, a la cual no tenemos permiso para acceder. Explotando una vulnerabilidad de comandos en linux es posible acceder como usuario root. El payload se encuentra en https://gtfobins.github.io/gtfobins/find/#sudo Accediendo al fichero root, se puede observar el documento root.txt el cual contiene un mensaje en base64

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT06.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Escalamiento vertical a la cuenta del usuario root.
</div>

Utilizando ciberchef.org se pudo determinar el valor del mensaje, el cual es un hash que es posible determinar mediante uso de bibliotecas.

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT07.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Determinación del mensaje utilizando cyberchef.
</div>

Finalmente obtenemos el valor de la flag

<div class="row mt-3 justify-content-center">
    <div class="col-8 col-sm-6 col-md-4 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/tonyTT08.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Obtención del valor de la flag de root.
</div>