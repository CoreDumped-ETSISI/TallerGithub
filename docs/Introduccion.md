# Introducción a Git & Github

- [Introducción a Git & Github](#introducción-a-git--github)
- [¿Qué es el Control de Versiones?](#qué-es-el-control-de-versiones)
- [¿Por qué Git?](#por-qué-git)
- [¿Qué es un repositorio?](#qué-es-un-repositorio)
- [Comandos básicos de Git](#comandos-básicos-de-git)
- [El papel de GitHub](#el-papel-de-github)
- [Flujos de trabajo de Git](#flujos-de-trabajo-de-git)
- [Modelos de desarrollo colaborativo](#modelos-de-desarrollo-colaborativo)

## ¿Qué es el Control de Versiones?

Un Sistema de Control de Versiones permite realizar un seguimiento del historial de cambios realizados en un proyecto al mismo tiempo que se trabaja en el mismo.   

A medida que el proyecto evoluciona, los colaboradores puede realizar pruebas, arreglar fallos y contribuir con nuevo código con la confianza de que en cualquier momento se puede recuperar cualquier versión anterior del proyecto. De esta forma los desarrolladores podemos revisar el historial de un proyecto para saber:
- Qué ha cambiado.
- Quién ha hecho esos cambios.
- Cuando se han hecho.
- Por qué eran necesarios esos cambios.


## ¿Por qué Git?

Git es de lejos el Sistema de Control de Versiones más usado en el mundo. Es usado tanto en proyectos de Código Libre (Open Source) como para soluciones empresariales. Algunos de los beneficios más significativos:

- Git permite ver a los desarrolladores el historial completo de cambios, decisiones y evolución de un proyecto en un solo lugar. Obteniendo desde el momento en que acceden a un proyecto todo el contexto necesario para entenderlo y empezar a contribuir en el.

- Trabajar de forma remota y asíncrona no es un problema. Las aportaciones al proyecto pueden suceder en cualquier momento y desde cualquier lugar sin comprometer la integridad del mismo. Usando varias líneas de desarrollo (*branches*) los desarrolladores pueden proponer cambios de forma segura sin comprometer el desarrollo general.


## ¿Qué es un repositorio?

Un *repositorio* o proyecto Git, comprende la colección completa de ficheros asociados con un proyecto, así como todo su historial de cambios. El historial de los ficheros se presenta en forma de "instantáneas" llamadas *commits*, los commits existen como relaciones de cambios entre estados del proyecto y se pueden organizar en múltiples líneas de desarrollo conocidas como *branches* (ramas).

Trabajar mediante repositorios mantiene los proyectos en desarrollo organizados y protegidos. Promoviendo que los desarrolladores realizen los cambios pertinentes para solucionar fallos o desarrollar nuevas características sin miedo a perjudicar a la linea de desarrollo principal.

A través de plataformas como Github, Git da más oportunidades para una colaboración transparente en proyectos públicos o privados.


## Comandos básicos de Git

Para usar Git los desarrolladores utilizan una serie de comandos para copiar, crear, cambiar y combinar código.  
Una vez se tiene git instalado se pueden ejecutar desde la línea de comandos del sistema o desde cualquier herramienta compatible.   
Aquí tenéis algunos de los comandos más usados:

- `git init` Inicializa un nuevo repositorio Git y empieza a hacer seguimiento sobre el directorio en el que se invoca.
Añade una subcarpeta oculta (.git) que alberga toda la información requerida para el control de versiones.
- `git clone` Crea una copia local de un proyecto ya existente en un repositorio romoto. El clone incluye todos los ficheros, historial y ramas del proyecto.
- `git add` Incluye cambios realizados para posteriormente ser guardados en el historial. Git sigue por defecto cualquier cambio que se realize en el repositorio,
sin embargo es necesario que dichos cambios se "preparen" (*stage*) y posteriormente se "guarden" (*commit*) para poder incluirlos en el historial del proyecto.
Este comando efectua el primero de los dos pasos que componen el proceso de "seguimiento de cambios" en un repositorio.
- `git commit` Guarda el estado del repositorio en el historial, completando así el proceso de seguimiento de cambios.
A grandes rasgos, hacer un commit es como hacer una foto. Todo cambio que se haya "preparado" con `git add` formará parte de la foto y pasará al historial del repositorio con `git commit`.
- `git status` Muestra el estado de los cambios como "untracked" (ficheros fuera de seguimiento),
"modified" (modificaciones sobre ficheros en seguimiento) o "staged" (preparados para commit).
- `git branch` Muestra las ramas sincronizadas en local.
- `git merge` Fusiona dos lineas de desarrollo. Se usa especialmente para combinar cambios entre dos ramas.
- `git pull` Actualiza tu repositorio local con los últimos cambios en su versión remota.
Por ejemplo si un compañero ha subido cambios al repositorio remoto y quieres que esos cambios se reflejen en tu local.
- `git push` Actualiza el repositorio remoto con los últimos commits hechos en tu rama local.

Si tenéis curiosidad podéis consultar [guía completa de comandos de Git](https://git-scm.com/docs).


## El papel de GitHub

Github es una plataforma de almacenamiento de repositorios Git, añadiendo sobre el control de versiones un útil set de herramientas para facilitar la gestión del código de forma visual, desarrollar discusiones, *pull requests*, revisar código o integrar una gran variedad de apps en tu flujo de trabajo.


## Flujos de trabajo de Git

Los flujos de trabajo son fórmulas o conjuntos de reglas acerca del uso de Git para llevar acabo tu trabajo de forma uniforme y productiva. Un buen flujo de trabajo es en proyectos colaborativos la principal defensa que tendrán los colaboradores contra el infierno de Control de Versiones.

Existen muchos flujos distintos, y cada equipo se adecúa mejor a uno o a otro, o crea el suyo propio. Algunos de los más usados son:
- Flujo básico o centralizado: Simple y estúpido, hay un repositorio central, cada desarrollador clona ese repositorio, realiza sus cambios y los envía (*push*) de vuelta para que otros colaboradores hagan *pull* y trabajen sobre ellos.
- [Github Flow](https://guides.github.com/introduction/flow/): El por defecto de GitHub, ligero y basado en ramas.
- [Gitflow](https://jeffkreeftmeijer.com/git-flow/): Estricto pero eficaz flujo de trabajo basado en ramas temáticas y convenciones de nomenclatura.
- [For & Pull](https://gist.github.com/Chaser324/ce0505fbed06b947d962): Basado en copias (*forks*) y *pull requests*, muy útil para proyectos Open Source o de libre colaboración.


## Modelos de desarrollo colaborativo

Hay principalmente 2 formas de colaborar en GitHub:
1. Repositorios compartidos.
2. Fork & pull.

Con un **repositorio compartido**, se designa explicitamente a un conjunto de desarrolladores como colaboradores, ya sea con acceso de lectura, escritura o administración.

Para un proyecto de código libre (Open Source), o para para proyectos en los que cualquiera puede participar manejar permisos individuales puede ser demasiado, de esa forma el modelo de **Fork & Pull** permite colaborar facilmente a cualquiera que pueda ver el repositorio. Un *fork* es una copia de un repositorio ajeno bajo tu cuenta personal. Cada desarrollador tiene control total sobre el flujo de trabajo en su copia. Esta copia puede evolucionar de forma completamente separada a su repositorio original o puede fusionarse de nuevo con una *pull request*, de esta forma los mantenedores originales pueden revisar los cambios sugeridos antes de incluirlos en el proyecto.