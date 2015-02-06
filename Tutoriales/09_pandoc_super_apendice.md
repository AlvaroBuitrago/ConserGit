# Apéndice: Automatización
No me quedaba a gusto sin comentar un aspecto más, también avanzado, pero que
creo puede ser interesante de cara a disponer de argumentos en defensa de estas
herramientas, o, incluso, puede seros útil si algún día intentáis entrar a
fondo en estos derroteros por vuestra cuenta.  Una utilidad inmediata puede
haberla particularmente para Enrique, ya que es jefe de departamento, y, quizá,
en su sistema operativo, lo que voy a describir también puede funcionar.

## Introducción
Una brevísima introducción sobre la filosofía de \programa{Unix}. Antes que
nada comentar que llamo \programa{Unix} a los programas que se basan en las
ideas y código original de quienes desarrollaron \programa{Unix}, allá por los
70 del siglo pasado, los mismos que cocrearon el lenguaje de programación
\programa{C}, que sigue siendo, según las estadísticas, en el que más se
escribe hoy en día.  No conviene tampoco olvidar que la Red global tal como la
conocemos debe mucho a esta época y a esta filosofía.

Resulta que estos lumbreras, Dennis Ritchie y Ken Thompson, que trabajaban
entonces en los laboratorios Bell, idearon algo realmente bueno, pues ha
mostrado su excelencia y resistencia al paso del tiempo. Hoy en día los
herederos popularmente más conocidos de aquel \programa{Unix} original son los
entornos \programa{Linux} y \programa{MacOSX}. Aquí habría que hacer muchas
matizaciones.  Quedémonos con que aquella filosofía no sólo persiste, sino que
muestra día a día su excelencia.

Entre el ideario \programa{Unix} están estos principios que tienen especial
relevancia para el asunto que nos toca:

1. El texto plano es el medio central en que se almacenan los datos que
los programas manipularán e intercambiarán.

2. Las herramientas que manipulan ese texto son pequeños programas que hacen
una sola cosa, pero que la hacen bien. 

De aquí se sigue que la complejidad de un proceso se reduce a la colaboración 
de pequeños programas especializados que trabajan sobre texto plano, texto
plano cuyo formato debe ser simple y fácil de analizar y manipular
programáticamente.

En concreto, cada uno de estos pequeños programas recibe un input en texto
plano fácilmente procesable y ejecuta sobre él la operación para la que está
diseñado. El resultado es otro texto plano que será consumido por otro programa
pequeño con otra función específica. La colaboración se prolonga hasta obtener
el output deseado.

¿Por qué esto es relevante para nosotros?  Por dos cosas. 

Primero, porque, como vamos viendo, nos estamos aprovechando de esta filosofía.
Editamos un texto plano en un formato simple y fácil de analizar
(\programa{Markdown}).  El resultado se lo pasamos a `pandoc`. `pandoc` analiza
esas marcas y genera otro texto plano que, en el caso de conversión a
\fichero{pdf}, se lo pasa a la máquina \LaTeX.  \LaTeX, por su parte, lo
convierte en formato \TeX\ para que una máquina \TeX\ lo procese.  Finalmente,
en nuestra anterior práctica, el \fichero{pdf} resultante es manipulado por
otro programa, \programa{PDFtk}, para insertarle la marca de agua.

Cada programa realiza su función específica, y todos pueden colaborar porque
conocen las convenciones del texto que cada uno maneja, convenciones que,
por norma, tratan de ser lo más simple posibles, con el fin de que ese
texto sea manipulado con facilidad.

La segunda razón es que este tipo de filosofía permite formas relativamente
cómodas o asequibles de automatización. Puesto que todo son textos fácilmente
analizables, siempre podemos encontrar mecanismos para automatizar operaciones
repetitivas sobre ellos, mecanismos que no impliquen crear grandes
y complejos programas cuya implementación exija un esfuerzo humano (de
número de personas y de horas de trabajo) demasiado grande para ser 
practicable.

## Automatizar la generación de actas
Como ejemplo de ello os muestro cómo tengo automatizada la generación
de las actas. Lo que vale para las actas sería aplicable, _mutatis mutandi_,
a otras situaciones parecidas.

