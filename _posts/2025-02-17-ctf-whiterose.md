---
layout: post
title: Whiterose
date: 2025-02-17 17:00:00
description: CTF sencillo con escalamiento a nivel root
tags: ctf pentesting idor template injection revshell payload sudoedit
categories: Seguridad Informática
thumbnail: assets/img/whiterose_00.png
featured: true
---

# **Datos Generales**
- **URL**: https://tryhackme.com/room/whiterose
- **Dificultad**: Fácil
- **Flags**: Usuario y Root
- **Aprendizaje**: acceso a información no autorizada mediante **IDOR**, inyección de plantillas del lado del servidor **SSTI** y escalamiento de privilegios mediante abuso de permisos de administrador en aplicaciones.


# **Conocimientos iniciales**
### IDOR
Un IDOR es una vulnerabilidad que ocurre debido a errores en la implementación de controles de acceso.Permite a un atacante acceder a información o recursos dentro de la aplicación que no deberían ser accesibles para su nivel de privilegios.

Información ampliada en el siguiente enlace: <a href="https://portswigger.net/web-security/access-control/idor" target="_blank">Portswigger - IDOR</a>

### SSTI
La Inyección de Plantillas del Lado del Servidor (SSTI) es una vulnerabilidad de seguridad que ocurre cuando una aplicación web procesa entradas de usuario de manera insegura dentro de un motor de plantillas. Esto sucede cuando las entradas del usuario se concatenan directamente en una plantilla sin la debida sanitización o validación. Una aplicación vulnerable a SSTI puede permitir la ejecución remota de código (RCE), la filtración de datos sensibles o la escalada de privilegios en el servidor, lo que representa un riesgo crítico para la seguridad del sistema.


Información ampliada en el siguiente enlace: <a href="https://portswigger.net/web-security/server-side-template-injection" target="_blank">Portswigger - SSTI</a>

### abuso de privilegio root con sudoedit
La vulnerabilidad de abuso de privilegios con sudoedit se refiere a una mala configuración en sudo que permite a un usuario editar archivos con privilegios de root sin necesidad de autenticación. Esto ocurre cuando un usuario tiene permisos para ejecutar sudoedit sobre archivos sensibles, lo que puede llevar a una escalada de privilegios. 

# **El CTF** 
### Preparación
Antes de iniciar, es necesario agregar un dominio a la ip otorgada por tryhackme para desplegar la web. Esto se realiza añadiendo la url del endpoint al archivo **/etc/hosts**. Como se ve en la imagen.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-whiterose-01.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
