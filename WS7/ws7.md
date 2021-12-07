# Taller 7

Para correr Virtuoso, se usó la [imagen de Docker oficial](https://hub.docker.com/r/openlink/virtuoso-opensource-7)

## Ejercicio 1

Crear una consulta que desde nuestro endpoint retorne lo siguiente: retorne el nombre de los robots que tienen identificación, nombre y peso. Este proviene de la ontología de robots.

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

Crear una consulta que desde nuestro endpoint retorne lo siguiente: retorne el nombre local “nameLocal” de los países que dependen de otro país “dependentTerritoryOf”. Este proviene de la ontología de países.

```SPARQL
PREFIX c: <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>

SELECT DISTINCT ?nombre
{
 ?dependiente c:dependentTerritoryOf ?pais.
 ?dependiente c:nameEnglish ?nombre.
}
```

## Ejercicio 3

Crear una consulta que desde nuestro endpoint retorne lo siguiente: Usando las consultas del ejercicio 1 y 2, las integre en una sola consulta. Es decir desde el grafo Robots retorne el nombre de los robots que tienen identificación, nombre y peso; Desde el grafo de la ontología de países el nombre local “nameLocal” de los países que dependen de otro país “dependentTerritoryOf”. Se recomienda usar GRAPH <> en la consulta.

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

Cree una operación de actualización para añadir una nueva clase llamada Capital y una nueva propiedad hasCapital con dominio Country y rango Capital, a la ontología de países “Countries.owl” que agregamos anteriormente

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

Cree una operación de actualización para añadir las capitales y su respectiva relación “hasCapital” de los siguientes países:

- Colombia -> Bogota
- Venezuela -> Caracas
- Ecuador -> Quito
- Argentina -> Buenos Aires
- Chile -> Santiago de Chile
- Brasil -> Brasilia
- Bolivia -> Sucre
- Uruguay -> Montevideo
- Paraguay -> Asuncion
- México -> Ciudad de Mexico
- Panamá -> Ciudad de Panama
- Nicaragua -> Managua
- Cuba -> LA Habana
- Estados Unidos -> Washington
- Canadá -> Ottawa

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

Cree una consulta de inserción en donde añada 2 propiedades a las capitales. Eres libre de decidir que propiedades, alguna podrían ser la población, clima, moneda, ubicación geográfica, idioma, etc.

```SPARQL
PREFIX countries: <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>

INSERT DATA {
  GRAPH <http://www.bpiresearch.com/BPMO/2004/03/03/cdl/Countries/>
  {
    countries:Bogota countries:temperature "Cold".
    countries:Bogota countries:population 51000000.
    # Same for other capitals
  }
}
```

## Ejercicio 7

Cree una operación de actualización para borrar el grafo de la ontología de Robots.

```SPARQL
DROP GRAPH <Robots>
```

## Ejercicio 8

Suba la ontología “pizzaGL.owl”, archivo de la ontología de las pizzas de los talleres pasados. Y configure lodview para visualizar dicha ontología en este aplicativo. Tome una captura de este ejercicio.
