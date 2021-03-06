# Etiquetar aspectos relativos a la movilidad desde el punto de la accesibilidad y diversidad funcional en OSM
Por: Carlos Cámara*, César Canalís

## Objetivos

Tal y como hemos visto en el capítulo ["¿Qué hace grande a OSM?"](/01.Intro-OSM/osm-relevancia.md) , una de las ventajas de utilizar OSM es la posibilidad de hacer mapas temáticos que, por sus características, no suelen tener cabida en otros mapas comerciales u oficiales. Un ejemplo de ello es que apenas existen mapas que sean de utilidad para personas con algún tipo de discapacidad, a pesar de que el colectivo de las personas con diversidad funcional se estima que en España era de 4.000.000 personas en 2013[^colectivo-ioe], lo cual supone más del 10% de la población.

En esta receta aprenderemos a añadir información relativa a la movilidad en la ciudad desde el punto de vista de la accesibilidad y la diversidad funcional.

{% hint %}
Debido a que el colectivo de las personas con diversidad funcional es a su vez muy diverso y cada tipo de discapacidad tiene unas necesidades distintas, este documento únicamente se refiere a las personas con discapacidad motriz o visual.
{% endhint %}


## Ingredientes

Para seguir los pasos que se detallan a continuación necesitaremos lo siguiente:

