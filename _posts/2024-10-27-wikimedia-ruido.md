---
layout: post
title: Wikimedia - Eliminación de ruido en imagenes
date: 2024-10-27 22:26:00
description: Tutorial para la eliminación de ruido en las imagenes de Wikimedia Commons 
tags: wikimedia, photoshop, edicion, imagenes 
categories: wikimedia
thumbnail: assets/img/9.jpg
featured: false
---

Existen procesos necesarios para que las imágenes añadidas a Wikimedia sean consideradas en el concurso Wikimedia Commons a nivel mundial. Uno de ellos es la eliminación de ruido, que reduce la granulación de la imagen en su máxima resolución, mejorando su calidad.

El proceso propuesto consiste en separar el ruido y la textura en diferentes capas, logrando una imagen con menos ruido y granulado. Este tutorial se divide en tres etapas:

- Duplicar la capa original y obtener los bordes.
- Extraer el ruido.
- Ajustar y tratar la textura.

### Primera etapa, duplicado de la capa original y obtención de los bordes
- Duplicamos el proyecto en el menu **Imagen -> Duplicar** y lo nombramos como (nombre_origina)_copia. Posteriormente en el **nuevo proyecto** utilizamos el modo Color Lab ubicado en el menu 
**Imagen -> Modo -> Color Lab**


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/reduccion-ruido2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/reduccion-ruido3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Creación de un nuevo proyecto y acceso al Modo Lab de edición.
</div>

En el panel de capas seleccionamos canal y activamos solo el canal de **luminosidad**. Posteriormente seleccionamos **Filtro -> Galeria de filtros**

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/reduccion-ruido23.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/reduccion-ruido4.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Selección del canal luminosidad e ingreso a galeria de filtros.
</div>

Una vez dentro de **galeria de filtros** elegimos **estilizar -> bordes resplandecientes** y adecuamos los valores para que los bordes tengan la mayor cantidad posible de contraste con el color negro de fondo. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/reduccion-ruido1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Obtención de los bordes con el filtro bordes resplandecientes.
</div>

Si es necesario realizamos un mayor contraste utilizando el filtro **brillo / contraste** para luego **seleccionar** nuestra imagen utilizando las teclas **ctrl + click izquierdo**. Notaremos que dentro de los bordes se rellenara con lineas como se ve en la tercera imagen.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido5.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido6.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido7.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Obtención de los bordes de la imagen utilizando el filtro brillo y contraste y selección de la imágen.
</div>

Posteriormente guardamos la **selección** que obtuvimos en el paso anterior utilizando el menu **Selección -> Guardar Selección**. Le damos un nombre, en este caso le di el nombre de **definición**. Con ello finalizamos la primera etapa del tutorial.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido8.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido12.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Guardado de la selección de bordes.
</div>

### Segunda etapa, Extracción del ruido.

En el **proyecto original** duplicamos la capa principal y la renombramos como ruido utilizando las teclas **ctrl+j**, esta nueva capa la convertimos en objeto inteligente utilizando el **boton derecho sobre el texto ruido** para desplegar el **menu de opciones**. Finalmente Seleccionamos convertir en **objeto inteligente**.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido9.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido10.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Creando la capa ruido y convirtiendola en objeto inteligente.
</div>

Una vez, convertida la capa en objeto inteligente, **cargamos** la selección realizada en la primera etapa, para ello vamos al menu **Selección -> Cargar Selección** y **seleccionamos el proyecto de la copia de la etapa 1**.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido11.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido12.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Carga de la selección del ruido del proyecto duplicado.
</div>

Añadimos una **mascara de capa** a la **capa ruido** 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido14.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido15.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Añadido de mascara de capa.
</div>

Tras esta acción se puede observar que la imagen muestra los bordes del detalle de la imagen

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido16.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Máscara de capa.
</div>

### Tercera etapa, Ajuste y tratado de la textura.

Para iniciar el tratamiento de la imagen es necesario invertir la capa, utilizando las teclas **ctrl+i** 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido17.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Inversión de la selección del ruido.
</div>

**renombramos la capa original** con un nombre diferente a fondo, en este caso lo renombre a detalles, posdteriormente con la capa ruido seleccionada, y utilizamos el menu **filtro -> Filtro de camera raw**

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido19.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido20.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Añadido de mascara de capa.
</div>

Finalmente ajustamos la reducción de ruido en el menu **Detalle -> Reduccion de ruido**

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido20.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Reducción de ruido.
</div>

Si es necesario ajustamos la textura para mejorar la calidad de la imagen en el menu **basico -> textura**

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/reduccion-ruido21.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Ajuste de la textura.
</div>
**Nota:**
- Los valores en cada paso se asignan según la necesidad de cada imagen
- Dependiendo el caso se verifica la funcionalidad del proceso.