En realidad, mi automatización era otra en el origen. No utilizaba
\programa{Pandoc}, sino \LaTeX\ puro. Ha sido a propósito de las prácticas en
el seno del grupo que me he planteado confiar a \programa{Pandoc} el grueso de
la tarea.

El problema inicial que me planteaba, aparte de lo comentado ya en el texto
del otro día, era el siguiente. Está bien producir un pdf de la forma que
hemos explicado, pero todavía hay cosas tediosas que podrían automatizarse.
En particular:

1. Los puntos del orden del día se repiten tal cual en el cuerpo del acta. Lo
ideal sería escribir sólo ese cuerpo, sin necesidad de cortar y pegar. Lo ideal
sería que un programa generase la lista que contiene el orden del día y que esa
lista se insertase antes del cuerpo del acta. El jefe de departamento se
limitaría a escribir el contenido del acta, nada más. Otra ventaja de ello es
que no tendría por qué haber ninguna marca extraña al puro \programa{Markdown}
dentro del acta, pues todas esas marcas e instrucciones de LaTeX quedarían
desplazadas a la plantilla de \LaTeX. Las actas serían \programa{Markdown}
puro.

2. A veces tengo varias actas redactadas. Es aburrido tener que generar
un pdf para cada una de las actas redactadas. Lo ideal sería que todos
los pdfs de todas las actas se generasen en una sola operación automáticamente.

Tratar de resolver estos problemas sería difilísimo en un entorno que no fuera
el entorno reducido de textos planos que siguen convenciones sencillas y
simples. Por ejemplo, los procesadores de textos utilizan marcas
\programa{XML}, pero la cantidad y especificaciones de esas marcas es tal que,
en esos entornos, no resulta factible plantearse una solución que pueda
diseñarse en un tiempo razonable.

### Generación automática del orden del día
El primero de los problemas se puede expresar más específicamente en la
filosofía anteriormente descrita como una tarea que realizar:

> Convertir un input dado, que contiene el cuerpo del acta, en un output, que
> contenga sólo el orden del día. Posteriormente, incluir ese orden del día
> de una forma automática.

Lo primero es fácil de conseguir mediante un filtro de \programa{Unix}, que
toma el cuerpo del acta (escrito en \programa{Markdown}) y selecciona aquellas
líneas en él que tienen un dígito como primer carácter de la línea, seguido de
punto, seguido de uno o más espacios y seguido de cualquier sucesión de
caracteres alfanuméricos. Esta descripción corresponde precisamente a lo que en
\programa{Markdown} es un ítem de lista numerada de primer nivel, justo la
forma en que hay que etiquetar, siguiendo la convención del Conservatorio, los
ítems de la lista del orden del día y los ítems del cuerpo del acta a los que
se añadirá su correspondiente comentario.

Por si interesa, el filtro es éste (funciona, aunque sea críptico):

    grep '^[[:digit:]]\. \+[[:alpha:]]' acta > acta_orden_del_dia



### Generación de un bloque de metadatos para el acta
El segundo problema principal tiene que ver con extraer información de la fecha
y hora para cada acta.

Para almacenar dicha información se debe pensar en alguna convención sencilla 
de forma que, dada un acta, un pequeño programa pudiera extraer
la información necesaria concerniente a su fecha y hora.

Hay varias formas de implementar una convención así.  Una natural sería
crear una especie de mini base de datos. Algo como esto:

    #acta;dia;mes;año;hora comienzo;hora fin
    acta1;12;septiembre;2014;12:00;13:00
    acta2:13;octubre;2014;13:00;14:00
    ...

De esta mini base de datos se podría obtener dicha información.

Lo primero que se me ocurrió, sin embargo, fue algo más críptico, pero a la vez
más breve: codificar la información relevante a cada acta en su nombre de
fichero.  Por ejemplo, el acta primera tendría un nombre de fichero como el
siguiente:

    a01_1209141200.md

