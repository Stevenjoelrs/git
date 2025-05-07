# Curso git/Github

## Control de versiones
El control de versiones es un sistema que nos permite tener un historial de los cambios realizados en un proyecto, saber cuándo y quién hizo los cambios

Esto es muy importante ya que nos permiten tener un mejor control, con la posibilidad de revertir errores, tener una colaboracion en equipo mas eficiente y flexible

## Que es Git?
Un sistema de control de versiones que aloja una copia del repo de manera local para luego subirlo a uno remoto para la colaboracion con terceros

## Y... qué es un repositorio?
un repositorio es donde se almacena las diferentes versiones de un proyecto, donde puede verse quienes hicieron los cambios y cuando los hicieron

# Creacion de un proyecto en Git
para iniciar un proyecto de manera correcta primero se debe de tener ya un entorno con las capetas creadas localmente, una vez dentro de la carpeta que almacenara nuestro proyecto se usa:

`git init ¨<nombre-de-proyecto>¨`

nos movemos dentro de la carpeta del proyecyo con `cd <nombre-de-proyecto>`

Asi ya tendriamos creado un proyecto en git, lo siguiente es conocer los estados y comandos de Git para poder trabajar de manera mas eficiente

## Estados de Git

<div align="center">

Estado       |Descripción|
|---------------|:--------------|
| Modified      |Este estado indica que un archivo fue creado, eliminado o contiene cambios a su version original.|
| Staged        |Los cambios realizados en el archivo se marcan para ser confirmados en el repo local.|
| Commited      |Los cambios realizados se guardan en el historial de cambios de ese archivo.|
</div>

## Pero... Cómo realizo ese cambio de estado a los archivos?
Para realizar cambios de estado a tus archivos primero debes de saber en que estado se encuentran actualmente, para esto se usa:

`git status` 

esto dentro de la carpeta donde están los aarchivos que quieres revisar

al realizar esto deberias tener un mensaje similar a este:

```
On branch feat/EfectoMalDeChagas
Your branch is up to date with 'origin/feat/EfectoMalDeChagas'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   src/main/java/com/scesi/vinchucamod/effect/ChagasEffect.java

no changes added to commit (use "git add" and/or "git commit -a")

```
En mi caso yo medifique el contenido del archivo y se cambio el estado a `modified`

## Ahora quiero cambiarlo a Staged, cómo lo hago?
Una vez que ya sepas en que estado esta tu archivo puedes continuar con el comando:

`git add <direccion-del-archivo>`

en el caso de que quieras poner en staged todos los archivos modificados en uno se usa:

`git add .`

Una vez tengas tus archivos en estado Staged podemos continuar con el commit

Para lo que es el commit podemos usar:

`git commit -m ¨<descripcion-de-los-cambios>¨

con esto debes de dejar una descripcion breve sobre los cambios que se hacen en este punto de guardado

## Mmm ya... pero cómo puedo asegurarme que el commit se hizo?
Para eso se usa:

`git log`

deberia de salirte un mensaje similar a este:

```
❯ git log
commit 778f85f3394dbf48280a053fce6b259cd9e90cd5 (HEAD -> feat/EfectoMalDeChagas, origin/feat/EfectoMalDeChagas)
Author: Steven Ramos <stevenjramossalazar@gmail.com>
Date:   Tue May 6 20:54:46 2025 -0400

    hotfix: se arreglo el error que el nombre del efecto no se mostraba correctamente

commit 7fea30e1a697dee0859da07808a8dd8ec415b705
Author: Steven Ramos <stevenjramossalazar@gmail.com>
Date:   Tue May 6 20:19:30 2025 -0400

    hotfix: se elimino un archivo innecesario por el cambio de DamageSource, ademas se cambio que se reciba dano ca
da 2 segundos en vez de cada 0.5s

commit ab18745f2fdc04c3a6629f863e40977cc2d5410b
Author: Steven Ramos <stevenjramossalazar@gmail.com>
Date:   Tue May 6 18:21:01 2025 -0400

    hotfix: se arreglo un error donde el efecto no realizaba danio al jugador aun cumpliendo las condiciones


