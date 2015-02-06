# \programa{Pandoc} Avanzado: LaTeX
Titulo _Pandoc Avanzado_ esta práctica. Pero no lo es. Sería más bien
\programa{Pandoc} a nivel intermedio.

## El verdadero proceso de conversión 
La conversión que realiza \programa{Pandoc} a la hora de obtener un
\fichero{pdf} se realiza en realidad a través de \LaTeX, solo que es
transparente al usuario, a no ser que el usuario solicite que no lo sea.

El proceso interno es, más bien, una conversión de \fichero{markdown} a \LaTeX\
y, después, la creación de un \fichero{pdf} a partir del fichero \LaTeX\
intermedio [Estos ficheros tienen la extensión \fichero{tex}]. Dicha creación
del \fichero{pdf} es obra de \TeX, o más exactamente de su más moderno y
popular descendiente pdf\TeX:


                 (pandoc)               (pdflatex)
    documento.md -------> documento.tex ---------> documento.pdf


Si queremos, podemos seguir estos mismos pasos nosotros mismos:

    pandoc -o mi_practica.tex mi_practica.md
    pdflatex mi_practica.tex

El último comando genera el fichero \fichero{mi\_practica.pdf}.

La utilidad del paso intermedio la veremos en otra práctica, más bien
demostración, ya que eso sí sería \programa{Pandoc} avanzado. Pero la redactaré
hacia el final de esta serie para mostrar la flexibilidad de estas
herramientas, abriendo quizá la posibilidad de que podáis investigar en el
futuro por vuestra cuenta.

## Plantillas
Cierto grado de flexibilidad para el usuario de a pie es en todo caso
posible gracias a lo que \programa{Pandoc} llama plantillas.

\programa{Pandoc} proporciona una plantilla de \LaTeX\ por defecto, que, por si
alguien quiere mirarla (con un editor de texto plano), está en:

    $PANDOC_DIR/data/templates/default.latex

(O con barras invertidas `\` en \programa{Windows})

Lo que a efectos prácticos esta plantilla permite es definir, mediante lo que
en terminología \programa{Pandoc} se llama _campo de metadatos_ (_meta-data
field_), ciertos valores variables del documento, como el título, la fecha, el
autor, el tamaño del papel, el tamaño de la fuente, y unos pocos más.

Lo interesante es que \LaTeX\ por defecto proporciona estas mismas variables y
actúa adecuadamente ante ellas.

Sin más palabras. La práctica de hoy sería sencilla. Añadir al principio de una
de vuestras prácticas previas un campo de metadatos como el siguiente [tres
guiones arriba y abajo y las claves en inglés seguidas de dos puntos]:

    ---
    lang: spanish
    title: Titulo de la práctica
    author: Vuestro nombre
    date: la fecha que queráis
    fontsize: 12pt
    ---

y generar el \fichero{pdf} como vimos el día pasado.

Por cierto, y puestos ya a experimentar, incluso os puede resultar interesante
encadenar varias de las prácticas como subpartes del mismo documento. La
primera es la que contendría el campo de metadatos.

El comando sería:

    pandoc -s -o todas_las_practicas.pdf practica1.md practica2.md practica3.md

las que sean, las que tengáis o queráis encadenar.

Esto último, solicitar la creación de un único \fichero{pdf} a partir de varios 
ficheros \fichero{md} es realmente útil, ya que podemos dividir un trabajo
grande en partes más pequeñas mucho más fáciles de manejar. 

## Ejercicios
Adjuntad un resultado como prueba de que todo sale como se espera. Como
queráis, una sola práctica con su campo de metadatos y el resultado en
\fichero{pdf}, o un único \fichero{pdf} derivado de múltiples prácticas, la
primera de las cuales contenga el campo de metadatos propuesto.
