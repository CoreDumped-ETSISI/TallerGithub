# Guía práctica

Aquí encontrarás una guía paso a paso de las prácticas que realizamos durante el taller.

## Pre-requisitos

- Tener una cuenta de GitHub.
- Tener instalado Git en tu sistema.

Puedes consultar la página de [Setup](docs/Setup.md) si tienes dudas.

## Contenidos

- [Inicio](#inicio)
  - [Inicializar un repositorio desde Github](#inicializar-un-repositorio-desde-github)
  - [Inicializar un repositorio desde local](#inicializar-un-repositorio-desde-local)
- [Git Workflow](#git-workflow)
  - [Git basics](#git-basics)
  - [Gitignore](#gitignore)
  - [Merge conflicts](#merge-conflicts)
  - [Branches](#branches)
  - [Remote branches](#remote-branches)
  - [Pull requests](#pull-requests)
  - [Git ammend](#git-ammend)
  - [Git revert](#git-revert)
  - [Git squash](#git-squash)
- [Github](#github)
  - [Github Forks](#github-forks)
  - [Readme.md & Markdown](#readmemd--markdown)
  - [Github issues](#github-issues)
  - [Github projects](#github-projects)
  - [Github pages](#github-pages)

# Inicio

Empecemos por crear nuestro propio repositorio.

### Inicializar un repositorio desde Github

1. Desde la interfaz de github busca el botón para crear un nuevo repositorio, está presente en múltiples localizaciones, por ejemplo una vez iniciado sesión desde la [página principal](https://github.com/):  
   ![New repository 1](/docs/images/new_repository_1.png) | ![New repository 1](/docs/images/new_repository_2.png)

2. Bautizamos nuestro nuevo repositorio con un nombre corto y fácil de recordar y escogemos el tipo de repositorio (público | privado).
   ![New repository 3](/docs/images/new_repository_3.png)

3. A la hora de crear nuestro repositorio desde Github podemos elegir algunos archivos iniciales por defecto, entraremos en detalle sobre esos archivos más adelante. Si no se añaden ahora siempre se pueden añadir despues no te preocupes.  
   ![New repository 4](/docs/images/new_repository_4.png)

4. Una vez completado el proceso GitHub nos redigirá a la vista principal del repositorio, desde ahí podemos descargarnos nuestro repositorio de muchas formas. Normalmente usaremos `git clone [url]`.  
   ![New repository 5](/docs/images/new_repository_5.png)

5. Para obtener la copia local de nuestro repositorio desde la consola de comandos utilizaremos el comando `git clone [url]` remplazando la url por la que hemos obtenido en la interfaz de github.

Ya tenemos nuestro repositorio en local y podemos empezar a trabajar!

### Inicializar un repositorio desde local

Los repositorios también se pueden inicializar desde tu equipo local. Esta es la forma más adecuada si ya tienes un proyecto en local que quieres subir a GitHub.  
En este caso vamos a hacerlo mediante linea de comandos pero también hay herramientas visuales que ya mencionaremos.

1. Abre tu consola de comandos desde un fichero ya existente donde quieras almacenar tu proyecto, puede no estár vacío.

2. Ejecuta el comando de inicialización de repositorios de git: `git init`. Desde este momento Git interepretará este directorio como la raíz de tu repositorio y comenzará a hacer seguimiento de todo su contenido. (Puedes ver que se ha creado una carpeta oculta .git).

3. Realizamos el primer commit:  
   Suponiendo que tu repositorio esté vacío el siguiente paso sería crear un commit inicial, una buena forma de empezar un repositorio es añadiendo un fichero README.md:

   ```shell
    echo "# <REPOSITORY NAME>" >> README.md
    git add README.md
    git commit -m "Initial commit"
   ```

   (Remplaza el contenido del `echo` por el nombre de tu repositorio)

   Si tu directorio no está vacío puedes añadir todos los archivos existentes al commit:

   ```shell
   git add --all
   git commit -m "Initial commit"
   ```

4. Nos vamos a la interfaz de Github y [creamos un repositorio remoto](#inicializar-un-repositorio-desde-github) si no lo hemos creado ya. **!Ojo**, esta vez queremos que el repositorio esté vacío, así que no marcamos ninguno de los archivos por defecto.

5. Enlazamos nuestro repositorio local con el remoto y subimos el primer commit (remplaza la url de abajo por la de tu repositorio):

   ```shell
   git remote add origin [url]
   git push -u origin main
   ```

## Git Workflow

Ahora que ya tenemos lo básico para empezar a trabajar en un flujo de control de versiones vamos a profundizar un poco más en los comandos que acabamos de ver y cómo los vamos a usar en nuestro proyectos de desarrollo.

No viene mal tener un poco de ayuda en caso de perdernos, esta [hoja de comandos](https://education.github.com/git-cheat-sheet-education.pdf) puede ayudar.

### Git basics

El flujo de trabajo habitual de Git es muy sencillo, desde nuestro repositorio local y la consola de comandos:

1. `git fetch` Para sincronizar el repositorio remoto.
2. `git pull` Para sincronizar y fusionar los cambios desde el romoto a nuestro local. (Para hacer un pull no hace falta hacer fetch previamente).
3. Hacemos nuestros cambios en local.
4. `git add [file]` o `git add --all` Para añadir los cambios realizados en local al _stage_ para incluirlos en el commit.
5. `git commit -m "Breve descripción de los cambios"` Para "capturar" los cambios realizados. Solo se incluiran en el commit los cambios que previamente hayamos incluido en _stage_.
6. `git push origin main` Para subir los últimos commits al repositorio remoto.

Extra:

- Con `git status` podemos consultar el estado del repositorio, que nos mostrará un breve resumen de nuestro estado con respecto del repositorio local (commits por delante o por detrás), y listará los cambios realizados desde el último commit según el estado de esos cambios (_staged_, _unstaged_ y _untracked_).
- Con `git reset [file]` podemos sacar un fichero del _stage_ que hayamos añadido previamente.
- Si sobre un fichero _unstaged_ ejecutamos `git checkout -- [file]` podemos descartar todos los cambios que hayamos hecho al fichero y devolverlo a su último estado registrado en un commit.
- Con `git log` podemos consultar los commits que hayamos realizado.

Para más comandos útiles podéis consultar la [guía de referencia de Git](https://git-scm.com/docs) o usar `git help`.

O instamos a probar a hacer vuestros primeros commits de prueba durante el taller, si no sabéis que ficheros incluir podéis usar los que hemos dejado en la carpeta [src](/src/).

### Gitignore

Qué pasa cuando tenemos ficheros en local de los que no queremos que se haga seguimiento (tokens, configuraciones, ficheros temporales, pruebas). Para eso existe el **.gitignore**. Si habéis seguido la [inicialización del repositorio desde github](#inicializar-un-repositorio-desde-github) os resultará familiar este fichero.

Este fichero lo podemos añadir y modificar en cualquier momento del proyecto y nos permitirá incluir una serie de reglas para que Git ignore determinados archivos de nuestra elección. Es tan sencillo como añadir un fichero .gitignore a la raiz del repositorio (el mismo directorio donde tenemos nuestro .git).

Existen multitud de [plantillas preparadas](https://github.com/github/gitignore) pero un ejemplo básico del contenido de un .gitignore podría ser el siguiente:

```bash
*.temp
private/
```

\*Se mantendrían fuera de seguimiento todos los ficheros con el sufijo .temp así como el subdirectorio private y todo su contenido.

### Merge conflicts

El flujo de trabajo básico de git es simple pero no es a prueba de conflictos.

Un merge conflict ocurre cuando se ha alterado el mismo fichero desde dos lineas de desarrollo paralelas y diferentes, al intentar funsionar las mismas git necesitará que especifiques que versión del fichero es la correcta.

Cómo puede ocurrir esto? Por ejemplo si trabajas en el mismo repositorio desde dos o más ordenadores diferentes o bien colaboras en el mismo repositorio y misma rama con otras personas.

- Equipo local A sincroniza el repositorio remoto y comienza a realizar cambios en un fichero.
- Equipo local B sincroniza el repositorio remoto y comienza a realizar cambios sobre el mismo fichero.
- Equipo local A registra sus cambios en un commit y lo sube al repositorio remoto.
- Equipo local B registra sus cambios en un commit sin previamente sincronizar con el repositorio remoto e intenta subirlos al remoto.

En este caso la propia consola de comandos le indicará al equipo local B que no se pueden subir los cambios ya que existe un conflicto con la versión en remoto en x ficheros. Las lineas de desarrollo han divergido y ni nos hemos dado cuenta!

Por suerte un conflicto no es el fin del mundo, Git automaticamente añadirá unas anotaciones a los ficheros en conflictos señalando ambas versiones de las lineas conflictivas de la forma:

```shell
<<<<<< HEAD
lineas de la versión de A
=======
lineas de la versión de B
>>>>>> commit
```

Solucionarlo es tan sencillo como escoger entre las lineas que han variado, o bien fusionarlas y eliminar las anotaciones.

Tras resolver nuestros conflictos registraremos los cambios con el flujo habitual `git add` > `git commit`, y en este caso automaticamente se creará un merge commit para indicar que se han fusionado dos lineas de desarrollo. Una vez hecho esto el equipo local A podrá subir sus cambios a remoto con `git push`.

Para trabajar sobre la misma rama y evitar los merge conflicts es muy útil interiorizar el flujo de trabajo de git como las sagradas escrituras que son:

```shell
git pull (que hace a la vez fetch & pull)
git add
git commit
git push
```

### Branches

En el anterior apartado hemos visto como cuando colaboramos en un mismo repositorio es fácil cometer un despiste y provocar un conflicto. Tanto para evitar que tu código se llene de vergonzosos merge conflicts como para organizar mejor el desarollo en proyectos grandes en Git se trabaja con ramas.

Las ramas son declaraciones explicitas de las líneas de desarrollo que mencionamos antes. En un repositorio por defecto existe una única rama (normalmente llamada _main_), es como su nombre indica la rama maesta y en buenas prácticas debería reflejar una versión "estable" del proyecto.

No siempre que hacemos commits estamos registrando versiones definitivas del código, puede que queramos registrar puntos intermedios que permitan colaborar a varias personas en la misma característica o bien que nos permita tener una versión previa a la que volver si la liamos en una racha de furia programadora.

En una gran cantidad de proyectos colaborativos podemos encontrar dos ramas principales: _main_ y _develop_. Pero podemos crear las ramas que consideremos siempre que empecemos a desarrollar una nueva característica, corregir un fallo o por cualquier otro motivo. Es tan sencillo como, desde la rama original de la que queremos partir:

```shell
git checkout -b nueva-rama
```

Este comando creará una rama nueva en local a la vez que moverá nuestro punto de seguimiento a esa rama, a partir de ahora cualquier nuevo commit se registrará única y exclusivamente en esta rama hasta que decidamos fusionarla.

- `git branch` listará todas las ramas sincronizadas en local.
- `git checkout [rama]` nos permitirá cambiar en cualquier momento entre nuestras ramas de desarrollo.

Una vez hayamos hecho los cambios partinentes en nuestra nueva rama de desarollo podemos fusionarlos a la rama original, para ello volveremos a la rama de la que hayamos partido, por ejemplo _main_ y efectuaremos un merge:

```shell
git checkout main
git pull
git merge [rama]
```

Si no hay conflictos automaticamente se generará un merge commit para todos los cambios hechos en la rama y estos pasarán a estar disponibles en _main_. No nos olvidemos luego de subir dichos cambios al remoto con `git push`.

- `git branch -d [rama]` nos permite borrar una rama cuando ya no la necesitemos.

### Remote branches

Las ramas no solo existen en local, podemos crear versiones remotas que nos permitirán organizar mejor nuestros cambios y/o colaborar varias personas en la misma rama.

Para ello una vez hayamos creado nuestra rama en local es tan simple como seguir un procedimiento muy similar al que hicimos al crear el proyecto desde local:

```shell
git checkout [nueva-rama-commits]
git push -u origin [nueva-rama-commits]
```

Si la rama no la hemos creado nosotros y está disponible en remoto podemos crear una copia en local con:

```shell
git fetch
git checkout -b [nueva-rama-remota] origin/[nueva-rama-remota]
```

- `git push origin --delete [rama-remota]` nos permite borrar una rama remota desde local cuando ya no la necesitemos, !cuidado con borrarle ramas a otros sin preguntar!.

### Pull requests

Fusionar ramas a pelo no es una práctica poco habitual, pero en proyectos más complejos nos puede interesar poder revisar todo el trabajo hecho en una rama de forma más visual, así como discutir sobre los cambios en equipo antes de fusionarlos a la rama original.

Con este y otros propósitos surgen las Pull Request, una funcionalidad de GitHub que es habitual encontrar en proyectos colaborativos. Una Pull Request es algo así como un merge supervisado.

Para crear una pull request necesitaremos contar con 2 ramas subidas a github con alguna diferencia en su historial.

- Podemos crearla directamente desde la vista principal del proyecto:  
  ![Pull request 1](/docs/images/pull_request_1.png)
- O desde la pestaña dedicada:  
  ![Pull request 2](/docs/images/pull_request_2.png)

Ambos métodos nos llevarán a la vista de creación de Pull Request, donde podemos añadir un título y descripción al PR, así como asignar a miembros del equipo para que revisen o trabajen en el, añadir labels, etc..

Una vez creada la Pull Request podemos empezar a apreciar las ventajas de esta funcionalidad:

- Un feed de seguimiento de los comentarios, revisiones, discusiones y demás operaciones que se hagan sobre el PR.
- Un registro general de todos los cambios fichero por fichero.
- Una ventana para visualizar posibles comprobaciones preconfiguradas con Github Actions: tests, builds, etc.

Una vez una PR esté lista para ser fusionada se lanza un merge desde la interfaz con un click y GitHub se encarga del resto.

### Git ammend

[WIP]

### Git revert

[WIP]

### Git squash

[WIP]

## Github

### Github Forks

Mediante un fork puedes obtener una copia de cualquier repositorio público asociado a tu cuenta. ![Fork a proyecto](/docs/images/fork.png)

Después podrás seleccionar la cuenta/organizacion o grupo al que quieres asociar el fork ya podrás acceder a esa copia del repositorio ![Selección de cuenta](/docs/images/fork2.png)

Tras hacer modificaciones en el fork, puedes pedir que se vuelva a fusionar con el proyecto original y si el propietario da su consentimiento, tus cambios serán registrados en su repositorio.

### Readme.md & Markdown

Los archivos Readme.md son archivos escritos en Markdown que se suelen usar para documentar los proyectos y hacer guías sobre su utilización/instalación. Markdown es un lenguaje de marcado que permite escribir texto plano, tags de html y añadir gráficos de un gran número de formatos. Puedes entrar en [esta pagina](https://guides.github.com/features/maining-markdown/) para aprender más sobre markdown.

### Github issues

Puedes usar las issues de un repositorio para definir las tareas a realizar en el proyecto. Encontrarás la pestaña de issues desde la vista general del repositorio

![Acceso a issues](/docs/images/issues.png)

Para crear una nueva issue haz click en el botón verde de "New issue"

![Crear issues](/docs/images/crear-issue.png)

En la siguiente vista podrás dar un título a la tarea, escribir una descripción, asignarle la tarea a miembros o colaboradores del proyecto y añadir tags predeterminados o personalizados ![Generación de issues](/docs/images/submit-issue.png)

### Github projects

Los projects de GitHub son tableros creados para manejar facilmente el progreso de issues. Puedes acceder a ellos en la siguiente pantalla

![Acceso projects](/docs/images/projects.png)

Para crear un nuevo tablero haz click en "Create a project"

![Botón Creación de project](/docs/images/create-project.png)

En la siguiente vista podrás darle un nombre al tablero así como una descripción y selccionar una plantilla para el proyecto. Por ejemplo si quieres un tablero con los clásicos "To Do", "In Progress" y "Done" puedes seleccionar "Basic KANBAN"

![Creación de project board](/docs/images/generate-project.png)

Ahora que ya tienes tu tablero puedes mover las issues creadas que aparecen a la derecha a tu tablero y moverlas según vayas haciendo progreso en ellas

![Generación de issues](/docs/images/edit-project.png)

### Github pages

[WIP]