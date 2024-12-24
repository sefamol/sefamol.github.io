---
layout: post
title: Wikipedia - Consultas sparql con petscan
date: 2024-12-24 14:20:00
description: Tutorial introductorio para hacer consultas sparql con petscan
tags: wikipedia, wikidata, sparql, petscan, nosql, base de datos 
categories: wikipedia
thumbnail: assets/img/wikipedia.png
featured: true
---

# **Datos Generales**
- **Plataforma**: Wikipedia, Wikidata
- **Dificultad**: Media
- **Duracion**: 20 minutos
- **Observaciones**: Realización de consultas no complejas en sparql con petscan

---

# **Un poco de teoría**
## **Que es sparql?** 
En términos simples es un lenguaje para la consulta de base de datos. Con lun par de particularidades.
- Primero, esta más cerca de ser un lenguaje de base de datos no relacional (NoSQL) aunque maneja una sintaxis parecida a SQL
- Segundo, Este lenguaje esta pensado para hacer consultas en la web semántica.
- Tercero, lo usa Wikipedia para las consultas de su data.

Más teoría en: https://datascience.recursos.uoc.edu/es/sparql/ y https://es.wikipedia.org/wiki/SPARQL

## **Que es una consulta?**
De forma muy pero muy básica, una consulta es una petición de algo a un catálogo existente. Por ejemplo si entramos a una tienda **consultamos** si tiene "x" producto la persona que atiende nos responderá sobre la existencia del mismo. Lo mismo sucede con las bases de datos, con la diferencia de que se manejan grandes cantidades de datos y dependiendo los permisos se puede realizar diferentes actividades en las **tablas** existentes en la base de datos.

Más teoría en https://www.hostinger.es/tutoriales/que-es-consulta-base-de-datos/

## **Como hago una consulta en sparql?**
La sintaxis utilizada en sparql esta determinada en la manipulación de grafos RDF en la web. Esta se se basa en tripletas que definen un universo que contiene **entidades** y **propiedades**. Las tripletas se componen de elementos que siguen el patrón: **sujeto - predicado - objeto**. En este sentido la consulta requiere de dos elementos importantes: las **propiedades** y las **entidades**.

Una mejor explicación, la podemos encontrar en: https://data.cervantesvirtual.com/noticia/tutorial-de-inicio-a-sparql 

# **Vamos a la práctica**
## Petscan
Empecemos conociendo como ingresar y realizar nuestra  consulta.
- 1. Ingresamos a https://petscan.wmcloud.org/
- 2. Seleccionamos la pestaña **Other sources** -> **Sparql**

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/intro-sparql-01.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

- 3. Realizamos nuestra consulta para conocer especies animales existentes en Bolivia

**Consulta utilizada**

```
SELECT ?especie ?especieLabel ?nombreCientifico ?claseLabel
WHERE {
  ?especie wdt:P31 wd:Q16521;                 # Instancia de especie
           wdt:P183 wd:Q750.                  # País de distribución nativa: Bolivia
  OPTIONAL { ?especie wdt:P225 ?nombreCientifico. } # Nombre científico (opcional)
  OPTIONAL { ?especie wdt:P105 ?clase. }      # Rango taxonómico o clase (opcional)
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
ORDER BY ?especieLabel
```

Notemos los campos **wd** y **wdt** son las entidades y propiedades de las que hablamos en la teoría.

**wdt (Wikidata Truthy Statements)**

- **wdt:** se refiere a las **declaraciones verificadas** o afirmaciones "truthy" en Wikidata. Estas son las relaciones directas entre un sujeto y un objeto, omitiendo información adicional como referencias, calificadores o rangos temporales.
    - Es ideal para consultas rápidas, ya que no incluye datos adicionales.

**En el ejemplo se entiende de esta manera:**

- **wdt:P31:** Representa la propiedad **"instancia de"** en Wikidata.
- **wdt:P183:** Representa la propiedad **"país de distribución nativa"**.

**Uso:**
    
    - Permite filtrar por elementos que tienen relaciones simples y directas. En este caso:
        - `?especie wdt:P31 wd:Q16521`: Busca elementos donde el sujeto (`?especie`) sea una **instancia de especie** (`Q16521`).
        - `?especie wdt:P183 wd:Q750`: Busca elementos donde el sujeto (`?especie`) tenga a **Bolivia** (`Q750`) como país de distribución nativa.
 
 ---

**wd (Wikidata Entity)**

    - `wd:` se refiere a las **entidades de Wikidata**. Estas entidades son identificadores únicos asignados a conceptos, personas, lugares, propiedades, etc., en Wikidata.
    - Los identificadores tienen el formato `Q#####` para elementos o `P#####` para propiedades.

**En el ejemplo se entiende de esta manera:**
    
    - `wd:Q16521`: Representa el concepto de **especie**.
    - `wd:Q750`: Representa el concepto de **Bolivia**.

**Uso:**
    
    - Se utiliza como valor de una propiedad en una declaración. En este caso:
        - `wd:Q16521` es el valor de `wdt:P31` para especificar que algo es una especie.
        - `wd:Q750` es el valor de `wdt:P183` para indicar que Bolivia es el país de distribución nativa.

## **De donde se obtiene los valores "P" y "Q" para la consulta?**
### **Para el valor Q**
- ingresamos a www.wikidata.org
- Realizamos la búsqueda de nuestro interés y observamos el valor Q de cada respuesta

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/intro-sparql-04.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

## **Para el valor P**
La lista de propiedades podemos encontrarla en https://www.wikidata.org/wiki/Wikidata:List_of_properties
En esta pagina ingresamos el **valor buscado**, oprimimos en **buscar** y obtenemos el resultado. En la imagen muestra el valor **P** de la propiedad endémico utilizado en nuestra búsqueda. 

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/intro-sparql-05.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

El resultado será el siguiente:

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/intro-sparql-03.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

podemos observar que cada artículo cuenta con su valor **Q**

## Hagamoslo sencillo

Hasta aqui es un enredo que a pesar de que es intuitivo es complicado de construir y de hallar la información. Por ello recurri a chatgpt, aplicación que construye la consulta de manera automática. El prompt que utilice es el siguiente:

```
ayudame a construir una petición que muestre todos las especies animales endemicas de bolivia existentes en la base de datos de wikipedia utilizando sparql.
```

Obteniendo la siguiente respuesta que se utilizo en la consulta de ejemplo

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/intro-sparql-07.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

copiamos el código propuesto a la consulta en sparql https://petscan.wmcloud.org/ y oprimimos en **do it**

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/intro-sparql-08.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

Parte del resultado se verá asi

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/intro-sparql-09.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

Es todo por esta entrada. La teoría y la práctica anterior explica brevemente el contenido de esta consulta. Si, falta las variables que filtra la consulta pero lo básico y de donde sale lo expuesto espero que se comprenda. Realizare más entradas para complejizar  estas consultas.

**Feliz Navidad¡¡¡ Abrazo fuerte :)**
