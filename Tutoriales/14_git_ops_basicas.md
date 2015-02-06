# \programa{Git}: Comandos básicos
Este tutorial es totalmente práctico. Se trata de realizar una sesión completa
con \programa{Git}, paso a paso, y ciñéndonos únicamente a sus operaciones
básicas en modo local. Lo que haya de hacerse para interactuar con un
repositorio remoto queda para otra práctica.

Mientras he escrito el tutorial he ejecutado la sesión en mi ordenador y lo
reproduzco aquí tal cual.

Casi la totalidad de los comandos \programa{Git} que he introducido os son
ya conocidos de la práctica online del día pasado. Pero ahora se trata de
comentarlos en nuestra lengua y de volver a ponerlos a prueba en un caso real
dentro de nuestro propio ordenador.

## El directorio de trabajo
Lo primero. Vamos a crear una carpeta o directorio de trabajo. Yo lo he llamado
\fichero{PruebaGit}. Podéis llamarlo así o elegir cualquier otro nombre. Utilizad
las herramientas de vuestro sistema operativo que queráis.

Ahora, ya desde el terminal, toca moverse a ese directorio. Creo que esto
ya sabéis hacerlo, algo así cómo:

- En \programa{Windows}: `cd C:\Users\Documentos\PruebaGit`

- En \programa{MacOSX}: `cd /Users/Documentos/PruebaGit`

- En \programa{Linux}: `cd ~/PruebaGit`

La ruta puede variar, dependiendo de dónde hayáis creado el directorio y de
la configuración de vuestro ordenador.

## Inicialización de \programa{Git} en el directorio de trabajo
Una vez que estamos ahí, ejecutamos \programa{Git} para que supervise y lleve
el control de versiones de lo que vayamos a hacer en nuestro directorio de
trabajo.

    git init

Si queremos una configuración especial para \programa{Git} en este directorio,
una distinta de la configuración global del día pasado, la podemos realizar
ahora:

    git config user.name "Luis Sanjuán"
    git config user.email luisj.sanjuan@gmail.com
    git config core.editor vim

Si la configuración va a ser igual que la global, no hay que hacer nada más.

A partir de este momento, \programa{Git} controla nuestro directorio y seguirá 
la pista de los ficheros que le digamos.

¿Qué ve \programa{Git} ahora?

~~~
$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
~~~

Como no hay nada en el directorio, \programa{Git} no ve nada, más que a él
mismo y la rama _master_ que acaba de crear. Está ahí esperando que le digamos
qué hacer y nos hace sugerencias, como la que va entre paréntesis. Podemos
prescindir de ellas, de momento, aunque a veces son útiles.

## Ficheros no rastreados
Creemos un fichero nuevo en nuestro directorio. Usad las herramientas habituales
para hacerlo. Mejor un fichero de texto, en \programa{Markdown} ;-), vamos a llamarle
\fichero{hola.md}. Y escribimos en él algo: "Hola".

Volvamos a preguntar qué es lo que \programa{Git} ve tras haber creado este
nuevo fichero.

~~~
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

  	hola.md

nothing added to commit but untracked files present (use "git add" to track)
~~~

Ahora sí que ya ve algo, aparte de a sí mismo. Ve nuestro fichero, y para él
está en el estado de no rastreado (_untracked_).

## Ficheros rastreados y preparados
Hagamos que \programa{Git} le siga el rastro. Al hacerlo, lo introduce
también en el área de preparación (_staging area_)

    git add hola.md

Veamos cómo ha cambiado la cosa:

~~~
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  	new file:   hola.md
~~~

Está claro, el fichero esta ahí, es ya un nuevo fichero al que \programa{Git}
está siguiendo la pista, preparado para que sus datos se almacenen en su base
de datos de un modo permanente, cuando se lo digamos, o dicho en terminología
\programa{Git}, para que el fichero quede _confirmado_ (_committed_).

## Confirmación de ficheros
Vamos a hacerlo. Al hacerlo incluimos un mensaje descriptivo de nuestro "cambio".
Es un cambio, aunque sea un cambio inicial.

    git commit -m "Primera versión de hola.md"

Esto nos va a devolver un mensaje con lo que \programa{Git} ha hecho:

~~~
[master (root-commit) b4a5186] Primera versión de hola.md
 1 file changed, 1 insertion(+)
  create mode 100644 hola.md
~~~

Y si ahora volvemos a ejecutar `git status` el ciclo se repite. Pero ahora
es más breve. Su base de datos ya está en funcionamiento y operativa, con
cambios permanentes almacenados. Todo lo demás está limpio y no hay nada
nuevo en el directorio en relación con lo que se ha grabado en la base de datos.

~~~
$ git status
On branch master
nothing to commit, working directory clean
~~~

