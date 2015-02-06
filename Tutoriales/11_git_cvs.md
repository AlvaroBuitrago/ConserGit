# \programa{Git}: Control de versiones distribuido
\programa{Git} es un programa de control de versiones. En esta introducción
comentaré qué es eso de un control de versiones, y un poco por
encima qué es lo que hace de \programa{Git} más interesante que otras
alternativas como software para realizar esa función.

## Control de versiones
Cuando trabajamos sobre cualquier tipo de ficheros, a menudo acabamos
modificándolos a lo largo del tiempo bastantes más veces de las previstas.

No es infrecuente el caso de que hagamos copias de ficheros o directorios 
completos para mantener una versión de lo antiguo, sin el peligro de alterar
el trabajo ya realizado, y continuemos añadiendo novedades a una de las
copias. Puede incluso darse el caso de tener más de dos copias, que recogen
versiones previas de lo que estamos haciendo, de forma que podamos volver
a ellas si cambiamos de opinión en las nuevas modificaciones que vamos
introduciendo.

A la larga, esto acaba teniendo un montón de problemas:

- Consumimos espacio en disco innecesario tratando de mantener todas las 
  copias.

- Acabamos perdiendo la pista de las diferentes versiones.

- Resulta engorroso andar copiando y eliminando de aquí y de allá para
  recuperar o actualizar distintas versiones.

- Es difícil, y tan engorroso que ni siquiera lo intentamos muchas veces,
  ver cuáles son las diferencias entre lo que hicimos hace cinco meses
  o cinco años y lo que estamos haciendo ahora sobre esos mismos ficheros.

Si pensamos en un trabajo conjunto, esta estrategia es ya más que chapucera.
Directamente, no funciona.

Un sistema de control de versiones trata de resolver estos problemas de un modo
sencillo, a saber, manteniendo una base de datos de los cambios, o, en general,
de las instantáneas a lo largo del tiempo, de un conjunto de ficheros sobre el
que continuamente estamos trabajando, individualmente o en grupo.

## Local _versus_ distribuido
Los sistemas de control de versiones existen desde hace mucho. En un principio,
eran sistemas _locales_. Lo que significa que la base de datos de los cambios
en el tiempo reside en un único ordenador, justo en el que tenemos 
esos ficheros que se están controlando.

Pronto se vio que un sistema puramente local tiene muchas desventajas.

Incluso para un único usuario. Si éste utiliza otro ordenador, tiene que recrear
en cada uno de sus ordenadores la base de datos.

De nuevo, cuando se trata de múltiples usuarios trabajando sobre unos mismos
ficheros, la cosa se hace impracticable. Cada vez que un usuario cambia algo
en los ficheros, tiene que enviar la base de datos, o la parte de ella que
corresponda, al resto de usuarios para que todos sigan trabajando sobre 
la última versión.

La solución es evidente. Dejar que sea un ordenador, al que puedan acceder
todos los usuarios, el que mantenga la base de datos de los cambios. Los
cambios que cada usuario efectúe se envían a la base de datos remota y
cualquier usuario puede recuperarlos o descargarlos para mantener sus ficheros
en su versión más actualizada.

## ¿Por qué \programa{Git}?
Otras dificultades surgen, sin embargo, en el escenario anteriormente
descrito.

- Si el servidor remoto que aloja la base de datos no está accesible, ya
  sea porque los usuarios no tienen acceso a Internet en ese momento, o porque
  el servidor se estropea temporalmente o la red está saturada, nadie puede
  enviar ni recibir cambios de él. Una parte del trabajo se tiene que posponer
  inevitablemente hasta que el usuario tenga acceso a Internet o el servidor
  resulte accesible de un modo eficaz.

- Si algo falla en el servidor y la base de datos se corrompe o destruye
  no hay forma de recuperarla. El trabajo puede resultar seriamente dañado.
  Si se han hecho copias de seguridad en el servidor remoto, se podrá rescatar
  parte de ese trabajo, pero no los cambios de último momento.

La idea original de \programa{Git} es que la propia base de datos se
distribuye entre todos los usuarios. Es decir, todos los usuarios mantienen
una réplica exacta del trabajo conjunto, que se actualiza continuamente bajo
demanda.

Los usuarios pueden trabajar sin conexión a Internet perfectamente, y remitir
y confirmar los cambios que vienen realizando en su espacio personal de
trabajo cuando vuelvan a estar conectados, así como descargar y recuperar
los cambios que cualquier otro usuario haya enviado ya. Si hay un fallo
en algún punto, es fácil recuperar los datos, puesto que cualquier usuario
en el grupo tiene una copia exacta de la base de datos que todos tienen.

Con \programa{Git} los usuarios trabajan esencialmente en modo local. Esto
implica que no hay ninguna merma de velocidad, como la que sí tiene lugar,
en mayor o menor medida, cuando se está trabajando directamente sobre un
lugar remoto a través de Internet (ejemplos: cuando se escribe en un foro,
cuando se escribe en un blog, etc.). Todo sucede en su ordenador y a la
velocidad de su propio ordenador. El único momento en que hay acceso a red
es cuando se envía o descarga de un host remoto como \programa{GitHub}
la última instantánea.

Es importante destacar que lo que se envía y recibe no son ficheros, lo cual
implica tiempo de carga y descarga, entre otras cosas, sino cambios mínimos,
y en el caso de \programa{Git} más concretamente, una instantánea de la
base de datos en el momento en que se confirma o remite la información.

Que \programa{Git} funciona muy bien para todos estos propósitos lo prueba 
que sea el software de control de versiones por excelencia de proyectos muy
grandes, donde trabajan a la vez cientos de personas en diferentes partes del
mundo. Tal es el caso del núcleo de \programa{Linux}. De hecho, \programa{Git}
nació para resolver los retos con los que se enfrentaba el trabajo de cientos
de desarrolladores, con una frecuencia brutal de cambios en el tiempo, en el
núcleo de Linux. Necesitaba ser algo muy rápido y muy seguro. Tras esta prueba
de fuego, muchos otros proyectos lo han adoptado. Y gracias a las cuentas
gratuitas de \programa{GitHub} es hoy casi un estándar _de facto_ también
para usuarios normales en lo que a control de versiones se refiere.

## ¿Inconvenientes?
Sí, hay uno, siempre hay uno. Hay que aprender a usarlo. Pero se trata del
mismo inconveniente que hay cuando queremos introducir un nuevo programa
a nuestro arsenal. Hay que aprenderlo. En el caso de un sistema de control
de versiones también hay que aprender a pensar en los términos de estos
sistemas.

## Enlaces
- Página de la wikipedia: <http://es.wikipedia.org/wiki/Git>

- Libro sobre \programa{Git} (en inglés): <https://progit.org/>

Hay versión castellana parcial de la primera edición del libro citado,
que es el mejor que conozco. Se trata de un libro libre muy completo. Yo 
lo estoy leyendo y extrayendo de él la mayor parte de la información para 
los próximos tutoriales. El libro va mucho más allá, desde luego. Y si
alguno es capaz de leerlo con más atención y detenimiento que yo, que es
seguro, sabrá bastante más de \programa{Git} que lo que yo pueda decir aquí.

## Nota
Mi competencia en \programa{Git} es limitada. He empezado a usarlo
recientemente y conozco las cuatro cosas super-básicas y poco más. Os animo
a indicarme los errores u omisiones que pueda cometer, en caso de que
profundicéis por vuestra cuenta.

