# Dibujar y etiquetar edificios

Por: Carlos Cámara, Alejandro Suárez

## Objetivos

Una parte importante (aunque a menudo descuidada en OSM) de las ciudades son los edificios. En esta receta veremos cómo dibujar la geometría de los edificios y también cómo etiquetarlos con información relativa a las propiedades del edificio. Gracias a este trabajo podremos visualizar, por ejemplo, los edificios en 3D en servicios como [OSMbuildings](http://osmbuildings.org/) o  [F4 Maps](http://demo.f4map.com/), tal y como muestra la imagen siguiente con información en 3D de Huesca.

![Captura de pantalla de Huesca en 3D desde el visor F4 Maps](/04.Recetas/img/huesca-3d.jpg)

{% hint style='danger' %}
A diferencia de programas como [Blender](http://blender.org), [Sketchup](http://sketchup.com), [Freecad](http://freecad.org)... OSM solo puede trabajar en 2D, ya que la única geometría que podemos utilizar son puntos, líneas y áreas. El efecto de 3D (o incluso el de 2.5D) se consigue gracias al uso extensivo de determinadas etiquetas, lo cual es un procedimiento completamente distinto al de modelado 3D, algo que puede acarrear cierta confusión para quienes están acostumbrados a usar este tipo de herramientas.
{% endhint %}


## Ingredientes

Para seguir los pasos que se detallan a continuación necesitaremos lo siguiente:

* Editor JOSM o iD \(aunque las capturas de pantalla hacen referencia a JOSM, los pasos también pueden reproducirse en iD\)
* Información de referencia para "calcar":
  * Catastro
  * PNOA
  * ...
  
  {% hint style='danger' %}
Para la elección de la referencia deberemos tener en cuenta especialmente tres cosas: 1) que su licencia de uso sea compatible con OSM; 2) las deformaciones derivadas de la proyección -especialmente importante en edificios altos o lugares con pendiente; y 3) que se trate de una fuente de datos fiable. Tanto Catastro como PNOA cumplen relativamente bien todos los requisitos, y además vienen incorporados por defecto en JOSM.
{% endhint %}

