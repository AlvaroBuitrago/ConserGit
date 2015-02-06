# Conversión de documentos con \programa{Pandoc}
La práctica de hoy es la más sencilla, la más corta, y a la vez, la más
gratificante. Se trata de obtener distintos documentos finales (en diversos
formatos) a partir de un documento \programa{Markdown}.

En definitiva, lo que conseguimos de este modo es atenernos a aquel ideal
comentado en el foro. El escritor escribe su texto y lo marca para que el
tipógrafo produzca el resultado deseado. El escritor debe desentenderse lo más
posible de las cuestiones de formateo y diseño. Idealmente, las marcas deben
ser muy ligeras. \programa{Markdown} es el lenguaje de marcas más ligero que
existe hasta la fecha y de ahí su conveniencia y su muy amplia difusión. El
resultado, desde el punto de vista tipográfico, será de mayor o menor calidad
dependiendo del tipógrafo, claro. Puesto que el tipógrafo más experto es \TeX,
el mejor resultado lo obtendremos al producir un documento \fichero{pdf}, que
es la salida que produce \TeX\ (concretamente, pdf\TeX, su moderno sucesor).
Los resultados en \fichero{odt}, que es un formato estándar (*Open Document
Text*) para documentos de texto, el nativo de \programa{OpenOffice} y
\programa{LibreOffice}, así como \fichero{docx}, que es el formato para
documentos de texto de \programa{Microsoft Office} actual, son más rupestres.
Al fin y al cabo en los procesadores de texto el escritor también tiene que
encargarse del resultado, diseño y tipografía, y lo que obtenemos en nuestra
conversión será el resultado tal como queda definido por la plantilla básica
que Jonh MacFarlane (el creador de \programa{Pandoc}) ha diseñado.

La otra gran ventaja, y que conecta directamente con el título de este curso,
es que es infinitamente más fácil editar conjuntamente un texto plano, como es
un texto etiquetado con \programa{Markdown}, que editar un texto con formato,
incluidos formatos indicados para esa función, como \fichero{odt} y
\fichero{docx} (\fichero{pdf} no fue  diseñado para ser editado). Todos sabemos
que cambiar un documento en un formato de procesador de texto puede ser
problemático. Que si la fuente se cambia, que si la imagen se va al garete, que
si el párrafo se desalinea, etc. Con un texto plano nada de esto sucede.

## Sintaxis de los comandos 
Los comandos, las órdenes, son muy simples. Nos atenemos a lo básico. Todos
estos comandos incluyen la opción `--standalone` o `-s` (su forma abreviada).
De esta forma obtenemos un documento independiente, en lugar de una parte de un
documento para ser incluida en un documento maestro. Todos los comandos tiene
la misma sintaxis:

    pandoc --standalone --output mi_documento.<formato_de_salida> mi_documento.md

O en su forma abreviada:

    pandoc -s -o mi_documento.<formato_de_salida> mi_documento.md

En estos comandos `mi_documento.<formato_de_salida>` es el nombre del fichero
de salida que quiero obtener, donde formato de salida es la extensión que
corresponde a dicho formato. Esto es, si quiero obtener un documento
\fichero{pdf} será \fichero{mi\_documento.pdf}; si quiero un documento
\fichero{docx} será \fichero{mi\_documento.docx}.  Naturalmente, en lugar de
`mi_documento`, utilizo el titulo de fichero que deseo.  Digamos
\fichero{memoria.pdf} o \fichero{acta.docx}, etc. No hace falta que coincidan
el nombre de fichero de entrada y el de salida, aunque es normal que lo hagan.
Es decisión del usuario, en todo caso.

## Los comandos concretos
Así, por tanto, estos serían los comandos para obtener los tres tipos de documentos
comentados:

- Documento \fichero{pdf}

    	pandoc -s -o mi_documento.pdf mi_documento.md

- Documento \fichero{odt}

    	pandoc -s -o mi_documento.odt mi_documento.md

- Documento \fichero{docx}

    	pandoc -s -o mi_documento.docx mi_documento.md

## Ejercicios
Simplemente poned en el foro el \fichero{pdf} y el \fichero{docx} (o el
\fichero{odt}) que resulte de procesar la práctica más compleja que hayáis
hecho hasta ahora. De esta manera sabremos si todas las marcas (enlaces,
imágenes, etc.) funcionan correctamente.
