---
tags: [tutorial]
alias: [github, git]
---

[GitHub Skills](https://skills.github.com/)
Libro [Pro Git](https://git-scm.com/book/en/v2)
[GitHub cheat sheet](https://training.github.com/downloads/es_ES/github-git-cheat-sheet/)

## Introducción

Lo primero que hay que entender es que aunque Git y GitHub suenen parecido y estén relacionadas entre ellas no son lo mismo.

Git es un sistema de control de versiones distribuido gratuito y de código abierto diseñado para manejar todo, desde proyectos pequeños hasta proyectos muy grandes, con rapidez y eficiencia.

- Fue diseñado por Linus Torvalds.
- Es fácil de aprender.
- Se puede utilizar sin internet.

GitHub es un servicio de alojamiento de repositorios de Git que proporciona una interfaz gráfica basada en web. Es la comunidad de codificación más grande del mundo. Poner un código o un proyecto en GitHub aumenta su exposición generalizada. Los programadores pueden encontrar códigos fuente en muchos idiomas diferentes y usar la interfaz de línea de comandos, Git, para realizar y realizar un seguimiento de cualquier cambio.

## Git

Git piensa en los datos como una serie de instantáneas (snapshots) de un sistema de archivos en miniatura. Con Git, cada vez que haces un commit, o guardas el estado de tu proyecto, Git básicamente toma una imagen del aspecto de todos tus archivos en ese momento y almacena una referencia a esa instantánea. Para ser eficiente, si los archivos no han cambiado, Git no almacena el archivo de nuevo, sólo un enlace al archivo idéntico anterior que ya ha almacenado. Git piensa en sus datos más bien como un flujo de instantáneas.

Git tiene tres estados principales en los que pueden residir sus archivos: modified, staged, and committed:

- Modified (Modificado): significa que ha cambiado el archivo pero no lo ha confirmado en su base de datos todavía.
- Staged (Preparado): significa que ha marcado un archivo modificado en su versión actual para que entre en su próxima instantánea de confirmación.
- Committed (Confirmado): significa que los datos se almacenan de forma segura en su base de datos local.

Esto nos lleva a las tres secciones principales de un proyecto Git: the working tree, the staging area, and the Git directory. 

El flujo de trabajo básico de Git es algo así:

1. Usted modifica los archivos en su árbol de trabajo
2. Usted pone en staged de forma selectiva sólo los cambios que desea que formen parte de su próximo commit, que añade sólo esos cambios a la staging area.
3. Usted hace un commit, que toma los archivos tal como están en el staging area y almacena esa snapshot permanentemente en su directorio Git.

Para ver la versión de Git se ejecuta el siguiente comando:

```plain
git --version
```

### Primera configuración de Git

Para ver todas las configuraciones y de donde vienen usa:

```plain
git config --list --show-origin
```

Lo primero que debes hacer al instalar Git es establecer tu nombre de usuario y dirección de correo electrónico. Esto es importante porque todos los commits de Git utilizan esta información, y está integrada de manera inmutable en los commits que empiezas a crear:

```plain
git config --global user.name "Ciro Bermudez"
git config --global user.email "cirofabian.bermudez@gmail.com"
```

Si se necesita sobrescribir con un nombre o email diferente para algún proyecto especifico, se puede ejecutar los comandos sin el `--global` .
Para seleccionar un editor para que Git lo utilice cuando lo necesite se utiliza el comando:

```plain
git -config --global core.editor vim
```

Por defecto Git creara una branch llamada *main* cuando se cree un nuevo repositorio con `git init`. Se puede poner un nombre diferente para el branch inicial con el siguiente comando:

```plain
git config --global init.defaultBranch principal
```

Para checar las configuraciones ejecutamos:

```plain
git config --list
```

Para checar una configuración en especifico ejecutamos por ejemplo:

```plain
git config user.name
```

Para obtener ayuda de Git se puede hacer con los siguientes comandos:

```plain
git help <verb>
git <verb> --help
man git-<verb>
```

Ejemplo:

```plain
git help config 
```

Si no se requiere la documentación completa se puede pedir la documentación concisa con el comando:

```plain
git <verb> -h
```

Ejemplo:

```plain
git add -h
```

## Obtener un repositorio de Git

Hay dos maneras típicas para obtener un repositorio:

1. Puedes tomar un directorio local que no esté actualmente bajo control de versiones, y convertirlo en un repositorio Git, o
2. Puedes clonar (*clone*) un repositorio Git existente desde otro lugar.

Para inicializar un repositorio en un directorio ya existente.

1. Ubicarse en la carpeta que se desea tener un control de versiones
2. Ejecutar:
   
   ```plain
   git init
   ```
   
   Esto crea un nuevo subdirectorio llamado `.git` el cual contiene todos los archivos necesarios del repositorio, un esqueleto del repositorio. En este punto, nada en tu proyecto es rastreado todavía. 
   Si quieres empezar con el control de versiones del los archivos existentes, debes empezar a realizar un seguimiento de esos archivos y hacer un commit inicial. Esto se puede llevar a cabo haciendo unos cuantos `git add` que especifiquen los archivos a los que quieres realizar un seguimiento (pasarlos al staging area), seguido de un `git commit`, para que se cree un snapshot del proyecto y se guarden en el directorio Git.
   
   ```plain
   git add *.txt
   git add README.md
   git commit -m "Initial project version" -m "Extended comments"
   ```
   
   Para revisar que los archivos ya estén en el directorio Git ejecutamos:
   
   ```plain
   git status
   ```
   
   El cual nos mostrará los archivos que aún no se les este haciendo seguimiento. Además nos dirá en que branch nos encontramos, si no diverge del branch del servidor y si hemos modificado algún archivo.

Si quieres una copia de algún repositorio ya existente, por ejemplo un proyecto en el que quieras contribuir, necesitas utilizar el comando `git clone <url>`. Con este comando Git recibe una copia completa de casi toda la información que el servidor tiene de ese repositorio. Casi todas las versiones de todos los archivos de la historia del proyecto se arrastran(pulled) por defecto cuando se ejecuta este comando.
Ejemplo:

```plain
git clone https://github.com/cirofabianbermudez/curso_matlab.git
```

Eso crea un directorio llamado `curso_matlab`, inicializa un directorio `.git` dentro de él, extrae(pulls down) todos los datos de ese repositorio y extrae(checks out) una copia de trabajo de la última versión.
Si se quiere guardar con otro nombre `matlab `se ejecuta:

```plain
git clone https://github.com/cirofabianbermudez/curso_matlab.git matlab
```

En este punto ya se tiene un reposito funcionando. Hay que recordar que un archivo puede estar en uno de dos estados. *tracked* o "untraked", y en palabras sencillas "tracked" files son archivos que Git ya conoce. "Untracked" files son todo lo demás, cualquier archivo en el directorio de trabajo que no estuviera en el último snapshot y que no esté en el staging area.

El comando `git add` es bueno pensarlo como "añadir precisamente este contenido a la siguiente commit".

El comando `git status` es bastante comprensivo pero también algo largo, si queremos que sea más corto podemos utilizar una bandera de la siguiente manera:

```plain
git status --short
git status -s
```

Si añadimos un archivo al staging area y después lo modificamos, necesitamos ejecutar el comando `git add` nuevamente para que Git haga el seguimiento del archivo correctamente antes de hacer el commit.

## Ignorar archivos

En muchas ocasiones se generan archivos temporales o de registro que no queremos que se guarden en nuestros repositorios, en estos casos creamos un archivo llamado `.gitignore` que contenga los patrones de los archivos que no queremos hacer seguimiento.

Reglas

- Líneas en blanco o líneas empezando con `#` son ignoradas. (comentarios)
- Los patrones glob estándar funcionan y se aplicarán recursivamente a lo largo de todo el árbol de trabajo.
- Puede comenzar los patrones con una barra diagonal (/) para evitar la recursividad.
- Puede terminar los patrones con una barra diagonal (/) para especificar un directorio.
- Puede negar un patrón empezando con un signo de exclamación (!).

Los patrones glob son como las expresiones regulares simplificadas que utilizan en el shells. Un asterisco (\*) coincide con cero o más caracteres; \[abc\] coincide con cualquier carácter dentro de los paréntesis (en este caso a, b o c); un signo de interrogación (?) coincide con un solo carácter; y los paréntesis que encierran caracteres separados por un guión (\[0- 9\]) coinciden con cualquier carácter entre ellos (en este caso del 0 al 9). También se pueden utilizar dos asteriscos para coincidir con directorios anidados; a/\*\*/z coincidiría con a/z, a/b/z, a/b/c/z, etc.
Ejemplo:

```plain
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

Para ver los cambios hechos en los archivos del repositorio podemos utilizar `git status` pero eso es muy general, solo nos dice si se han modificado o no, para ver a mayor detalle los cambios realizados pero que aún no se han mandando al staging area utilizamos `git diff` sin ningún argumento:

```plain
git diff
```

Ese comando compara lo que está en el directorio de trabajo con lo que está en el staging area. El resultado indica los cambios que ha realizado y que aún no están en el staging area.

Si quieres ver lo que has agregado al staging area que irá en el próximo commit, utiliza el comando `git diff --staged`. Este comando compara los cambios en el staging area con el último commint.

```plain
git diff --staged
git diff --cached
```

`--staged` y `cached` son sinónimos.
Ahora que el staging area solo contiene los archivos que queremos, podemos guardar los cambios. La manera más sencilla para guardarlos es con

```plain
git commit
```

El cual abrirá nuestro editor por defecto configurado, ir a [[git-github_tutorial#Primera configuración de Git]] para más información sobre como configurar el editor por defecto, comentado al principio del mensaje del commit se encontrará la última información de comando `git status`, se puede borrar o dejarlo ahí para futuras referencias. Si se quiere información más explicita se puede modificar el comando con la bandera `-v`. De esta manera se muestran los diff en el mensaje del commit comentados.

```plain
git commit -v
git commit -m "Some description"
git commit -m "Basic description" -m "detail description"
```

Si se esta escribiendo el mensaje utilizando únicamente el comando commit sin ninguna bandera. La primera línea corresponde al mensaje básico, y dejando una renglón en blanco, es decir en la tercera línea escribir los detalles.

Si deseas saltarte el staging area, esto se puede hacer con el siguiente comando, 

```plain
git commit -a -m "Some description"
```

Git automáticamente mandará al staging area todos los archivos a los que ya se les este dando seguimiento antes de este commit.

Para eliminar archivo hay que removerlo de los archivos en seguimiento, (en realidad, quitarlo del staging area) y después hacer un commit. El comando `git rm` hace esto, y también remueve el archivo del directorio de trabajo.

```plain
git rm <filename>
```

Es equivalente a ejecutar `rm` y después `git add <filename>`, `git rm` lo hace en un solo paso. Si el archivo ya se modificó o ya esta en el staging area es necesario utilizar la bandera `-f` o `--force`. Esta es una medida de seguridad para prevenir la perdida de datos.
Si se desea mantener el archivo dentro de nuestro directorio de trabajo pero removerlo del staging area, en otras palabras, mantener un copia en nuestro disco duro pero hacer que Git ya no haga un seguimiento de el, esto es particularmente útil cuando olvidamos agregar algún archivo en `.gitignore`, utilizamos:

```plain
git rm --cached <filename>
```

Para mover archivos o cambiarles el nombre es necesario decirle a Git explícitamente. Para cambiar de nombre un archivo se hace con:

```plain
git mv old_filename new_filename
```

Esto es equivalente a ejecutar:

```plain
mv old_filename new_filename
git rm old_filename
git add new_filename
```

Para ver los commits hechos podemos ejecutar el comando:

```plain
git log
git log --oneline
```

Se enlista en orden cronológico inverso, primero lo último que pasó. Y pone el hash del commit, el nombre y correo de la persona y la fecha.
Si agregamos la bandera `--patched`, `-p`, nos muestra las diferencias introducidas en ese commit, y el `-2` nos indica que solo nos muestre los últimos 2 commits.

```plain
git log -p -2
```

Si queremos ver estadísticas resumidas de los commits podemos utilizar el comando:

```plain
git log --stats
```

Otras variaciones útiles para cambiar el formato en que se muestra el log es:

```plain
git log --pretty=oneline
git log --pretty=short
git log --pretty=full
git log --pretty=fulller
```

La opción más interesante es utilizando el valor `format` donde puedes especificar tu propio formato:

```plain
git log --pretty=format:"%h - %an, %ar : %s"
```

Para ver más sobre este formato leer la pagina 49 del libro [Pro Git](https://git-scm.com/book/en/v2). Una manera muy útil de ver los commits es forma de grafo, esto lo hacemos con el comando:

```plain
git log --pretty=format:"%h %s" --graph
git log --oneline --graph
```

Para limitar la salida del log por fecha podemos utilizar el comando:

```plain
git log --since=2.weeks
git log --since="2008-01-15"
git log --since="2 years 1 day 2 hours 3 minutes ago"
```

También se pueden filtrar los commits por otros criterios como `--author` o `--grep` que busca por palabras especificas en el mensaje del commit. Para que `--grep` ignore si es mayúsculas o minúsculas utilizar la bandera `-i`, con la bandera `--all-match` la búsqueda necesita que cumplir todos los patrones de `--grep`.

```plain
git log --oneline --grep="Initial"
git log --oneline --grep="Initial" -i
git log --oneline --author="Ciro"
git log --oneline --grep="Initial" --grep="Prueba"
git log --oneline --author="Ciro" --grep="Prueba"
git log --oneline --grep="Initial" --grep="commit" -i --all-match
```

Para buscar en el log commits que hayan cambiado, agregado o eliminado una palabra en particular utilizamos:

```plain
git log -S "print_matrix"
```

Otras banderas útiles son `--since`, `--until`, `--author`, `--commiter`, `--grep`, `-S`, `-p`, `-<n>`, `--no-merges`
Para filtrar logs que son específicos que alteraron el contenido de una carpeta con:

```plain
git log -- path/to/file
```

Ejemplo: Ver los commits de Ciro en el mes de Octubre 2008 

```plain
git log --pretty=format:"%h %s" --author="Ciro" --since="2008-10-01" --until="2008-11-01" --no-merges 
```

Localmente para cambiar el nombre de una rama se puede hacer con el comando:

```plain
git branch -m main
```

Para hacerlo en un repositorio de hace de manera diferente, primero hay que eliminar la rama con el comando:

```plain
git push origin --delete master
```

y subir la rama con el nombre correcto con el comando:

```plain
git push origin -u main
```

## Deshacer cosas

En algún momento, vas a necesitar deshacer algo. Pero ten cuidado, no siempre se pueden deshacer lo que ya deshiciste. Esta es una de las pequeñas áreas en las que Git puede perder información si haces algo mal.
Con este siguiente comando puedes modificar el mensaje del commit es caso de haber cometido un error

```plain
git commit --amend -m "Mensage" -m "Detalles"
```

si falto agregar un archivo en el commit se puede agregar y corregir el commit de la siguiente manera:

```plain
git commit -m "Commit en el que se olvido algo"
git add forgotten_file
git commit --amend -m "Mensaje normal"
```

Para sacar un archivo del staging area el comando status nos dice como sacarlo de ahi:

```plain
git restore --staged <filename>
```

Si quieres eliminar los cambios hechos hasta ese momento porque te das cuenta que no tiene ningún sentido seguir con ese cambio y todavía no esta el archivo en el staging area, CUIDADO puedes perder la información, puedes ejecutar el siguiente comando para regresar el archivo al estado que tenía en el último commit:

```plain
git restore <filename>
```

## Trabajando con remotes

Para ver que servidores remotos están configurados podemos ejecutar el comando de abajo, enumera los nombres abreviados de cada controlador remoto que se ha especificado:

```plain
git remote
git remote -v
git remote --verbose
```

si el repositorio fue clonado se mostrará `origin`, con la bandera `-v` se mostrará también el url. Si se tienen multiples remotes se mostrarán todos.

Para añadir un remote explícitamente ejecutamos el siguiente comando:

```plain
git remote add <shortname> <url>
git remote add origin https://github.com/username/reponame.git
```

Por ejemplo las instrucciones de github para subir un repositorio ya existente son:

```plain
git remote add origin https://github.com/cirofabianbermudez/obsidian_demo.git
git branch -m main
git push -u origin main
```

Si el repositorio es compartido o simplemente modificaste algo desde la página de GitHub o desde otra computadora puedes ejecutar el comando

```plain
git fetch <remote_shortname>
git fetch origin
```

para traer los cambios, pero los deja en otro branch (oculta), hasta que se hace el `git merge` para traerlos al branch local. Después de hacer el fetch deberías tener referencias a todas las branches del remote. y se puede hacer merge o inspeccionarlas.
Para ver las ramas ocultas que pudieron crearse por el fetch ejecutamos:

```plain
git branch -a
```

para ver que cambios hay se puede ejecutar el comando

```plain
git diff main remotes/origin/main
```

Para que los cambios unan a a nuestro repositorio local necesitamos hacer un merge

```plain
git merge FETCH_HEAD
```

Para hacer todo en un solo paso podemos ejecutar

```plain
git pull <remote>
git pull origin
```

Para inspeccionar un remote ejecutamos

```plain
git remote show <remote>
git remote show origin
```

este comando te da información de cuales son los URLs del remote, te dice que si te encuentras en la rama main y haces un pull automáticamente hará el merge en main e información acerca de los push y pull que se pueden hacer sin necesidad de especificar el nombre del remote.

Una vez hecho el pull podemos ver los cambios con:

```plain
git diff HEAD^ HEAD
git show
git diff <hash>^ <hash>
```

## Branching

Para crear una rama lo hacemos con el comando:

```plain
git branch <branch_name>
git branch testing
```

Para ver las ramas ejecutamos:

```plain
git branch --list
git branch -a
```

La rama actual en la que nos encontramos ahora se llama `HEAD`. El comando `git branch <name>` solo creo la rama, no se ha movido a ella.
Cambiar de rama es igual que cambiar a un estado anterior en un commit, esto se hace con el comando:

```plain
git chechout <branch_name>
```

Esto mueve `HEAD` a apuntar al nombre de la rama. Dentro de esa rama puedes hacer cambios y commits. Cuando quieras regresar a la rama principal, lo haces con:

```plain
git checkout main
```

Si ejecutamos el comando `git log` no podremos ver nada los cambios recientemente hechos en la rama que hayamos creado y editado. Para esto podemos utilizar el siguiente comando:

```plain
git log <branch_name> --oneline
git log --all --oneline
```

Un comando muy utilizado para ver los commits y las ramas es:

```plain
git log --oneline --decorate --graph --all
```

Para crear una rama y saltar inmediatamente a esa rama utilizamos:

```plain
git checkout -b <new_branch_name>
```

En nuevas versiones de git podemos utilizar el comando `git switch` en lugar de `git checkout`, por ejemplo para cambiar de rama utilizamos:

```plain
git switch testing_branch
```

para crear una nueva rama y cambiarnos a ella utilizamos:

```plain
git switch -c new_branch
```

la bandera `-c` es una manera de decir `--create`. Para cambiar a la rama anterior utilizamos

```plain
git switch -
```

Si se desea combinar el trabajo de una rama a la rama principal se tiene que hacer lo siguiente:

```plain
git checkout main
git merge hotfix
```

Lo primero es hacer un commit en la rama auxilar en la que se estaba trabajando, después es necesario cambiarse a la rama principal donde se van a combinar las ramas, desde ahí se hace el merge indicando la rama de donde vienen los cambios. Finalmente se puede borrar la rama ya que los cambios necesarios ya se hicieron.
Para borrar una rama lo hacemos con:

```plain
git branch -d <branch_name>
```

Para subir una rama al repositorio se hace con la primera vez, la bandera `-u` sirve para que tanto el nombre de la rama en el remote y en el repositorio local sea el mismo y tengamos la posibilidad de hacer un push o pull sin necesidad de especificar el remote o la rama, solo se necesita hacer la primera vez

```plain
git push -u origin <branch_name>
```

después basta con utilizar

```plain
git push origin <branch_name>
git push
```

Para eliminar una rama del remote lo hacemos con;

```plain
git push --delete origin <branch_name>
git push -d origin <branch_name>
```

Hay que recordar que podemos ver el nombre de las ramas del remote con:

```plain
git branch -a
```

Finalmente podemos darnos cuenta que ya no se encuentran en el remote con el comando:

```plain
git remote show origin
```

En caso que todavía aparezcan podemos ejecutar lo siguiente:

```plain
git fetch origin --prune
git fetch origin -p
```

el cual remueve las referencias que ya no existen en el remote antes de hacer el fetch

Algo importante es que cuando hacemos una rama y no queremos que se haga el fast forward lo cual tiene la ventaja que ahora memoria y es más rápido pero se pierde la visualización inicial de la rama. podemos ejecutas:

```plain
git merge <branch_name> --no-ff
```

## Branch managment

Para ver las ramas podemos utilizar el siguiente comando:

```plain
git branch 
git branch -a
git branch --all
```

Para ver las ramas y su último commit  podemos utilizar:

```plain
git branch -v
```

Para ver si la rama ya se a combinado con otras podemos utilizar las banderas `--merged` y `--no-merged`

```plain
git branch --merged
git branch --no-merged
```

Los resultados que aparezcan con la bandera merge son seguros de borrar ya que la historia de esas ramas se ha agregado a la otra rama. Los resultados con la bandera `--no-merge` hay que tener más cuidado y es necesario poner la bandera `-D` para eliminar.

Para cambiarle el nombre a una rama de manera local utilizamos:

```plain
git branch -m <old_branch_name> <new_branch_name>
git branch --move <old_branch_name> <new_branch_name>
```

Para cambiar el nombre en el remote utilizamos:

```plain
git push -u origin <new_branch_name>
```

Ahora hay que borrar la rama con el nombre equivocado del remote, eso lo hacemos con:

```plain
git push --delete origin <old_branch_name>
```

Para cambiar el nombre `master` que  se genera por defecto al hacer un repositorio por `main` utilizamos:

```plain
git branch --move master main
```

Para subir una rama local al remote utilizamos:

```plain
git push origin <branch_name>
git push origin <branch_name_local>:<branch_name_remote>
```

Si te pide la contraseña cada vez que haces un push puedes utilizar

```plain
git config --global credential.helper cache
```

para que no te la pida tan seguido.
Cuando alguien sube una rama al remote, tu puedes traer los cambios para verlos con `git fetch origin` y para ver más información con `git remote show origin`. pero no tenemos una copia local de esa rama, solo tenemos un apuntador a `origin/<branch_name>` que no podemos modificar. Para combinar estos cambios con la rama en la que actualmente estamos trabajando lo hacemos con:

```plain
git merge origin/<branch_name>
```

Pero si queremos nuestra propia copia podemos ejecutar:

```plain
git checkout -b <branch_name> origin/<branch_name>
git checkout -b test_branch origin/test_branch
```

Al hacer el checkout automáticamente se genero el `uptream`, se puede ver esto ejecutando, `git remote show origin`. Una vez modificada nuestra rama podemos subir los cambios con

```plain
git push origin test_branch
```

Una manera corta de hacer el checkout anterior es con el comando:

```plain
git checkout --track origin/test_branch
git checkout test_branch
```

Si después de hacer el fetch se detecta que la rama test_branch no existe y ese nombre ya existe en las ramas de origin se puede escribir como atajo solo el nombre de la rama.
Se puede configurar el upstream de una rama manualmente y estando en la rama lo hacemos con:

```plain
git branch -u origin/branch_name
```

Para ver las ramas y sus upstreams ejecutamos

```plain
git branch --v
```

Si trabajamos con varios servidores podemos ejecutar:

```plain
git fetch --all; git branch -vv
```

para actualizar todo y ver las ramas y el estado en que nos encontramos actualmente.



## Crear llaves SSH

Abrir Git Bash y ejecutar el comando

```plain
ssh-keygen -t ed25519 -C "cirofabian.bermudez@gmail.com"
```

este comando pedira un nombre para el par de llaves, si solo maneja una cuenta personal puede presionar directamente Enter, de lo contrario poner un nombre diferente. Despues solicitará una frase como contraseña, no es recomendable dejar sin contraseña y solo presionar Enter. Una vez terminado este proceso se habrán creado un par de llaves, una pública y una privada para que pueda comunicarse de manera segura utilizando SSH.

Una vez generado el par de llaves ejecutar el siguiente comando:

```plain
clip < ~/.ssh/id_ed25519.pub
```

esto pondra en el portapapeles la clave pública. 

Finalmente es necesario entrar a su Github, Settings -> SSH and GPG Keys -> New SSH Key. Seleccionar Authentication Key y poner un nombre que haga referencia al equipo donde se encuentra la llave privada.

Una vez agregada la lleva ya puede comunicarse con Github por medio de SSH.
