# Etiquetar aspectos relativos a la movilidad desde el punto de la accesibilidad y diversidad funcional en OSM
Por: Carlos Cámara, César Canalís

## Objetivos

Tal y como hemos visto en el capítulo ["¿Qué hace grande a OSM?"](/01.Intro-OSM/osm-relevancia.md) , una de las ventajas de utilizar OSM es la posibilidad de hacer mapas temáticos que, por sus características, no suelen tener cabida en otros mapas comerciales u oficiales. Un ejemplo de ello es que apenas existen mapas que sean de utilidad para personas con algún tipo de discapacidad, a pesar de que el colectivo de las personas con diversidad funcional se estima que en España era de 4.000.000 personas en 2013[^colectivo-ioe], lo cual supone más del 10% de la población.

En esta receta aprenderemos a añadir información relativa a la movilidad en la ciudad desde el punto de vista de la accesibilidad y la diversidad funcional.

{% hint %}
Debido a que el colectivo de las personas con diversidad funcional es a su vez muy diverso y cada tipo de discapacidad tiene unas necesidades distintas, este documento únicamente se refiere a las personas con discapacidad motriz o visual.
{% endhint %}

{% hint style='tip' %}
La wiki de OSM tiene una [página específica dedicada a la discapacidad](http://wiki.openstreetmap.org/wiki/Disabilities) en la que todo tipo de etiquetados y proyectos relativos a este tema.
{% endhint %}

## Ingredientes

Para seguir los pasos que se detallan a continuación necesitaremos lo siguiente:

1. Disponer de los datos recogidos a partir de observaciones de campo (ver capítulo "[Recoger datos](/02.Workflow-osm/recoger-datos.md)" de este mismo libro)
2. Utilizar un editor, ya sea id o JOSM
3. Estar familiarizado con el etiquetado en OSM (en su defecto puedes empezar a leer [este enlace](http://learnosm.org/es/beginner/start-osm/) )

## Procedimiento

Se han identificado los siguientes aspectos relevantes con relación a la movilidad y la discapacidad y en esta receta aprenderemos a etiquetarlas y colocarlas en pasos de peatones y calles a partir de la geometría existente (aunque en algunos casos deberemos añadir nuevos puntos, recortar vías existentes o añadir nuevas):

* Discapacidad visual:
  * Pavimento táctil: `tactile_paving=yes/no/incorrect`
  * Mapas en relieve:  `information=tactile_map`
  * Escritura táctil: `information=braille`
  * Sonidos (descripciones sonoras): `acoustic=voice_description`
  * Semáforos con sonido: `traffic_signals:sound= yes/no`
* Discapacidad motriz:
  * Accesible en silla de ruedas: `wheelchair=yes/no/limited`
  * Tipo de bordillo: `kerb=lowered/raised/flush`
  * Rampa para silla de ruedas: `ramp:wheelchair=yes/no`
    * Pasamanos: `handrail=yes/no`
    * Situación del pasamanos: `handrail=right/center/left`
  * Escaleras: `highway=steps`
    * Número de escalones: `step_count= número de escalones`
    * Anchura de las escaleras: `width= anchura`
  * Parking para discapacitados: `amenity= parking` / `capacity:disabled=yes/no`
  * Parques adaptados: `leisure=playground`/ `wheelchair= yes/no`


### Pasos de peatones

a

## Resumen

Resumirlo brevemente.

[^colectivo-ioe]: Colectivo Ioé (2013): “Diversidad funcional en España. Hacia la inclusión en igualdad de las personas con discapacidades”, _Revista Española de Discapacidad_, 1 (1): 33-46. doi:[http://dx.doi.org/10.5569/2340-5104.01.01.02](http://dx.doi.org/10.5569/2340-5104.01.01.02)