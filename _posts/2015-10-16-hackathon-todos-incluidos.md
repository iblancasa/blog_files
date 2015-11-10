---
layout: post
title: Comentando el hackathón "Todos incluidos" en Granada
excerpt: "Pequeña crónca sobre el hackathón \"Todos incluidos\" organizado por Telefónica en octubre de 2015"
modified: 2015-10-16
tags: [hackathon, telefonica, granada, parque de las ciencias, thinking things, iot, internet de las cosas, hardware]
comments: true
category: eventos
---
Durante los días 2, 3 y 4 de octubre, el Parque de las Ciencias de Granada se llenó de programadores y gente relacionada con las nuevas tecnologías. Telefónica organizaba un hackathón (en el que previamente había que ser seleccionado tras rellenar una solicitud a través de un formulario web) sobre Internet de las Cosas.


De forma paralela, se celebraban algunas actividades en otra sala: algunas charlas sobre drones, impresión 3D, realidad virtual...

<div style="margin: 0 auto; display: block;">
<a data-flickr-embed="true"  href="https://www.flickr.com/photos/136559810@N04/albums/72157660036554232" title="Hackathón Telefónica &quot;Todos incluidos&quot;"><img src="https://farm1.staticflickr.com/772/22306797055_fdf945ab83.jpg" width="500" height="375" alt="Hackathón Telefónica &quot;Todos incluidos&quot;"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
</div>

El dispositivo se encuentra formado por varios módulos, como puede verse en las imágenes anteriores. Los posibles módulos son:
* Batería
* Comunicación
* Sensor de presencia (opcional y no lo tuvimos disponible)
* Un sensor de humedad, luminosidad y temperatura (opcional)
* Un "actuador", con un led y un zumbador (opcional)

Según uno de los miembros organizadores del hackathón, la carga de la batería podía durar semanas o, incluso, meses pero, tras haber cargado completamente el módulo (a través de un cable USB) y dejarlo encendido (a propósito) antes de abandonar el recinto, la carga había sido agotada durante la noche (tal vez debido a que se había usado demasiado en anteriores ocasiones o que la batería no cumple lo que promete).

La comunicación se realiza por medio de una tarjeta SIM, distinta a la que se utiliza para los teléfonos móviles, pero con similar funcionalidad.

En cuanto a los sensores... la temperatura parece que no era todo lo correcta que debiera y la luminosidad y humedad estaban en unidades desconocidas.

El acceso a los datos se realizaba mediante una API REST. En nuestro caso, no se precisaba de token de seguridad y los Thinkin Thing estaban sirviendo los datos en un puerto distinto al habitual (para que nos fuese más sencillo desarrollar una aplicación). Si hacíamos una petición al servidor, como la siguiente:

{% highlight bash %}
curl http://hackathon.ttcloud.net:10026/v1/contextEntities/[ID de tu dispositivo] -s -S --header 'Accept: application/json' --header 'fiware-service: todosincluidos' --header 'x-auth-token: ' --header "fiware-servicepath: /iot"
{% endhighlight %}

Obteníamos un JSON como este:

{% highlight json %}
{
  "contextElement" : {
    "type" : "thinkingthing",
    "isPattern" : "false",
    "id" : "[ID]",
    "attributes" : [
      {
        "name" : "cellid",
        "type" : "string",
        "value" : "1f3c"
      },
      {
        "name" : "charger",
        "type" : "integer",
        "value" : "0"
      },
      {
        "name" : "charging",
        "type" : "integer",
        "value" : "1"
      },
      {
        "name" : "color",
        "type" : "string",
        "value" : " "
      },
      {
        "name" : "dbm",
        "type" : "integer",
        "value" : "-69"
      },
      {
        "name" : "desconnection",
        "type" : "integer",
        "value" : "0"
      },
      {
        "name" : "humidity",
        "type" : "float",
        "value" : "1043108.50"
      },
      {
        "name" : "lac",
        "type" : "integer",
        "value" : "70c"
      },
      {
        "name" : "luminance",
        "type" : "float",
        "value" : "38.90"
      },
      {
        "name" : "mcc",
        "type" : "integer",
        "value" : "214"
      },
      {
        "name" : "melody",
        "type" : "string",
        "value" : " "
      },
      {
        "name" : "mnc",
        "type" : "integer",
        "value" : "07"
      },
      {
        "name" : "mode",
        "type" : "integer",
        "value" : "1"
      },
      {
        "name" : "sleepcondition",
        "type" : "string",
        "value" : "Wake"
      },
      {
        "name" : "sleeptime",
        "type" : "string",
        "value" : "3"
      },
      {
        "name" : "state",
        "type" : "integer",
        "value" : "1"
      },
      {
        "name" : "temperature",
        "type" : "float",
        "value" : "28.73"
      },
      {
        "name" : "voltage",
        "type" : "float",
        "value" : "6.52"
      }
    ]
  },
  "statusCode" : {
    "code" : "200",
    "reasonPhrase" : "OK"
  }
}
{% endhighlight %}

De los actuadores poco puedo decir ya que, salvo alguna indicación que se nos dió sobre la marcha, no recibimos más documentación. Había que realizar una petición POST a nuestro dispositivo enviándole un fichero JSON con los valores que queríamos que tomase el actuador (en el caso del LED, teníamos que dar valores a una terna RGB -siendo los posibles valores 0 ó 1- y en el caso del zumbador, no había documentación a través de Internet -gracias a uno de los organizadores, tuvimos una ligera idea de cómo funcionaba por que nos envió, a través de Google Drive, un documento con parte de la especificación-).

Siento decir que no me gusta mucho esta plataforma hardware ya que creo que tiene un coste demasiado elevado para la escasa funcionalidad que tiene. Además, tener que utilizar la plataforma online de forma obligatoria lo considero una desventaja aunque claro, ahí está el negocio. También echo de menos más documentación.

En cuanto a la comida y la conectividad... eso ya es otro tema.
