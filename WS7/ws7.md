## Ejercicio 1

```SPARQL
PREFIX robot: <http://all-robotics.com#>

SELECT DISTINCT ?nombre
{
 ?robot robot:Nombre ?nombre.
 ?robot robot:Identificacion ?x.
 ?robot robot:Peso ?y.
}
```

## Ejercicio 2

```SPARQL
PREFIX c: <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>

SELECT DISTINCT ?nombre
{
 ?dependiente c:dependentTerritoryOf ?pais.
 ?dependiente c:nameEnglish ?nombre.
}
```

## Ejercicio 3

```SPARQL
PREFIX robots: <http://all-robotics.com#>
PREFIX countries: <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>

SELECT DISTINCT ?nombre ?namePais
FROM <Robots>
FROM NAMED <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>
{
  ?robot robots:Nombre ?nombre.
  ?robot robots:Identificacion ?id.
  ?robot robots:Peso ?peso.
  GRAPH ?g {
    ?pais countries:dependentTerritoryOf ?paisDominante.
    ?pais countries:nameLocal ?namePais.
  }
}
```

## Ejercicio 4

```SPARQL
PREFIX countries: <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>

INSERT INTO GRAPH <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>
{
    countries:Capital rdf:type owl:Class.
    countries:hasCapital rdf:type owl:ObjectProperty;
                        rdfs:domain countries:Country;
                        rdfs:range countries:Capital.
}
```

## Ejercicio 5

```SPARQL
PREFIX countries: <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>

INSERT INTO GRAPH <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>
{
    countries:Bogota rdf:type owl:Class.
    countries:Bogota rdf:type owl:Capital.
    countries:Colombia countries:hasCapital countries:Bogota.
    countries:Caracas rdf:type owl:Class.
    countries:Caracas rdf:type owl:Capital.
    countries:Venezuela countries:hasCapital countries:Caracas.
    countries:Quito rdf:type owl:Class.
    countries:Quito rdf:type owl:Capital.
    countries:Ecuador countries:hasCapital countries:Quito.
    countries:Buenos_Aires rdf:type owl:Class.
    countries:Buenos_Aires rdf:type owl:Capital.
    countries:Argentina countries:hasCapital countries:Buenos_Aires.
    countries:Santiago_de_Chile rdf:type owl:Class.
    countries:Santiago_de_Chile rdf:type owl:Capital.
    countries:Chile countries:hasCapital countries:Santiago_de_Chile.
    countries:Brasilia rdf:type owl:Class.
    countries:Brasilia rdf:type owl:Capital.
    countries:Brazil countries:hasCapital countries:Brasilia.
    countries:Sucre rdf:type owl:Class.
    countries:Sucre rdf:type owl:Capital.
    countries:Bolivia countries:hasCapital countries:Sucre.
    countries:Montevideo rdf:type owl:Class.
    countries:Montevideo rdf:type owl:Capital.
    countries:Uruguay countries:hasCapital countries:Montevideo.
    countries:Asuncion rdf:type owl:Class.
    countries:Asuncion rdf:type owl:Capital.
    countries:Paraguay countries:hasCapital countries:Asuncion.
    countries:Ciudad_de_Mexico rdf:type owl:Class.
    countries:Ciudad_de_Mexico rdf:type owl:Capital.
    countries:Mexico countries:hasCapital countries:Ciudad_de_Mexico.
    countries:Ciudad_de_Panama rdf:type owl:Class.
    countries:Ciudad_de_Panama rdf:type owl:Capital.
    countries:Panama countries:hasCapital countries:Ciudad_de_Panama.
    countries:Managua rdf:type owl:Class.
    countries:Managua rdf:type owl:Capital.
    countries:Nicaragua countries:hasCapital countries:Managua.
    countries:La_Habana rdf:type owl:Class.
    countries:La_Habana rdf:type owl:Capital.
    countries:Cuba countries:hasCapital countries:La_Habana.
    countries:WashingtonDC rdf:type owl:Class.
    countries:WashingtonDC rdf:type owl:Capital.
    countries:UnitedStates countries:hasCapital countries:WashingtonDC.
    countries:Ottawa rdf:type owl:Class.
    countries:Ottawa rdf:type owl:Capital.
    countries:Canada countries:hasCapital countries:Ottawa.
}
```

## Ejercicio 6

## Ejercicio 7

```SPARQL
DROP GRAPH <Robots>
```