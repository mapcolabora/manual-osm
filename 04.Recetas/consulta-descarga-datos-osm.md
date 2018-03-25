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

{% hint style='tip' %}
Las consultas son en realidad búsquedas que, a diferencia de lo que ocurre con el buscador de OSM[^nominatim], permiten la utilización de varios parámetros y devuelve todos los resultados que coinciden con los criterios de búsqueda. 
{% endhint %}

### Paso 2: Construir la consulta a OSM
Uno de los servicios más habituales para hacer consultas es [Overpass Turbo](http://overpass-turbo.eu/). Overpass Turbo es una web que ofrece una interfaz gráfica para ejecutar consultas utilizando la sintaxis de la [API Overpass](https://wiki.openstreetmap.org/wiki/Overpass_API) (ver captura).

![Captura de pantalla de Overpass Turbo. La mitad izquierda muestra la consulta en sintaxis Overpass. La mitad derecha, un mapa con los resultados de la consulta](/assets/overpass-turbo.png)

Para construir la consulta podemos escribirla directamente en la parte izquierda de la pantalla, utilizando la sintaxis Overpass, o bien utilizar el asistente que la escribirá por nosotros. Optaremos por esta segunda opción. Para ello basta con hacer clic en el botón `Asistente` que aparece en la parte superior de la pantalla. Al hacerlo, se abre una ventana nueva con un cuadro de texto en el que deberemos introducir nuestros términos de búsqueda (ver captura).

![El asistente de Overpass Turbo permite introducir nuestra búsqueda y ofrece también ejemplos de ayuda.](/assets/overpass-turbo-wizard.png)

Hemos visto en el paso anterior que para encontrar todos los museos debemos introducir la consulta `tourism=museum`. Ahora falta indicarle que, de todos los museos de todo el mundo que están en OpenStreetMap, únicamente queremos los que se encuentran en Zaragoza. Por defecto, Overpass busca los resultados que se encuentran en los límites del mapa que se muestra en la parte derecha de la pantalla. Por tanto, para limitar los resultados a los que se encuentran en Zaragoza tenemos dos opciones: la primera consiste en desplazarnos por el mapa hasta encuadrar la totalidad de Zaragoza en la pantalla derecha y ejecutar la consulta. La segunda consiste en añadir `in Zaragoza` (o el nombre de la ciudad o región que queramos buscar) a la consulta anterior[^region]. Tal y como muestra la figura, nuestra consulta final quedaría de la forma siguiente: `tourism=museum in Zaragoza`.

Una vez hayamos escrito los criterios de la consulta deberemos ejecutarla, para lo cual haremos clic en el botón `construir y ejecutar la consulta`. Al hacerlo, se producen dos cosas: 

1. Se redacta la consulta en la parte izquierda de la pantalla utilizando la sintaxis de Overpass (es lo que se llama "construir la consulta").
2. Se buscan todos los elementos que cumplen las condiciones de la consulta (la consulta se ejecuta) y se muestran en el mapa de forma destacada (además, también podemos hacer clic sobre los resultados para conocer la información de ese elemento y comprobar el resultado).

{% hint style='tip' %}
Las consultas de overpass pueden tener más de un criterio a la vez añadiendo el operador `and`. Si, por ejemplo, quisiésemos buscar todos los museos de Zaragoza gestionados por el Ayuntamiento, podríamos hacer una consulta como esta: `tourism=museum and operator="Ayuntamiento de Zaragoza" in Zaragoza`.
{% endhint %}

{% hint style='tip' %}
Hasta ahora siempre hemos introducido búsquedas que tenían una clave y un valor, pero también pueden hacerse búsquedas que únicamente tengan una clave, sin especificar el valor. De este modo obtendremos todos los elementos que tienen información sobre esa clave (sea la que sea, siempre que no esté vacía). Imaginemos por un momento que, en lugar de buscar todos los museos, queremos buscar todos los elementos relativos al turismo, como hoteles, hostales, galerías de arte... y, por supuesto y como hemos visto a lo largo de esta explicación, también los museos[^key:tourism]. En este caso, deberíamos escribir `tourism=*` donde `*` funciona como comodín para indicar que buscamos todos los posibles valores de esta clave.
{% endhint %}

{% hint style='tip' %}
En caso de no recordar todo esto, el propio asistente ofrece unos ejemplos de las casuísticas más habituales.
{% endhint %}

### Paso 3: Descargar los resultados

Al final del paso anterior hemos conseguido visualizar todos los elementos que cumplen nuestras condiciones de búsqueda (la consulta propiamente dicha). Sin embargo, por el momento únicamente podemos hacer clic sobre ellos para ver qué información tiene OSM sobre ellos.

Dado que lo que buscamos es poder utilizar esos datos en una aplicación externa (como podría ser QGIS) sería estupendo si pudiésemos hacer una copia de los datos específicos que tiene OSM para poder usarlos sin conexión y sin necesidad de recurrir a OSM para nada más. De eso es de lo que se encarga la opción **Exportar** que aparece en la barra superior.

![La ventana Exportar ofrece opción de exportar los datos de la consulta, una imagen con el mapa y los resultados o la propia consulta](/assets/overpass-turbo-export.png)

Al hacer clic en el botón **Exportar** se abrirá una ventana (ver captura de pantalla superior) que ofrece varias opciones:

1. Exportar los **datos**: con esta opción lo que se exporta son los resultados de la consulta, tanto la información geográfica como los atributos que describen a cada entidad. Dentro de esta sección podemos elegir distintos formatos así como descargarlos o copiar el contenido del archivo.
2. Exportar el **mapa**: con esta opción se exporta un mapa como el que se mostraba en la parte derecha de la pantalla. Este mapa puede ser estático (una imagen) o interactivo.
3. Exportar la **consulta**: con esta opción se exporta el código de la consulta Overpass que se escribe en la parte izquierda de la pantalla.

Para nuestro ejemplo elegiríamos la opción 1: exportar datos y haríamos clic sobre el enlace "descargar como GeoJSON", por tratarse de un formato abierto muy utilizado para visualizar información geoespacial ya que puede ser abierto por la gran mayoría de programas que trabajan con estos datos.

Al hacerlo, tendremos un archivo en formato GeoJSON que podremos utilizar en un gran número de softwares y servicios que trabajan con información geográfica, entre ellos QGIS, y ya habríamos terminado.

### (Opcional): Utilizar QGIS y el plugin QuickOSM

En el supuesto de que lo que quisiéramos fuese trabajar con los museos de Zaragoza en QGIS, podemos utilizar el plugin QuickOSM en sustitución de los pasos anteriores.
 
QuickOSM es un plugin para QGIS 2.18 que realiza consultas Overpass de forma muy similar a OVerpass Turbo pero mostrando un cuadro de diálogo


## Resumen

En esta receta hemos visto cómo podemos descargar información específica de OSM mediante la creación de consultas overpass, que pueden ser tan complejas y específicas como queramos, y cómo podemos descargar los resultados para poder utilizarlos sin conexión a OSM e incluso en programas y servicios de terceras partes.

[^nominatim]: El buscador que utiliza OSM se llama "[Nominatim](https://nominatim.openstreetmap.org/)" y es en realidad un servicio externo a OSM y uno de los múltiples buscadores de direcciones que existen. Para reducir los tiempos de búsqueda, Nominatim únicamente busca los valores de las etiquetas relativas a los nombres de los lugares y de sus direcciones. Además, también asume que estamos buscando cosas cercanas a la zona que estamos viendo en la pantalla en ese momento.
[^region]: Para que este método funcione es necesario que la región geográfica que escribamos (puede ser el nombre de un país, una comunidad autónoma, una provincia, una ciudad, un barrio...) esté definida como área y, por tanto, tenga una superfície dentro de la cual buscar. Esto no pasa, por ejemplo, con los barrios de Zaragoza, que están introducidos como puntos y, por tanto, si quisieramos limitar nuestra búsqueda a un barrio concreto deberíamos utilizar el método anterior y encuadrar en el mapa los límites del barrio.
[^key:tourism]: Para una descripción de todos los elementos que incluye la clave `tourism` debemos visitar la wiki específica para esta categoría: [https://wiki.openstreetmap.org/wiki/Key:tourism](https://wiki.openstreetmap.org/wiki/Key:tourism). Por regla general, siempre es recomendable visitar la wiki de las categorías antes de realizar una consulta para saber si describen lo que realmente estamos buscando.
