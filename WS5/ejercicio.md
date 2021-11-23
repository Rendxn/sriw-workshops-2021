# Taller 5 - SPARQL

## Ejercicio 1

Cree una consulta que obtenga las ciudades(individuals) sin repetir que están representadas en la ontología de las farolas.

```SPARQL
PREFIX ap: <http://vocab.linkeddata.es/datosabiertos/def/urbanismo-infraestructuras/alumbrado-publico#>
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT DISTINCT ?ciudad
{
    ?farola a ap:PuntoDeAlumbrado.
    ?farola dbo:city ?ciudad.
}
```

## Ejercicio 2

Cree una consulta que obtenga las diferentes propiedades que puede tener una farola.

```SPARQL
PREFIX ap: <http://vocab.linkeddata.es/datosabiertos/def/urbanismo-infraestructuras/alumbrado-publico#>
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT DISTINCT ?property
{
    ?farola a ap:PuntoDeAlumbrado.
    ?farola ?property ?value.
}
```

## Ejercicio 3

Cree una consulta que obtenga la latitud y la longitud de las farolas que tienen una altura Alta.

```SPARQL
PREFIX ap: <http://vocab.linkeddata.es/datosabiertos/def/urbanismo-infraestructuras/alumbrado-publico#>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>
PREFIX skosaltura: <http://vocab.linkeddata.es/datosabiertos/kos/urbanismo-infraestructuras/alumbrado-publico/altura/>

SELECT DISTINCT ?farola ?latitud ?longitud
{
    ?farola a ap:PuntoDeAlumbrado.
    ?farola geo:lat ?latitud.
    ?farola geo:long ?longitud.
    ?farola ap:altura skosaltura:Alta.
}
```

## Ejercicio 4

Cree una consulta que obtenga el id y la potencia de las farolas con una potencia mayor a 100.

```SPARQL
PREFIX ap: <http://vocab.linkeddata.es/datosabiertos/def/urbanismo-infraestructuras/alumbrado-publico#>
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT DISTINCT ?farola ?id ?potencia
{
    ?farola a ap:PuntoDeAlumbrado.
    ?farola ap:id ?id.
    ?farola ap:potencia ?potencia.
    FILTER(?potencia > 100)
}
```

## Ejercicio 5

Cree una consulta que obtenga el nombre de la persona y el nombre de la categoría del premio nobel que gano, de los primeros 100 resultados y ordénelos de manera ascendente según su nombre.

```SPARQL
SELECT ?nombre ?categoria
{
    ?persona a dbo:Person.
    ?persona rdfs:label ?nombre.
    ?persona dbo:award ?premio.
    ?premio dct:subject dbc:Nobel_Prize.
    ?premio rdfs:label ?categoria.
}
ORDER BY ASC(?nombre)
LIMIT 100
```

## Ejercicio 6

Realice una consulta en DBPedia que retorne el NOMBRE de todos los recursos de tipo Software que su lenguaje de programación sea JAVA y estén disponibles para GNU/Linux ó OS_X sin resultados repetidos.

```SPARQL
SELECT DISTINCT ?name ?os ?lang
{
    ?resource a dbo:Software.
    ?resource rdfs:label ?name.
    ?resource dbp:programmingLanguage ?lang.
    ?resource dbp:operatingSystem ?os.
    FILTER(?lang = dbr:Java_\(programming_language\))
    FILTER(?os = dbr:MacOS || ?os = dbr:Linux)
}
```

## Ejercicio 7

Realice una consulta en DBPedia que retorne el NOMBRE de todas las empresas privadas que tiene como producto Motocicletas o Cuatrimotos y que tenga su sede en Japón.

```SPARQL
SELECT ?nombre ?country
{
  ?company dbo:type dbr:Public_company.
  ?company rdfs:label ?nombre.
  ?company dbo:product ?product.
  ?company dbp:locationCountry ?country
  FILTER(?product = dbr:Motorcycle || ?product = dbr:All-terrain_vehicle)
  FILTER(STR(?country) = "Japan")
}
```

## Ejercicio 8

Crear una consulta que obtenga el nombre y el género de los videojuegos distribuidos por Ubisoft que vienen para Windows.

```SPARQL
SELECT ?name ?genre
{
  ?game a dbo:Software.
  ?game dbp:publisher dbr:Ubisoft.
  ?game dbp:platforms dbr:Microsoft_Windows.
  ?game rdfs:label ?name.
  ?game dbp:genre ?genre.
}
```

## Ejercicio 9

Crear una consulta que obtenga las bandas de rock alternativo de los Estados Unidos.

```SPARQL
SELECT ?band
{
  ?band a dbo:Band.
  ?band dbo:genre dbr:Alternative_rock.
  ?band dbp:origin ?origin.
  FILTER regex(STR(?origin), "U.S.")
}
```
