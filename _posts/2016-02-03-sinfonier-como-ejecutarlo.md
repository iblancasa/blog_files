---
layout: post
title: Comentando Sinfonier y un "arreglillo"
excerpt: "Contando qué es Sinfonier y cómo ejecutar los test sin tener que utilizar la máquina virtual que han colgado en su blog"
tags: [sinfonier, eleven path, software]
comments: true
category: tutoriales
---
Hoy vengo a hablaros de [Sinfonier](http://sinfonier-project.net/). Tengo que aclarar, antes de empezar, que cuando escribo este post no lo he utilizado ni una vez. Solo lo he trasteado, aunque sin mucha idea pero, como veréis más adelante, mi intención no es hacer un tutorial sobre cómo se usa (aunque no descarto hacer una breve guía porque la documentación que me he encontrado es bastante escasa).

En el siguiente vídeo podréis ver qué es Sinfonier y para qué se utiliza.

<iframe src="https://player.vimeo.com/video/109057651" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<p><a href="https://vimeo.com/109057651">Sinfonier: Storm Builder for Security Intelligence</a> from <a href="https://vimeo.com/sinfonierproject">Sinfonier Project</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

Como podemos ver, es un software que hace de capa de abstracción sobre [Apache Storm](http://storm.apache.org/) (un sistema para realizar computación de forma distribuida).

[Aquí podéis acceder a su organización en GitHub](https://github.com/sinfonier-project).

[Este artículo es el más interesante (al menos para mí de su blog. Es un "getting started".)](http://blog.sinfonier-project.net/2015/12/sinfonier-quick-start.html)

## Pero... ¿cómo funciona?
Consiste en conectar, de forma gráfica, una serie de módulos para realizar procesamiento de datos.

Tenemos tres tipos de "módulos":
* Spout: estos módulos leen de una fuente de datos. Un ejemplo de ellos podría ser la API Streaming de Twitter.
* Bolt: realiza procesamiento sobre un flujo de datos
* Drain: almacena los datos o los muestra en alguna interfaz como un "dashboard"

Estos módulos se conectan entre sí en lo que se llama una topología. Los "spouts" se conectan a los "bolts" y estos a su vez a los "drains" (donde cada conexión implica un flujo de datos).

 ## Vale pero... ¿y lo del arreglillo?
Para crear un bolt (o cuarquier otro tipo de módulo) solo tenéis que seguir las instrucciones que hay en el artículo ["Creación de un bolt: ¿he sido hackeado?"](http://blog.sinfonier-project.net/2015/10/creacion-de-un-bolt-he-sido-hackeado.html). Como podéis comprobar, la depuración del código puede ser algo pesada: copiar el código a un gist, enviarlo a Sinfonier, procesarlo y comprobar los errores.

Para agilizar el proceso, los desarrolladores han creado una máquina virtual para VirtualBox [(en este artículo puedes ver cómo ejecutarla)](http://blog.sinfonier-project.net/2016/02/development-vm-support-python-exceptions.html) donde han instalado Eclipse y han creado los ficheros del proyecto necesarios para desarrollar nuestro propio módulo.

 Estos ficheros están disponibles en [un repositorio de GitHub](https://github.com/sinfonier-project/sinfonier-dev-tool). Si echamos un vistazo (aunque la documentación del código es nula y cuesta comprenderlo) lo que se está haciendo es ejecutar una batería de tests (de esto ya nos avisan en el artículo que enlacé en el párrafo anterior) es decir, los test no se ejecutan sobre "Apache Storm" y mucho menos sobre "Sinfonier". Teniendo en cuenta que ejecutar Eclipse ya puede ser un auténtico desafío a la velocidad de nuestro PC, decidí intentar ejecutar estos test en mi máquina (sin utilizar ningún tipo de virtualización).

### ¿Cómo ejecutar los test en mi máquina?
Tengo que avisar que yo lo he hecho en un sistema operativo Linux, así que no sé cómo funciona en Windows o Mac.

#### ¿Qué necesito instalar?
 * Python (versión 2.7)
 * Módulo Python "APScheduler"
 * Java JDK
 * Maven
 * Haz un clone de [este repositorio](https://github.com/iblancasa/sinfonier-dev-tool). Como podrás comprobar, es un fork del de "Sinfonier" (que a su vez es un fork de otro). Cuando traté de ejecutar los test en la máquina virtual, todos fallaban debido a que faltaban parámetros y algunas cosas para poder ejecutar Maven desde terminal.

#### ¿Cómo ejecuto?
Ve al directorio raíz del repositorio que has clonado y ejecuta ``mvn package``. Se descargarán las dependencias y ejecutarán los test. Si quieres saber cómo cambiar de ejecutar los test de los ficheros Java a los de Python, [echa un ojo a este artículo](http://blog.sinfonier-project.net/2016/01/sinfonier-development-virtual-machine_26.html).

#### ¿Cómo añado nuevos test?
Son test unitarios, mira los ficheros y los artículos que he ido enlazando.

## Algunos artículos interesantes relacionados con Sinfonier son:
* [Chatterbot with Sinfonier](http://blog.sinfonier-project.net/2015/12/chatterbot-with-sinfonier.html)
* [Creando información "dummy"](http://blog.sinfonier-project.net/2014/10/creando-informacion-dummy.html)
* [Have I been pwned?](http://blog.sinfonier-project.net/2014/10/have-i-been-pwned.html)
* [Recibe un mensaje, emite varios](http://blog.sinfonier-project.net/2014/10/recibe-un-mensaje-emite-varios.html)
* [TickTuples: ejecución de código por intervalo de tiempo](http://blog.sinfonier-project.net/2014/11/ticktuples-ejecucion-de-codigo-por.html)
* [Vuela barato con Sinfonier y Ryanair](http://blog.sinfonier-project.net/2014/10/vuela-barato-con-sinfonier-y-ryanair.html)
* [Using Mongolab with Sinfonier](http://blog.sinfonier-project.net/2015/08/using-mongolab-with-sinfonier.html)
* Sinfonier para el procesamiento del lenguaje natural: [parte I](http://blog.sinfonier-project.net/2015/08/sinfonier-para-procesamiento-del.html) y [parte II](http://blog.sinfonier-project.net/2015/10/sinfonier-para-procesamiento-del.html)
* [How to use Telegram modules?](http://blog.sinfonier-project.net/2015/09/how-to-use-telegram-modules.html)

Y (al menos por ahora) no puedo ayudar mucho más. Aunque no he trabajado con Sinfonier y solo conozco el concepto, me pareció necesario un artículo como este para poder ejecutar los tests sin tener que utilizar una máquina virtual. Espero que haya sido útil.
