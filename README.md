# Practica_Git_AGGA
Entrega de la práctica del modulo de GIT

# - ¿Qué comando utilizaste en el paso 11? ¿Por qué?

Tendríamos varias maneras, la primera que descarto (vamos a suponer que el ejercicio se centra en que cada paso, no sepamos el anterior) sería la de hacer un  checkout a la rama main ya que sabemos que está inmediatamente detrás del commit nuevo.

Debemos desplazarnos tanto la rama como el HEAD a la posición anterior y hacer un restore

    git reset HEAD~1

    git restore git-nuestro.md

Podríamos haber usado un git reset --hard HEAD~1 pero prefiero en este caso ir con más cuidado, pero lo más optimo era esta última solucion.

# - ¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?

Lo primero es averiguar cual es el identificador del commit que acabamos de deshacer con:

    git reflog

Aquí nos indica un identificador, en mi caso el número 84893ea tiene la posición previa al reset por lo que ahora haremos un reset a ese punto.

    git reset e3b0b4c

De esta manera ya nos encontramos en el commit anterior (SOLO EL PUNTERO). Comprobamos con:

    git log

Efectivamente la rama styled y HEAD se encuentran en el punto más avanzado.

Ahora realizamos:

    git restore git-nuestro.md

# - El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?

No, no ha causado ninguno debido a que ha sido un merge de tipo fast forward. Al estar en un grapho de mismo camino, es decir main es ancestro de styled y eso no genera ningún tipo de problema.

    git merge main

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

    git checkout main

    git merge styled

No ha causado un conflicto como tal pero si me ha generado un texto añadido en git-nuestro donde se encuentran los cambios. Me lo ha mergeado con la strategia 'ort' obligando a escribir un mensaje.

# - ¿Qué comando o comandos utilizaste en el paso 25?

He utilizado para este caso el siguiente grafo

    git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset' --all

Sinceramente no se cada parte que hace, pero lo ha dejado muy bonito.

Este es el resultado:

* eb6c50a - (origin/title, title) Creacion ramam Title y Añadido el titulo en el salmo (hace 49 segundos) <Alejandro Alberto Gavira García>
*   e469a4a - (HEAD -> main) Merge de la rama 'styled' a la rama main (hace 5 minutos) <Alejandro Alberto Gavira García>
|\  
| *   5b37e44 - (origin/styled, styled) Merge de htmlify en styled, documento git nuestro es el de styled (hace 6 minutos) <Alejandro Alberto Gavira García>
| |\  
| | * 4e6afed - (origin/htmlify, htmlify) Modificado en la rama HTMLIFY el salmo git-nuestro (hace 10 minutos) <Alejandro Alberto Gavira García>
| |/  
|/|   
| * e3b0b4c - Modificado en la rama styled el archivo git-nuestro (hace 21 minutos) <Alejandro Alberto Gavira García>
|/  
* 8933279 - (origin/main, origin/HEAD) Añadiro el primer poema o salmo y actualizado el gitignore y subido el readme (hace 29 minutos) <Alejandro Alberto Gavira García>
* bc8e310 - Initial commit (hace 40 minutos) <Alejandro Alberto Gavira García>


# - El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?

Sí, porque como dije en el merge de main con styled, no dejan de ser ancestros y por ende pasan por el mismo camino (uno es hija de otra) por lo que GIT nos hace un fast forward directamente.

    git checkout main

    git merge title

# - ¿Qué comando o comandos utilizaste en el paso 27?

Voy en el orden de todos los pasos realizados:

    git reflog

    git reset e469a4a

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

    git checkout 985e914 

    git restore git-nuestro.md

# - ¿Qué comando o comandos usaste en el paso 32?

    git reflog

    git checkout 8933279

    git log

Para confirmar que estamos en el principio

# - ¿Qué comando o comandos usaste en el punto 33?

