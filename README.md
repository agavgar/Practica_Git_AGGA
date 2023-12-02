# Practica_Git_AGGA
Entrega de la práctica del modulo de GIT

# - ¿Qué comando utilizaste en el paso 11? ¿Por qué?

Tendríamos varias maneras, la primera que descarto (vamos a suponer que el ejercicio se centra en que cada paso, no sepamos el anterior) sería la de hacer un  checkout a la rama main ya que sabemos que está inmediatamente detrás del commit nuevo.

Debemos desplazarnos tanto la rama como el HEAD a la posición anterior y hacer un restore

    git reset HEAD ~1

    git restore git-nuestro.md


# - ¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?

Lo primero es averiguar cual es el identificador del commit que acabamos de deshacer con:

    git reflog

Aquí nos indica un identificador, en mi caso el número 84893ea tiene la posición previa al reset por lo que ahora haremos un reset a ese punto.

    git reset 84893ea

De esta manera ya nos encontramos en el commit anterior (SOLO EL PUNTERO). Comprobamos con:

    git log

Efectivamente la rama styled y HEAD se encuentran en el punto más avanzado.

Ahora realizamos:

    git restore git-nuestro.md

# - El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?

No, no ha causado ninguno debido a que ha sido un merge de tipo fast forward. Al estar en un grapho de mismo camino, es decir main es ancestro de styled y eso no genera ningún tipo de problema.

# - El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?

Para el paso 19, para fusionar htmlify a styled he realizado el siguiente paso:

    git checkout styled

    git merge htmlify

En este caso si que existe un conflicto ya que no es un fast forward. Ambas ramas se encuentran en caminos distintos, es decir, desde styled no podemos acceder a htmlify con saltos hacia atras, es decir que no son parientes entre sí por lo que GIT nos deja la decisión en nuestras manos.

En este caso lo resolvemos facilemnte

    git add git-nuestro.md

Ya que estamos en styled y es el que queremos quedarnos simplemente lo agregamos al stagging area y hacemos un commit para cerrar la operacion de merge

    git commit (confirmar en nano el texto del merge)

# - El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?

No ha causado un conflicto como tal pero si me ha generado un texto añadido en git-nuestro donde se encuentran los cambios. Me lo ha mergeado con la strategia 'ort'.

# - ¿Qué comando o comandos utilizaste en el paso 25?

He utilizado para este caso el siguiente grafo

    git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset' --all

Sinceramente no se cada parte que hace, pero lo ha dejado muy bonito.

Este es el resultado sin colores:

* dbb4c8f - (title) Añadido el titulo en la rama titulo (hace 9 minutos) <Alejandro Alberto Gavira García>
*   e6a7435 - (HEAD -> main) Merge branch 'styled' (hace 13 minutos) <Alejandro Alberto Gavira García>
|\  
| *   42a35fe - (styled) Merge branch 'htmlify' into styled (hace 15 minutos) <Alejandro Alberto Gavira García>
| |\  
| | * 0eb32ac - (htmlify) Añadido el cambio git nuestro de htmlify (hace 20 minutos) <Alejandro Alberto Gavira García>
| |/  
|/|   
| * 84893ea - Añado al repositorio los cambios de git nuestro (hace 66 minutos) <Alejandro Alberto Gavira García>
|/  
* afa263c - (origin/main, origin/HEAD) Commit de git-nuestro y actualización de readme con las preguntas (hace 73 minutos) <Alejandro Alberto Gavira García>
* 84c7636 - Initial commit (hace 82 minutos) <Alejandro Alberto Gavira García>

# - El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?

Sí, porque como dije en el merge de main con styled, no dejan de ser ancestros y por ende pasan por el mismo camino (uno es hija de otra) por lo que GIT nos hace un fast forward directamente.

En la rama main:

    git merge title

# - ¿Qué comando o comandos utilizaste en el paso 27?

Voy en el orden de todos los pasos realizados:

    git reflog

    git reset e6a7435

Hacemos un reset al commit anterior justo del merge para volver atrás. Podríamos hacer trampa y hacer:

    git reset HEAD~2

Ya que main estaba por detrás de Title y ahora es al revés, volveriamos atrás pero seguimos en el supuesto que no sabemos en que punto estamos.



# - ¿Qué comando o comandos utilizaste en el paso 28?

    git status

    git restore git-nuestro.md

# - ¿Qué comando o comandos utilizaste en el paso 29?

    git branch -D title

El -d no me ha dejado, ya que title se encuentra en una rama superior y solamente nos deja borrarlo si es con fuerza bruta ya que dejamos un commit solo.

# - ¿Qué comando o comandos utilizaste en el paso 30?

Al estar el commit perdido, debemos buscarlo a través de reflog para popder situarnos en el.

    git reflog

    git reset f42b8c8

    git restore git-nuestro.md

# - ¿Qué comando o comandos usaste en el paso 32?

    git reflog

    git reset afa263c

    git log

Para confirmar que estamos en el principio

# - ¿Qué comando o comandos usaste en el punto 33?

Para confirmar el final, en el commit pusimos un comentario de titulo añadido con el que aprovechamos y con reflog lo buscamos y nos situamos en él.

    git reflog

    git reset dbb4c8f

    git log

Siempre hacemos un check de si todo está bien.

_________________________________________________________________________
