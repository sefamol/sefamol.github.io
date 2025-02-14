---
layout: post
title: Wikipedia - Conversión y almacenamiento de videos en formato webm
date: 2025-02-12 21:20:00
description: Tutorial para almacenar videos en Wikimedia en formato webm 
tags: wikipedia, wikimedia, webm 
categories: wikipedia
thumbnail: assets/img/wikipedia.png
featured: true
---

# **Datos Generales**
- **Plataforma**: Wikipedia, Wikimedia
- **Dificultad**: Baja
- **Duracion**: 10 minutos
- **Observaciones**: Wikipedia solo permite almacenamiento de videos en formato webm por ello la importancia de este documento

---

# **Un poco de teoría**
## **Qué es el formato webm?** 
El formato webm (codec vp8 y vp9), es un formato optimizado para la web. Es una alternativa al codec h264 (mp4) siendo su principal característica su uso libre de regalías.

Más teoría en: [https://es.wikipedia.org/wiki/WebM](https://es.wikipedia.org/wiki/WebM) y [https://www.arsys.es/blog/webm-video-pagina-web](https://www.arsys.es/blog/webm-video-pagina-web)

# **Vamos a la práctica**
## Si editas con la suite de adobe
La solución es sencilla instalando o agregando el preset para exportar en formato webm
- 1. Descargamos el preset de [https://fnord.com/](https://fnord.com/)
- 2. instalamos el paquete o copiamos el contenido de la carpeta **5765624D_5765624D** a **/Applications/Adobe Media Encoder CC 2014/Adobe Media Encoder CC 2014.app/MediaIO/systempresets/5765624D_5765624D** (sigue las instrucciones en Presets.txt del archivo descagado)
- 3. Verifica que es posible exportar en formato webm

## **Si es necesario convertir de cualquier formato a webm**
Probé software instalado en windows y paginas web de conversión. Ambos reducen la calidad del video convertido
### **Utilizando video2commons, la herramienta de wikimedia**
Esta herramienta permite la creación del archivo y simultaneamente agrega el video a la galeria de videos de wikimedia.
#### Ventajas
- Es una herramienta en línea y soporta videos de hasta 2 gb
- El codigo de la herramienta se encuentra en [https://github.com/toolforge/video2commons](https://github.com/toolforge/video2commons)
- Mantiene la calidad de video y lo prepara directamente para su uso
#### Desventajas
- Si es para un proyecto independiente no es posible eliminar el video, pero se puede  pedir la eliminación a los administradores.

### Agregando el video a video2commons
- Ingresamos a wikimedia e iniciamos sesión
- Ingresamos a [https://video2commons.toolforge.org/](https://video2commons.toolforge.org/)
- Seleccionamos el archivo a ser convertido y hacemos click en next
- Subimos el archivo 

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/webm_imagen_07es.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

- Agregamos un título al video (no se admiten caracteres especiales ni acentos)
- Esperamos a que termine de subir y convertir el video

### Agregando la licencia y descripción

Una vez almacenado el video se generará la entrada del video, la cúal hay q configurar de la siguiente manera:

- Ingresando al enlace generado veremos que no existen datos acerca del video

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/webm_imagen_01es.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

- Hacemos click en el boton **edit** a lado del título Summary y se desplegará la siguiente ventana

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/webm_imagen_02es.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

- Editamos los campos con los datos que tengamos a disposición, la vista prevía mostrará los cambios. Una vez llenado el formulario hacemos click en **publish changes**

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/webm_imagen_03es.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

- Agregamos la licencia, generalmente se usa CC BY-SA 4.0. Haciendo click en el boton edit a lado del título Licensing.

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/webm_imagen_04es.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

- Si deseamos agregamos categorias y etiquetas
Por comodidad realice este procedimiento en la página en ingles, pero es posible cambiar el idioma y realizar los mismos pasos en el idioma español. </n>


Es todo por esta entrada, **Buen edit¡¡**