Para confirmar el final, en el commit pusimos un comentario de titulo añadido con el que aprovechamos y con reflog lo buscamos y nos situamos en él.

    git reflog

    git checkout 985e914

    git log

Siempre hacemos un check de si todo está bien.

_________________________________________________________________________

Final del reflog:

985e914 (HEAD -> main, origin/main, origin/HEAD) HEAD@{0}: checkout: moving from 4e6afed85d8c21b07e5fd20cc1d80de11c6431a8 to main
4e6afed (tag: v0.18, origin/htmlify) HEAD@{1}: checkout: moving from 5b37e44e53ba405df1123404ca11170417885a17 to v0.18
5b37e44 (tag: v0.11, origin/styled) HEAD@{2}: reset: moving to 5b37e44
4e6afed (tag: v0.18, origin/htmlify) HEAD@{3}: reset: moving to 4e6afed
5b37e44 (tag: v0.11, origin/styled) HEAD@{4}: reset: moving to 5b37e44
eb6c50a (tag: v0.3, origin/title) HEAD@{5}: reset: moving to eb6c50a
bc8e310 (tag: v0.1) HEAD@{6}: reset: moving to bc8e310
985e914 (HEAD -> main, origin/main, origin/HEAD) HEAD@{7}: checkout: moving from main to 985e914
985e914 (HEAD -> main, origin/main, origin/HEAD) HEAD@{8}: checkout: moving from main to main
985e914 (HEAD -> main, origin/main, origin/HEAD) HEAD@{9}: reset: moving to 985e914
e469a4a HEAD@{10}: checkout: moving from 985e91489af301fcf4e67206c5e87ec7e149b0f0 to main
985e914 (HEAD -> main, origin/main, origin/HEAD) HEAD@{11}: checkout: moving from main to 985e914
e469a4a HEAD@{12}: reset: moving to e469a4a
985e914 (HEAD -> main, origin/main, origin/HEAD) HEAD@{13}: merge title: Merge made by the 'ort' strategy.
e469a4a HEAD@{14}: checkout: moving from main to main
e469a4a HEAD@{15}: checkout: moving from title to main
eb6c50a (tag: v0.3, origin/title) HEAD@{16}: commit: Creacion ramam Title y Añadido el titulo en el salmo
e469a4a HEAD@{17}: checkout: moving from main to title
e469a4a HEAD@{18}: merge styled: Merge made by the 'ort' strategy.
8933279 HEAD@{19}: checkout: moving from styled to main
5b37e44 (tag: v0.11, origin/styled) HEAD@{20}: commit (merge): Merge de htmlify en styled, documento git nuestro es el de styled
e3b0b4c HEAD@{21}: checkout: moving from htmlify to styled
4e6afed (tag: v0.18, origin/htmlify) HEAD@{22}: commit: Modificado en la rama HTMLIFY el salmo git-nuestro
8933279 HEAD@{23}: checkout: moving from main to htmlify
8933279 HEAD@{24}: checkout: moving from styled to main
e3b0b4c HEAD@{25}: reset: moving to e3b0b4c
8933279 HEAD@{26}: checkout: moving from e3b0b4c8c00ebcd24f689f21b4e1448cb353b411 to styled
e3b0b4c HEAD@{27}: checkout: moving from styled to e3b0b4c
8933279 HEAD@{28}: checkout: moving from e3b0b4c8c00ebcd24f689f21b4e1448cb353b411 to styled
e3b0b4c HEAD@{29}: checkout: moving from styled to e3b0b4c
8933279 HEAD@{30}: reset: moving to Head~1
e3b0b4c HEAD@{31}: commit: Modificado en la rama styled el archivo git-nuestro
8933279 HEAD@{32}: checkout: moving from main to styled
8933279 HEAD@{33}: commit: Añadiro el primer poema o salmo y actualizado el gitignore y subido el readme
bc8e310 (tag: v0.1) HEAD@{34}: clone: from github.com:agavgar/Practica_Git_AGGA.git
