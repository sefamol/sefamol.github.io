---
layout: post
title: Copia de código fuente de una web con Httrack
date: 2025-04-15 10:00:00
description: Copiar código fuente de una página web con HTTRACK
tags: Copia, HTTRACK, Herramientas, ciberseguridad, pentesting web 
categories: Seguridad Informática
thumbnail: assets/img/logo-cisco.svg
featured: false
---

# **Datos Generales**
- **Software**: HTTRACK
- **Dificultad**: Fácil
- **Duracion**: 10 minutos
- **Observaciones**: Herramienta eficiente para la copia de páginas web, en caso de que la página contenga demasiada información no obtiene una información completa.

## **Descarga e instalación**
Para equipos con SO **Windows** descargar el archivo ejecutable de [https://www.httrack.com/](https://www.httrack.com/) 
Para equipos con SO Linux/Ubuntu instalamos el paquete desde el repositorio apt 

```
sudo apt update && sudo apt install httrack -y
```

En caso de que se pida instalar Las firmas siguientes porque la clave pública no está disponible de **NO_PUBKEY 0E98404D386FA1D9 NO_PUBKEY 6ED0E7B82643E131** Utilizamos el siguiente comando para instalar las claves publicas

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0E98404D386FA1D9 6ED0E7B82643E131
```

Y continuamos con la intalación normal

```
sudo apt install httrack -y
```

## **Copiando la web**
Una vez instalado el paquete, descargamos la web completa utilizando el comando
```
httrack http://test.website.com -O./website_clone -F "Mozilla/5.0" r5 -%h -v
```
**Donde:**
- **-F "Mozilla/5.0"** Finge ser un navegador.
- **-r5** Profundidad de descarga (ej: 5 niveles).
- **%h** Respeta la estructura de directorios del sitio.

Luego podemos utilizar nuestro editor de código preferido y realizar el análisis deseado.