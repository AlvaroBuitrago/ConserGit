# \programa{Markdown}: Otras marcas interesantes
Conocido ya lo básico, os comento otras marcas útiles, aunque de uso, quizá,
menos frecuente.

## Listas anidadas
Una lista anidada es una lista dentro de otra lista. En \programa{Markdown},
para distinguir la lista interna se utilizan 4 espacios o 1 tabulador delante
de cada uno de sus elementos:

    1. Primer ítem, que contendrá una lista de subapartados:
        - El primer subapartado
        - El segundo
        - El tercero
    2. Ahora sigo con otro elemento de la lista principal
    3. Y otro

## Listas con más de un párrafo en alguno de sus ítems
Aunque tampoco es frecuente, a veces un elemento de una lista consta de varios
párrafos. Para que \programa{Markdown} entienda que no estamos empezando un
párrafo nuevo fuera de la lista, sino dentro de un elemento de la lista, se
utilizan otros 4 espacios o 1 tabulador delante de ese nuevo párrafo dentro del
ítem:

    1. Esto es un ítem largo. El primer párrafo sería éste.

        Dentro del mismo elemento está este nuevo párrafo.
    2. Ahora viene un segundo elemento.
    3. Y un tercero.

## Hipervínculos (enlaces web)
Existen varias formas, la más sencilla para que aparezca una dirección web o de correo, que se pueda pinchar y llevarnos al sitio correspondiente 
es rodearla de ángulos.:

    <http://conservatoriodeavila.es/web>
    <usuario@correo.com>

## Imágenes
Para incluir imágenes dentro de un documento se utiliza la siguiente sintaxis.
Es la más compleja que hemos visto hasta ahora:

    ![título de la imagen](dirección de la imagen)

Por ejemplo, si tengo una imagen de un violín (violin.jpg) guardada en la
ruta `C:\Fotos\violin.jpg`, para insertarla pondría:

    ![un violín](C:\Fotos\violin.jpg)

Lo que va entre corchetes es el título de la imagen, el que queramos nosotros.
Lo que va entre paréntesis es la ruta del fichero que contiene la imagen. He
puesto una ruta típica en \programa{Windows}. Para usuarios de
\programa{MacOSX} o \programa{Linux}, las rutas tienen otra forma, por ejemplo:

    ![un violín](/home/luis/Fotos/violin.jpg)

Para ser más breves, podemos suprimir el título y, si la imagen está en
la misma carpeta en la que está el documento \programa{Markdown}, simplificar la
ruta. Por ejemplo:

    ![](violin.jpg)


¡Ojo! El signo `!` y los corchetes y paréntesis son obligatorios.

## Tablas
Hay muchas opciones para hacer tablas, pero, en general, son engorrosas. La
más sencilla tendría una forma parecida a esta:

    Alumno    Nota    Faltas
    ------    ----    ------
    Pepita    10      0
    Juanín    0       10

Los encabezados van arriba separados de las filas de las tablas por
sucesiones de guiones. Luego van en lineas distintas cada una de las
filas. Alguien pude estar interesado en probar cómo afecta la alineación
de los items en cada celda con respecto a la linea de guiones. En el
ejemplo, esos elementos están alineados con el comienzo de la línea de
guiones para cada columna. ¿Qué pasaría si estuvieran alineados con
el final de la línea de guiones en cada columna, o no alineados ni a
la izquierda ni a la derecha?

Sin embargo, esta sintaxis sólo funcionaría con \programa{Pandoc} u otros
interpretes online de \programa{Markdown} que la implementen. En el
\programa{Markdown} original no hay soporte para tablas. Dicho soporte, junto
con otros como el soporte para ecuaciones matemáticas, es una extensión al
\programa{Markdown} original, y depende de los intérpretes. 

<http://Dillinger.io> y muchos de los intérpretes online, aceptan esta otra
sintaxis, algo más engorrosa:

    |Alumno|Nota|Faltas|
    |------|----|------|
    |Pepita|10  |0     |
    |Juanín|0   |10    |

(Nota: Los separadores `|` no tienen porque estar alineados. Lo pongo
así porque es más fácil de ver para el ojo humano.)

## Un par de extras
Dos marcas muy usuales en documentos técnicos son: texto *verbatim* (que
aparecerá con tipo de letra _typewritter_ y donde el espaciado original,
el que pone el que lo escribe, se respeta) y ecuaciones matemáticas.

El texto *verbatim* es el que uso yo para poner los ejemplos de cada
marca. Y se consigue poniendo cuatro espacios delante de cada línea de
este texto. Por ejemplo:

    Aquí estoy en el texto normal, pero el siguiente párrafo va a contener
    un ejemplo de uso de Markdown y lo voy a desplazar cuatro espacios
    respecto de este texto normal:

        <http://www.example.com>
        <http://conservatoriodeavila.es/web>

Termino con una ecuación matemática. ¿Qué tal la fórmula de la media? Esto
no funciona habitualmente en intérpretes online, salvo aquellos que además
soportan \programa{MathJax}. Habrá que esperar a pandoc para ver el resultado.

    $\mu = \frac{1}{n}\sum_{i=1}^n a_i$

## Ejercicios
1. Probar independientemente cada una de las marcas explicadas. Tened en cuenta
que las siguientes seguramente no funcionen en <http://Dillinger.io> u otros
intérpretes online de \programa{Markdown} como los que indiqué en la primera
entrega:

    - Imágenes. Si el sitio en concreto no permite cargar imágenes, y es
    improbable que lo haga, esto no funcionará.  
    - Tablas. Sólo funcionará (en <http://Dillinger.io>) la segunda comentada.
    - Ecuaciones. No funciona salvo que el sitio soporte \programa{MathJax}
    (improbable).

2. Aún sin comprobar online (esperemos a \programa{Pandoc}), crear un 
mini-documento donde se incluyan listas anidadas, hipervínculos e 
imágenes (ej. el logo del conser). Y opcionalmente, tablas.
