# Recursos utiles/urls
* https://learngitbranching.js.org/
* https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
* https://github.com/settings/repositories



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
* Si el que hace `push` es un usuario diferente al que creo el repositorio, este usuario deberia ser agregado como 
* colaborador en las settings del repositorio al que quiere hacer `push`, sin embargo una vez que es agregado debe
* aceptar la notificacion de GitHub que le llegara por correo.
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