# Curso de Git



Git es un **programa** el cual podemos denominar como un manejador de versiones.

GitHub es un **repositorio**, es un lugar remoto donde almacenamos nuestros proyectos. ejemplot: GitLab, Sourcetree.



## Pasos para crear un nuevo repositorio en GitHub



1. Crear un repositorio en Github
	- Agregar con antelacion el archivo .gitignore si es necesario
	- Agregar el archivo README.md
2. Clonar el repositorio en la computadora
	- git clone https://github.com/cirofabianbermudez/Tesis.git
		Automaticamente ya se ejecutaron los comandos
		-- git init																		inicializa el git				
		-- git remote add origin https://github.com/cirofabianbermudez/Tesis.git		crea el alias origin
3. Agregar  las credenciales 
	- git config --global user.name "Ciro Bermudez"
	- git config --global user.email "cirofabian.bermudez@gmail.com"
4. Editar el repositorio local en la computadora
	- git add .																			añade todo a la staging area
	- git commit -m "Nombre del commit" -m "Comentario del commit"
5. Subir a Github
	- git push origin master





1. Ingresar a la cuenta de Github, dar clic en el signo de más ubicado en la parte superior derecha de la pagina y después dar clic en **New repository**.
   * Público y Privado
   * `.gitignore`
   * **README.md**
   * Licencia 

2. Después de crear el repositorio lo clonamos con el comando
   * `git clone <url>`
   * Ejemplo: `git clone https://github.com/julisaverdejo/poemas.git`

**Notas:**

* IMPORTANTE de preferencia siempre agregar el **README.md** para que se genere el primer commit.

* La primera vez que se configura git es necesario ejecutar los comandos
  * `git config --global user.name "username"`
  * `git config --global user.email "email@mail.com"`



| Comando                                           | Descripción |
| ------------------------------------------------- | ----------- |
| `git clone <url>`                                 |             |
| `git config --global user.email "email@mail.com"` |             |
| `git config --global user.email "email@mail.com"` |             |
| `git status`                                      |             |
| `git add <filename>`                              |             |
| `git restore --staged <filename>`                 |             |
| `git commit -m "Descripción" -m "Detallado"`      |             |
| `git log --oneline`                               |             |
| `git push origin main`                            |             |

