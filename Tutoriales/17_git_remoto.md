# \programa{Git}: Operaciones en repositorios remotos. 
En la sección anterior vimos cómo asociar nuestro repositorio local con la
réplica remota, y vimos también cómo hacer que el repositorio remoto
se actualizase por primera vez con el contenido del repositorio local.

En esta sección veremos las operaciones básicas entre repositorio local y
repositorio remoto. Nos dejaremos unas cuantas en el tintero. De nuevo, sólo
lo inmediatamente útil y lo que usaremos continuamente. La sección por ello
será muy breve, pero ciertamente esencial.

¿Cuáles pueden ser estas operaciones? Es evidente que sólo pueden ser dos:
subir nuestros datos locales al repositorio remoto y bajar del repositorio remoto
los datos que otro usuario del grupo haya añadido y que todavía no están en
nuestro repositorio local. La primera operación se denomina _push_; la segunda,
_pull_ o _fetch_, dependiendo de lo que sucede o no después de la descarga. 
Aquí nos limitaremos a _pull_. 

## Actualizar el repositorio remoto
La operación para actualizar el repositorio remoto con el contenido de nuestro
repositorio local la vimos el otro día y es la que hay que usar siempre que
queramos actualizar el repositorio remoto, no sólo la primera vez. Además,
si ya aplicamos la opción `-u` comentada el otro día, a partir de ese momento
los comando son más simples:

    git push

en lugar del más largo:

    git push origin master

## Actualizar nuestro repositorio local
La operación inversa es actualizar nuestro repositorio local con lo que haya
en el remoto. Aquí hay dos variantes, _fetch_ y _pull_. La diferencia básica
es que _fetch_ obtiene los datos del repositorio remoto y nos deja a nosotros
la opción de actualizar los nuestros a partir de ellos. Cosa que debemos hacer
con otro comando nuevo. Para ceñirnos a lo más simple, nos concentraremos en
_pull_, que a la vez que captura los datos remotos, actualiza nuestro repositorio
local automáticamente. Esto funciona normalmente en repositorios de una sola
rama, como, de momento, los nuestros. Por tanto, para poner al día nuestro
repositorio local con lo que haya en el remoto, la operación sería también
muy simple (aunque no la ejecutaremos todavía):

    git pull

## Clonar repositorios
Evidentemente carece de sentido `pull` cuando somos los únicos contribuidores de
nuestro repositorio. Los cambios siempre irán en un sentido, desde nuestro
repositorio local al remoto, que funcionará únicamente como replica (a efectos
de copia de seguridad o comunicación de nuestro trabajo al exterior). No
podrá darse el caso de que el repositorio remoto contenga algo que el local no 
contenga ya. Y, en consecuencia, el único comando útil sería `git push`.

Para que tenga sentido `git pull` hay que ser el receptor de nueva información no
subida antes por nosotros mismos. Esto sucede si "descargamos" un repositorio
público de otra persona y creamos una réplica suya de él, o bien, más claramente
en nuestro caso particular, hacia el que nos dirigimos, si somos miembros 
de un grupo que comparte el mismo repositorio.

Pondremos en práctica el comando, no obstante, y muchas veces, pero para ello 
vamos a hacer un _excursus_ necesario.

He creado en \programa{GitHub} otro repositorio con nombre \fichero{ConserGit}.
Nos servirá como la plataforma final para las prácticas que queden. Por lo
pronto, nos servirá para aprender a clonar (_clone_) repositorios remotos.

La URL del repositorio es la siguiente:

<https://github.com/LuisSanjuan/ConserGit>

Ahora id a un directorio "normal" con el terminal, ¡no al directorio de las
pruebas anteriores, \fichero{PruebaGit}!, sino a un lugar habitual de vuestro
espacio de usuario, que puede ser \fichero{Documentos} u otro cualquiera. Sea
como sea, tiene que ser un lugar que no sea ya un directorio sobre el que se
ha iniciado \programa{Git}. Una vez que estéis en ese espacio "normal",
ejecutad este comando:

    git clone https://github.com/LuisSanjuan/ConserGit

Se habrá creado un directorio \fichero{ConserGit} que será una replica exacta
del repositorio remoto del mismo nombre alojado en \programa{GitHub}.

Doy por hecho que para este repositorio \programa{ConserGit} seguiréis usando
las mismas configuraciones que establecísteis al principio de esta serie de
tutoriales con `git config --global`.

## Añadir colaboradores a un proyecto \programa{GitHub}
Para que se pueda hacer algo más que clonar un repositorio, esto es, para poder
subir y bajar datos, es necesario ser un contribuidor de dicho repositorio.

\programa{GitHub} proporciona interfaces web sencillísimas para dar de alta a
usuarios como contribuidores a un proyecto o repositorio a través de opciones
de configuración de ese proyecto que aparecen en su página web (la del
repositorio en cuestión). Omito la explicación, porque es algo obvio que se
descubre navegando por la página.

Para poder daros de alta como contribuidores a \programa{ConserGit} tenéis
que ser usuarios de \programa{GitHub} con una cuenta creada en
\programa{GitHub}.  A fecha de hoy, el único que lo es ya es Álvaro (supongo que
será él, porque con el mismo nombre y un repositorio \fichero{MuseScore} ...).
Es el único al que puedo añadir ahora, pues el formulario sólo me permite
añadir usuarios existentes ya en \programa{GitHub}. Cuando paséis por las
sesiones anteriores, indicadme, a través del foro, vuestros nombres de usuario
en \programa{GitHub} antes de ejecutar las prácticas que a continuación
expongo.

## Ejercicio. Subir datos a un repositorio remoto
La estrategia es la ya conocida. O sea, repetimos una práctica anterior.

Propongo que creéis un nuevo documento con nombre \fichero{docLuis.md} (el
nombre será distinto según el usuario) y lo subáis al repositorio remoto. Los
pasos, los recuerdo, serían los siguientes:

1. Ir con el terminal al directorio \fichero{ConserGit} local.

2. Crear ahí el documento con vuestro editor de siempre.

3. Prepararlo y confirmarlo:

        git add docLuis.md
        git commit -m "Primera versión de docLuis.md"

4. Subir los cambios efectuados:

        git push -u origin master

    Notad, que ahora uso el comando largo. Esto es necesario, porque es la
    primera vez que ejecutáis este comando. Las próximas veces, bastará
    la versión corta:

        git push

## Ejercicio. Bajar datos de un repositorio remoto
Siempre que se vaya a añadir o cambiar algo en el repositorio
local \programa{ConserGit}, antes de efectuar tales cambios, así como
siempre que se quiera actualizar el repositorio local con las
últimas novedades que los demás miembros del grupo hayan introducido, hay que
actualizar nuestro repositorio local con el contenido del remoto. El comando
es el comentado. Ejecutadlo ahora:

    git pull

## Resumen de comandos
- `git clone <repo_url>`: Clona el repositorio remoto alojado en `repo_url`.

- `git push`: Actualiza el repositorio remoto con nuestra instantánea local.


- `git pull`: Actualiza el repositorio local a la última instantánea remota.
