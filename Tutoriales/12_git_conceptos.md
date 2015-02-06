# \programa{Git}: Conceptos básicos
Antes de entrar en materia, me parece necesario introducir algunos conceptos
clave que nos servirán para no perdernos en el manejo de \programa{Git}.

Hasta ahora hemos estado trabajando y aprendiendo nuevas herramientas de
software dentro de un marco relativamente familiar. Convertir de un formato a
otro es algo que hemos hecho ya o nos hemos planteado ya con otras herramientas
antes de conocer \programa{Pandoc}. Marcar la estructura de un texto es quizá
más novedoso. Pero la idea nueva se puede explicar en poco más de un párrafo
para que sea perfectamente comprensible.

Sin embargo, un sistema de control de versiones puede ser algo completamente
nuevo y un cierto marco de referencia sobre qué clase de funcionamiento o
lógica tiene todo esto, en particular la lógica de \programa{Git}, pienso que
es imprescindible. 

A la vez que esa lógica veremos la terminolgía que se emplea para referirse a
ella. Ésta será necesaria para entender lo que hacemos y por qué. Junto con los
términos técnicos ingleses doy la traducción que suele hacerse de ellos al
castellano. De todas formas, la referencia es siempre la terminología en el
idioma original. Las traducciones a veces no captan del todo el sentido o
pueden resultar un poco forzadas.

## Estados de un fichero y lugares
Cuando decidimos establecer un control de versiones sobre un conjunto de
ficheros en un directorio o carpeta, lo que hacemos es crear una base de datos
en ese directorio donde se almacenarán los datos que se van a controlar. En el
caso de \programa{Git} esta base de datos es un subdirectorio de nombre
\fichero{.git} dentro del directorio que controlaremos.

No tendremos que navegar por \fichero{.git} normalmente, y no nos interesa
conocer ni su estructura ni lo que contiene. Hay una interfaz para consultar e
interactuar con esa base de datos que nos evita tratar directamente con su
contenido. Dicha directorio \fichero{.git}, que contiene la base de datos y
otros metadatos, se llama _repositorio_ (_repository_).

Nuestro _directorio de trabajo_ (_working directory_) sigue siendo el mismo, 
el directorio inicial que ponemos bajo el control del sistema de versiones. Todo
en él, así como sus ficheros, es exactamente igual a efectos prácticos, esté
o no controlado por \programa{Git}.

Además del repositorio y el directorio de trabajo, hay una especie de índice,
llamado _staging area_ (área de preparación), que funciona como un lugar lógico
intermedio por el que pasan los datos desde el directorio de trabajo al
repositorio.

Para \programa{Git} nuestros ficheros están siempre en alguno de estos estados:

- _no rastreado_ (_untracked_). Es como ve \programa{Git} un fichero que no está
  bajo su control, que no está bajo el seguimiento del control de versiones,
  pero que al residir en el directorio que queremos que \programa{Git}
  supervise pudiera estarlo si se lo indicamos. De hecho, lo primero que hay
  que hacer es decidir qué ficheros en nuestro directorio vamos a poner bajo la
  supervisión de \programa{Git}.

- _rastreado_ o _bajo seguimiento_ (_tracked_). Es el fichero al que
  \programa{Git} le está ya siguiendo la pista y está bajo su supervisión.

Un fichero rastreado en nuestro directorio de trabajo puede, a su vez, estar en
uno de estos estados:

- _no modificado_ (_unmodified_). Simplemente un fichero que está controlado por
  \programa{Git}, que está en su base de datos, pero que desde la última vez
  que lo remitimos a ella no ha sido modificado.

- _modificado_ (_modified_). Lo contrario de lo anterior. El fichero ha sido
  modificado respecto de su última versión en el repositorio.

- _preparado_ (_staged_). El fichero está en el área de preparación dispuesto
  a ser confirmado, a que sus datos se almacenen definitivamente, en la base 
  de datos

El estado final de un fichero, cuando sus datos (cambios, modificaciones) tal
como están en el área de preparación, acaban definitivamente almacenados en el
repositorio \fichero{.git}, es lo que se llama estar o haber sido _confirmado_
(_committed_).

Podéis echar un vistazo a las áreas descritas y al ciclo que recorre un fichero
de un estado a otro observando las figuras siguientes:

