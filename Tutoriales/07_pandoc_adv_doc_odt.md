# Documentos de referencia
Del mismo modo que es posible personalizar con bloques de metadatos la salida a
\fichero{pdf}, es posible también personalizar la salida a \fichero{odt} (formato
de \programa{OpenOffice} o \programa{LibreOffice}) o \fichero{docx} (formato de
\programa{Microsoft Office}).

[En lo que sigue me referiré a documentos de \programa{Microsoft Office}
(\fichero{docx}), porque es lo que usáis, según creo. Pero funciona igual para
los documentos de \programa{OpenOffice} o \programa{LibreOffice}
(\fichero{odt}). ]

En el caso de este tipo de documentos la forma habitual de personalizar es lo
que \programa{Pandoc} denomina una _reference_, que es simplemente un documento
de referencia en formato \fichero{docx} al que se le han aplicado, mediante las
correspondientes herramientas gráficas de los procesadores de textos, los
estilos que interese mantener en nuestro documento de salida.

La idea es simple:

1. Creo un documento en \programa{Office}, puramente esquemático, pero que
contenga todos los elementos estructurales que contendrá el verdadero documento
\programa{Markdown} que voy a convertir a \fichero{docx}.

2. Aplico los estilos que me interesen a cada uno de esos elementos
estructurales.

3. Ejecuto `pandoc` para que convierta a \fichero{docx} mi documento en formato
\fichero{md}, pero indicándole que tome como referencia ese otro documento
esquemático al que he aplicado ya los estilos que me interesa reproducir.

En principio, nada impide que el documento de referencia, en lugar de ser un
documento real, aunque muy esquemático, sea un documento vacío, sobre el que se
han definido los estilos con la herramienta correspondiente del procesador de
textos, algo en la línea de lo que se explica en este blog:

<http://hackademic.postach.io/pandoc-and-academic-docx-files>

No puedo poner un ejemplo concreto con \programa{Office}, porque no lo tengo
instalado.  Si me insistís puedo poner un ejemplo con \programa{LibreOffice},
que tampoco uso, pero que sí tengo instalado.  Pienso que de todas formas la
idea es bastante simple y podéis ser vosotros mismos quienes experimentéis.

## El comando
Falta decir el comando que requiere \programa{Pandoc} para conocer nuestro documento
de referencia. Supongamos que el documento de referencia lo hemos
guardado con el nombre \fichero{plantilla.docx} y que nuestro documento 
es \fichero{mi\_documento.md}. El comando para convertir a \fichero{docx} siguiendo los
estilos de referencia en \fichero{plantilla.docx} sería:

    pandoc -s -o mi_documento.docx --reference-docx plantilla.docx mi_documento.md

Por si sirve para aclarar la sintaxis, una transcripción a nuestra forma
más expresiva de hablar sería:

> \programa{Pandoc}, genera un documento autónomo (opción `-s`) a partir de
> \fichero{mi\_documento.md}, cuya salida (opción `-o`) sea
> \fichero{mi\_documento.docx}, y que tome como referencia de estilos (opción
> `--reference-docx`) el fichero \fichero{plantilla.docx}.

Notad que `--reference-docx` lleva dos guiones al principio, pues es una opción
en formato largo.

## \LaTeX\ _versus_ procesadores de texto
Uno de los problemas de esta estrategia es que los nombres de los estilos en
los procesadores de texto pueden cambiar de versión en versión, y por supuesto
de un procesador a otro. Por no hablar de las fuentes. Según el sistema
operativo, unas fuentes pueden estar instaladas o no. Cuando un sistema no
dispone de la fuente, los procesadores de texto declaran fuentes virtuales,
Así, por ejemplo, _Arial_ no está disponible en \programa{Linux} por defecto y
mi \programa{LibreOffice} la declara como _Arial_ virtual. La conversión de un
_Arial_ virtual a una fuente real en mi sistema operativo no va a tener el
mismo aspecto que el _Arial_ de Microsoft. 

Todos estos problemas de incompatibilidad entre sistemas operativos, distintos
programas o, incluso, distintas versiones del mismo programa, son prácticamente
inexistentes en el caso de \LaTeX\, puesto que es igual para todos los sistemas
operativos y no ha variado en el soporte esencial a lo largo de muchos años.

## El ciclo de trabajo ideal
Termino hoy con una reflexión sobre lo que, en mi opinión, sería el
proceder ideal en la generación de documentos oficiales que han de pasar
por varias manos y revisiones, al menos la mayoría de ellos, por ejemplo,
programaciones y memorias.

El mejor formato de salida posible, por su perfección tipográfica y su
coherencia es \fichero{pdf}. No hay nada mejor para ser impreso, y con fuentes
adecuadas, para ser visto en pantalla de ordenador. Si se requiriese un
documento para ser visto en cualquier tipo de pantalla (tablet, móvil, etc. )
\fichero{epub} sería seguramente la mejor opción (\programa{Pandoc} soporta
conversión a \fichero{epub}).

La edición conjunta se realizaría sobre el documento \fichero{markdown}. Texto
plano que no da problemas y es fácil de editar, modificar, etc.

Una vez obtenida una versión final, se procesaría con \programa{Pandoc} para
convertirlo a \fichero{pdf}. Si se requiriesen, por lo que fuera, cosas
especiales, se podrían crear plantillas especiales en lugar de la plantilla
\LaTeX\ por defecto de \programa{Pandoc}.

Si, en todo caso, fuese necesario distribuir un \fichero{docx}, habría que
crear documentos de referencia para cada tipo de documento. En todo caso la
necesidad de obtener \fichero{docx} queda ya muy limitada, pues las virtudes de
la flexibilidad de la edición ya las proporciona \programa{Markdown}.

Naturalmente, es sólo un ideal. No creo que, hoy por hoy, hubiese disposición
general de aprender \programa{Markdown}. Y la creación de plantillas lleva, por
supuesto, un buen trabajo.

Pero hablar de lo ideal creo que no viene mal.

En otro ámbitos lo ideal se hace real a base de ser un requisito insoslayable
;-) Por ejemplo, es típico en el ámbito de los analistas de datos divulgar sus
análisis etiquetados con \programa{Markdown} y procesarlos con
\programa{KnitR}, que usa \programa{Pandoc} por detrás. O si nos vamos a
editoriales científicas, es típico que los autores tengan que enviar sus obras
etiquetadas directamente con \LaTeX.

## Ejercicios 
Experimentar con la creación de un documento de referencia y
procesad una de vuestras prácticas anteriores, o una nueva, en la forma
indicada.

