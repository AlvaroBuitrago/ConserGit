# \programa{Git}: Otros comandos útiles
En esta entrega comentaré algunos otros, los menos posibles, comandos útiles.
\programa{Git} es muy rico en comandos y opciones. Es impensable ver aquí
todo lo que se puede hacer, y menos pretender agilidad haciéndolo.  En estas 
entregas sobre \programa{Git} el objetivo es más bien limitarse únicamente a
lo básico. Si alguna vez surge la necesidad de otro tipo de operaciones, lo mejor
es recurrir a la documentación, a algún libro o a la Web.

## Ignorar ficheros
A veces tenemos ficheros en nuestro directorio de trabajo que no queremos que
\programa{Git} rastree ni supervise en forma alguna. No obstante, en la medida
en que \programa{Git} los ve como no rastreados, tal y como comprobamos el día
pasado, seguirán apareciendo en los mensajes producidos por `git status`. Esto
es algo molesto. Aún más, existen opciones (aunque no las veremos aquí) para
aplicar comandos habituales como `add` o `commit` a múltiples ficheros o a
todos los ficheros que existen en el directorio.  Los ficheros que no nos
interesa que \programa{Git} supervise, y que, sin embargo, sigue viendo como no
rastreados, pueden hacer complicadas o impracticables dichas operaciones
masivas.

Por todo ello, resulta muy útil y prácticamente imprescindible, aleccionar a
\programa{Git} para que ignore ciertos ficheros. Ficheros de esta clase que,
sin duda, no tenemos ninguna intención de que \programa{Git} los supervise, son,
por ejemplo, las copias de seguridad que muchos editores crean automáticamente
en segundo plano. 

Supongamos que esas copias tienen la extensión \fichero{.bak}, una extensión
común a este tipo de ficheros.  Mi editor aún no ha creado ninguna copia de
seguridad de \fichero{hola.md}, el fichero con el que trabajamos la sesión
anterior. Vamos, no obstante, a hacer como si la hubiese producido, creándola
nosotros mismos con nombre \fichero{hola.md.bak} 

Ahora en mi directorio de trabajo que, recuerdo, llamé \fichero{PruebaGit} habrá
dos ficheros: \fichero{hola.md} y \fichero{hola.md.bak}

Si ejecutamos `git status`, \fichero{hola.md.bak} aparecerá como no rastreado.
(Comprobadlo).

Nuestro propósito es indicarle a \programa{Git} que _ignore_ por completo ese
tipo de ficheros, ficheros \fichero{.bak}, como si no existiesen para él, ni
siquiera como no rastreados. Para lograrlo, creamos un fichero en nuestro
directorio, con nombre \fichero{.gitignore} y este contenido:

    *.bak

El asterisco es un comodín que indica cualquier conjunto de caracteres. Por
tanto, este patrón corresponderá a cualquier nombre de fichero que acabe 
con `.bak`. Y al incluirlo en \fichero{.gitignore} esa clase de ficheros
serán ignorados por \programa{Git}.

Volved a ejecutar `git status` y observad que ya no aparece nada relativo a
\fichero{hola.md.bak}. Aunque sí sobre el propio \fichero{.gitignore}!

Pero como \fichero{.gitignore} sí es un fichero esencial al directorio,
ya que contiene algo que afecta a su propia configuración, toca ahora añadirlo
al repositorio, a la base de datos, mediante los comandos conocidos:

    git add .gitignore
    git commit -m "Creado .gitignore"

Ahora `git status` producirá un mensaje "limpio". Comprobadlo.

## Eliminar ficheros
Creemos un fichero tonto, \fichero{tonteria.md}, con el contenido que sea, con el
único propósito de eliminarlo y entender cómo se hace esta operación con
\programa{Git}. Una vez creado, \programa{Git} lo verá, naturalmente, como  _no
rastreado_. Comprobadlo.

Lo añadimos ahora al área de preparación:

    git add tonteria.md

\programa{Git} no sólo lo ve, sino que le está siguiendo la pista:

~~~
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

  	new file:   tonteria.md

