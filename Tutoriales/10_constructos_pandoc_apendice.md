# Apéndice: condicionales y bucles en \programa{Pandoc}
En este apéndice comento los típicos constructos que aparecen en las
plantillas de \programa{Pandoc}. La documentación oficial es concisa y no
propone apenas ejemplos. Supone un lector que ya entiende con claridad
la función de estos constructos y que es capaz de realizar experimentos
por sí mismo para confirmar su significado y aplicación. Salvo
programadores, es difícil que usuarios avanzados con interés sean
capaces de obtener una guía suficiente de dicha documentación. Este
apéndice propone ejemplos de uso para intentar hacer poco más digerible 
estas características avanzadas de \programa{Pandoc}. Aspectos relativos
a \LaTeX\ no se comentan. 

**Nota**: Cuando los comandos son muy largos los divido a través de un `\`,
como es convencional en \programa{Unix}.

## Variables en \programa{Pandoc}
Una variable en \programa{Pandoc} tiene la siguiente sintaxis:

    $nombre-de-variable$

Cuando ejecutamos `pandoc` cada variable de la plantilla se substituye por
su valor. Este valor se puede pasar a `pandoc` de distintas formas. Una de
ellas, como veremos más adelante, es pasárselo a través de la opción de
línea de órdenes `-M nombre-de-variable=valor`(donde `-M` es la forma
abreviada de `--metadata`).

Por lo respecta a las variables pre-definidas por \programa{Pandoc} y que están
incluidas en la plantilla por defecto, más información sobre la mayoría de
ellas se encuentra en la documentación oficial
(<http://johnmacfarlane.net/pandoc/README.html\#templates>).

Para saber en concreto qué variables hay en la plantilla por defecto podemos
también utilizar un filtro \programa{Unix} como el siguiente:

    grep -o '\$.*\$' /usr/share/pandoc/data/templates/default.latex \
    | grep -v '\$endif\$\|\$else\$\|\$endfor\$'

Es especialmente importante destacar que hay una variable crítica pre-definida,
la variable `$body$`, que toda plantilla debería incluir, puesto que el
contenido propiamente tal de nuestro documento de entrada será introducido en
su lugar.

Comprobemos esto último. Creemos una platilla \LaTeX\ \fichero{simple.latex} con
este contenido:

    \documentclass{minimal}
    \begin{document}
    $body$
    \end{document}

y ejecutemos `pandoc` para que reciba el input de la entrada estándar desde un
terminal. El resultado de nuestra sesión de prueba es el siguiente:

    $ pandoc -s --template="simple.latex" --to latex
    Hola
    Ctrl+D
    \documentclass{minimal}
    \begin{document}
    Hola
    \end{document}

La primera línea es el comando ejecutado. Estoy pidiendo a `pandoc` que aplique
nuestra plantilla, \fichero{simple.latex} a la entrada que le vamos a pasar y
que la convierta a formato \LaTeX. Las dos siguientes líneas reproducen lo que
he tecleado para que `pandoc` lo consuma. `Ctrl+D` señala `EOF` (fin de
fichero) y cierra la entrada estándar. El resto es la salida que `pandoc`
produce. Nótese que lo que he tecleado, "Hola", aparece tras el procesamiento,
como esperábamos, en el lugar en que estaba `$body$` en la plantilla.

Intentemos algo un poco más complicado. Añadamos una variable de nuestra
cosecha, que llamaremos `$saludo$`, a la plantilla:

    \documentclass{minimal}
    \begin{document}
    $saludo$
    $body$
    \end{document}

y comprobemos qué pasa:

    $ pandoc -s -M saludo="Hola gente" --template="simple.latex" --to latex
    Esto es Pandoc
    Ctrl+D
    \documentclass{minimal}
    \begin{document}
    Hola gente
    Esto es Pandoc
    \end{document}

La orden es casi idéntica a la de antes. El añadido clave es la opción
`-M` comentada previamente. A diferencia de la variable predefinida `$body$`,
tenemos ahora que pasar los valores de nuestras propias variables a `pandoc` a
través de la opción `-M`. Como vemos, en la salida, la variable en la plantilla
es sustituida por el valor que hemos dado.

## Condicionales
Los condicionales tienen esta sintaxis:

    $if(variable)$
    X
    $else$
    Y
    $endif$ 

donde la cláusula `$else$` es opcional.

Supongamos que nos interesa poder elegir, cuando sea necesario, entre
diferentes clases de documentos para el mismo documento de entrada. En
concreto, supongamos que queremos crear un documento `minimal` por defecto, a
no ser que pidamos expresamente que el documento sea de otra determinada clase.
Podemos conseguirlo a través de este condicional:

    $if(mi-clase-doc)$
    $mi-clase-doc$
    $else$
    minimal
    $endif$

Hay que tener cuidado con la sintaxis. Cada cláusula (`if()`, `else`, `endif`)
va rodeada por el signo `$`. Las variables que serán remplazadas por sus
valores también van entre `$`. Los valores literales, así como las referencias
a la variable en la cláusula `if` van sin ese signo.

Naturalmente, nuestro condicional debe colocarse en el lugar adecuado en
la plantilla, a saber, la instrucción `\documentclass`:

    \documentclass{$if(mi-clase-doc)$
                   $mi-clase-doc$
                   $else$
                   minimal
                   $endif$}

Escribir lo anterior en una sola línea quizá sea menos legible, pero también
más característico del estilo \LaTeX. Pongámosla, pues, así:

    \documentclass{$if(mi-clase-doc)$$mi-clase-doc$$else$minimal$endif$}
    \begin{document}
    $saludo$
    $body$
    \end{document}

Toca poner a prueba la plantilla:

    $ pandoc -s -M saludo="Hola gente" --template="simple.latex" --to latex
    Esto debería ser minimal
    Ctrl+D
    \documentclass{minimal}
    \begin{document}
    Hola gente
    Esto debería ser minimal
    \end{document}

¡Funciona!

Probemos ahora la otra posibilidad:

    $ pandoc -s -M saludo="Hola gente" -M mi-clase-doc="book" \
    --template="simple.latex" --to latex
    Y esto, book
    Ctrl+D
    \documentclass{book}
    \begin{document}
    Hola gente
    Y esto, book
    \end{document}

¡También funciona! Nótese que en esta ocasión hemos establecido el valor de la
variable `mi-clase-doc` a `book` a través de la opción `-M`, tal como hicimos
anteriormente con `$saludo$`.

## Bucles
Los bucles funcionan de una manera semejante. La sintaxis básica de un bucle es
la siguiente:

    $for(variable)$
    X
    $sep$separador
    $endfor$

La línea `$sep$separador` es opcional. Sirve para definir un separador entre
elementos consecutivos.

Digamos que queremos anotar los participantes a una reunión en la primera línea
de nuestro documento. Podemos definir una variable `$partipante$` en nuestra
plantilla y dejar que \programa{Pandoc} rellene su contenido. Queremos además
que los nombres de los participantes aparezcan separados por una coma.
Podríamos hacer todo esto añadiendo lo siguiente a nuestra plantilla:

    $for(participante)$
    $participante$
    $sep$, 
    $endfor$

O en una sola línea y en el lugar de la plantilla que corresponde:

    \documentclass{$if(mi-clase-doc$$mi-clase-doc$$else$minimal$endif$}

    \begin{document}
    Participantes: $for(participante)$$participante$$sep$, $endfor$

    $saludo$
    $body$
    \end{document}

Hagamos de nuevo una prueba. Ahora añadiremos a la orden `pandoc` tantos `-M
participante=nombre-del-participante` como participantes queremos incluir.

    $ pandoc -s -M saludo="Hola gente" \
    -M participante="W. Shakespeare" -M participante="Edgar A. Poe" \
    --template="simple.latex" --to latex
    Menudo plantel
    Ctrl+D
    \documentclass{minimal}
    \begin{document}
    Participantes: W. Shakespeare, Edgar A. Poe

    Hola gente
    Menudo plantel
    \end{document}

¡Estupendo! Todo funciona perfecto.

## Bloques de meta-datos
Es, como poco, engorroso tener que pasar todas estas cosas a la línea de
órdenes. No es obligatorio, por supuesto. \programa{Pandoc} proporciona para
esta tarea los así llamados *bloques de meta-datos*. Un bloque de meta-datos
para nuestro experimento anterior tendría este aspecto:

    ---
    mi-clase-doc: minimal
    saludo: Hola gente
    participante:
    - William Shakespeare
    - Edgar A. Poe
    ---

Este bloque no es más que un fragmento de texto que sigue las especificación
\programa{YAML} (<http://yaml.org/spec>). Aparte de esto, los bloques YAML que
se incluyen en un documento para que `pandoc` lo procese deben empezar con una
línea de tres guiones y terminar con una línea de tres puntos o tres guiones
como se ve en el ejemplo.

Un bloque de meta-datos consta de campos. Cada campo tiene un nombre y un valor
asociado a ese nombre, separado del nombre por dos puntos.  Algunos campos
pueden contener varios valores, los cuales van precedidos por un guion, tal y
como aparecen para el campo `participante` en el ejemplo.

Estos bloques nos permiten pasar a pandoc toda la información requerida sin
tener que complicarnos la vida con las opciones en la línea de órdenes. La
forma habitual de usar estos bloques es añadirlos al principio de nuestro
documento de entrada. Otra forma, en mi opinión mejor, es crear un fichero
\fichero{yaml} que pasamos a la vez que el fichero de entrada.

Por ejemplo, si guardamos la entrada de nuestro último experimento (la cadena
"Menudo plantel") en un fichero con nombre \fichero{mi\_documento.md} y el
bloque de meta-datos en un fichero con nombre \fichero{variables.yaml}, podemos
llamar a `pandoc` como sigue para conseguir exactamente la misma salida que
obtuvimos antes:

    pandoc -s --template="simple.latex" --to latex mi_documento.md variables.yaml

