# Apuntes del curso

# Comados para git

## git init 
Crea un reposritorio .git donde se guardan los registros de cambios atómicos. Lo usamos para determinar la carpeta en la que vamos a trabajar.

## git status
Lo usamos para saber si tenemos un archivo añadido o borrado en nuestro proyecto, para saber en la rama en la que estamos y si tenemos commits.

## git add
Es para añadir un archivo a nuestra rama seguidamente ponemos entre comillas el nombre de nuestro archivo o poner un punto para añadir todos los archios de nuestra carpeta.

`git add "tuArchivo"` Envía específicamente el archivo

`git add .` Agrega todo el contenido de la carpeta en la que ejecutas el comando


## git rm
Lo usamos para borrar un archivo que hayamos añadido

`git rm --cached` Elimina los archivos de nuestro repositorio local y del área de staging, pero los mantiene en nuestro disco duro. Básicamente le dice a Git que deje de trackear el historial de cambios de estos archivos, por lo que pasaran a un estado untracked.

`git rm --force` Elimina los archivos de Git y del disco duro. Git siempre guarda todo, por lo que podemos acceder al registro de la existencia de los archivos, de modo que podremos recuperarlos si es necesario (pero debemos usar comandos más avanzados).

## git commit
se usa para añadir un commit a nuestra rama, también podemos ponerle un -m seguidamente ponemos entre comillas nuestro ensaje.

`git commit -m "Mensaje de commit"`

Puedo hacer commit y add al mismo tiempo de la siguiente manera

`git commit -am` Solo funciona con archivos a los que ya les he hecho git add anteriormente

## git config
Muestra configuraciones de git también podemos usar –list para mostrar la configuración por defecto de nuestro git y si añadimos --show-origin inhales nos muestra las configuraciones guardadas y su ubicación.

`git config --global user.name`

Cambia de manera global el nombre del usuario, seguidamente ponemos entre comillas nuestro nombre.

`git config --global user.email`

Cambia de manera global el email del usuario, seguidamente ponemos entre comillas nuestro nombre.

## git log
Se usa para ver la historia de nuestros archivos, los commits, el usuario que lo cambió, cuando se realizaron los cambios etc. Seguidamente ponemos el nombre de nuestro archivo.

`git log "tuArchivo"`

`git log --stat` 
Para ver los cambios específicos que se hicieron en cada archivo a partir del commit

`git log --all --graph` Para ver los cambios en las ramas

`git log --all --graph --decorate --oneline` Igual que el anterior pero más decorado

## git show 
Muestra los cambios que han existido en un archivo

`git show "tuArchivo"`

## git diff
Sirve para comparar entre las versiones o commits

`git dif "código del commit más antiguo" "código del commit más nuevo"`

## git reset
Nos permite volver a una versión anterior borrando la historia

`git reset "Código del commit" --hard` Borra todo. Todo todito, absolutamente todo. Toda la información de los commits y del área de staging se borra del historial.

`git reset "Código del commit" --soft` Borramos todo el historial y los registros de Git pero guardamos los cambios que tengamos en Staging, así podemos aplicar las últimas actualizaciones a un nuevo commit.

`git reset HEAD` Este es el comando para sacar archivos del área de staging. No para borrarlos ni nada de eso, solo para que los últimos cambios de estos archivos no se envíen al último commit, a menos que cambiemos de opinión y los incluyamos de nuevo en staging con git add, por supuesto.

## git checkout

Sirve para observar cómo era el archivo en una versión en especifico y permite observar, modificar y volver

`git checkout "Código del commit" "tuArchivo"` Muestra el archivo en la version indicada. Si se da commit se pierde todo lo anterior CUIDADO

`git checkout master "tuArchivo"` Vuelve al estado actual del archivo

## git fetch 
Trae un repositorio remoto a mi repositorio local

## git merge
Fusiona la ultima versión del repositorio local con la version actual del directorio de trabajo

