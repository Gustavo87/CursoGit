# Comandos GIT para trabajar con el Repositorio Local
* Crear el Staging y Repositorio Local. 
```bash
git init
```
* Movemos los cambios en un archivo al Staging para trackearlo.
```
git add archivo
```
* Enviamos lo que esta en staging a nuestro repositorio
```
git commit
```
# Comandos GIT para trabajar con el Repositorio Remoto
* En lugar de git init
* Para clonar un repositorio publico a traves de https, no se piden ni usuario ni clave.
```
git clone url
```
* Seguimos usando `git add` para mover a staging
* Seguimos usando `git commit` para mover de staging al repositorio local
* Cuando queremos mandar los cambios al directorio remoto.
```
git push
```
* Si el que hace `push` es un usuario diferente al que creo el repositorio, este usuario deberia ser agregado como colaborador en las settings del repositorio al que quiere hacer `push`, sin embargo una vez que es agregado debe aceptar la notificacion de GitHub que le llegara por correo. En la imagen siguiente, agregare al usuario `GusBaca` como colaborador del repositorio `CursoGit`
![](https://raw.githubusercontent.com/Gustavo87/CursoGit/master/AddCollaboratorToRepo.png)

* Si queremos traer una actualizacion tras haber clonado, el push de otra persona
```
git fetch 
```
* `git fetch`. Trae la actualizacion a mi repositorio local, pero no lo copia a mi directorio de trabajo. Para esto ultimo debemos hacer
```
git merge
```
* Hay un comando que hace estas dos cosas.
```
git pull
```
* Agregar un origen remoto
```
git remote add origin https://github.com/Gustavo87/CursoGit.git
```
* Verificamos que tenemos un origin
```
git remote
```
* Que nos muestre los origin para fetch y push
```
git remote -v
```

* Enviar la rama master del repo local a GitHub
```
git push origin master
```

* Traer del origin a la rama master
```
git pull origin master
```

# Otros comandos importantes 

* Ver las settings del usuario, por ejemplo, username y correo.
```
git config -l
```

* Hace add y commit al mismo tiempo, solo funciona si le hemos echo add al archivo anteriormente, es decir, no hay creación de archivos nuevos.
```
git commit -am
```
* Vemos los archivos afectados.
```
git log --stat
```
* Muestra el ultimo cambio
```
git show
```
* Ver lo que ha cambiado
```
git diff
```
* Para ver el log de commit de una forma más amigable
```
git log --all --graph --decorate --oneline
```
* Crear un alias del comando anterior
```
 alias arbolito="git log --all --graph --decorate --oneline"
```
* Ver el status, o sea, si tenemos algo pendiente de agregar al Staging `git add` o al repository local `git commit`.
```
git status
```
# Comandos para trabajar con las ramas 
* Crear una rama
* Lo normal es crear una rama siempre desde la rama que tenga los cambios mas recientes, esta es, por lo general, la rama master.
```
git branch nombre_rama
```
* Moverme a otra rama
```
git checkout nombre_rama
```
* Ver las ramas
```
git branch
```
* Unir ramas
* Primeramente, nos movemos a la rama master.
```
git checkout master
```
* Luego, hacemos el merge.
```
git merge nombre_rama
```
* Nos muestra cuales son las ramas que existen y cual ha sido su historia
```
git show-branch
```
```
git show-branch --all
```
* Nos muestra cuales han sido la historia de las ramas, en una interfaz de ventanas (GUI)
```
gitk
```
* Subir una rama a GitHub
* Primeramente, nos movemos a la rama.
```
git checkout nombre_rama
```
* Subimos la rama
```
git push origin nombre_rama
```
* Un posible flujo de trabajo podria ser el siguiente: Supongamos que tengo una rama principal `master` esta representa, segun las mejoras practicas los cambios en `produccion`, sin embargo he creado una rama `header` para que otro dev trabaje esa rama para, posteriormente, fusionarla con la rama `master`.
* En primer lugar el dev, debera traer la rama a su repositorio local: `git pull origin header`
* En este punto hara sus cambios: `commit`, `add`
* Luego debera subir sus cambios a GitHub: `git push origin header`
* Luego de esto, se deberan fusionar los cambios del branch `header` con el branch `master`
* Por tanto, nos movemos al branch `master`: `git checkout master`
* Unimos los cambios de `header` a `master`: `git merge header`
* Subimos los cambios en `master`, pero antes tenemos que hacer  `git pull origin master` por si algo paso en el server de GitHub: `git push origin master`

# Generar llaves publicas/privadas para la conexion ssh al servidor de Github
```
ssh-keygen -t rsa -b 4096 -C un_correo
```
* Crear una llave publica/privada por cada repositorio en GitHub.
* Siempre crea un llave publica/privada por cada computadora

* Verificar que el servidor de llaves que se encarga de hacer la conexion, esta corriendo
```
eval $(ssh-agent -s)
```
* Agregar la llave privada al servidor de llaves del Sistema Operativo.
```
ssh-add ruta_llave_privada
```
* Copiamos la llave publica a GitHub
* Cambiamos la url del repo para usar `ssh` en lugar de `https`
* Para ver la url actual
```
git remote -v
```
* Para cambiar la url
```
git remote set-url origin git@github.com:Gustavo87/CursoGit.git
```
* Hacer cambios con la nueva url
* Primeramente, nos traemos todo del repo de GitHub
```
git pull origin master
```
* Luego, podemos subir los cambios que tenemos en el repositorio local al repositorio remoto.
```
git push origin master
```
# Comandos para gestionar `tag`
* Los `tag` se usan para identificar las versiones de nuestro proyecto.
* Definimos un versión a traves del comando `tag` para un commit en concreto.
```
$ git tag -a v0.1 -m "Resultado de las primeras clases del curso" 12629e9
```
* Ver los `tag` que tenemos creados
```
git tag
```
* Ver el hash que se creo para identificar un `tag` en concreto.
```
git show-ref --tags
```
* Luego de crear el `tag`, igual que los `commit`, tenemos que enviarlos al servidor de GitHub.
```
git push origin --tags
```
* Borrar un tag de nuestro repositorio local.
* Primerante, usamos el comando
```
git tag -d nombre_tag
```
* Luego, mandamos los cambios con git `push origin --tags`
* Borrarlo tambien de GitHub
```
git push origin :refs/tags/nombre_tag
```

# Buenas Practicas/ Notas Generales
* Los archivos binarios, por ejemplo, imagenes no deberian ser agregados al repositorio.
* En la rama `master` solo debe estar aquello que esta listo para ir a `produccion`.
* Normalmente se bloquea el acceso a la rama master, de modo que no cualquiera pueda hacer `merge` sin antes pasar por un `code review`
* `Servidores de Desarrollo` o `Servidores de Stating` son normalmente los nombres para describir nuestros ambientes de pruebas.
* `Pull request` que es una caracteristica exclusiva de `GitHub`, es un estado intermedio antes de hacer un `merge`. En `GitLab` se conoce como `merge request`. En `Bitbucket` se conoce como `push request`. Esta tarea es del `Dev Ops` la persona que es el administrador del entorno de desarrollo.
* Utilizar `Jenkis` como buena práctica de integración continua al momento de hacer `deploy`
* Tener un archivo `.gitignore` and `readme.md`

# Flujos de trabajo/ Escenarios
## Pull Request
* Imaginemos que tenemos 2 bugs, por tanto vamos a crear una rama aparte tomando como base la rama principal, luego vamos a fusionar dicha rama con la rama principal. 
* `git pull origin master`
* `git branch fix-bug`
* `git checkout fix-bug`
* Reparamos el bug.
* `git status`
* `git diff`
* `git add .` 
* `git commit -m`
* `git push origin fix-bug`
* Desde GitHub vamos a crear un `new pull request`. En este punto definimos que vamos a comparar la `master` contra `fix-bug`.  Al hacer un `pull request` nos permite ver los cambios, agregar detalles, por defecto, se toma el comentario del `commit` como el nombre del `pull request`, agregar un comentario, agregar `reviewers` que son personas que van a revisar el `pull request`, agregar `labels` al `pull request` y muchas otras cosas utiles para el proceso de `dev ops`. 
* El `pull request` no ejecuta el `merge` simplemente describe lo que esta pasando, luego alguien puede revisarlo y ejectuarlo. 
* Ahora vamos a ver desde la perspectiva de un `reviewers`. El `reviewers` ve la notificacion de que tiene un `pull request`, dentro del `pull request` podemos ver detalles como por ejemplo que la rama `fix-bug` no tiene conflictos con `master`, por tanto se puede fusionar, o sea; darle al boton `Merge pull request`; ver los `commits` asociados a este `pull request`; ver los archivos cambiados y lo que se cambio. Supongamos que el `reviewer` no va a aceptar el `pull request`, entonces le damos al boton `review changes`, escribimos un comentario y el damos al boton `Request changes`.
* Tras el envio de un `request changes` por parte del `reviewer` al `pull request` volvemos a la vista de la persona que creo el `pull request`. Esta persona mira que el `pull request` no se ha aprovado, por tanto, hace el cambio definido en el `request changes`. 
* `git pull origin fix-bug`
* Hacemos el cambio.
* `git commit -m`
* `git push origin master`
* Volvemos a `GitHub` y en el `pull request` le damos a la opcion de `conversacion` para agregar un comentario notificandole al `reviewer` que lo sugerido en el `request changes` esta aplicado.
* Volvemos al punto de vista del `reviewer`. En el `pull request` en `review changes` escribimos un comentario para notificar que por ejemplo ahora si todo esta ok y finalmente, escogemos la opcion `Approve` y le damos al boton de `Submit review`. Esto significa que hemos aprovado los cambios, pero eso no significa que el `merge` se ha ejecutado, significa solamente que yo, como `reviewer` estoy aprovando los cambios. Alguien tiene que tomar la decision de hacer el `merge`, ese alguien es un `colaborador` del repositorio en cuestion.  Todo lo descrito antes es lo que se llama `code review`. Para hacer `pull request` alguien debe darle al boton `Merge pull request`. Ponemos un comentario, confirmamos en el boton `Confirm merge`. Tras hecho el `merge` nos sale la opcion de borrar el branch en este caso `fix-bug` (la decision de borrar o no depende del equipo de trabajo). 
* Tras el `merge` en mi repositorio local deberia hacer:  `git pull origin master`, luego `git log`
* En resumen, el `pull request` es como un `stating` del lado del servidor.
## Fork
* Vamos a entender como funciona un proyecto Open Source, donde tenes al dueño de proyecto y personas que les gusta el proyecto y que quiere aportar al mismo. Este tipo de personas pueden hacer `clone` del proyecto, pero no hacer `push` de ningun tipo. Desde la perspectiva de esa persona que le gusta el proyecto y quiere aportar sin ser un colaborador, podemos darle al boton `watch` y de esta manera me llegaran notificaciones en el momento que salgan cosas. Otra cosa que podemos hacer es hacer un `fork` que es tomar una copia del estado actual de un proyecto/repositorio publico de GitHub y clonarlo, esto es una caracteristica unica de GitHub, no esta presente en Git. Tras hacer `fork` de algun proyecto, lo siguiente seria hacerle cambios, por tanto, vamos a traerlo a nuestro pc a traves de `git clone`. En este punto podemos hacer cambios y su respectivo `commit` y `push`, luego vendría el como hacer el `pull request` entre proyectos/repositorios diferentes? Puesto que GitHub sabe que el proyecto es un `fork` nos facilita la parte del `pull request` al repositorio original. Por tanto, pinchamos el boton `new pull request`, presenta luego, una interfaz para comparar los `branch`, ver los archivos modificados. Luego pinchamos el boton `Create pull request` tras dejar un comentario. Desde la perspectiva del propietario del repositorio original, podemos ver los cambios, en el botón `Review changes`, dejar un comentario, `Approve` (checkbox) y subir el comentario picando en el botón `submit review`. Luego damos al boton `Merge pull request`, confirmamos picando en `Confirm merge`. Listo hemos contribuido al proyecto original! 
Es interesante que una vez que alguien hace cambios en el proyecto original, tendre un notificacion en mi proyecto que es un `fork` que me dice que estoy 3, por ejemplo, del proyecto original, luego puedo comparar estos `commit` para ver que son, debo hacer, `switching the base`, porque por defecto la comparación es del `fork` al original, pero voy a comparar del original al `fork`. En este punto puede picar el boton `Create pull request` para luego hacer `merge`. Sin embargo lo podemos hacer desde consola. En este punto lo interesante es que vamos a crear una fuente distinta para hacer `pull`. Escribamos el comando `git remote -v` para ver ambas fuentes `pull` and `push`. Entonces voy a cambiar la fuente de `pull` para que venga del proyecto original con el comando: `git remote add upstream url_proyecto_original`. Luego con `git remote -v`, veremos que hay una nueva fuente de datos. Ahora si ya podemos actualizar con el comando: `git pull upstream master` para traer los cambios a nuestra base de datos local. Finalmente hacer `push` para mandar el `pull` que bajamos a nuestro repositorio `fork` con el comando: `git push origin master`.

## Deployment a un servidor
* En primera instancia, copiamos la url de https de GitHub. En nuestro server al que haremos `deployment` debemos tener instalado `git`. Luego `git clone url_GitHub_repo` en el directorio de nuestro server http. Listo el `deployment`!
* Es buena practica proteger el archivo `.git` puesto que esto representa la base de datos de `git`. Hay una herramienta `Travis CI` que conecta tus `branch` de GitHub con tu servidor, de modo que cuando haces `push` a la rama `master` o a la rama que ira a produccion, `Travis CI`, detecta el cambio y lo mandara al server, sin embargo `Travis CI` es de paga, salvo para proyectos Open Source. Otra alternativa es `Jenkis`.

# Archivo .gitignore
* Creamos un nuevo archivo que vamos a guardar en la raiz de nuestro proyecto, el archivo se debe llamar  `.gitignore`, aca listamos los archivos que no van a estar versionados (ejemplo archivos binarios), para el caso de las imagenes, introducimos la siguiente linea en ese archivo `.gitignore`: 
 `*.jpg` 
* Igualmente el archivo `.gitignore` debe ser agregado a traves de `git add .`
* Las imagenes en un proyecto web deberian ir en un `content delivery network`. Podríamos subir las imagenes a `imgur.com` y referenciarlas en nuestro proyecto.

# Readme.md
* En un archivo `readme.md` puedes agregar html o `markdown`.
* Un editor para `markdown` https://pandao.github.io/editor.md/en.html

# Hosting gratis en GitHub: GitHub Pages
* Nos vamos a https://pages.github.com/

# Mas alla de estas notas.
* Que son los releases en GitHub.

# Recursos utiles/urls
* https://learngitbranching.js.org/
* https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
* https://github.com/settings/repositories
* https://pandao.github.io/editor.md/en.html
* https://imgur.com/
* https://pages.github.com/