## Ficheros modificados
Ahora toca trabajar sobre nuestro fichero \fichero{hola.md} de la forma habitual,
cambiándolo. Vamos a escribir en él "Hola, Git", en lugar del "Hola" que había.

¿Qué ve \programa{Git} después del cambio?

~~~
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    	modified:   hola.md

no changes added to commit (use "git add" and/or "git commit -a")
~~~

Aparte de los mensajes de antes, lo nuevo ahora es que \programa{Git} observa
que hemos modificado el fichero \fichero{hola.md}. Para él ahora está en un
nuevo estado: modificado. \programa{Git} sabe esto, porque está comparando
lo que tiene en su base de datos con lo que hay ahora en el directorio de
trabajo.

Desde aquí, el ciclo anterior se repetiría. Añadiríamos otra vez el fichero
\fichero{hola.md} al área de preparación y desde ahí lo confirmaríamos. Por
supuesto, no tenemos porque ejecutar estas operaciones inmediatamente. Podemos
seguir trabajando y modificando nuestro fichero, y dejar el proceso de
preparación y confirmación para cuando decidamos almacenar en la base de datos
de \programa{Git} los cambios de forma permanente. Vamos hacerlo ahora:

    git add hola.md
    git commit -m "Segunda versión de hola.md"

Los mensajes de estado y el mensaje final serán semejantes a los anteriormente
vistos.

## El historial de versiones
Para terminar esta primera sesión real con \programa{Git} podemos pedirle que
nos muestre lo que hay en su repositorio, esto es, los cambios (versiones)
que hemos confirmado para que se almacenen permanentemente en su base de datos.

~~~
$ git log
commit b383d7aea7baacba70db9fe7827232f35882ecd5
Author: Luis Sanjuán <luisj.sanjuan@gmail.com>
Date:   Mon Feb 2 17:18:41 2015 +0100

    Segunda versión de hola.md

commit b4a5186a71e3ebf712de2f340f1d2ee7fa28cf7a
Author: Luis Sanjuán <luisj.sanjuan@gmail.com>
Date:   Mon Feb 2 17:05:01 2015 +0100

    Primera versión de hola.md
~~~

Aquí están nuestras dos versiones, con su autor, hora, fecha de confirmación
y el mensaje que introducimos en el momento de confirmarlas. También hay
un número arriba, un identificador único de cada confirmación. Como se ve,
se muestran en orden cronológico descendente.

Algo más interesante es pasar la opción `-p` o `--patch` (de parche).
Nos mostrará no sólo el historial de versiones, sino, además las diferencias
entre la versión original y la versión "parcheada", o sea, cambiada.

~~~
$ git log --patch
commit b383d7aea7baacba70db9fe7827232f35882ecd5
Author: Luis Sanjuán <luisj.sanjuan@gmail.com>
Date:   Mon Feb 2 17:18:41 2015 +0100

    Segunda versión de hola.md

diff --git a/hola.md b/hola.md
index a19abfe..68ec2cd 100644
--- a/hola.md
+++ b/hola.md
@@ -1 +1 @@
-Hola
+Hola, Git

commit b4a5186a71e3ebf712de2f340f1d2ee7fa28cf7a
Author: Luis Sanjuán <luisj.sanjuan@gmail.com>
Date:   Mon Feb 2 17:05:01 2015 +0100

    Primera versión de hola.md

diff --git a/hola.md b/hola.md
new file mode 100644
index 0000000..a19abfe
--- /dev/null
+++ b/hola.md
@@ -0,0 +1 @@
+Hola
~~~

La segunda versión de nuestro fichero \fichero{hola.md} es una versión
"parcheada" de la primera. Se muestran las líneas en que difiere de ella. La
línea en la versión original, sin el parche, aparece precedida por `-`,
mientras que la nueva línea que está en su lugar, la que incluye el parche o
modificación de la línea original aparece precedida por `+`. Estos signos `-` y
`+` son convencionales para mostrar diferencias entre líneas de ficheros. Se
observa además que en la información sobre la primera de nuestras versiones, no
hay nada de lo que la línea `Hola` difiera. Es lógico, fue nuestra primera
versión, no hay nada (`/dev/null`) con la que compararla.

## Resumen de comandos
- `git init`: Inicia \programa{Git} sobre el directorio en el que estamos.
- `git status`: Muestra el estado de los ficheros en el directorio de trabajo.
- `git add <fichero>`: Añade el fichero al área de preparación. Además, si el
  fichero no estaba rastreado, cambia su estado a rastreado.
- `git commit -m "<mensaje>"`: Confirma lo que resida en el área de preparación.
  Los datos se almacenan permanentemente en el repositorio con el mensaje
  asociado.
- `git log`: Muestra el historial de versiones.
- `git log --patch`: Muestra historial de versiones con diferencias incluidas.

## Ejercicios
Reproducir la misma sesión que he ejecutado aquí.