1. Disponer de los datos recogidos a partir de observaciones de campo (ver capítulo "[Recoger datos](/02.Workflow-osm/recoger-datos.md)" de este mismo libro)
2. Utilizar un editor, ya sea el editor integrado en el navegador (llamado [iD](http://learnosm.org/en/beginner/id-editor/)) o el editor avanzado JOSM ([ver parte 3](/03.JOSM/readme.md "Parte 3: JOSM"))
3. Estar familiarizado con el etiquetado en OSM (en su defecto puedes empezar a leer [este enlace](http://learnosm.org/es/beginner/start-osm/) )

## Tabla de contenidos
<!-- toc -->


## Procedimiento

El procedimiento a seguir es el mismo en todos los casos:

1. Seleccionar la geometría existente que representa el elemento a etiquetar (cruces, calles, escaleras...) o, si no existe, dibujarlaa partir de nuestras notas de campo mediante puntos o vías.
1. Etiquetar el elemento seleccionado en el paso anterior siguiendo las etiquetas específicas que se explican a continuación


## Etiquetas relacionadas con la discapacidad

Para esta receta nos centraremos en dos tipos de discapacidades, las relativas a la discapacidad motriz y a la visual, y para ello utilizaremos las etiquetas siguientes:

{% hint style='tip' %}
La wiki de OSM tiene una [página específica dedicada a la discapacidad](http://wiki.openstreetmap.org/wiki/Disabilities) en la que se recopila y discute información sobre etiquetados posibles y proyectos relativos a este tema.
{% endhint %}

{% hint %}
A lo largo de esta receta escribiremos a menudo cosas como `wheelchair=yes/no/limited` o `width=<anchura en metros>`. Se trata de las mismas convenciones utilizadas en la wiki de OSM para representar las distintas [claves con sus respectivos valores](http://wiki.openstreetmap.org/wiki/Tags) y que se traducen en lo siguiente: 
* El item que está a la izquierda del símbolo `=` es la clave, mientras que el item que está a la izquierda es su valor
* En caso de que haya varias opciones posibles para un valor se escribirán de este modo `*=yes/no/limited`, siendo respectivamente `yes`, `no` y `limited` las opciones posibles, pero dado que son excluyentes, solo se podrá utilizar una de ellas.
* El símbolo `*` es un comodín y significa que puede tener cualquier valor. 
* El  texto entre los símbolos `<` y`>` es una explicación para el lector. Cuando queramos utilizarlo en OSM no se pondrán dichos símbolos y se sustituirá por el valor real que corresponda.
* Las claves y valores siempre **se escribirán en minúsculas y sin espacios entre ellos**.
{% endhint %}

### Discapacidad motriz

Característica  | Comentarios  | Valores posibles  | Etiquetado OSM equivalente | Enlace en la Wiki OSM
--|---|---|---|--
Accesibilidad en silla de ruedas  | Se trata de un valor subjetivo basado en el resto de características a analizar o basado en observación empírica  | Sí / No / Limitada /Con ayuda  | `wheelchair=yes/no/limited` | [Key:wheelchair](https://wiki.openstreetmap.org/wiki/Key:wheelchair)
Anchura de la acera  | Se describirá la anchura en metros (valor objetivo)  | Cualquier medida (en metros)  | `width=<anchura en metros>` | [Key:width](https://wiki.openstreetmap.org/wiki/Key:width)
Tipo de bordillo  | El tipo de bordillo (y su altura) condicionan notablemente si un paso de peatones es accesible o no. Es posible que el tipo de bordillo sea distinto en los dos extremos de un cruce de peatones.  | **Elevado** (Existe un desnivel de más de 5cm entre calzada y acera); **Rebajado** (desnivel entre 5 y 3 cm entre acera y calzada que puede ser salvado con silla de ruedas -con o sin ayuda); **Enrasado** (no hay ningún desnivel entre acera y calzada)  |  `kerb=raised`, `kerb=lowered`, `kerb=flush` [^bordillos-distintos]| [Key:kerb](https://wiki.openstreetmap.org/wiki/Key:kerb)
Tipo de pavimento |  En esta tabla se detallan únicamente los pavimentos más habituales. Dada la gran variedad de opciones, reomendamos visitar [esta página de la wiki de OSM](https://wiki.openstreetmap.org/wiki/Key:surface)  | Pavimento sin espeficar, Adoquines, Asfalto, Pavimento, Sin pavimentar  | `surface=paved`, `surface=sett`, `surface=asphalt`, `surface=paving_stones`, `surface=unpaved`  | [Key:surface](https://wiki.openstreetmap.org/wiki/Key:surface)
Calidad del firme  | Valoración subjetiva del estado del firme con respecto a la rugosidad de la superficie y lo fácil o difícil que resulta desplazarse sobre él   |   |  `smoothness=excellent / good/ intermediate / bad` |  [Key:smoothness](https://wiki.openstreetmap.org/wiki/Key:smoothness)
Peldaños  | La existencia de peldaños debería complementarse con  el etiquetado `wheelchair=no` | Número de peldaños  | `step_count=*`  | [Key:step_count](https://wiki.openstreetmap.org/wiki/Key:step_count)
 

### Discapacidad motriz

Característica  | Comentarios  | Valores posibles  | Etiquetado OSM equivalente | Enlace en la Wiki OSM
--|---|---|---|--
Semáforos acústicos  |   |  Sí o no | `traffic_signals:sound= yes / no`  | [Key:traffic_signals:sound](https://wiki.openstreetmap.org/wiki/Key:traffic_signals:sound)
Pavimento táctil  | Existencia de pavimento rugoso que avisa de la finalización de acera e inicio de calzada. En algunos casos también sirve para orientarse en una parada de bus, metro o tranvía   | Sí, ornamental, decorativo  | `tactile_paving=yes/primite/no`  | [Key:tactile_paving](https://wiki.openstreetmap.org/wiki/Key:tactile_paving)
Anchura de la acera  | Se describirá la anchura en metros (valor objetivo)  | Cualquier medida (en metros)  | `width=<anchura en metros>` | [Key:width](https://wiki.openstreetmap.org/wiki/Key:width)
Tipo de bordillo  | El tipo de bordillo (y su altura) condicionan notablemente si un paso de peatones es accesible o no. Es posible que el tipo de bordillo sea distinto en los dos extremos de un cruce de peatones.  | **Elevado** (Existe un desnivel de más de 5cm entre calzada y acera); **Rebajado** (desnivel entre 5 y 3 cm entre acera y calzada que puede ser salvado con silla de ruedas -con o sin ayuda); **Enrasado** (no hay ningún desnivel entre acera y calzada)  |  `kerb=raised`, `kerb=lowered`, `kerb=flush` [^bordillos-distintos]| [Key:kerb](https://wiki.openstreetmap.org/wiki/Key:kerb)
Tipo de pavimento |  En esta tabla se detallan únicamente los pavimentos más habituales. Dada la gran variedad de opciones, reomendamos visitar [esta página de la wiki de OSM](https://wiki.openstreetmap.org/wiki/Key:surface)  | Pavimento sin espeficar, Adoquines, Asfalto, Pavimento, Sin pavimentar  | `surface=paved`, `surface=sett`, `surface=asphalt`, `surface=paving_stones`, `surface=unpaved`  | [Key:surface](https://wiki.openstreetmap.org/wiki/Key:surface)
Calidad del firme  | Valoración subjetiva del estado del firme con respecto a la rugosidad de la superficie y lo fácil o difícil que resulta desplazarse sobre él   |   |  `smoothness=excellent / good/ intermediate / bad` |  [Key:smoothness](https://wiki.openstreetmap.org/wiki/Key:smoothness)
Peldaños  | La existencia de peldaños debería complementarse con  el etiquetado `wheelchair=no` | Número de peldaños  | `step_count=*`  | [Key:step_count](https://wiki.openstreetmap.org/wiki/Key:step_count)
 

## Etiquetado de Pasos de peatones

Los pasos de peatones son elementos clave que condicionan la movilidad de las personas con diversidad funcional debido a la gran variables que contienen y a su ejecución dispar. Veamos el caso de la imagen siguiente: en este caso vemos que este cruce de peatones sería relevante etiquetar sus bordillos en forma de rampa que hacen posible que se pueda cruzar en silla de ruedas o el pavimento táctil y la presencia de semáforos acústicos.

![Cruce de peatones frente a la estación de Delicias, con rampas, pavimento táctil, semáforos acústicos y cruce de bicicletas (Fuente: CCM)](/04.Recetas/img/IMG_20160609_081418.jpg)

{% hint style='danger' %}
La representación geométrica de un paso de peatones puede ser un punto o una vía, en función de si el cruce está sobre una vía única (punto) o conecta varias vías (vía), ya sea porque cruza calles con dos vias independientes o porque cruza calzada y carriles bici o porque conecta dos aceras que están representadas gráficamente como vías independientes. A continuación se detallan las dos casuísticas de forma separada.
{% endhint %}

### Cruces de peatones como nodos:
En el caso de los cruces como nodos es el caso más sencillo, ya que el nodo representa, a la vez, tanto el propio cruce como los semáforos (si existen) y los bordillos. Por tanto, deberemos **añadir todas las etiquetas identificadas en las tablas anteriores sobre el mismo punto**. La única excepción a esa regla la encontraremos en el caso en el que los bordillos sean distintos en los extremos de los cruces. Para ello añadimos el sufijo `:left` o `:right` a la propiedad que queramos matizar, como por ejemplo `tactile_paving:right=yes` o `kerb:left=flush`.

{% hint style='tip' %}
**Caso práctico:** Supongamos que tenemos un cruce de peatones con semáforo acústico representado por un punto en el que en el lado derecho (siempre en el sentido de la marcha de la vía sobre la que está el punto) tiene una rampa y pavimento táctil pero el lado izquierdo, más antiguo, todavía no ha sido adaptado. En este caso tendríamos que etiquetar lo siguiente:

* `highway=crossing` para indicar que se trata de un paso de peatones
* `crossing=traffic_signals ` para indicar que se trata de un paso de peatones regulado por semáforos
* `traffic_signals:sound=yes` para indicar que tiene señales acústicas.
Hasta aquí todo normal, pero ahora viene la complicación, dado que deberemos especificar etiquetados distintos para el lado derecho y el izquierdo, quedando de este modo:
* `kerb:right=lowered` para indicar que en el lado derecho hay rampa
* `kerb:left=raised` para indicar que en el lado izquierdo hay un bordillo elevado
* `tactile_paving:right=yes`
* `tactile_paving:left=no`
* Finalmente, como una persona en silla de ruedas no podría cruzar el paso de peatones por ser incapaz de subir al lado izquierdo, habría que añadir `wheelchair=no`, ya que es una característica que evalúa todas las anteriores.
{% endhint %}

### Cruces de peatones como vías:
Se trata del caso más complejo, dado que la vía representa el cruce en sí (el zebreado que interseca las distintas vías que cruza) mientras que los nodos de los extremos representan los bordillos, rampas, pavimentos y semáforos (si los hubiere). También pueden existir nodos intermedios que representen isletas o cruces que intersecan con carriles bici (a menudo no tienen semáforos ni pavimentos específicos). 

{% hint style='danger' %}
Hay que tener en cuenta las siguientes consideraciones: 

1. A menudo se da el caso que ambos extremos del cruce tienen las mismas característcas físicas (en ese caso se usarán las mismas etiquetas en ambos extremos), pero no siempre es así. A veces puede ocurrir que en un extremo haya una rampa 
2. A veces hay casos en los que deberemos etiquetar más puntos que los de los extremos, como en el caso de cruces en isletas o cruces que intersecan con carriles bici (a menudo no tienen semáforos ni pavimentos específicos). Deberemos prestar mucha atención a estos puntos intermedios debido a que únicamente podremos etiquetar algunas partes.
{% endhint %}

Por esos motivos las etiquetas e información que pondremos en un caso u otro dependerán de la geometría, tal y como se especifica a continuación:



1. Etiquetado **en la vía**:
  * **Cruces de peatones** `highway=crossing`
    * Si únicamente está pintado en el suelo, sin que haya semáforos: `crossing=uncontrolled` y `crossing_ref=zebra`. Como no tendrá semáforos con señales acústicas podremos añadir directamente `traffic_signals:sound=no`
  * Si está regulado por **semáforos**, añadiremos `crossing=traffic_signals`, pero especificaremos cómo son los semáforos en los nodos
  * Rugosidad del pavimento: que permita la circulación sin dificultad en patines o carritos de la compra con ruedas pequeñas (excelente); bicis de carreras (buena) o bicis de ciudad o silla de ruedas (intermedio), `smoothness=excellent/good/intermediate/bad...` (para más información sobre los criterios de clasificación de la rugosidad remitimos a [este artículo de la wiki](http://wiki.openstreetmap.org/wiki/Key:smoothness))
  * Tipo de cruce de peatones: OSM establece una categorización de los cruces de peatones según tengan o no semáforos o permitan el paso de bicicletas. Podemos aprovechar la ocasión para añadir esta información.
    * Si **tiene semáforos** y **permite el paso de bicicletas** `crossing_ref=toucan`
    * Si **tiene semáforos** y **no permite el paso de bicicletas** `crossing_ref=pelican`
    * Si **no tiene semáforos** y **permite el paso de bicicletas** `crossing_ref=tiger`
    * Si **no tiene semáforos** y **no permite el paso de bicicletas** `crossing_ref=zebra`
2. Etiquetado **en los nodos** (extremos o intermedios):
  * Existencia de semáforo `traffic_signals: yes/no` (en caso de que no exista, añadiremos automáticamente `traffic_signals:sound=no`).
    * **Semáforos con señal acústica** en los semáforos si/no `traffic_signals:sound=yes/no`
  * **Pavimento táctil** si/no/decorativo `tactile_paving=yes/no/primitive`
  * **Tipo de bordillo** ya sea: enrasado (0cm),rebajado (3cm o menos) o elevado (más de 3 cm): `kerb_flush/lowered/raised` . Esto es importante porque determina en gran medida la siguiente etiqueta, si es accesible en silla de ruedas
  * **Accesible en silla de ruedas** si, no, o si se puede cruzar con ayuda o con una silla de ruedas motorizada `wheelchair=yes/no/limited`


## Etiquetado de Aceras
En las aceras anotaremos su anchura, el tipo de pavimento y si se puede acceder en silla de ruedas o no. De nuevo, nos encontramos ante un caso en el que el etiquetado variará en función de cómo estén representadas gráficamente las aceras, pudiendo estar representadas como vías independientes o como etiquetas de una vía[^sideways].

![Acera estrecha, con pendiente y rampas para coches que dificultan enormemente la circulación en silla de ruedas (Fuente: CCM)](/04.Recetas/img/IMG_20161203_121327.jpg)

### Aceras como vías independientes: 
En este caso tenemos una vía que representa la calzada de la calle y otra(s) distinta(s) que representa(n) la acera. Este sistema simplifica mucho el etiquetado pero exige que exista la geometría. Usaremos el siguiente etiquetado:
* Especificaremos que se trata de una acera: `highway=footway`
* Anchura (en metros) `width=<anchura en metros y usando el . como separador decimal>`. Esto es relevante porque en anchuras inferiores a 80cm no puede pasar una silla de ruedas. Con anchuras inferiores a 1m puede pasar pero con dificultad.
  {% hint style='danger' %}
Hay que tener en cuenta que la anchura de la acera puede variar o incluso tener pequeñas estrecheces. En tal caso deberá dividirse la vía en segmentos más pequeños seleccionando primeramente la vía y posteriormente los puntos que usaremos para cortar (si no existen los dibujaremos) y pulsando la tecla `P` o haciendo clic en el menú `Herramientas\Dividir una vía`) ![Acera con un estrechamiento considerable que dificulta el paso con silla de ruedas por toda la acera (Fuente: CCM)](/04.Recetas/img/2016-05-07_11-25-54.jpg)
{% endhint %}
* Tipo de pavimento: Adoquines planos y regulares (`surface=sett`), adoquines redondeados  (`surface=cobblestone`), baldosas (`surface=paving_stones`), asfalto (`surface=asphalt`) u otros (ver [descripción de la clave en la wiki de OSM](http://wiki.openstreetmap.org/wiki/Surface) para más valores).
* Rugosidad del pavimento (ver punto anterior): `smoothness=excellent/good/intermediate/bad...`
* Todo lo anterior determinará si el tramo de acera que estamos etiquetando es accesible en silla de ruedas, no lo es en absoluto o se necesita ayuda (por ejemplo debido a una pendiente excesiva): `wheelchair=yes/no/limited`

### Aceras como etiquetas a una vía existente:
En este caso no existe una geometría específica, y si anotamos etiquetas como la anchura o el pavimento, OSM entiende que en realidad se está describiendo la calzada en lugar de la acera. Por ello deberán hacerse estas dos consideraciones:

1. Añadir la etiqueta `sidewalk=both/left/right/none` en función de si hay acera en ambos lados, a la izquierda o derecha (con respecto al sentido de la vía) o en ningún lado.
1. Utilizar las mismas etiquetas que en el caso de aceras como vías independientes pero añadiendo el prefijo `sidewalk:both:<nombre etiqueta>=*`. En caso de que las propiedades sean distintas a un lado u otro se añadirá, respectivamente: `sidewalk:right:<nombre etiqueta>=*` o `sidewalk:left:<nombre etiqueta>=*`. Ejemplo de ello serían:
  * `sidewalk:both:width=*`
  * `sidewalk:both:smoothness=*`
  * `sidewalk:both:surface=*`
  * `sidewalk:both:wheelchair=*`

## Etiquetado de Escaleras

En caso de que existan escaleras dibujaremos una vía (o etiquetaremos una vía existente) como se detalla a continuación:

1. En la via:
  * Escaleras: `highway=steps`
  * Número de escalones: `step_count=<número de escalones>`
  * Anchura de las escaleras: `width=<anchura en metros>`
  * Sentido de subida de la escalera: viene determinado por la dirección de la flecha. Por defecto la punta de la flecha es el extremo alto, aunque es recomendable utilizar las etiquetas `incline=up/down` para ello (siempre en relación al sentido de la flecha).
  * Pasamanos `handrail=both/left/right`
2. En los nodos de sus extremos:
  * Pavimento táctil: `tactile_paving=yes/no`

## Etiquetando otros elementos
Además de aceras, pasos de peatones o escaleras, pueden aplicarse los mismos criterios para etiquetar todo tipo de elementos que tengan relación con la accesibilidad de personas con discapacidad.

Ejemplos de otros elementos interesantes podrían ser:

* Paradas de autobús
* Postes informativos (por ejemplo con información turística)
* Lavabos públicos
* Accesibilidad en silla de ruedas en edificios públicos, tiendas...
* ...

## Resumen

En esta receta hemos aprendido como añadir información relativa a la movilidad urbana desde el punto de vista de la accesibilidad a través del etiquetado de unas etiquetas muy concretas. Estas etiquetas se pueden aplicar a distintas geometrías (puntos, líneas) en función del elemento que describan (pasos de peatones, aceras, escaleras, paradas de bus...) y se resumen en las siguientes:

* Discapacidad visual:
  * Pavimento táctil: `tactile_paving=yes/no/incorrect`
  * Mapas en relieve:  `information=tactile_map`
  * Escritura táctil: `information=braille`
  * Sonidos (descripciones sonoras): `acoustic=voice_description`
  * Semáforos con sonido: `traffic_signals:sound= yes/no`
* Discapacidad motriz:
  * Accesible en silla de ruedas: `wheelchair=yes/no/limited`
  * Rugosidad del pavimento: `smoothness=exellent/good/...`
  * Tipo de bordillo: `kerb=lowered/raised/flush`
  * Rampa para silla de ruedas: `ramp:wheelchair=yes/no`
    * Pasamanos: `handrail=yes/no`
    * Situación del pasamanos: `handrail=right/center/left`
  * Escaleras: `highway=steps`
    * Número de escalones: `step_count= número de escalones`
    * Anchura de las escaleras: `width= anchura`
  * Parking para discapacitados: `amenity= parking` / `capacity:disabled=yes/no`
  * Parques adaptados: `leisure=playground`/ `wheelchair= yes/no`

También hemos aprendido a cómo modificar ligeramente las geometrías añadiendo nuevos puntos o partiendo elementos existentes.

{% hint %}
*Esta receta recoge el conocimiento generado en el proyecto de investigación [Zaragoza Accesible](http://zaccesible.usj.es), liderado por la [Universidad San Jorge](http://usj.es), cuya metodología e implantación técnica se ha desarrollado junto a [Mapeado Colaborativo](https://mapcolabora.org)
{% endhint %}



[^colectivo-ioe]: Colectivo Ioé (2013): “Diversidad funcional en España. Hacia la inclusión en igualdad de las personas con discapacidades”, _Revista Española de Discapacidad_, 1 (1): 33-46. doi:[http://dx.doi.org/10.5569/2340-5104.01.01.02](http://dx.doi.org/10.5569/2340-5104.01.01.02)
[^bordillos-distintos]: En caso en los que los bordillos sean distintos en los extremos de un mismo paso de peatones y este esté dibujado con un solo punto, el etiquetado variará ligeramente (ver sección específica)
[^sideways]: Para más información al respecto remitimos a este artículo de la wiki de OSM: [http://wiki.openstreetmap.org/wiki/Sidewalks](http://wiki.openstreetmap.org/wiki/Sidewalks)