que significa: acta1, del día 12 del mes 09 del año 14, comienzo 12:00h. Por
cierto, en mi implementación he suprimido la fecha de cierre de sesión y la
computo como una 1h más que la de inicio, que viene a ser aproximadamente eso.
Pero sería una tarea pendiente implementar una fecha de cierre exacta.

Suponiendo que hemos extraído adecuadamente esa información, ¿qué hacer con
ella? Si recordamos lo del día pasado, esa información debía introducirse
como los valores respectivos en el bloque de metadatos \fichero{variables.yaml}.

En definitiva, la solución del problema se puede describir como una composición 
de dos tareas:

> (Primero): Extraer del nombre de fichero la información relevante y
> convertirla de modo adecuado. Por ejemplo los dígitos '09' correspondientes
> al mes, deben extraerse y convertirse a 'septiembre'.
>
> (Segundo): Introducir los datos extraídos y adecuadamente convertidos en los
> correspondientes campos del bloque de metadatos perteneciente al acta
> del caso.

De nuevo, las dos tareas son viables porque se basan en secuencias de texto
plano que obedecen convenciones simples. En el primer caso, se trata de obtener
datos de un formato plano basado en una convención simple:

    nombreacta_dia(dos dígitos)mes(dos dígitos)año(dos dígitos)hora(cuatro dígitos)

En el segundo, de insertar datos en un texto que a su vez sigue una convención
simple:

    nombre_del_campo: valor_del_campo

En otras palabras, gracias a la simplicidad de la convención, es sencillo
generar un fichero \fichero{yaml} donde los datos procedentes del nombre de
fichero del acta acaben insertados como sigue:

~~~yaml
# fichero a1.yaml

day: 12
month: septiembre
year: 2014
start: 12:00
end: 13:00
~~~

### Variable para el fichero que contiene el orden del día 
Dando por hecho que hemos conseguido crear un fichero \fichero{md} que contiene
el orden del día a partir del fichero que contiene el cuerpo del acta, podemos
recurrir de nuevo a las variables y plantillas \LaTeX\ de \programa{Pandoc} con
la idea de introducir una nueva variable en la plantilla, correspondiente al
nombre del fichero que contiene el acta. Esta variable se declararía, a su vez,
en el bloque de metadatos del acta del caso de un modo parecido al siguiente:

~~~
# fichero a01_1209141200.yaml

day: 12
...
od: <nombre_del_fichero_que_contiene_el_orden_del_dia>
...
~~~

Por su parte, en la plantilla podríamos incluir el contenido de ese fichero
con una instrucción `\input` de \LaTeX. Esta sería la parte de la plantilla 
relevante con dicho añadido:

~~~
% plantilla_acta.latex
...
\subsection{Orden del día}
\input{$od$}

\begin{flushright}\rule{5mm}{.5mm}\end{flushright}
...
~~~

La segunda línea incluye el fichero del orden del día, a través de la variable
`$od$`, que acabamos de crear en el bloque de metadatos del acta.

He añadido de paso la siguiente línea de la plantilla con la intención de
destacar una ventaja más, una esencial, que hemos ganado. Si recordáis, la
línea final de este fragmento era la que producía la pequeña línea de
separación entre el orden del día y el cuerpo del acta. Al ser capaces, en esta
versión de la plantilla, de introducir programáticamente el orden del día sin
intervención del usuario, ya no queda rastro de nada que no sea puro
\programa{Markdown} en el contenido del acta. Dicho de otra forma, lo que
realmente va a redactar el jefe de departamento es el cuerpo del acta en
\programa{Markdown} puro:

~~~
1.  Lectura y aprobación, si procede, del acta de la reunión anterior. 

    Se lee el acta de la reunión anterior, que se aprueba.

2.  Comentario del borrador de la programación. 

    Se pone en conocimiento de Patricio del borrador de la nueva programación. 
    No hay ningún cambio esencial con respecto de la del curso pasado. 
    Pero hay muchos cambios formales, particularmente en la programación 
    de conjunto.

    Asimismo, se decide (como quedó comentado en la última reunión del 
    curso pasado) mantener la idea de una audición pública final donde el 
    grueso de la participación corresponderá a grupos, surgidos de las 
    clases colectivas y la de conjunto.