- **Áreas**: <https://github.com/progit/progit2/blob/master/book/01-introduction/images/areas.png>

- **Ciclo de vida y estados**: <https://github.com/progit/progit2/blob/master/book/02-gitbasics/images/lifecycle.png>

Durante la práctica propuesta, tomaremos un primer contacto con cómo se pasa
de un estado al siguiente.

## Ramas
El otro concepto clave es el de las _ramas_ (_branches_). \programa{Git} permite
la creación de distintas ramas de trabajo sobre un conjunto de ficheros. La
idea es tan simple como la que comentamos al principio de la serie: seguir
trabajando en una zona, digamos, de pruebas o desarrollo, sin tocar la zona
estable o principal. 

La diferencia con el modelo trivial (varias copias del mismo conjunto de
ficheros), es que \programa{Git} crea ramas que no son copias de ficheros, sino
punteros a ficheros y sus instantáneas en el tiempo, lo que implica que no hay
redundancia, que los cambios entre ramas son rápidos y seguros y que, no
obstante, cara al usuario, se obtiene el mismo beneficio de distinguir áreas
estables de áreas en desarrollo sobre el mismo conjunto de ficheros.

Las operaciones básicas sobre ramas son las esperadas:

- Crear o eliminar ramas.
- Cambiar (_checkout_) de una rama a otra.
- Observar diferencias entre ellas.
- Mezclar (_merge_) una rama con otra, por ejemplo, mover los cambios en 
  la rama de desarrollo a la rama estable.

La rama principal, que es la que por defecto siempre se crea cuando se inicia
\programa{Git} para que supervise nuestro directorio de trabajo, se llama _rama
maestra_ (_master branch_ o, brevemente, _master_).

## Servidores remotos
Las rama _master_ en un servidor remoto que clonamos (_clone_) en nuestro
ordenador se denomina _orígen_ (_origin_). 

Las operaciones habituales entre el servidor remoto y nuestro repositorio local
que llevaremos a cabo serán:

- _subir_ o _meter_ (_push_) nuestras instantáneas en el servidor remoto, al que
  otros ordenadores pueden estar conectados y acceder.
- _descargar_ o _tirar de_ (_pull_) las novedades que haya en el servidor remoto
  y que se actualice nuestra copia local con ellas. (Cuando el segundo paso, la
  actualización de la rama _origin_ con la rama local, no se produce
  automáticamente, se habla de _capturar_, _fecthing_, en lugar de _pulling_.
  Creo que en las prácticas que realizaremos, utilizaremos únicamente _pull_.)

## Ejercicios
Todo lo visto hoy es aún demasiado teórico e, incluso, difícil de pillar. Sólo
la práctica concreta puede iluminar estos conceptos y términos. La práctica,
a su vez, ha de ser progresiva y no es nada fácil imaginar primeras prácticas
suficientes.

Como anticipo, diré que para usar \programa{Git} necesitaremos, claro está,
instalarlo. Hay interfaces de línea de comandos e interfaces gráficas. La
interfaz de línea de comandos tiene ventajas. A la larga es la única que puede
hacer todo. Nosotros no vamos a hacer todo lo que se puede hacer con
\programa{Git}.  No obstante, hay una segunda ventaja para el principiante, que
es que nos vemos obligados a utilizar la terminología de \programa{Git} en
secuencias muy breves de comandos (son más, pero más fáciles que los de
\programa{Pandoc}). Con ese bagaje, luego cada cual podrá seguir usando la línea
de comandos o la interfaz gráfica. La interfaz gráfica será diferente según el
programa de interfaz gráfica que se instale. Lo común a todas las instalaciones
de \programa{Git} es la interfaz de línea de comandos, y en ella basaré lo que
venga en próximos días.

Dicho esto, la práctica que propongo se puede hacer ya, sin instalar siquiera
\programa{Git}.  Es un primer contacto con las nociones que hemos visto y los
términos explicados.  Tomad el tiempo que sea necesario. Tampoco es
imprescindible entenderlo todo.  Basta con familiarizarse con términos y
operaciones. Se trata de un tutorial web interactivo con lo básico. Y se puede
repetir cuantas se veces se quiera. Que yo sepa está sólo en inglés:

<https://try.github.io/levels/1/challenges/1>