Fusiona ramas. Es recomendable ubicar el HEAD en el master
Cuando hay conflicto en la fusión, se debe elegir qué línea dejar, y despues hacer commit de nuevo

`git merge "nombre de la rama o branch" -m "Mensaje"`

## git pull
Union entre fetch y merge

## git branch
Crea una nueva rama

`git branch "nombre de la rama"`

Para cambiar a una rama en específico se usa checkout

`git checkout "nombre de la rama a la que te quieres mover"`

`git branch -m master main` Cambia el nombre de la rama master a main, debido a que ahora Github usa el nombre "main"

`git show-branch --all` Muestra las ramas que exiten y su historia

`gitk` Muestra la historia de las ramas de manera gráfica en un software

`git push origin "nombre de la rama"` Para subir a github una rama en específico

## git remote 
Sirve para administra el conjunto de repositorios "remotos" cuyas ramas va a rastrear.

`git remote add origin "link del repositorio e github"`
Establece el origen en el repositorio remoto

`git remote -v` Da la lista de conexiones existentes

`git remote set-url origin "url en SSH"` Para cambiar la url a SSH

# git clone
Con este comando puedes clonar un repositorio online en tu pc

`git clone "url del repositorio"`

# Crear llave SSH

`ssh-keygen -t rsa -b 4096 -C "diegojulisorh@gmail.com"`

`eval $(ssh-agent -s)` Para saber si el servidor está corriendo

`ssh-add ~/.ssh/id_rsa` Agregar la llave

# Alias

Funciona de tal manera que puedes ponerle un alias a cierto comando para no tener que escribirlo cada vez que lo necesitas

Por ejemplo:

`alias arbolito="git log --all --graph --decorate --one"`

De ahora en adelante cuando necesites ejecutar este comando, solo tienes que ejecutar `arbolito`

# TAGS
Agregar tags a los commits

`git tag -a nombre-del-tag -m "mensaje" id-del-commit` 
Crear un nuevo tag y asignarlo a un commit

`git tag -d nombre-del-tag`
Borrar un tag en el repositorio local 

`git tag` o `git show-ref --tags`
Listar los tags de nuestro repositorio local 

`git push origin --tags`
Publicar un tag en el repositorio remoto 

`git tag -d nombre-del-tag` y `git push origin :refs/tags/nombre-del-tag`
Borrar un tag del repositorio remoto 

# Pasos para subir tu repositorio a Github

1. Crea el repositorio manualmente en Github. No olvides incluir el README.md como buena práctica
2. Copia la URL
3. Abre la consola y escribe `git remote add origin "link del repositorio e github"`
4. `git remote -v` Revisa la lista de conexiones existentes
5. `git branch -m master main` Cambia el nombre de la rama master a main, debido a que ahora Github usa el nombre "main"
6. `git pull origin main` Traer lo que se encuentra en el servidor remoto
7. `git pull origin main --allow-unrelated-histories` en caso de que el paso anterior de haya dado error
8. `git push origin main` Sube el repositorio local a Github

# Cómo hacer un fork y pull request

1. En Github, buscar el repositorio y dar en el botón "Fork"
2. Clona el repositorio en tu dispositivo local
`git clone "linkrepositorio"`
3. Edita los archivos que deseas
4. Realiza commit para guardar agregar los cambios 
5. Realiza push para subir los cambios a tu Github
6. Inicia el pull request desde Github, el proceso es bastante intuitivo

# Readme

README.md es una excelente práctica en tus proyectos, md significa Markdown, que es una especie de código que te permite cambiar la manera en que se ve un archivo de texto.

Lo interesante de Markdown es que funciona en muchas páginas, por ejemplo la edición en Wikipedia; es un lenguaje intermedio que no es HTML, no es texto plano, es una manera de crear excelentes texto formateados.

Una buena herramienta para editar el readme es : [editor.md](http://https://pandao.github.io/editor.md/en.html "editor.md")

O directamente desde VS Code