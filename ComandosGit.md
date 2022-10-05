# Recursos utiles/urls
* https://learngitbranching.js.org/
* https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
* https://github.com/settings/repositories



# Comandos GIT para trabajar con el Repositorio Local
* Crear el Staging y Repositorio Local. 
```
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
```
git clone url
```
* Seguimos usando `git add` para mover a staging
* Seguimos usando `git commit` para mover de staging al repositorio local
* Cuando queremos mandar los cambios al directorio remoto.
```
git push
```
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
# Comandos para trabajar con las ramas 
* Crear una rama
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
*Unir ramas
* 1.Nos movemos a la rama master.
```
git checkout master
```
* 2. Hacemos el merge.
```
git merge nombre_rama
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
* Agregar la llave privada al servidor de llaves del os.
```
ssh-add ruta_llave_privada
```
* Copiamos la llave publica a GitHub
* Cambiamos la url del repo para usar ssh en lugar de https
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