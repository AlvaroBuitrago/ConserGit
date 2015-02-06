# Introducción a \programa{Pandoc}
\programa{Pandoc} es un programa que convierte documentos de un formato a otro.
La potencia de \programa{Pandoc} es muy grande. Nosotros sólo vamos a utilizarlo
a una pequeña escala, la necesaria para nuestros propósitos.

Pero bueno es conocer que las posibilidades son bastantes más de las que vamos
a ver. En concreto, mirad el comienzo de la documentación aquí:

<http://johnmacfarlane.net/pandoc/README.html#general-options>

Se especifican los formatos `from` y `to` soportados. `from` indica el
formato de origen del documento y `to` el de salida. Por ejemplo,
\programa{Pandoc} puede convertir un documento \fichero{epub} (típico de ebooks)
a \fichero{beamer} (típico de diapositivas para conferencias).

Para nuestros propósitos nos limitaremos a documentos \fichero{markdown} (con
extensión \fichero{md}, como formato de entrada y a \fichero{pdf},
\fichero{odt} y \fichero{docx} como formatos de salida.

## La línea de comandos
Lo primero es entrar en la línea de comandos (es spanglish, siendo correctos
sería línea de órdenes, pero el uso dominante es _comandos_). Tendréis que 
mirar en vuestro correspondiente sistema operativo la forma de entrar en la 
línea de comandos. Si hay dudas en esto, el foro está ahí.

Una vez en la línea de comandos, desplazáos a la carpeta (= directorio) donde
tenéis vuestros documentos \programa{Markdown}, las prácticas que hemos hecho
hasta ahora.  Suponiendo que están en el directorio _GrupoTrabajo_ dentro de la
carpeta _Documentos_ tendréis que hacer algo así (las rutas son aproximadas, ya
que dependen de cada sistema operativo):

- En \programa{Windows}: 
    
        cd C:\Users\Documentos\GrupoTrabajo

- En \programa{MacOSX}:

        cd /Users/Documentos/GrupoTrabajo

- En \programa{Linux}:

    Si alguno tiene \programa{Linux} ya sabrá cómo hacerlo y dónde ir.


## Ejecutar \programa{Pandoc}
Como esto es una práctica donde hay que utilizar la línea de comandos, aparte
de ejecutar \programa{Pandoc}, nos limitaremos a lo más simple: ver cómo
ejecutar el programa de la forma más elemental posible y ver cuál es el
resultado.

Escoged una de vuestras prácticas, mejor la más breve posible. Digamos que el 
fichero de esa práctica es \fichero{practica1.md}. Si no las habéis guardado en
ningún fichero hacedlo ahora. No olvidad terminar el fichero con la extensión
\fichero{md}. El punto marca el comienzo de la extensión y no hay espacio entre
el nombre, el punto y la extensión. En general conviene que los nombres de
ficheros no contengan espacio alguno ni caracteres raros. Como separador, si el
nombre del fichero contiene varias palabras, es útil el guión bajo. Por
ejemplo: \fichero{practica\_1.md}.

La ejecución de \programa{Pandoc} sobre este fichero es muy simple:

    pandoc practica1.md

Por defecto, `pandoc` produce el resultado y lo muestra en pantalla. El
formato de conversión por defecto es \fichero{html}.

Terminemos añadiendo una opción a la ejecución, la opción `--standalone`, que
genera un documento autónomo. Veremos qué significa tal cosa en breve.

Las opciones van justo después de `pandoc` y separadas por un espacio. Típicamente,
se proporcionan dos formas equivalentes para la mayoria de las opciones, una con
formato largo y una abreviada. Las primeras van precedidas por dos guiones;
las segundas por uno solo. Más fácil es verlo en acción. Ejecutad:

    pandoc --standalone practica1.md

Y con la forma abreviada:

    pandoc -s practica1.md

El resultado es el mismo.

## Ejercicios
Como prueba de que habéis realizado con éxito esta practica, enviad al foro
el resultado de la última ejecución. Normalmente se puede cortar y pegar desde
la línea de órdenes.

Finalmente, ¿por qué lo de _autónomo_? La respuesta en próximas prácticas. Pero
si alguien no puede esperar que ejecute:

    pandoc -s -o practica1.html practica1.md

y visite el recién creado documento \fichero{practica1.html} 
desde su navegador web.