3.  Otros asuntos. 

    - Se decide fecha para la audición final, que será, dependiendo de 
      la ocupación, en el aula de Orquesta o de Coro, un viernes en torno 
      a las 18.00h (para facilitar la participación de los más pequeños) y a 
      principios de junio. Se trasmitirá a Jefatura dicha solicitud.

    - En otro orden de cosas, se informa de la novedad para este curso de 
      que la memoria del departamento debe incluir un adjunto con las faltas 
      de los alumnos durante el curso.
~~~

El jefe del departamento sólo tendría una o dos tareas más:

1. Nombrar los ficheros de sus actas siguiendo la convención referida antes.

2. En caso de que tuviera ausencias de profesores a la reunión, editar, antes
de ejecutar el programa, el fichero \fichero{variables.yaml} _comentando_
aquellos profesores de su departamento que no asistieron. _Comentar_ es una
palabra técnica que se refiere a poner un carácter especial delante de una
línea.  Ese carácter que, dependiendo del formato del fichero o lenguaje en que
está escrito, es uno u otro, hace que la línea precedida por él no exista para
las programas que lo procesan. En el caso de un fichero \fichero{yaml}, el
carácter para comentar una línea es `#`. Así, por ejemplo, en mi fichero
\fichero{variables.yaml}, si tuviese que ocultar a Patricio, porque no hubiese
asistido, para que no apareciese en la nota al margen de los asistentes,
tendría que hacer esto:

~~~
# fichero variables.yaml
...
prof:
#- a: Gómez Varas
#  n: Patricio
- a: Rodríguez García
  n: Julia Beatríz
- a: Sanjuán Pernas
  n: Luis
~~~

Idealmente, mi programa debería ser flexible y aceptar opciones, como
hace `pandoc`, de forma que pudiese decir, por ejemplo:

    generar_acta --excluir Patricio a01_1209141200.md

Quede esto como tarea pendiente para el futuro.

### Por qué a veces es conveniente no usar `--standalone` con `pandoc`
Pensemos de nuevo en el tipo de documento que es nuestra
\fichero{plantilla\_acta.latex}.  Como su extensión claramente indica, es un
documento de \LaTeX. Si alguno ha seguido hasta aquí la explicación, le habrá
surgido la siguiente duda:

> Antes hicimos que se crease programáticamente un fichero que contiene el
> orden del día. Ese fichero resultaba de filtrar las líneas adecuadas del
> fichero del acta, que es un fichero `markdown`. Puesto que el fichero de
> origen es `markdown`, lo que resulta de aplicarle el filtro será necesariamente
> un fichero `markdown`. Después, hemos incluido el contenido de ese fichero en
> la plantilla con la instrucción `\input` de \LaTeX. Aquí hay algo que no
> cuadra. ¿No estamos diciendo que el fichero \LaTeX debe contener etiquetas
> \LaTeX únicamente y no etiquetas \programa{Markdown}?

Si alguno de vosotros se ha hecho esta reflexión, enhorabuena, ha sido muy
agudo y da plenamente en el clavo.

Evidentemente, no podemos incluir \programa{Markdown} directamente en \LaTeX.
Ya vimos el otro día, por ejemplo, que las etiquetas \programa{Markdown} para
encabezados debían, al pasarse a la plantilla, etiquetarse con sus
correspondientes equivalentes \LaTeX\ (`\section`, `\subsection`, etc). Con el
fichero \fichero{md} del orden del día sucede lo mismo. La lista y sus
elementos deben etiquetarse con sus equivalentes para \LaTeX\ si queremos que
todo funcione correctamente en nuestra plantilla \LaTeX. En consecuencia, no
podemos incluir allí directamente nuestro orden del día en formato
\programa{Markdown}, tenemos que convertir antes ese formato a \LaTeX. ¿Cómo
hacerlo? ¿A mano? Esto no parece tan simple como cambiar `'#'` por
`'\section'`. De hecho sería un engorro hacerlo a mano.  Lo podemos hacer
programáticamente por nuestra cuenta, pero eso también es absurdo, porque
`pandoc` puede hacerlo por nosotros:

    pandoc -o orden_del_dia.tex orden_del_dia.md

