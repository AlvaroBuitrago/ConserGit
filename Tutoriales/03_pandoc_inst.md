# Instalación de \programa{Pandoc}
\programa{Pandoc} es la utilidad más completa y potente para convertir
cualquier tipo de documento en cualquier otro tipo de documento. Es
especialmente apropiada para convertir de \programa{Markdown} a otros múltiples
formatos.

Naturalmente, el primer paso es instalar \programa{Pandoc}. Pero para poder usar la
conversión a \fichero{pdf}, tendremos que instalar también una distribución de \TeX.

## \TeX\, la máquina tipográfica
Dicho muy sumariamente, llamo distribución de \TeX\ al conjunto de paquetes y
utilidades en torno a la máquina de tipografía digital conocida en términos
genéricos como \TeX. Inventada por D. Knuth, uno de los padres de la teoría
de algoritmos. En la actualidad, la máquina que se usa es una variante de \TeX,
a saber, pdf\TeX. Pero se acostumbra a utilizar el término \TeX\ para todas estas
herramientas de tipografía digital cuyo origen es la obra de Knuth. Estas
herramientas son, hoy por hoy, y desde hace ya mucho tiempo, la opción profesional
más potente que existe, y es la que utilizan las editoriales más prestigiosas
del mundo para producir sus libros y revistas científicas.

Hay muchas distribuciones de \TeX, varias según el sistema operativo. Yo uso
\programa{Linux} y sólo tengo experiencia en instalar \TeX\ en \programa{Linux}.
Lo único que puedo en este sentido es indicar los sitios donde están las
distribuciones más conocidas para \programa{Windows} y \programa{MacOSX}. Si
alguno tiene \programa{Linux}, añadiré más tarde cómo se instala en
\programa{Linux}.

La distribución completa de \TeX\ es un programa muy grande, en torno a 2GB.
Una instalación completa permite olvidarse de todo, todas las fuentes estarán
instaladas, todos los paquetes. Pero, dado el tamaño, normalmente se opta
por instalar una base a la que se van añadiendo paquetes según se necesitan.

Las distribuciones más usadas son las siguientes. Las instrucciones de
instalación aparecen en sendas páginas:

- Para \programa{Windows}: \programa{Mik\TeX} (<http://miktex.org/download>)
- Para \programa{MacOSX}: \programa{Mac\TeX} (<http://www.tug.org/mactex/morepackages.html>)

## \programa{Pandoc}, el conversor
Una vez instalado \TeX, la instalación de \programa{Pandoc} no debería entrañar
ningún problema. En enlace está aquí. En la parte inferior de la página
aparecen botones para cada sistema operativo.

<https://github.com/jgm/pandoc/releases>

Las instrucciones de instalación, que indican, sumariamente, lo que he comentado
antes están aquí:

<http://johnmacfarlane.net/pandoc/installing.html>

## Terminal, la interfaz de usuario
\programa{Pandoc} se utiliza sobre el terminal. No hay que tener miedo. El
terminal es mucho más potente y flexible, y para el uso que le vamos a dar, es
cosa de aprender unas pocas órdenes.

Una primera toma de contacto con el terminal nos servirá para confirmar que
\programa{Pandoc} se ha instalado correctamente.

Para eso hay que seguir las instrucciones indicadas en el punto _Step2_ de esta
página:

<http://johnmacfarlane.net/pandoc/getting-started.html>

Hay instrucciones para cada sistema operativo. Si encontráis dificultades con
el inglés, me lo decís y lo traduzco.

## Ejercicios
El ejercicio esta vez es muy simple: proceder a la instalación de \TeX\ y
\programa{Pandoc} y pasar por las instrucciones comentadas en la sección
anterior. Como confirmación de que hemos seguido el proceso, propongo que,
quien quiera, envié un post al foro donde aparezca lo que resulta de ejecutar
en el terminal estas dos órdenes:

    pdftex --version

y, tras copiar el resultado para postearlo en el foro,

    pandoc --version

Son dos órdenes independientes. Por cierto, a este tipo de órdenes se les llama
también _comandos_ (spanglish del original inglés *command*)
