# Introducción práctica al uso de \programa{Markdown}

## Qué es \programa{Markdown}
No merece la pena entretenerse con cuestiones técnicas y otros detalles.
Al final pongo un enlace a lo que considero exposiciones más precisas, así
como la documentación oficial.

Para el usuario, \programa{Markdown} no es más que un conjunto de marcas, de
etiquetas, de signos, que se colocan delante o rodeando a un fragmento de texto
para indicar su estructura y también su formato.

Así, por ejemplo, si queremos que una línea de un documento que estamos
redactando sea el título de una sección, ponemos una marca delante de esa
línea:

    ## Sección principal

La marca aquí es la doble almohadilla (`##`).

Otro ejemplo, si queremos que un trozo de una línea se destaque (digamos,
en negrita) rodeamos ese texto con otra marca.

    El **piano** es un instrumento.

La marca es ahora un doble asterisco rodeando la palabra que queremos
destacar, "piano".

Para cada elemento estructural de un documento (encabezados, listas, etc.)
hay una marca característica, como también la hay para negritas, cursivas,
vínculos a páginas web, etc.

Nuestro primer objetivo es aprender esas marcas básicas y usarlas en la
práctica.

Cuando empleamos un procesador de textos como \programa{Word} u
\programa{OpenOffice}, tenemos que ir por los botones y los menús para
conseguir estas mismas cosas.  Internamente, el procesador de textos está
marcando el documento. La diferencia es que las marcas que pone son demasiado
complicadas y por eso proprociona herramientas gráficas para introducirlas (los
botones y los menús). \programa{Markdown} permite olvidarse de levantar la mano del
teclado, puesto que la mayoría de sus marcas son sencillas y se aprenden en muy
poco tiempo.

La otra ventaja es que existen poderosos conversores de documentos etiquetados
con estas marcas de \programa{Markdown} a otros formatos conocidos, \fichero{pdf},
\fichero{docx}, \fichero{html}, etc. Lo que significa que podemos escribir
nuestro documento con las marcas de \programa{Markdown} y convertirlo a
cualquier otro formato muy fácilmente.

## Marcas básicas
La primera parte del trabajo sería conocer y usar las marcas más sencillas,
las que se usan en prácticamente todo tipo de documentos. Las listo aquí.
Algunas tienen varias posibilidades. Elijo una que me parece más sencilla,
por unificar también lo que vayamos a usar todos. Después de listarlas,
propongo unas prácticas.

### Párrafos
Un párrafo es algo tan basico como dejar una línea en blanco entre un
párrafo y el siguiente:

    Bla, bla, bla, bla, bla, bla, bla, bla, bla, bla, bla,
    bla, bla, bla, bla.

    Y ahora empieza otro párrafo: bla, bla, bla, bla, bla,
    bla, bla.

### Títulos o encabezados de secciones y subsecciones
Para los títulos usamos almohadillas.

El título de una sección principal va con una almohadilla delante:

    # Título de primer nivel

El título de una subsección van con dos almohadillas delante:

    ## Mi titulo de subsección

El de una subsubsección con tres:

    ### Título de una subsubsección

Y así sucesivamente.

### Negritas, cursivas
Las palabras o grupos de palabras en cursiva van rodeados de un asterisco:

    Hola Hola Hola Hola *adiós adiós*. Los dos adiós en cursiva.

Lo mismo para la negrita, pero ahora dos asteriscos:


    Hola Hola Hola Hola **adiós adiós**. Los dos 'adiós' en negrita.

### Listas
Las listas numeradas se etiquetan poniendo el número que corresponde a cada 
item seguido de un punto

    Lo que sigue será una lista numerada:

    1. El primer item de la lista
    2. El segundo item
    3. El tercero

Para listas no numeradas se pone un asterisco delante de cada item, o un guión,
o un `+`. Como el asterisco lo hemos usado para otra cosa, propongo poner
un guión:

    Lo que sigue será una lista no numerada:

    - El primer item de la lista
    - El segundo
    - El tercero

### Citas
Para citas se usa el ángulo `>` delante del párrafo que se cita:

    Como dijo Cervantes:

    > En un luguar de la Macha de cuyo nombre no quiero
    acordarme ...

Si la cita contiene varios párrafos cada párrafo citado debe ir precedido
por esa marca:

    Como dijo Cervantes:

    > En un luguar de la Macha de cuyo nombre no quiero
    acordarme ...

    > En los nidos de antaño no hay pájaros hogaño

## Dónde practicar
Para prácticar propongo dos sitios web. Ambos constan de una ventana dividida
en dos partes. La de la izquierda es para escribir el texto con las marcas.
La de la derecha muestra como aparecería en una página web:

[http://dillinger.io/](http://dillinger.io/)

[http://markable.in/editor/](http://markable.in/editor/)

## Ejercicios
1. Probar una a una las marcas citadas en cualquiera de los
sitios web que acabo de mencionar (u otros semejantes).

2. Seguir probando (2 min. al día) ...

3. Elegir cualquier texto vuestro, un acta, una página de la programación,
lo que sea, y ponerle estas marcas. O bien, crear un documento donde se
usen. Propongo que el texto etiquetado así lo adjuntemos a un email para 
que los demás podemos ver si está bien o sugerir correcciones si es necesario.
El asunto del email podría ser "GrupoTrabajo práctica 1".

## Información más detallada sobre \programa{Markdown}
- Documentación original de \programa{Markdown} (en inglés): [http://daringfireball.net/projects/markdown/](http://daringfireball.net/projects/markdown/)
- Página de wikipedia en español sobre \programa{Markdown}: [http://es.wikipedia.org/wiki/Markdown](http://es.wikipedia.org/wiki/Markdown)

