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
Estar familiarizado con el etiquetado en OSM (en su defecto puedes empezar a leer [este enlace](http://learnosm.org/es/beginner/start-osm/) )





## Procedimiento

Para la realización de esta receta vamos a suponer que queremos realizar un mapa que muestre información sobre los museos de Zaragoza y para ello queremos descargar toda la información disponible en OSM sobre ellos.

### Paso 1: Elegir las claves y valores adecuados

{% hint %}
A lo largo de esta receta escribiremos a menudo cosas como `wheelchair=yes/no/limited` o `width=<anchura en metros>`. Se trata de las mismas convenciones utilizadas en la wiki de OSM para representar las distintas [claves con sus respectivos valores](http://wiki.openstreetmap.org/wiki/Tags) y que se traducen en lo siguiente: 
* El item que está a la izquierda del símbolo `=` es la clave, mientras que el item que está a la izquierda es su valor
* En caso de que haya varias opciones posibles para un valor se escribirán de este modo `*=yes/no/limited`, siendo respectivamente `yes`, `no` y `limited` las opciones posibles, pero dado que son excluyentes, solo se podrá utilizar una de ellas.
* El símbolo `*` es un comodín y significa que puede tener cualquier valor. 
* El  texto entre los símbolos `<` y`>` es una explicación para el lector. Cuando queramos utilizarlo en OSM no se pondrán dichos símbolos y se sustituirá por el valor real que corresponda.
* Las claves y valores siempre **se escribirán en minúsculas y sin espacios entre ellos**.
{% endhint %}

Como recordaréis de capítulos anteriores, la información de OSM se almacena siempre siguiendo un par de valores en un formato como este `building=hotel` o `name=` o `building:levels=2`: el primero es la clave, y es la encargada de definir una propiedad del elemento al que están asociados. Esa propiedad puede ser genérica, como el nombre (`name=*`) o más concreta como `building=*` o incluso matizar alguna etiqueta previa, como el caso de `building:levels=*` o de `social_facility= *` que se utiliza para describir el tipo de equipamiento social cuando previamente se ha indicado que se trata de un equipamiento de tipo social utilizando `amenity=social_facility`. El segundo elemento se le llama "valor" y describe con más precisión el tipo de clave.

{% hint style='tip' %}
Después de esta explicación queda más claro el motivo por el cual todas las claves y la mayoría de valores (salvo los nombres propios) se escriben siempre en inglés: de este modo podemos hacer la misma consulta en todo el mundo, en lugar de tener que aprender cómo se dice lo mismo en distintos lugares e idiomas. ¡Recordad que OpenStreetMap es un proyecto de escala mundial, y por ello se utiliza el inglés como *lingua franca*!
{% endhint %}

Imaginemos que queremos descargar todos los museos de Zaragoza. Lo primero que deberíamos hacer es informarnos de qué claves y valores se utilizan para describir los museos. A medida que trabajamos con OSM esto es algo que aprenderemos de memoria, pero es habitual que, al principio, no estemos tan familiarizados con las etiquetas que se utilizan. Si no lo sabemos, tenemos dos opciones:

1. **Buscar en el buscador de la wiki el nombre del concepto que buscamo**s, en nuestro caso `museum` (recordad que la wiki está escrita mayormente en inglés, así que por lo general encontraremos mejor información si buscamos también en inglés). El buscador nos dará información de las etiquetas a utilizar (ver captura) ![Resultados de búsqueda de la wiki. El primer resultado muestra que la combinación de clave y valor más habituales](/assets/wiki-search-museum.png)
2. **Buscar en OpenStreetMap un elemento de la misma categoría que estamos buscando** y fijarnos en qué etiquetas utiliza para describirlo. ![](/assets/museo-caixa-forum.png)

 En la captura de pantalla superior hemos buscado el "Caixa Forum Zaragoza" porque sabemos que es uno de los museos de la ciudad, y allí nos aparecen un montón de etiquetas como la dirección (todas tienen el prefijo `addr:*`), su web (`website=*`), fecha de inauguración (`start_date=2014`), la entidad que gestiona el museo (`operator=*`) o incluso el nombre de la arquitecta que diseñó el edificio (`architect=Carme Pinòs`). De entre todas las etiquetas, la que nos interesa es esta: `tourism=museum`, ya que es la que indica que se trata de una atracción turística y, más concretamente, de un museo.  
 
Ahora que ya tenemos claro que lo que estamos buscando se describe siempre en OSM de este modo `tourism=museum` podemos hacer una consulta a la base de datos para que nos devuelva todos los museos que existen en Zaragoza. 

{% hint style='tip' %}Las consultas son en realidad búsquedas que, a diferencia de lo que ocurre con el buscador de OSM[^nominatim], permiten la utilización de varios parámetros y devuelve todos los resultados que coinciden con los criterios de búsqueda. 
{% endhint %}

### Paso 2: Hacer la consulta a OSM mediante 
Uno de los servicios más habituales para hacer consultas es [Overpass Turbo](http://overpass-turbo.eu/). Overpass Turbo es una web que ofrece una interfaz gráfica para ejecutar consultas utilizando la sintaxis de la [API Overpass](https://wiki.openstreetmap.org/wiki/Overpass_API) (ver captura).

![Captura de pantalla de Overpass Turbo](/assets/overpass-turbo.png)



## Resumen

Resumirlo brevemente.

[^nominatim]: El buscador que utiliza OSM se llama "[Nominatim](https://nominatim.openstreetmap.org/)" y es en realidad un servicio externo a OSM y uno de los múltiples buscadores de direcciones que existen. Para reducir los tiempos de búsqueda, Nominatim únicamente busca los valores de las etiquetas relativas a los nombres de los lugares y de sus direcciones. Además, también asume que estamos buscando cosas cercanas a la zona que estamos viendo en la pantalla en ese momento.


