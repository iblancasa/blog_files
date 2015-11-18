---
layout: post
title: Cómo utilizar ExpressJS con HTTPS
excerpt: "Una pequeña guía sobre cómo utilizar ExpressJS, el paquete de NodeJS, para funcionar sobre HTTPS en vez de HTTP"
tags: [nodejs, javascript, ssl, tls, https, http, server, servidor, programar, guía, tutorial]
comments: true
category: tutoriales
---


![HHTPS Node ExpressJS](http://fotos.subefotos.com/6529a9aca846a939dac313a0b1a2dbc4o.jpg)

En esta guía voy a explicar, brévemente, como hacer que nuestro servidor realizado con [NodeJS](https://nodejs.org) (mediante el paquete [ExpressJS](http://expressjs.com/)). Si no sabes Javascript, no conoces nada de NodeJS y/o no conoces ExpressJS, comienza por ahí y vuelve aquí más tarde (es fácil, no tardarás mucho tiempo en volver).

## Generando los certificados

Primero será necesario generar los certificados del servidor. Cuando un usuario acceda a nuestro sitio web, obtendrá un aviso indicando que la conexión no es segura, debido a que el certificado no estará firmado por una entidad de certificación. Puedes adquirir certificados a través de Internet.

Podemos generar nuestros propios certificados. La conexión seguriá estando cifrada, aunque los navegadores no podrán certificar que el servidor sea el correcto (es decir, que los usuarios no están sufriendo un ["man-in-the-middle"](https://es.wikipedia.org/wiki/Ataque_Man-in-the-middle), por ejemplo).


```bash
openssl genrsa -out chat-key.pem 1024
openssl req -new -key chat-key.pem -out certrequest.csr
openssl x509 -req -in certrequest.csr -signkey chat-key.pem -out chat-cert.pem
```


## Editando el código

Simplemente, colocaremos los ficheros generados anteriormente dentro de nuestra aplicación y los referenciaremos desde el fichero donde se lance el servidor. La ruta será relativa al "package.json". Las claves las introduciremos en un diccionario y las pasaremos como parámetro a la hora de crear el servidor.

```javascript
var fs = require('fs');
var hskey = fs.readFileSync('chat-key.pem');
var hscert = fs.readFileSync('chat-cert.pem')
var options = {
  key: hskey,
  cert: hscert
};

var express = require('express');
var app = express();

var https = require('https');

var server = https.createServer(options, app);
```

Como podemos apreciar, respecto al "código clásico" de ejemplo, el resto del código cambia poco.

Estos certificados deben generarse con la máquina que servirá las peticiones, es decir, con el servidor. No funcionará si generamos los certificados en nuestro ordenador personal y lo subimos a un VPS, por ejemplo.