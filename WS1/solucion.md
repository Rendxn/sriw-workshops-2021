# Taller 1

Santiago Rendón Giraldo

- [Taller 1](#taller-1)
  - [Ejercicio 1](#ejercicio-1)
    - [Solución](#solución)
  - [Ejercicio 2](#ejercicio-2)
    - [Solución](#solución-1)
  - [Ejercicio 3](#ejercicio-3)
    - [Solución](#solución-2)
  - [Ejercicio 4](#ejercicio-4)
    - [Solución](#solución-3)
  - [Ejercicio 5](#ejercicio-5)
    - [Solución](#solución-4)
  - [Ejercicio 6](#ejercicio-6)
    - [Solución](#solución-5)

## Ejercicio 1

Identifique algunos de los elementos más relevantes que se observan en el siguiente código.

### Solución

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- SISTEMAS DE RECUPERACIÓN WEB -->
<!-- Namespace: Todos los elementos hijos pertenecen a este namespace -->
<libros xmlns="https://books.org/">
    <!-- Atributo ISBN -->
    <libro ISBN="1613820917">
        <titulo>Hamlet</titulo>
        <autor>W. Shakespeare</autor>
        <paginas>330</paginas>
        <!-- &amp; para poner &, ya que es un caracter reservado -->
        <editorial>Simon &amp; Brown</editorial>
    </libro>
    <libro ISBN="97895684254726">
        <titulo>La sombra del viento</titulo>
        <autor>Carlos Ruiz Zafon</autor>
        <paginas>575</paginas>
        <editorial>Planeta Booket</editorial>
    </libro>
    <libro ISBN="0765367297">
        <!-- &lt; y &gt; para poner <>, ya que son caracteres reservados -->
        <titulo>&lt; Halo &gt;: The Fall of Reach</titulo>
        <autor>Eric Nylund</autor>
        <paginas>448</paginas>
        <editorial>Tor Books</editorial>
    </libro>
</libros>
```

## Ejercicio 2

Haciendo uso de la extensión o del siguiente validador WEB para XML https://jsonformatter.org/xml-editor Identifique los errores del siguiente código XML e indique como corregirlos.

```xml
<!-- Falta el signo de interrogación final y el escape es innecesario -->
<?xml version="\1.0">
<!-- Falta el signo de adminarción que inicia el comentario -->
<--Sistemas de Recuperacion-->
<mensaje>
    <!-- La etiqueta de cerrado no coincide -->
    <remite.>
        <!-- Falta la apertura del tag (<) -->
        <!-- Los atributos deben estar dentro del tag (después de < y antes del >) y encapsuladas en comillas dobles -->
    nombre id=8976>Alfredo Reino</nombre>
    <email>alf@ibium.com</email>
    </remite>
    <!-- Caracter especial > duplicado -->
<destinatario>>
<nommbre>>
    <!-- Los atributos deben estar encapsulados en comillas doble -->
<nombre id=0976>Bill Clinton</nombre>
    <!-- Caracter especial > duplicado y tag sin cerrado -->
<email>>president@whitehouse.gov
    <!-- Solo se usa el slash al principio del cerrado de un tag -->
</destinatario/>
    <!-- Caracter especial ("") usado dentro de definición del tag -->
<asunto">Hola Bill</asunto>
    <!-- La etiqueta de cerrado no coincide -->
<texto.>
    <!-- Mala apertura y cerrado de CDATA -->
    <[CDATA[
    <mensaje> trabajo de clase <>
        ejemplos

 ]
 <!-- Caracter especial < duplicado y el tag enfasis no coincide -->
<<parrafo>¿Hola qué tal? Hace <enfasis->mucho</enfasis> que no escribes. A ver si llamas
y quedamos para tomar algo.</parrafo>
</texto>
</mensaje>
<!-- Cerrado de tag innecesario -->
</mensaje>
```

### Solución

Corrigiendo los errores del código anterior, tenemos:

```xml
<?xml version="1.0"?>
<!-- Sistemas de Recuperacion -->
<mensaje>
    <remite>
        <nombre id="8976">Alfredo Reino</nombre>
        <email>alf@ibium.com</email>
    </remite>
    <destinatario>
        <nombre id="0976">Bill Clinton</nombre>
        <email>president@whitehouse.gov</email>
    </destinatario>
    <asunto>Hola Bill</asunto>
    <texto>
        <![CDATA[
            <mensaje> trabajo de clase <>
                ejemplos
        ]]>
        <parrafo>
            ¿Hola qué tal? Hace
            <enfasis>mucho</enfasis>
            que no escribes. A ver si llamas
            y quedamos para tomar algo.
        </parrafo>
    </texto>
</mensaje>
```

## Ejercicio 3

Represente 5 productos de LEGO y algunas de sus propiedades usando XML, represente 3 propiedades como atributos y 3 propiedades como elementos use el siguiente enlace para observar los productos y propiedades: [https://www.target.com/c/lego-technic/-/N-k5gdj](https://www.target.com/c/lego-technic/-/N-k5gdj).

### Solución

```xml
<?xml version="1.0"?>
<!-- Sistemas de Recuperacion -->
<products category="technic">
    <!-- 1 -->
    <product id="42122" sale="true" rating="4.7">
        <name>LEGO Technic Jeep Wrangler</name>
        <price>39.99</price>
        <shipping>Shipping not available</shipping>
    </product>
    <!-- 2 -->
    <product id="42119" sale="false" rating="4.9">
        <name>LEGO Technic Monster Jam Max-D</name>
        <price>19.99</price>
        <shipping>Shipping not available</shipping>
    </product>
    <!-- 3 -->
    <product id="42120" sale="false" rating="4.6">
        <name>LEGO Technic Rescue Hovercraft Building Toy</name>
        <price>29.99</price>
        <shipping>Free standard shipping with $35 orders</shipping>
    </product>
    <!-- 4 -->
    <product id="42123" sale="false" rating="4.9">
        <name>LEGO Technic McLaren Senna GTR</name>
        <price>49.99</price>
        <shipping>Free standard shipping</shipping>
    </product>
    <!-- 5 -->
    <product id="42111" sale="false" rating="4.5">
        <name>LEGO Technic Fast &amp; Furious Dom's Dodge Charger Race Car Building Set</name>
        <price>99.99</price>
        <shipping>Free standard shipping</shipping>
    </product>
</products>
```

## Ejercicio 4

Tome el siguiente documento XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mc:micasa
    xmlns:mc='http://www.geneura.org/micasa'
    xmlns:mueble='http://www.geneura.org/mueble'>
</mc:micasa>
```

Haga uso de este como base para construir un documento que tenga las características siguientes haciendo uso de los espacios de nombre en vez de sus direcciones de donde provienen los elementos:

1. mc:micasa contendrá un elemento habitación proveniente del vocabulario 'http://www.geneura.org/micasa' y que contiene el atributo id="comedor".
2. El anterior elemento habitación contendrá un elemento mueble del vocabulario 'http://www.geneura.org/micasa' elemento quien a su vez contendrá:
   - Un elemento nombre del vocabulario 'http://www.geneura.org/mueble' quien contiene una cadena de caracteres Sofá
   - Un elemento descripción del vocabulario 'http://www.geneura.org/mueble' quien contiene una cadena de caracteres Peludo

### Solución

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mc:micasa xmlns:mc='http://www.geneura.org/micasa' xmlns:mueble='http://www.geneura.org/mueble'>
    <mc:habitacion id="comedor">
        <mc:mueble>
            <mueble:nombre>Sofá</mueble:nombre>
            <mueble:descripcion>Peludo</mueble:descripcion>
        </mc:mueble>
    </mc:habitacion>
</mc:micasa>
```

## Ejercicio 5

Cree un archivo XML schema (XSD) que defina una familia, la familia está compuesta por un conjunto de únicamente de 4 personas, cada persona debe contener un nombre, un apellido, una edad entre 0 y 120, al menos definir 2 hijos, incluyendo el nombre o la edad de los hijos de esa persona, y representar el mes de nacimiento, estas propiedades deben definirse en este orden.

**Nota**: Tenga en cuenta los tipos de datos, y en la propiedad mes usar restricciones para definir los meses del año.

Use http://www.utilities-online.info/xsdvalidation/#.U-AEI_mBN8E para validar los XSD o la extensión de VSCode, esta se encarga de verificar sintaxis.

### Solución

Ver [familia.xsd](./familia.xsd).

## Ejercicio 6

Realizar un documento XML que tenga como modelo de datos el Esquema XML realizado en el ejercicio 5 y valídelo con la extensión de VSCode o el enlace del anterior ejercicio.

**Nota:** para referirse a la ubicación del XSD al momento de definir un XML puede hacerlo usando
`<?xml-model href="ubicacion"?>` en la primer línea del archivo XML.

### Solución

Ver [familia.xml](./familia.xml).
