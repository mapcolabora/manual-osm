# **Cómo taguear las paradas de bus en OSM**

Por: Héctor Ochoa, CC-BY-SA

Problemas:

* Nuevo esquema de transporte público \(aceptado hace 2 años\)

* La gran mayoría de apps no lo aceptan aún


Solución: Hacer una mezcla entre ambos esquemas.

**Mi propuesta:**

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
  * `Mapeado avanzado:`

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