~~~

Podríamos tener la tentación de eliminarlo directamente con las
herramientas que proporciona el sistema operativo. Pero, en realidad, resulta
más engorroso, pues tendremos que hacer más operaciones luego con
\programa{Git} para que éste quede en un estado limpio. Por tanto, sigamos
mejor el camino que proporciona el propio \programa{Git}:

    git rm tonteria.md

\programa{Git} produce el siguiente mensaje:

~~~
luis@sams9:~/PruebaGit$ git rm tonteria.md
error: the following file has changes staged in the index:
    tonteria.md
    (use --cached to keep the file, or -f to force removal)
~~~

Interesante. Puesto que eliminar un fichero es cosa seria, no nos deja hacerlo
tan a la ligera. Tenemos que insistir como nos dice que hagamos, pasando la
opción `-f` (o `--force`):

    git rm --force tonteria.md

Esto elimina el fichero de nuestro directorio de trabajo, así como del área
de preparación, dejando el espacio de trabajo limpio, como puede comprobarse
si se ejecuta `git status`. Comprobadlo.

¿Qué pasa si usamos este comando cuando ese fichero está ya registrado en la base
de datos? Probémoslo. 

Volvamos a crear ese fichero, \fichero{tonteria.md}. Una vez creado, lo
incluimos en la base de datos con los comandos que ya hemos visto:

    git add tonteria.md
    git commit -m "Creado tonteria.md"

Si consultamos lo que hay en la base de datos, lo veremos ahí:

~~~
$ git log --oneline
5ffca83 Creado tonteria.md
553ac55 Creado .gitignore
f6ec250 Segunda versión de hola.md
e5f613e Primera versión de hola.md
~~~

Por cierto, he añadido la opción `--oneline` a `git log` para obtener una visión
abreviada del historial en la base de datos. Veremos su utilidad en breve.

Ahora veamos qué pasa si lo eliminamos con `git rm --force`, como antes:

    git rm --force tonteria.md

El estado del fichero eliminado es:

~~~
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

  	deleted:    tonteria.md
~~~

Podemos comprobar además que ya no está en nuestro directorio de trabajo. Pero
debemos confirmar la eliminación. Interesante. A medida que solicitamos operaciones
de eliminado que afectan más profundamente a la base de datos, se nos dan más
oportunidades para dar marcha atrás. En este caso, confirmaremos:

    git commit -m "Eliminado tonteria.md"

¿Y qué queda en la base de datos?

~~~
$ git log --oneline
3711ce4 Eliminado tonteria.md
5ffca83 Creado tonteria.md
553ac55 Creado .gitignore
f6ec250 Segunda versión de hola.md
e5f613e Primera versión de hola.md
~~~

Esto es lo esperado, o lo que deberíamos esperar. Queda constancia de la
operación de eliminación en la base de datos. Aunque los datos del fichero
eliminado siguen ahí, y podrían recuperarse. Existen medios de borrar todo
rastro, pero, en principio, esto debería carecer de sentido. Nos interesa al
máximo la integridad de nuestros datos y eso implica hacer seriamente
desaconsejable borrar todos los rastros por entero.

## Mover o renombrar ficheros
En ocasiones puede surgir la necesidad de mover un fichero a un subdirectorio
dentro del directorio de trabajo, o cambiar el nombre de un fichero. En
general, estas acciones, se llaman _mover_ un fichero. 

Si directamente "movemos" el fichero con las herramientas habituales
que nos proporcione el sistema operativo será de nuevo más engorroso. Es
mejor la herramienta que proporciona el propio \programa{Git}.

Veamos un ejemplo. Como no tengo subdirectorios aún en mi \fichero{PruebaGit},
voy a renombrar un fichero, lo cual es una operación "mover". El fichero único
que tengo, \fichero{hola.md}, lo renombraré como \fichero{hola\_git.md}:

    git mv hola.md hola_git.md

`git status` (comprobadlo) nos sugerirá que confirmemos. Hagámoslo:

    git commit -m "Renombrado hola.md a hola_git.md"

