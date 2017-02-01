\(Puedes copiar esta receta y usarla como base para desarrollar una nueva\)

# Añadir edificios

Por: Alejandro Suárez, Carlos Cámara

## Objetivos

Dibujar edificios y etiquetarlos con detalle suficiente para que se visualicen en 3D en otros servicios como [OSMbuildings](http://osmbuildings.org/) o  [F4 demo](http://demo.f4map.com/) , tal y como muestra la imagen siguiente con información en 3D de Huesca.![](/03.Recetas/img/huesca-3d.jpg)

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

Explicar qué se dibuja primero, cuando se necesita trocear...




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

