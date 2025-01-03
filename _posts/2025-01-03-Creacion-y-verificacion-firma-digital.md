---
layout: post
title: Creación y verificación de una firma dígital
date: 2025-01-03 10:20:00
description: Creación y verificación de una firma dígital
tags: SOC, Firma Dígital, Criptografía, ciberseguridad, Network Defense
categories: Seguridad Informática
thumbnail: assets/img/logo-cisco.svg
featured: false
---

# **Datos Generales**
- **Software**: openssl
- **Dificultad**: Fácil
- **Duracion**: 10 minutos
- **Observaciones**: Laboratorio fácil para la implementación de una firma dígital 

## **Creación de clave privada**

Para la creación de una llave pública el primer paso es la creación de una llave privada, para ello se ejecuta el siguiente comando:

```
cisco@labvm:~$ openssl genpkey -algorithm RSA -out private_key.pem
```

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/firma_digital-01.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

**Donde:**
- **openssl:** Es la herramienta para ejecutar operaciones criptográficas como generación de claves, creación de certificados, encriptación, etc.
- **genpkey:** Es la subcomando para generar claves privadas. En versiones modernas de OpenSSL, se recomienda usar genpkey en lugar de genrsa, ya que es más versátil y admite varios algoritmos.
- **-algorithm RSA:** Especifica el algoritmo que se utilizará para generar la clave será RSA. RSA (Rivest–Shamir–Adleman) es un algoritmo de cifrado de clave pública muy común en protocolos de seguridad como TLS/SSL.
- **-out private_key.pem:** Indica el nombre del archivo de salida donde se guardará la clave privada generada.  El formato del archivo será PEM (Privacy-Enhanced Mail), que es un formato codificado en texto plano (Base64) para almacenar datos criptográficos.

Utilizando **cat** o cualquier lector/editor de texto, la llave privada téndra la siguiente forma

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/firma_digital-02.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>


## **Creación de la llave publica**
```
cisco@labvm:~$ openssl pkey -in private_key.pem -pubout -out public_key.pem
```
**Donde:**
- **openssl:** Herramienta de línea de comandos para realizar operaciones criptográficas.
- **pkey:** Subcomando utilizado para trabajar con claves públicas y privadas.
- **-in private_key.pem:** Especifica el archivo de entrada que contiene la clave privada desde la cual se derivará la clave pública. En este caso,  private_key.pem contiene la clave privada en formato PEM.
- **-pubout:** Indica que se desea extraer la clave pública asociada a la clave privada proporcionada. Esto generará la clave pública correspondiente en un archivo separado.
- **-out public_key.pem:** Especifica el archivo de salida donde se guardará la clave pública generada. El formato será PEM, que utiliza codificación Base64 para representar la clave en texto plano.

Una vez creada la llave pública se verá de la siguiente manera

<div class="row mt-3 justify-content-center">
    <div class="col-10 col-sm-8 col-md-6 mt-3 mt-md-0">
        <div class="img-container">
            {% include figure.liquid path="assets/img/firma_digital-03.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>

para objeto práctico se creó el documento contract.txt para demostración, utilizando el comando **echo**

```
cisco@labvm:~$ echo Porfavor transfiere 200000 de dolares a Alexa las 6 pm de hoy > contract.txt
```
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/firma_digital-04.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Firma del documento**
Firmaremos el documento, para ello se usará la clave privada creada anteriormente para posteriormente verificar su firma, el comando a utilizar es **signature**

```
cisco@labvm:~$ openssl dgst -sha256 -sign private_key.pem -out signature contract.txt
```
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/firma_digital-05.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Verificación de la firma**

```
cisco@labvm:~$ openssl dgst -sha256 -verify public_key.pem -signature signature contract.txt
```

**Donde**
- **openssl:** Herramienta de línea de comandos para realizar operaciones criptográficas.
- **dgst:** Subcomando para calcular o verificar hashes.
- **-sha256:** Especifica el algoritmo de hash que se usará durante la verificación. En este caso, SHA-256, que es un algoritmo seguro y ampliamente utilizado.
- **-verify public_key.pem:** Indica que se usará la clave pública almacenada en el archivo public_key.pem para verificar la firma. La clave pública corresponde a la clave privada que generó la firma.
- **-signature signature:** Especifica el archivo que contiene la firma digital generada previamente. Esta firma es el resultado de firmar el archivo contract.txt con la clave privada correspondiente.
- **contract.txt:** Es el archivo original cuyo hash se comparará con la firma digital.

En  el caso de una firma verificado se vera de la siguiente manera
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/firma_digital-06.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Firma en documento alterado**

Editamos el documento contract.txt
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/firma_digital-07.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Verificamos la firma
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/firma_digital-08.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