Para \programa{Git}, nuestro anterior fichero recibe ahora otro nombre, y así
queda constancia en su base de datos. En nuestro directorio de trabajo su
nombre habrá cambiado también. Comprobad ambas cosas.

## Cambiar el mensaje explicativo de un `commit`
Otra operación que nos puede interesar en algún momento, una operación más 
cosmética que otra cosa, es cambiar el mensaje explicativo de una confirmación.
Es posible hacerlo para toda confirmación. Pero no es especialmente fácil, así
es que lo omito. Más fácil es hacerlo para la última confirmación realizada. A
modo de ejemplo, supongamos que justo después de confirmar el cambio de nombre
de \fichero{hola.md} nos arrepentimos y queremos poner otro mensaje, por
ejemplo, "hola.md pasa a llamarse hola_git.md", en lugar del mensaje anterior. 
El comando de \programa{Git} sería éste:

    git commit --amend

Esto nos abrirá nuestro editor para que pongamos otro mensaje. Tras editar el
mensaje guardamos el documento.

Una vez hecho, queda constancia del cambio del mensaje en la base de datos:

~~~
$ git log --oneline
25c9862 hola.md pasa a llamarse hola_git.md
3711ce4 Eliminado tonteria.md
5ffca83 Creado tonteria.md
553ac55 Creado .gitignore
f6ec250 Segunda versión de hola.md
e5f613e Primera versión de hola.md
~~~

## Volver a una versión previa
Una operación clave es la de volver a una versión previa de un fichero (_revert_),
de forma que el fichero en nuestro directorio de trabajo acabe estando en una de 
sus versiones anteriores, en lugar de en la versión actual, que ya no nos interesa.

Aquí tenemos varias posibilidades y comandos. Vamos a ver una nada más.

En primer lugar, vamos a crear una versión más de nuestro \fichero{hola\_git.md}.
con el fin de tener varias versiones y ver más claramente como volver de la
actual a una anterior. Recordemos que cambiamos el nombre de \fichero{hola.md}
por \fichero{hola\_git.md} hace un momento.

Hecho. He creado una nueva versión con el texto "Hola, Git. Cómo estás?"

Registremos la nueva versión en la base de datos:

    git add hola_git.md
    git commit -m "Tercera versión de hola_git.md"

A propósito, ¿cansados de hacer `add` y luego `commit`, dos operaciones? Se puede
hacer en una (aunque no lo haya dicho hasta ahora):

    git commit -a -m "Tercera versión de hola_git.md"

Queda registrado:

~~~
$ git log --oneline
c5be9aa Tercera versión de hola_git.md
25c9862 hola.md pasa a llamarse hola_git.md
3711ce4 Eliminado tonteria.md
5ffca83 Creado tonteria.md
553ac55 Creado .gitignore
f6ec250 Segunda versión de hola.md
e5f613e Primera versión de hola.md
~~~

Fijémonos en los números identificativos. Son las versiones breves de los
auténticos identificadores, más largos. Estos identificadores los genera
\programa{Git} aleatoriamente para cada `commit` que se efectúa, y serán
distintos en cada ordenador. Sus versiones breves nos servirán justo ahora.

Nuestro objetivo es hacer que \fichero{hola\_git.md} vuelva a otra versión anterior.
La sintaxis general es:

    git checkout id_version_anterior -- fichero

Este comando (atención a los dos guiones que separan el número del
nombre fichero y los espacios antes y después de los guiones) hará que
`fichero` vuelva a la versión indicada. Nuestro fichero en el directorio de
trabajo quedará modificado correspondientemente, esto es, perderá lo que hay en
él ahora y recuperará lo que había en él en la versión anterior.

La versión que nos interesa recuperar se puede identificar de varias formas.
Aunque engorrosa, la más fácil, puesto que no implica aprender cosas nuevas, es
usar el identificador numérico que hemos visto antes, en su forma breve.
Valdría poner su forma larga (el número completo), pero para qué ponerlo si
podemos utilizar el número corto.

