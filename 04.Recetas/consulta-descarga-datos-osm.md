{% hint style='tip' %}
Esto es tan solo una plantilla. Puedes copiar esta receta y usarla como base para desarrollar una nueva receta sobre cualquier tema relacionado con OSM.
{% endhint %}

# Consulta y descarga de datos de OSM

Por: Carlos Cámara

## Objetivos

A lo largo de las páginas anteriores ha quedado claro que OpenStreetMap es una base de datos espaciales en la que hay muchísima más información que la que se muestran en la web de OSM. En esta receta veremos cómo buscar, mostrar y descargar información muy concreta de esta base de datos para poder utilizarla en aplicaciones de terceras partes, como por ejemplo [QGIS](http://qgis.org "Página oficial de QGIS").

## Ingredientes

Para seguir los pasos que se detallan a continuación necesitaremos lo siguiente:

1. Tener claro cómo se almacena la información textual en OSM
2. Conocer las claves y valores que describen los elementos que queremos buscar
3. Un constructor de consultas para OSM como [Overpass Turbo](http://overpass-turbo.eu/)
4. Opcionalmente (y como alternativa al punto anterior): QGIS y su plugin QuickOSM

## Procedimiento

Para la realización de esta receta vamos a suponer que queremos realizar un mapa que muestre información sobre los museos de Zaragoza y para ello queremos descargar toda la información disponible en OSM sobre ellos.

### Paso 1: Elegir las claves y valores adecuados

Como recordaréis de capítulos anteriores, la información de OSM se almacena siempre siguiendo un par de valores en un formato como este `building=hotel` o `name=` o `building:levels=2`: el primero es la clave, y es la encargada de definir una propiedad del elemento al que están asociados. Esa propiedad puede ser genérica, como el nombre (`name=*`) . Como se trata de un valor que 

![](http://learnosm.org/images/josm/josm_preferences.png)

### Paso n

Explicar paso n

## Resumen

Resumirlo brevemente.
