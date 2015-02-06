# \programa{Git}: Instalación y configuración inicial
De la instalación en sí poco tengo que decir más que apuntar las posibilidades
"normales" disponibles. Con "normales" me refiero a instalar el software con
nuestras herramientas habituales de instalación. Lo no "normal" sería instalar
desde las fuentes, es decir, coger el código entero de \programa{Git}, que, como
el de \programa{Pandoc}, es código abierto, y compilarlo. Ni siquiera me
referí a esa posibilidad con \programa{Pandoc}. Si la comento de pasada es por
si os topáis con ella en alguna web, para que la descartéis.

## Diferentes opciones de instalación
Con \programa{Git} tenemos la posibilidad de instalar lo básico, es decir,
la infraestructura \programa{Git} necesaria, que incluye la interfaz de línea
de comandos, o una versión más grande que incluye una interfaz gráfica y/o,
incluso, alguna clase de interfaz para interactuar con \programa{GitHub}.

En \programa{Linux} y \programa{MacOSX}, la primera opción es lo habitual en
un principio. En \programa{Windows} se suele recomendar la segunda opción, pues
los instaladores de versiones más grandes suelen tomar medidas, en el proceso
de instalación, que son necesarias en \programa{Windows}, de un modo automático 
y que hacen más sencillo el proceso de instalación.

En todo caso os cito todas las opciones que he visto recomendadas en distintos
libros. No comento nada de \programa{Linux}, pues ninguno lo usáis. En cualquier
caso la instalación en \programa{Linux} es trivial.

### \programa{Windows}
El instalador está aquí: 

<http://windows.github.com>

Una mini-guía inicial se puede consultar en: 

<https://help.github.com/articles/getting-started-with-github-for-windows/>

En principio, no crearía ninguna cuenta en \programa{GitHub} aún ni un repositorio
local (pasos 2 y 3 comentados en la mini-guía), para poder hacerlo en las prácticas
siguientes.

### \programa{MacOSX}
Se puede usar el instalador oficial:

<http://git-scm.com/download/mac>

Del mismo modo que en \programa{Windows}, se puede también utilizar el
instalador de \programa{GitHub}, que incluye \programa{Git}:

<http://mac.github.com>

Lo dicho respecto a \programa{Windows} hace un momento vale aquí igualmente.

Dadas las diferentes interfaces y formas de instalación, unido al hecho de que
yo sólo tengo \programa{Linux}, no me es posible determinar diferencias entre
unos instaladores u otros y los pasos específicos que se pidan. En general,
salvo lo comentado respecto de crear ya un repositorio o cuenta en
\programa{GitHub}, supongo que aplicar las opciones por defecto no supondrá
ningún problema. El foro está ahí para que comentéis los procesos concretos de
instalación, por si os podéis ayudar unos a otros.

## Configuración inicial
\programa{Git} requiere de una configuración inicial. Aunque gran parte de esa
configuración se realiza de modo transparente cuando se instala, hay valores que,
a no ser que el instalador os los haya pedido en el proceso de instalación, 
hay que establecer.

Como no conozco los pasos exactos de vuestro proceso de instalación, lo primero
quizá sería comprobar si ya habéis configurado esos valores al instalar.

Ejecutar los siguientes comandos desde el terminal:

    git config user.name

Esto devuelve el nombre de usuario por defecto. A no ser que se os haya solicitado
al instalar, estará probablemente vacío.

    git config user.email

Lo mismo en relación con la dirección de correo electrónico.

    git config core.editor

Esto devuelve el editor que se elige como editor por defecto. De nuevo vacío si
no se os ha solicitado al instalar, o con uno que \programa{Git} ponga por defecto,
pero que no tiene por qué ser el que hayáis elegido vosotros. En todo caso, las
instalaciones modernas de \programa{Git} suelen poner por defecto el editor
que en vuestro sistema operativo es el editor por defecto de ficheros 
\fichero{.txt}. O sea, que esta opción puede ser perfectamente válida.

Si dichos campos están ya establecidos, porque así lo hicísteis al instalar, nada
más hay que hacer. En caso contrario hay que ejecutar estos comandos. Cada uno
es un comando independiente, aunque los pongo en el mismo párrafo.

    git config --global user.name "Pepito Pérez"
    git config --global user.email pepito@example.com

Opcionalmente:

    git config --global core.editor "vuestro editor"

Este último paso puede ser innecesario. Además, la forma de definir el editor
puede o no requerir poner simplemente el nombre del editor o, si eso no
funciona, su ruta en vuestro sistema. De esto no puedo decir mucho más y
tendréis que investigar por vosotros mismos.  

## Ejercicios 
Como con \programa{Pandoc}, enviad el resultado de ejecutar:

    git --version