El registro de la primera versión del fichero en cuestión tiene en mi ordenador
el identificador e5f613e, como se ha mostrado antes en el log arriba. En el
vuestro tendrá otro número. Así pues, el comando para volver a esa versión
sería:

    git checkout e5f613e -- hola.md 

Tengo que poner \fichero{hola.md}, porque ese era el nombre de la versión inicial,
y a ese nombre volverá nuestro fichero, y tendremos que añadirlo y confirmarlo,
para volverlo a restaurar. No hubiese sido necesario si el fichero no hubiera
cambiado de nombre entre unas versiones y otras.

    git commit -a -m "Recuperada versión inicial de hola.md"

Veremos que el fichero se habrá recreado en nuestro directorio de trabajo en
su versión inicial.

Veamos qué sucede si aplicamos otra vez el comando anterior, pero ahora para
hacer que \fichero{hola.md} recobre lo que era en su segunda versión.

    git checkout f6ec250 -- hola.md

Echad un vistazo al fichero \fichero{hola.md}. Habrá cambiado su contenido como
esperamos. Habrá vuelto a la segunda versión.

Queda dejar las cosas limpias en la base de datos:

    git commit -a -m "hola.md cambiado a su segunda versión"

Mirad al historial de cambios para recordar todo lo que hemos hecho hasta ahora:

~~~
$ git log --oneline
2d8fc4e hola.md cambiado a su segunda versión
c21ba2a Recuperada versión inicial de hola.md
c5be9aa Tercera versión de hola_git.md
25c9862 hola.md pasa a llamarse hola_git.md
3711ce4 Eliminado tonteria.md
5ffca83 Creado tonteria.md
553ac55 Creado .gitignore
f6ec250 Segunda versión de hola.md
e5f613e Primera versión de hola.md
~~~

## Advertencia esencial
Lo que sigue lo voy a poner bien destacado.

**Abstenerse de realizar operaciones que eliminen cosas en el repositorio, cuando
el repositorio es compartido y se está trabajando en grupo**. Incluso cambiar el
nombre de un fichero debe ser consultado y cualquier decisión de eliminación
que afecte al repositorio, acordada. En caso contrario, los compañeros pueden
volverse locos intentando comprender qué ha pasado, y dónde están las cosas que
había antes.

En general, hay que eludir la tentación de funcionar como habitualmente hacemos
cuando no tenemos un control de versiones. En general, es mejor evitar comandos
que eliminen cosas. Es mejor aprovecharse de las ventajas del control de
versiones y crear nuevas versiones, en lugar de eliminar. La base de datos ocupa
muy poco espacio y no debe agobiarnos que crezca y acumule todo nuestro 
trabajo sucio, nuestras idas y venidas, a lo largo del tiempo. Al final lo que
cuenta es que la última versión esté en el punto que queremos.

## Ejercicios
Reproducir los comandos comentados en vuestro directorio de pruebas. Cada sección
puede considerarse una práctica. Este texto es largo y puede ser dividido en
tantos como secciones contiene.

En todo caso, los comandos clave de uso frecuente son los comentados el día
pasado. Se puede usar \programa{Git} sin problemas con lo explicado allí. Lo
único realmente básico que faltaría, en caso de querer disponer de una repositorio
remoto y, claro esta, de trabajar sobre un mismo proyecto en equipo, queda
para próximas entregas.

## Resumen de comandos
- `git rm --force <fichero>`: Elimina `fichero` de nuestra espacio de trabajo y
  del área de preparación.
- `git log --oneline`: Produce un historial del repositorio en formato breve.
- `git mv <fichero> <fichero_nuevo>`: Cambia el nombre de `fichero` por 
  `fichero_nuevo`.
- `git --amend`: Permite enmendar la confirmación inmediatamente anterior. Se
  usa normalmente para cambiar el mensaje de dicha confirmación.
- `git commit -a -m "<mensaje>"`: Añade los cambios actuales al área 
  de preparación y los confirma, en un solo paso.
- `git checkout -- <id_commit> <fichero>`: Revierte `fichero` a una versión
  anteriormente confirmada con el identificador `id_commit`.
