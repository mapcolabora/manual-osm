# Añadir edificios

Por: Carlos Cámara, Alejandro Suárez

## Objetivos

Una parte importante (aunque a menudo descuidada en OSM) de las ciudades son los edificios. OSM proporciona una gran flexibilidad que permite conocer 
Dibujar edificios y etiquetarlos con detalle suficiente para que se visualicen en 3D en otros servicios como [OSMbuildings](http://osmbuildings.org/) o  [F4 Maps](http://demo.f4map.com/), tal y como muestra la imagen siguiente con información en 3D de Huesca.

![](/03.Recetas/img/huesca-3d.jpg)

## Ingredientes

Explicar si necesitamos algún material o algo en especial \(ej: "Usaremos JOSM", "necesitaremos fieldpapers para tomar datos"...\)

* Editor JOSM o iD \(aunque las capturas de pantalla hacen referencia a JOSM, los pasos también pueden reproducirse en iD\)
* Información de referencia para "calcar":
  * Catastro
  * PNOA
  * ...
* Plugin
* Preset de JOSM: 3D buildings para simplificar el proceso de añadir etiquetas con información en 3D.

Además, es recomendable tener a mano las siguientes páginas de la wiki de openstreetmap:

* [Key:building](http://wiki.openstreetmap.org/wiki/Key:building) contiene información sobre los tipos de edificios
* [3D Building](http://wiki.openstreetmap.org/wiki/OSM-4D/3D_building) contiene información sobre cómo etiquetar los edificios para que sean visualizados en OSM

## Procedimiento

Explicar el procedimiento paso a paso

### Dibujar

Lo primero que debemos hacer es dibujar la geometría de los edificios. En este primer paso empezaremos por lo más general (el perímetro) y posteriormente iremos añadiendo más detalles.

1. **Activar las capas de Catastro y PNOA**, que nos servirán de guía en todo momento. Utilizaremos la capa del Catastro para calcar la geometría de los edificios y saber el número de pisos de los edificios[^catastro]. La imagen satélite del PNOA nos servirá, más adelante, para obtener información acerca de las alturas, tipo de cubiertas o materiales.
![](/03.Recetas/img/edificios-josm-catastro.webm)

1. **Calcar sobre el catastro el perímetro de los edificios** (en este caso dibujaremos la totalidad de la manzana). Para ello utilizaremos la herramienta `línea` y marcaremos los puntos sobre la capa del catastro con la mayor precisión posible.
{% hint style='tip' %}
Podemos ayudarnos en todo momento de las herramientas `zoom` y `encuadre` que se activan con la rueda central del ratón para obtener una mejor precisión.
{% endhint %}
![](/03.Recetas/img/edificios-josm-perimetro.webm)
1. Añadir las medianeras de los edificios.
1. Partir el perímetro en segmentos, para ello (Atajo de teclado: `P`)
1. Seleccionar los distintos segmentos que conforman un edificio y crear una relación (Atajo de teclado: `CTRL+B`)

<video width="875" height="5255" controls preload> 
    <source src="img/edificios-josm-catastro.webm?raw=true"></source> 
</video>


## Crear la relación

Explicar qué elementos deben formar parte de la relación y cómo crearla. Copiado de email en tak-es:

>Tendrías que cambiar la existente y crear nuevas. Con josm es fácil, dibuja todas las vías que delimitarán edificios o partes de estás. Después parte las vías (P) en todos los nodos donde intersecten 3 o más vías. Después selecionas todas las vías que delimitan una parte y le das a Ctrl+b ¡Chas! Multipoligono creado. 
>
>Para editar las etiquetas de una relación: selecionas una vía que sea parte de la relación y en el panel de la derecha donde aparecen las etiquetas, haces doble clic en la relación recién creada. En la ventana recién creada puedes editar las etiquetas de la relación y sus miembros. 


Cada edificio debería tener su relación independiente, reflejando sus características generales:

*  `type=multipoligon` Valor fijo para que se cree una relación 
*  `building=<lo que sea>`Aquí especificamos el tipo de edificio \(puede ser una iglesia, un edificio residencial, una vivienda aislada o un edificio público, entre otros - para ver los valores posibles referimos a la wiki [Key:building](http://wiki.openstreetmap.org/wiki/Key:building))
*  `building:levels=<el máximo>`Aquí especificamos el número de pisos por encima del nivel del suelo del edificio en su conjunto. En caso de que tenga partes con alturas distintas lo especificaremos más adelante \(Ver paso siguiente\).
*  `height=<la máxima` Aquí especificamos el número de pisos por encima del nivel del suelo del edificio en su conjunto. En caso de que tenga partes con alturas distintas lo especificaremos más adelante \(Ver paso siguiente\).
* ...

## Añadir detalles a los edificios

Después si se quiere hilar fino, las partes distintas de cada edificio se hacen con building parts:

* `Building:part=lo que sea`
* `Building=lo que sea`
* `Building:levels=el de esa zona `
* `Height=la de esa zona `
* ...

### Paso n

Explicar paso n

## Resumen

Resumirlo brevemente.

[^catastro]: Aunque el Catastro es un documento legal, no hay que confiar ciegamente en él, dado que puede contener información incorrecta o desactualizada. De ahí que sea recomendable contrastarla con otras fuentes o, si tenemos oportunidad, visitando el emplazamiento y conociéndolo de primera mano.