# Apéndice: Comandos esenciales de \programa{Git} u buenas prácticas

## Sumario de comandos tratados
A continuación refiero los comandos vistos ordenados por su función. Destaco
aquellos que me parecen imprescindibles.

### Comandos de configuración
- **`git config --global user.name <usuario>`**: Establece el nombre de usuario para
  todos los repositorios de los que éste sea propietario.

- **`git config --global user.email <correo>`**: Establece el correo electronico
  de usuario para todos los repositorios de los que éste sea propietario.

- `git config --global core.editor <editor>`: Establece el editor por defecto
  que mostrará \programa{Git} en todos los repositorios de los que el usuario sea
  propietario.

- `git config user.name "<usuario>"`: Establece el nombre de usuario para el
  repositorio actual.

- `git config user.email <correo_usuario>`: Establece el correo electrónico de
  usuario para el repositorio actual.

- `git config core.editor <editor>`: Establece el editor por defecto que mostrará
  \programa{Git} para el repositorio actual.

### Comando de inicialización
- **`git init`**: Inicializa \programa{Git} para que supervise el directorio actual.

### Comandos para obtención de información interna
- **`git status`**: Muestra el estado de los ficheros que hay en nuestro espacio
  de trabajo.

- **`git log`**: Muestra el historial de confirmaciones en orden cronológico
  descendente.

- `git log --oneline`: Muestra el historial de confirmaciones en orden 
  cronológico descendente y en formato breve.

- **`git log --patch`**: Muestra el historial de confirmaciones en orden cronológico
  descendente, incluidas diferencias entre versiones de los ficheros implicados.

### Comandos básicos 
- **`git add <fichero>`**: Añade `fichero` al área de preparación. 

- **`git commit -m "<mensaje>"`**: Confirma lo que haya en el área de preparación
  para que se registre en la base de datos del repositorio. `mensaje` quedará
  asociado como descripción de dicha operación.

- `git --amend`: Muestra un editor para modificar la confirmación inmediatamente
  anterior. Normalmente, para modificar su mensaje descriptivo asociado.

- `git commit -a -m "<mensaje>" <fichero>`: Añade `fichero` al área de preparación
   y lo confirma, ambas operaciones en un único paso. 

- `git rm --force <fichero>`: Elimina `fichero` de nuestro espacio de trabajo
  y del área de preparación.

- `git mv <fichero> <fichero_nuevo>`: Cambia el nombre `fichero` por 
  `fichero_nuevo`.

- `git mv <fichero> <directorio>`: Mueve `fichero` a `directorio`.

- `git checkout -- <id_commit> <fichero>`: Revierte `fichero` a la forma
  que tenía en la confirmación con identificador `id_commit`.

### Comandos de interacción con repositorios remotos
- **`git clone <repo_url>`**: Clona el repositorio remoto alojado en `repo_url`.

- `git push origin master`: Actualiza la rama `master` del repositorio remoto
  (`origin`) con la instantánea actual de nuestra rama `master`.

- **`git push -u origin master`**: Actualiza la rama `master` del repositorio
  remoto con la instantánea actual de nuestra rama `master`, y guarda datos 
  de configuración que evitan incluir los términos `master` `origin` en 
  futuros `git push`.

- **`git push`**: _Idem_. Asume que el anterior comando (con la opción `-u`) fue
  ejecutado en un `push` previo.

- **`git pull`**: Actualiza el repositorio local a la última instantánea del 
  repositorio remoto.

## Buenas prácticas de trabajo en grupo con \programa{Git}
- Antes de efectuar ningún `commit` hacer un `git pull`.

- No hacer `git commit` hasta que se esté convencido de la versión en que vamos
  a dejar el fichero. El fichero puede permanecer en nuestra área de preparación
  por el tiempo que queramos. Hasta que no se confirma, la base de datos del
  repositorio no cambia.

- Elegir un mensaje breve y claro para cada confirmación.

- Hacer `git push` después de terminar la sesión, en caso de haberse realizado
  algún `git commit` en ella.

- No temer que el número de versiones de un mismo fichero se multiplique. Si
  hay razón para un cambio, hágase. Si luego, nos arrepentimos, podemos volver
  a cambiar el fichero sin problemas.

- No ejecutar operaciones de borrado de ficheros, ni operaciones que cambien
  el nombre del fichero o su ubicación, salvo cuando sea estrictamente necesario,
  o bien cuando la parte activa del grupo acuerde hacerlo.

- No revertir un fichero a una versión previa salvo por ser de absoluta necesidad
  y tratar de hacerlo previa consulta a los miembros con mayor responsabilidad
  en el grupo.
