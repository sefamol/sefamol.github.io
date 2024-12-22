---
layout: post
title: Wikipedia - Creación de listas
date: 2024-12-21 21:20:00
description: Tutorial para la creación de listas en wikipedia 
tags: wikipedia, listas, edicion 
categories: wikipedia
thumbnail: assets/img/wikipedia.png
featured: true
---

# **Datos Generales**
- **Plataforma**: Wikipedia
- **Dificultad**: Baja
- **Duracion**: 10 minutos
- **Observaciones**: Este tutorial es introductorio a una serie de tutoriales genrados para la edición en wikipedia.

---

## Un poco de teoría
En wikipedia se usa los terminos prosa y lista para la descripción de los elementos relevantes de una publicación, de esta manera estos terminos se definen de la siguietne manera:
**prosa**: teoría acerca del tema (narrado)
**lista**: información clave. (lista de tareas)

## Preparación de ambiente de prueba
Para el proposito de este tutorial es necesario crear un ambiente de prueba que nos permita realizar los cambios sin afectar a una publicación existente

**Creación de un taller**

Click en la pestaña del menu del usuario para luego seleccionar **taller**

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/wikipedia-listas-01.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

Luego seleccionamos la opción **editar código**
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/wikipedia-listas-02.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

Con estos pasos ya podemos iniciar las pruebas

## Lista simple numerada
**Código utilizado**

```
# Elemento de lista 1
# Elemento de lista 2
# Elemento de lista 3
```
**Resultado**
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/wikipedia-listas-04.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

## Lista numerada con subelementos
**Código utilizado**
```
'''lista numerada'''
# Elemento 1
:# Subelemento 1
:# Subelemento 2
# Elemento de lista 2
# Elemento de lista 3
```
**Resultado**
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/wikipedia-listas-06.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

## Lista con viñetas
**Código utilizado**
```
'''lista con viñetas y subelementos'''
* Viñeta 1
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 2
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 3
```
**Resultado**
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/wikipedia-listas-07.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

## lista en columnas
```
'''lista dividida en columnas'''
\{\{lista_de_columnas|3|
* Viñeta 1
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 2
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 3
* Viñeta 4
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 5
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 6
* Viñeta 7
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 8
:* Viñeta subelemento 1
:* Viñeta Subelemento 2
* Viñeta 9
}}
```
**Resultado**
<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/wikipedia-listas-08.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>