¿En qué es diferente este comando respecto de los que ya conocemos? En dos
cosas:

- La extensión del fichero de salida es \fichero{tex}, que quiere decir
  documento de \LaTeX. Estamos, pues, convirtiendo de `markdown` a `latex`,
  algo que todavía no habíamos hecho, puesto que no lo habíamos necesitado.

- No estamos aplicando la opción `--standalone`, o `-s` en su versión abreviada.
  Y no lo hacemos, porque no queremos que `pandoc` genere un preámbulo para el
  resultado. Necesitamos únicamente la lista sin preámbulo, puesto que esa
  lista (con etiquetas \LaTeX) la vamos a incluir en un fichero que consta
  ya de su propio preámbulo, nuestra plantilla \LaTeX, y ningún documento \LaTeX
  correcto puede tener más que un único preámbulo.

En general, no usar `--standalone` con `pandoc` es apropiado cuando queremos
obtener algo que será insertado en un documento más grande, este sí, independiente.
En el caso que analizamos, es un documento \LaTeX; en otros casos podría ser, por
ejemplo, \programa{HTML} para ser incluido en una página web más grande.

### Procesar todas las actas de un golpe
Una vez que hemos creado un script siguiendo la lógica descrita, llamémosle
\fichero{generar\_acta.sh}, que permite producir un \fichero{pdf} del acta de
la forma automatizada que hemos previsto, conseguir que todas las actas se
generen a la vez es fácil en entornos \programa{Unix}. Estos entornos
proporcionan constructos de línea de comandos, llamados _bucles_, para este
tipo de tareas. En el nuestro, se podría hacer de la siguiente forma, asumiendo
que estamos en el directorio que contiene todas las actas en formato
\fichero{md}:

    for acta in $(ls *.md); do ./generar_acta.sh $acta; done

El pero es que esta instrucción asume que todos los profesores han asistido
a las reuniones correspondientes. Para que fuera sensible a las ausencias,
es necesario flexibilizar y mejorar el script. Tarea pendiente.

## Epílogo
Todo esto parece endemoniadamente complicado. Os aseguro que no lo es. Los comandos
necesarios para ejecutar todas estas tareas son comandos que todo usuario
intermedio de Linux que trabaje habitualmente y predominantemente en el terminal
conoce y sabe utilizar. Lo que lleva más trabajo es organizarlo todo en un
script que sea fácil de entender, modificar y extender en el futuro.

Lo que me importa destacar es que las posibilidades de automatización se abren
porque los programas que empleamos y los formatos y convenciones de esos formatos
son fieles a las ideas brillantes que pergeñaron los creadores de 
\programa{Unix} y del lenguaje \programa{C}.

No estamos ante programas mastodónticos (un procesador de texto lo es: millones
de líneas de código), sino programas pequeños y especializados que se combinan
como piezas de un Lego. Incluso la instalación completa \TeX{}Live, que pesa tanto 
en megas, es tan grande porque recoge una infinidad de pequeños paquetes 
que expanden lo que el ofrece núcleo de \TeX\ / \LaTeX, muy pequeño en sí mismo.

## Aplicación práctica
El script, unido a los ficheros que comenté el otro día, son aplicables
directamente en cualquier plataforma (\programa{Linux}, quizá también
\programa{MacOSX}) que tenga instalado \programa{Pandoc}, \programa{PDFtk},
\TeX, los paquetes de \TeX\ mencionados el otro día, `bash` y algunos
mini-programas, típicos de \programa{Unix}, que utilizo en el script.

La plantilla está retocada respecto de la que presente en la sección anterior.
Ahora tiene en cuenta la geometría del modelo original, utiliza fuentes más
parecidas a las del modelo, y produce un resultado tan semejante que no es
fácil decidir cuál es el modelo y cuál el original.

Como referencia, adjuntaré en el foro un archivo comprimido con todos los
ficheros necesarios, entre los cuales se incluye una explicación de su 
contenido y uso.


