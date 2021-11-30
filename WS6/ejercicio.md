# Taller 6

## Ejercicio 1

Cree una consulta para obtener el nombre de las diferentes razas de perro.

```SPARQL
SELECT DISTINCT ?breedLabel ?breed
{
?dog wdt:P31 wd:Q144 .
?dog wdt:P4743 ?breed
SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en" }
}
```

## Ejercicio 2

Cree una consulta para obtener el nombre y la descripción de las personas que nacieron en Medellín y son futbolistas.

```SPARQL
SELECT DISTINCT ?person ?personLabel ?personDescription
{
?person wdt:P31 wd:Q5 .
?person wdt:P19 wd:Q48278.
?person wdt:P106 wd:Q937857.
SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en" }
}
```

## Ejercicio 3

Cree una consulta para obtener el nombre y la cantidad de exoplanetas que ha descubierto una persona o instituto.

```SPARQL
SELECT (COUNT(?planet) as ?numPlanets) ?personLabel
{
  ?planet wdt:P31 wd:Q44559.
  ?planet wdt:P61 ?person.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en"}
} GROUP BY (?personLabel) ORDER BY DESC(?numPlanets)
```

## Ejercicio 4

Cree una consulta para obtener el nombre y la cantidad de exoplanetas que ha descubierto una persona o instituto.

```SPARQL
SELECT ?moon ?moonLabel
{
  ?moon wdt:P31 wd:Q1972.
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en"}
} ORDER BY ?moonLabel
```

## Ejercicio 5

Usando subconsultas, cree una consulta obtenga el nombre y el nombre del país de las personas que ganaron un premio nobel el mismo año en que Gabriel Garcia Marquez gano el suyo. (Tenga en cuenta en no incluir en el resultado a Gabriel Garcia Marquez).

```SPARQL
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX nobel: <http://data.nobelprize.org/terms/>

SELECT DISTINCT ?name ?placeName
{
    ?p nobel:nobelPrize ?nobel.
    ?p foaf:name ?name.
    ?nobel nobel:year ?year.
    ?p dbo:birthPlace ?place.
    ?place a dbo:Country.
    ?place rdfs:label ?placeName.
    FILTER REGEX(?name, "^((?!Gabriel García Márquez).)*$")
    FILTER(LANG(?placeName) = 'en')
    {
        SELECT DISTINCT ?year
        {
            ?s rdfs:label ?na.
            ?s nobel:nobelPrize ?prize.
            ?prize nobel:year ?year
            FILTER(REGEX(?na, "Gabriel García Márquez"))
        }
  }
}
```

## Ejercicio 6

Cree una consulta que obtenga el nombre y el número de veces que gano un nobel, de las personas que ganaron más de un premio nobel en sus vidas.

```SPARQL
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX nobel: <http://data.nobelprize.org/terms/>

SELECT DISTINCT ?name (COUNT(DISTINCT ?prize) as ?numPrizes)
{
    ?p a nobel:Laureate.
    ?p foaf:name ?name.
    ?p nobel:nobelPrize ?prize
} GROUP BY (?name) HAVING (?numPrizes > 1)
```

## Ejercicio 7

Cree una consulta que obtenga el nombre y el nombre de la categoría de las personas que ganaron el premio nobel de física o química y el año en que ganaron.

```SPARQL
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX nobel: <http://data.nobelprize.org/terms/>

SELECT DISTINCT ?name ?categoryNobel ?year
{
    ?person nobel:nobelPrize ?nobel.
    ?person foaf:name ?name.
    ?nobel nobel:year ?year.
    ?nobel nobel:category ?categoryNobel.
    {
        ?nobel nobel:category nobel:Chemistry.
    }
    UNION
    {
        ?nobel nobel:category nobel:Physics.
    }
}
```
