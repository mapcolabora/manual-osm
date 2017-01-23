# **Cómo etiquetar las paradas de bus en OSM**

Por: Héctor Ochoa

## Objetivos

En esta receta aprenderemos cómo deben de etiquetarse las paradas de bus de manera que 1) los datos puedan ser interpretados por la mayoría de aplicaciones y 2) que a su vez siga el [nuevo esquema de transporte público](https://wiki.openstreetmap.org/wiki/Public_transport)[^nuevoesquema] especificado en la wiki.

Para dar respuesta a ambos objetivos se propone realizar una mezcla entre ambos esquemas.

## Procedimiento

Mapeado simple:

Un único nodo dónde para el bus en la vía con:

* `highway=bus\_stop\(heredado del antiguo esquema\)`
* `public\_transport=stop\_position`
* `bus=yes`
* `network=Autobuses Urbanos de Zaragoza`
* `operator=Auzsa`
* `name=\(el nombre de la parada\)`
* `ref=\(el número de poste\)`
* `.`
* `.`
* `.`
* `wheelchair=yes/no`
* `tactile\_paving=yes/no`
* `shelter=yes/no`
* `bench=yes/no`

Mapeado intermedio \(recomendado\):

* Un nodo dónde para el bus en la vía con:

  * `public\_transport=stop\_position`
  * `bus=yes`
  * `Un nodo dónde esperan los viajeros con:`
  * `highway=bus\_stop`
  * `public\_transport=platform`
  * `bus=yes`
  * `.`
  * `.`
  * `.`
  * `wheelchair=yes/no`
  * `tactile\_paving=yes/no`
  * `shelter=yes/no`
  * `bench=yes/no`

* Una relación con ambos nodos:

  * `public\_transport=stop\_area`
  * `network=Autobuses Urbanos de Zaragoza`
  * `operator=Auzsa`
  * `name=\(el nombre de la parada\)`
  * `ref=\(el número de poste\)`

Mapeado avanzado:

* Un nodo dónde para el bus en la vía con:

  * `public\_transport=stop\_position`
  * `bus=yes`

* Un nodo dónde está el poste para que las aplicaciones con el antiguo esquema lo reconozcan:\`

  * `highway=bus\_stop`

* Una vía dónde esperan los viajeros con:

  * `public\_transport=platform`
  * `bus=yes`
  * `.`
  * `.`
  * `.`
  * `wheelchair=yes/no`
  * `tactile\_paving=yes/no`
  * `shelter=yes/no`
  * `bench=yes/no`

En el caso en el que se quiera dibujar la marquesina como área, quitar las tags `shelter` y `bench` de la plataforma y dibujarla con las tags:

* `amenity=shelter`
* `shelter\_type=public\_transport`
* `bin=yes/no`
* `bench=yes/no`

Una relación con todo lo anterior:

* `public\_transport=stop\_area`
* `network=Autobuses Urbanos de Zaragoza`
* `operator=Auzsa`
* `name=\(el nombre de la parada\)`
* `ref=\(el número de poste\)`

NOTA: Quizás estaría bien poner también el nombre, red y operador en el _stop\_position_ y en la _platform_, para que sea reconocido por más aplicaciones. En la wiki no queda claro.

¿Recomendar plugins de transporte público para JOSM?

[https://wiki.openstreetmap.org/wiki/JOSM/Plugins/public\\_transport](https://wiki.openstreetmap.org/wiki/JOSM/Plugins/public\_transport)

[https://wiki.openstreetmap.org/wiki/JOSM/Plugins/CustomizePublicTransportStop](https://wiki.openstreetmap.org/wiki/JOSM/Plugins/CustomizePublicTransportStop) &lt;= Este parece sencillo para las paradas, e implementa lo de la nota

[^nuevoesquema]: El 29 de octubre de 2010 se hizo una propuesta para cambiar el sistema de etiquetado de transporte que se venía utilizando hasta el momento, y durante el 31 de marzo de 2011 hasta el 20 de abril del mismo año se realizaron votaciones que dieron como resultado el nuevo esquema de etiquetado. Dicho proceso está documentado en este enlace: https://wiki.openstreetmap.org/wiki/Proposed_features/Public_Transport

