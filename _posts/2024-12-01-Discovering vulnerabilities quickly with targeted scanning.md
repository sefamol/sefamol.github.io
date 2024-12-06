---
layout: post
title: Discovering vulnerabilities quickly with targeted scanning
date: 2024-12-01 20:01:00
description: Laboratorio introductorio a la herramienta Burpsuite
tags: Burpsuite, Portswigger, pentesting, ciberseguridad, Web
categories: Seguridad Informática
thumbnail: assets/img/burp-logo.png
featured: true
---

# **Datos Generales**
- **Software**: Burpsuite Profesional 
- **Dificultad**: Fácil
- **Duracion**: 10 minutos
- **Observaciones**: Es posible hallar la vulnerabilidad utilizando la versión Community pero el laboratorio esta diseñado para realizarlo con la versional Profesional. 
- **CVSS 3.1**: AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N  **7.5 Alto**

## **Reconocimiento**
- Al ser un laboratorio inicial la vulnerabilidad se encuentra expuesta. Para iniciar la resolución, capturamos el tráfico de la página en **product/stock**. Hacemos **click derecho** y activamos **active scan** y esperamos un poco de tiempo esperando que finalice el scaneo

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Burp_lab_01-3.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

La vulnerabilidad detectada es **out-of-band resource load (HTTP)** la cual es catalogada con severidad alta.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Burp_lab_01-2.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## **Explotación**

Conociendo la vulnerabilidad, enviamos la petición a **repeater** donde la modificaremos.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Burp_lab_01-5.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Modificamos la petición en **productId** con el siguiente payload:

```test
<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo>
```
Explicación del payload

```
xmlns:xi = Declara el prefijo xi asociado al estándar XInclude.
xi:include = Utilizado para incluir contenido externo en el documento XML.
parse="text" = Indica que el contenido del recurso externo, se debe tratar como texto plano.
href="file:///etc/passwd" = Especifica la ubicación a la que se accedera. En este caso al fichero /etc/passwd.
```

### Funcionamiento del payload

Cuando este XML se procesa con un parser que soporta XInclude, el parser intenta incluir el contenido del archivo especificado en href (en este caso, file:///etc/passwd) en el documento XML. Por lo tanto, si el parser tiene acceso al sistema de archivos y no hay restricciones de seguridad, el contenido del archivo /etc/passwd será incluido en el lugar donde se define el **xi:include**.

Finalmente podemos observar la resolución del laboratorio
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Burp_lab_01-7.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## **Enlaces de interés**

Tutorial inicial con descripción de las herramientas de Burpsuite realizado por SniferLabs

<div class="row mt-3">
    <ul class="list-unstyled d-flex flex-wrap justify-content-center">
        <li class="col-12 col-sm-6 col-md-4 mt-3">
            <a href="https://www.youtube.com/watch?v=i2VL_rGDKac&list=PL4TbrTdoQBY_h0-ZxC0LbZ8Fsz7F91d1c&index=6" target="_blank" class="text-decoration-none">
                <div class="card">
                    <img src="https://yt3.googleusercontent.com/N4lYl6YUl79SgE8WgLGxWejU4DeQGNy-1HLd5CDFvnWgSsupCKbqLRiABoJDT12HpsX4Fq_5=w1707-fcrop64=1,00005a57ffffa5a8-k-c0xffffffff-no-nd-rj" class="card-img-top img-fluid rounded" alt="Thumbnail of YouTube Video">
                    <div class="card-body">
                        <h5 class="card-title">Curso de introducción a Burpsuite</h5>
                    </div>
                </div>
            </a>
        </li>
    </ul>
</div>