```
## Vale, a todo esto... mmm... Qué es un commit? xd
Vale, expliqué qué es el estado commited, pero no qué es un commit, un commit es un punto de guardado de tu progreso, como se ve en la informacion del `git log` un commit tiene:

* Su ID (identficador)
* El autor del commit
* La fecha y hora en la que se hizo el commit
* La descripcion de los cambios de ese commit

## Mmm ya... mi idea ahora es realizar un cambio al proyecto pero no quiero afectarlo directamente aún, que deberia de hacer?

Lo que debes de hacer primero es saber qué son las ramas en git, una rama es una version separada de la linea principal de proyecto, al estar separada y ser independiente cualquier cambio que hagas no afecta en al proyecto principal, asi es mas dificil que existan errores molestos

Estas ramas las puedes usar para agregar funcionalidades o arreglar errores, es escencial usar las ramas para esto ya que mantienen un orden en el proyecto

## Ahora... como veo que ramas tengo en este momento?
dentro de la carpeta del proyecto usa:

`git branch` que muestra tus ramas locales

`git branch -a` que muestra todas tus ramas, incluyendo las remotas

deberia de salirte algo similar a esto:

```
❯ git branch -a
* feat/EfectoMalDeChagas
  main
  remotes/origin/HEAD -> origin/main
  remotes/origin/feat/EfectoMalDeChagas
  remotes/origin/feat/item-de-curacion
  remotes/origin/feature/vinchuca-mob
  remotes/origin/main
```
Si notas, al inicio hay un asterisco en la rama `feat/EfectoMalDeChagas`, esto es porque actualmente me encuentro haciendo cambios en esa rama.

Y también se pueden ver las demas ramás creadas por compañeros de grupo xd


## Qué es lo que dice ahí como ¨HEAD¨?
en un commit, el HEAD indica donde te ubicas, en los ejemplos de los commits se puede ver que el HEAD señala a la rama en la que estaba trabajando

```
❯ git log
commit 778f85f3394dbf48280a053fce6b259cd9e90cd5 (HEAD -> feat/EfectoMalDeChagas, origin/feat/EfectoMalDeChagas)
```
## Vale ahora creemos una rama nueva
para eso haremos:

`git branch <nombre-rama>`

y nos movemos a esa rama:

`git switch <nombre-rama>`

> De hecho ésta informacién está hecha desde una rama diferente a la principal

## Vale ahora quiero que mis cambios sean integrados a la rama principal?
Una vez que hayas terminado tus cambios, realiza lo siguiente:

cambia a tu rama principal:
`git switch main`

revisar que tienes la version más actualizada del main:

`git pull origin main`

> Un momento, que es eso de pull?
> En git existen los comandos `pull` y `push`, que como su traduccion lo dice uno jala la informacion, en > > este caso al main, y el `push` empuja la informacion como será en este caso de la rama que se creó a la main

continuemos...

Ahora toca fusionar la rama con el main:

`git merge <nombre-de-tu-rama>`

en mi caso sería:

`git merge feat/EfectoMalDeChagas`

y si quieres subirlo a tu repo remoto haces esto:

`git push origin main`

## Y que pasa si existen conflictos? pregunto por un amigo, no es como que me haya pasado xd

En el caso de que haya un conflicto Git te avisará al momento de la fusion.

primero usa `git status` para ver que archivos tienen los conflictos.

Cuando abras los archivos se verá algo similar a esto:
```
<<<<<<< HEAD
código en la rama main
=======
código en tu rama
>>>>>>> feat/EfectoMalDeChagas

```

Elimina las marcas `<<<<`, `====`, `>>>>>` y dejar el codigo correcto

Luego de eso agrega el archivo de nuevo con `git add` y un commit `git commit`

## Después de hacer eso puedo y/o debería eliminar la rama?
Si, de hecho una buena practica es eliminar las ramas, para eso usa:

`git branch -d <nombre-de-rama>` esto elimina la rama local, la que esta tu computadora

`git push origin --delete <nombre-de-rama>` esto elimina la rama remota

> No eliminaré la rama de la explicación por temas de documentación xd

# Flujos de trabajo
Los flujos de trabajo son maneras de organizar nuestras ramas y archivos durante el trabajo en equipo en un repositorio remoto

Una manera de organizar es darle prefijos a nuestras ramas:

1. Main: Contiene el codigo en produccion, almacena el historial de lanzamientos (no se toca directamente esta rama, solo para hotfix)
2. Develop: Esta rama nace directamente del main y contiene el codigo en pre-produccion,sirve como una rama de integracion para las caracteristicas.
3. Feature: Estas ramas nacen de los develop, aqui se integran funcionalidades.
4. Release: Se crean para preparar/mantener/registrar lanzamientos. Las correciones de errores deben ser aplicadas a esta rama antes de fusionarlas con el main.
5. Hotfix: Puede llegar a generar confusion con la rama Release pero la diferencia clave es que estas se crean directamente del main y corrigen errores puntuales en este, posteriormente se fusionan con el main y develop.

