---
layout: post
title: Hola mundo
excerpt: "Inicio el blog y explico por qué razones he decidido abandonar Wordpress y unirme a Jekyll"
modified: 2015-10-06
tags: [nuevo, post, hola mundo]
comments: true
---
Tras mucho pensarlo, decidí pasar de Wordpress y empezar a utilizar Jekyll. ¿Por qué?

Durante algunos años, para distintos tipos de cosas, he utilizado Wordpress. Siempre he tenido, entre otras, la misma queja: el sitio web, pese a tener poco contenido y un número bastante bajo de visitas, siempre ha ido muy lento. Incluso si utilizaba las plantillas por defecto. Por si el problema había sido a lo largo de todo este tiempo la utilización de hostings o VPS de mala calidad, probé a utilizar la plataforma PaaS (*Platform as a service*) de [Red Hat](http://www.redhat.com/es/global/spain), [OpenShift](https://www.openshift.com/). A pesar de utilizar un modelo *premium*, el resultado  fue el mismo.

La necesidad de instalar sistemas de seguridad para evitar ataques o estar pendiente de las actualizaciones (que pueden ser críticas para mantener tu sitio web en pie) han sido otras de las razones.

La obligación de cumplir la [LSSI](http://www.lssi.gob.es/) y la [LOPD](https://www.agpd.es/portalwebAGPD/canaldocumentacion/informes_juridicos/reglamento_lopd/index-ides-idphp.php) me llevaron a desactivar los comentarios del blog (que tampoco necesitaba), crear el típico documento declarando qué cookies utilizaba...

Todo esto me hizo abandonar Wordpress. Estudié cómo funcionaban otras plataformas como [Ghost](https://ghost.org/), [Blogger](https://www.blogger.com/home) (que nunca me terminó de convencer) o [Octopress](http://octopress.org/) (que funciona sobre Jekyll).

No quise utilizar un sistema que me obligase a estar en el hosting/cloud de la empresa que lo desarrolla (por lo que ya eliminaba unas cuantas posibilidades).

Por otro lado, pensé en los problemas que había encontrado respecto a velocidad de respuesta. ¿Qué hay más rápido que una web realizada solo en HTML, CSS y JavaScript? Por lo que desestimé cualquier sistema generado de forma dinámica: nada de preguntar a bases de datos. El sistema que más me llamó la atención (y en el que entendí un mejor soporte) fue Jekyll.

En cuanto a hosting, simplemente estoy utilizando [GitHub Pages](https://pages.github.com/), por lo que no me tengo que preocupar por la calidad (que es bastante buena) o de pagarlo. En vez de utilizar directamente la opción que nos da GitHub para construir nuestro blog Jekyll, hice un fork de una plantilla que me gustó y soy yo mismo quien construye los ficheros que forman la web, utilizando [Travis](https://travis-ci.org/) (de esta forma, añado algunas cosas como la posibilidad de comprimir las imágenes y las páginas generadas en HTML, con lo que la velocidad de respuesta aumenta algo, aunque tampoco es algo notable).

El subirlo a GitHub ayuda, además, a que lo que escriba se vea reflejado en más de un sitio.


Empiezo con esto una nueva etapa

![](https://jekyllrb.com/img/logo-2x.png)