Además de lo anterior, puede facilitarnos mucho trabao los siguientes plugins y presets de JOSM:
* Plugins (para más información sobre qué son los plugins y como se instalan, ver receta "Cómo Añadir plugins a JOSM"): 
    * [Building tools](https://wiki.openstreetmap.org/wiki/JOSM/Plugins/BuildingsTools): un sencillo plugin para dibujar edificios rectangulares.
    * [CAD Tools](https://wiki.openstreetmap.org/wiki/JOSM/Plugins/CADTools): herramientas que emulan ciertas funcionalidades de programas de CAD para poder dibujar con mayor precisión.
    * Measurement: para obtener información sobre los ángulos que utilizaremos en las cubiertas.
    * [Relation Toolbox](https://wiki.openstreetmap.org/wiki/JOSM/Plugins/Relation_Toolbox)
    * [Terracer](https://wiki.openstreetmap.org/wiki/JOSM/Plugins/Relation_Toolbox): ideal para crear viviendas pareadas (aunque no se ha utilizado en esta receta porque el contexto en el que se sitúa -Centro de Zaragoza- no tiene estas tipologías edificatorias).
    {% hint style='tip' %}
**Protip:** Puede utilizarse el plugin Terracer para crear matrices de elementos equidistantes, aunque no sean edificios. Un buen ejemplo de ello sería, por ejemplo, una hilera de árboles plantados en un parque o paseo.
{% endhint %}
* Presets (para más información sobre qué son los presets y como se instalan, ver receta "Cómo usar presets en JOSM"): 
    * **Building preset** para simplificar los datos generales de un edificio
    * **3D Simple Buildings** para simplificar el proceso de añadir etiquetas con información en 3D.
    

Y por último es recomendable tener a mano las siguientes páginas de la wiki de OpenStreetMap:

* [Key:building](http://wiki.openstreetmap.org/wiki/Key:building) contiene información sobre los tipos de edificios
* [Simple 3D Buildings](https://wiki.openstreetmap.org/wiki/Simple_3D_buildings)
* [3D Building](http://wiki.openstreetmap.org/wiki/OSM-4D/3D_building) contiene información sobre cómo etiquetar los edificios para que sean visualizados en OSM

## Procedimiento

Hay muchas maneras de crear edificios en OSM, siendo lo más habitual crear edificios a partir de áreas cerradas o usando relaciones. En esta receta explicaremos cómo crear edificios a partir de relaciones, ya que aunque el procedimiento es algo menos intuitivo tiene la gran ventaja de que se evitan crear líneas superpuestas (por ejemplo medianeras), con el consiguiente ahorro de tiempo.

### Crear el contorno de un edificio

Lo primero que debemos hacer es dibujar la geometría de los edificios. En este primer paso empezaremos por lo más general (el perímetro) y posteriormente iremos añadiendo más detalles.

{% hint style='danger' %}
Consideramos que la unidad mínima a representar es un edificio. Debemos evitar caer en la tentación de querer ahorrar tiempo dibujando directamente una manzana para, más adelante, dividirla. Aunque tiene mucho sentido el procedimiento, al hacerlo JOSM nos advertirá de que hay edificios dentro de otros (dado que la relación inicial se mantendría).
¿Cómo podemos identificar los límites de un edificio? En caso de no disponer el conocimiento local para distinguir los límites de un edificio podemos usar las líneas gruesas del Catastro que determinan las parcelas y compararlas con las fotografías por satélite.
{% endhint %}


1. **Activar las capas de Catastro y PNOA**, que nos servirán de guía en todo momento. Utilizaremos la capa del Catastro para calcar la geometría de los edificios y saber el número de pisos de los edificios[^catastro]. La imagen satélite del PNOA nos servirá, más adelante, para obtener información acerca de las alturas, tipo de cubiertas o materiales.
<video width="100%" controls preload> 
    <source src="img/edificios-josm-catastro.webm?raw=true"></source> 
</video>

1. **Calcar sobre el catastro el perímetro de los edificios** (en este caso dibujaremos la totalidad de la manzana). Para ello utilizaremos la herramienta `línea` y marcaremos los puntos sobre la capa del catastro con la mayor precisión posible. En esta fase ignoraremos todas aquellas terrazas, torres o segmentos interiores del edificio, con la única excepción de los patios interiores que estén completamente dentro del edificio (sin tocar la medianera, dado que si no, formarían parte del perímetro).
{% hint style='tip' %}
Podemos ayudarnos en todo momento de las herramientas `zoom` y `encuadre` que se activan con la rueda central del ratón para obtener una mejor precisión.
{% endhint %}
{% hint style='danger' %}
Debemos evitar superponer líneas, incluso aunque nos parezca que el perímetro del edificio no está cerrado. Para evitar superponer líneas y tener edificios abiertos (algo que JOSM no nos dejará hacer) utilizaremos relaciones (ver a continuación).
{% endhint %}
<video width="100%" controls preload> 
    <source src="img/edificios-josm-perimetro.webm"></source> 
</video>
1. **Partir el perímetro en segmentos** delimitados por aquellos nodos en los que converjan más de tres aristas para ello. Para ello deberemos hacer lo siguiente:
    1. seleccionar la línea a dividir
    1. pulsar la tecla `MAY` y seleccionar aquél o aquellos nodos en los que converjan más de 2 segmentos.  
    1. ir al menú `Herramientas\Dividir vía` o usar directamente el atacjo de teclado: `P`.

Con esto ya tenemos dibujado todo el perímetro del edificio, solo que está troceado y por tanto no podemos etiquetarlo todavía, dado que las etiquetas de edificios solo pueden ir en áreas cerradas y no sobre elementos lineales o sobre puntos. Y como aún no hemos añadido ninguna etiqueta, no es conveniente subir todavía nuestro trabajo a OSM (si intentamos hacerlo JOSM nos advertirá de que estamos queriendo subir geometría que no está etiquetada).

{% hint style='tip' %}
Dado que el proceso de crear y etiquetar edificios es relativamente tedioso, es recomendable trabajar en un único edificio a la vez para poder crear changesets relativamente pequeños y que, por tanto, se puedan hacer en poco tiempo. 
{% endhint %}


### Convertir segmentos en un edificio

Las relaciones son una entidad específica de OSM que resulta muy versátil ya que permite agrupar elementos que tienen algún aspecto en común y establecer relaciones entre sus miembros. En este caso las utilizaremos para agrupar los segmentos independientes que conforman el perímetro de un edificio y luego le asignaremos las propiedades del edificio. Para ello deberemos realizar lo siguiente:

1. **Seleccionar los distintos segmentos** que conforman un edificio, asegurándonos que siempre tengamos un polígono cerrado (de lo contrario JOSM nos mostrará una advertencia en el siguiente paso)
{% hint style='tip' %}
Para seleccionar más de un objeto a la vez podemos hacer clic pulsando simultáneamente la tecla `MAY`. En caso de querer deseleccionar algún elemento, podemos pulsar la tecla `CTRL` mientras hacemos clic.
{% endhint %}

1. **Crear una relación** a partir de los elementos seleccionados haciendo clic en el menú `Herramientas\Crear multipolígono` o con el atajo de teclado: `CTRL+B`.
<video width="100%" controls preload> 
    <source src="img/edificios-josm-perimetro-02.webm"></source> 
</video>
{% hint style='tip' %}
En el caso de los edificios que contengan un patio en su interior, deberemos seleccionar, además, el perímetro cerrado que define el patio. Al crear la relación JOSM le asignará el rol `role=inner` a dicho perímetro para crear así el hueco. 
{% endhint %}


Con los pasos anteriores hemos creado una relación, pero falta decir que dicha relación es en realidad un edificio, para ello deberemos:

1. **Seleccionar una vía (línea)** que sea parte de la relación que acabamos de crear.
1. **Seleccionar la relación** a la que pertenece la vía seleccionada en el caso anterior. Para ello hay que hacer doble clic en la relación recién creada que se muestra en el panel lateral derecho `Etiquetas|Membresías`.  
![El panel "Tags" muestra que el segmento seleccionado pertenece a tres relaciones, la primera de las cuales está seleccionada](/04.Recetas/img/edificios-josm-seleccionar-relación.png)
{% hint style='danger' %}
Hay que tener en cuenta que un elemento puede pertenecer a más de una relación a la vez (en realidad, las medianeras pertenecerán, como mínimo, a dos relaciones, una para cada edificio que separan). Por eso debemos de estar seguros de que seleccionamos la relación que queremos modificar y no otra. 
En la imagen superior, el panel "Tags" muestra que el segmento seleccionado pertenece a tres relaciones, la primera de las cuales está seleccionada.
Algunas relaciones tienen nombre, lo cual facilita mucho saber qué relación estamos modificando. Una buena práctica consiste en darles nombres a las relaciones, para ello podemos usar la etiqueta `name=<nombre oficial>` (en caso de que tenga un nombre oficial) y para aquellos casos  en los que queremos dar un nombre descriptivo a nivel interno, podemos usar `note=<breve descripción>`.
{% endhint %}

3. **Añadir las siguientes etiquetas** a la relación seleccionada:
    *  `type=multipoligon` (este es un valor fijo añadido automáticamente al crear una relación e indica, precisamente, que se trata de una relación -aka, un polígono virtual) 
    *  `building=<lo que sea>` El valor por defecto será `yes`, sin embargo, ese valor solamente indica que se trata de un edificio, sin indicar de qué tipo se trata. Si queremos ser más concretos podemos especificar el tipo de edificio, como por ejemplo una iglesia (`building=church`), un edificio residencial (`building=residential`), una vivienda aislada (`building=detached`) o un edificio público (`building=public`), entre otros)
    
{% hint style='tip' %}
El listado completo de los valores posibles se encuentra en esta página de la wiki OSM: [Key:building](http://wiki.openstreetmap.org/wiki/Key:building))
{% endhint %}

¡Ahora sí! Ya tenemos una geometría que define un perímetro y le hemos añadido las etiquetas mínimas para definir un edificio. **Este sería un buen momento para publicar nuestro changeset y compartirlo con la comunidad de OSM**, sin embargo podemos hacer todavía más cosas.

### Añadir información 3D

Cada edificio debería tener su relación independiente, reflejando sus características generales:

La **altura del edificio**:
*  `building:levels=<el máximo>`Aquí especificamos el número de pisos por encima del nivel del suelo del edificio en su conjunto. En caso de que tenga partes con alturas distintas lo especificaremos más adelante \(Ver paso siguiente\).
*  `height=<la máxima>` Aquí especificamos la altura por encima del nivel del suelo del edificio en su conjunto. En caso de que tenga partes con alturas distintas lo especificaremos más adelante \(Ver paso siguiente\). 

{% hint %}
Para calcular la altura de los edificios, OSM utiliza la clave `height`. En caso de que esta etiqueta no exista, utiliza la regla de multiplicar `x3` el número de pisos (`building:levels`), algo que puede ser una aproximación razonable para muchos edificios de viviendas habituales, pero tremendamente erróneo en edificios singulares como iglesias, que a pesar de tener una sola planta, la nave central suele tener una altura muy superior a los 3 metros.
{% endhint %}

Otro aspecto interesante son las cubiertas del edificio. 

* `roof:shape`
* `roof:direction`
* `roof:orientation`
* `roof:material`
* ...

{% hint style='tip' %}
Las cubiertas son uno de los temas más complejos del modelado en 3D de un edificio, y también del etiquetado en OSM. El sistema de etiquetado de cubiertas de OSM permite "modelar" una gran variedad de formas, pero exige ser sistemáticos. Para una descripción completa del sistema de etiquetado referimos a la lectura de los siguientes enlaces de la wiki:
* [Sección de "cubiertas" en la entrada 3D-Buildings](http://wiki.openstreetmap.org/wiki/OSM-4D/3D_building#Roof) 
* [Roof table](http://wiki.openstreetmap.org/wiki/OSM-4D/Roof_table)
{% endhint %}

Todo esto funciona de maravilla en edificios relativamente sencillos que tienen siempre la misma altura, el mismo tipo de cubierta, materiales... ¿pero qué ocurre con aquellos edificios cuyas propiedades no son constantes? Pues para eso está el siguiente paso.

#### Añadir "partes" con más información a los edificios 

Para edificios cuyas propiedades (altura, cubiertas, materiales...) no son constantes, deberemos descomponerlo en "partes" que sí mantienen las mismas propiedades. El procedimiento es muy similar al que hemos seguido anteriormente, con la salvedad de que añadiremos nuevas relaciones con la etiqueta `building:part=yes`, tal y como detallamos a continuación:

1. Dibujar segmentos (vías) que dividan las distintas partes del edificio
1. Dividir el perímetro de los edificios en aquellos nodos que conecten más de dos vías (mismo procedimiento que el que hemos explicado anteriormente)
1. Seleccionar los elementos que conforman la parte del edificio (deberán delimitar un área cerrada) y crear una relación.
1. Etiquetar la relación con las mismas etiquetas que hemos visto anteriormente:
    * `building:part=<yes>` Esta es la única etiqueta distinta a las anteriores. Con ella estamos definiendo que la relación no es un edificio (de lo contrario tendríamos un edificio dentro de otro) sino una parte del mismo, y como tal, puede tener las mismas propiedades (etiquetas) que si se tratase de un edificio normal.
    * `building=<lo que sea>`
    * `building:levels=<el de esa zona>`
    * `height=<la de esa zona>`
    * Cualquiera de las etiquetas que podemos añadir a un edificio ...
1. Repetir el proceso por cada una de las partes que conformen el edificio.


## Resumen

Resumirlo brevemente.

[^catastro]: Aunque el Catastro es un documento legal, no hay que confiar ciegamente en él, dado que puede contener información incorrecta o desactualizada. De ahí que sea recomendable contrastarla con otras fuentes o, si tenemos oportunidad, visitando el emplazamiento y conociéndolo de primera mano.


