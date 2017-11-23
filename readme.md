A continuación se muestran las respuestas del ejercicio 1 de la práctica de git.

------
### 1. ¿Qué comando utilizaste en el paso 11?
```
$ git reset --hard HEAD~1
```

#### ¿Por qué?
El `reset` mueve el `HEAD` y la rama a la que apunta a donde se indique (en este caso `HEAD~1` al commit padre que, al tratarse del primer commit, se queda donde está).

Con el parámetro `hard` además indicamos que la *working copy* y el *staging area* también se deshacen, cargando el contenido del commit al que nos hemos dirigido al ejecutar este `reset`.

### 2. ¿Qué comando o comandos utilizaste en el paso 12?
Mediante un `reflog` localizo el commit al que quiero dirigirme y:

```
$ git reset --hard 35bc8ec
```

#### ¿Por qué?
En esta ocasión vuelvo a indicar con el `reset` que nuestro `HEAD` y la rama **styled** a la que está apuntando  se muevan al commit **35bc8ec**. Usando `--hard` indicamos que machaque la *working copy* actual con el contenido de dicho commit y vacíe el *staging area*.

### 3. El merge del paso 13, ¿Causó algún conflicto?
No, ninguno.

#### ¿Por qué?
Porque el commit al que apunta la rama actual **styled** es hijo del commit al que apunta la rama absorvida **master**. Es decir, la rama **styled** ya tiene todos los commits que tiene **master** (uno, para ser más exactos).

De hecho así lo indica git en la consola:

```
$ git merge master
Already up-to-date.
```


### 4. El merge del paso 19, ¿Causó algún conflicto?
Si.

```
$ git merge htmlify

Auto-merging git-nuestro.md
CONFLICT (content): Merge conflict in git-nuestro.md
Automatic merge failed; fix conflicts and then commit the result.
```

#### ¿Por qué?
La rama **styled** apuntaba a un commit cuyos ancestros no contemplaban al commit al que apuntaba **htmlify**. Es decir, se nos presenta un grafo con bifurcación en el que el grafo de la rama **styled** no contiene el commit de la rama **htmlify**.

### 5. El merge del paso 21, ¿Causó algún conflicto?
No, ninguno.

```
Updating e36a8e7..431abe5
Fast-forward
 git-nuestro.md | 18 +++++++++---------
 1 file changed, 9 insertions(+), 9 deletions(-)
```

#### ¿Por qué?
Porque la rama **master** absorve la rama **styled**, la cual contiene todos los commits que contemplaba **master**. Así lo indica también la consola con el `Fast-forward`.

### 6. ¿Qué comando o comandos utilizaste en el paso 25?

$ git log --graph --pretty=oneline

```
$ git log --graph --pretty=oneline
*   431abe575eed963cf8f59c6f300829be7b277d06 (HEAD -> master, styled) Merge branch 'htmlify' into styled
|\  
| * 347f4c61b9dfb547b2e2a4c3f48cb2aef75dc97a (htmlify) Añado estilo HTML a git-nuestro
* | 35bc8ec20425c529a3390bb1d1092101f8fdb9a4 Añado formato MarkDown a git-nuestro
|/  
* e36a8e7852a112b276976ce7ca88ac69ef137e7e Añadimos git-nuestro

```


### 7. El merge del paso 26, ¿Podría ser fast forward?
Si, podría ser *fast forward*.
#### ¿Por qué?
Porque la rama **title** contiene todos los commits que contiene la rama **master**.

### 8. ¿Qué comando o comandos utilizaste en el paso 27?

`$ git reset HEAD~1`

### 9. ¿Qué comando o comandos utilizaste en el paso 28?

`$ git checkout git-nuestro.md`

### 10. ¿Qué comando o comandos utilizaste en el paso 29?

`$ git branch -D title`

He tenido que forzarlo ya que ese commit se queda fuera de cualquier rama.

### 11. ¿Qué comando o comandos utilizaste en el paso 30?

Hago un `checkout` al *commit* en el que añadí el título.
Para localizar dicho *commit* reviso el `reflog`:

```
$ git reflog
431abe5 (HEAD -> master, styled) HEAD@{0}: reset: moving to HEAD~1
b92c13f HEAD@{1}: merge title: Merge made by the 'recursive' strategy.
431abe5 (HEAD -> master, styled) HEAD@{2}: checkout: moving from title to master
5d3d50f HEAD@{3}: commit: Añado título a git-nuestro
431abe5 (HEAD -> master, styled) HEAD@{4}: checkout: moving from master to title
431abe5 (HEAD -> master, styled) HEAD@{5}: merge styled: Fast-forward
e36a8e7 HEAD@{6}: checkout: moving from styled to master
431abe5 (HEAD -> master, styled) HEAD@{7}: commit (merge): Merge branch 'htmlify' into styled
35bc8ec HEAD@{8}: checkout: moving from htmlify to styled
347f4c6 (htmlify) HEAD@{9}: commit: Añado estilo HTML a git-nuestro
e36a8e7 HEAD@{10}: checkout: moving from master to htmlify
e36a8e7 HEAD@{11}: checkout: moving from styled to master
35bc8ec HEAD@{12}: reset: moving to 35bc8ec
e36a8e7 HEAD@{13}: reset: moving to HEAD~1
35bc8ec HEAD@{14}: commit: Añado formato MarkDown a git-nuestro
e36a8e7 HEAD@{15}: checkout: moving from master to styled
e36a8e7 HEAD@{16}: commit (initial): Añadimos git-nuestro

```
Y hago el checkout al *commit* en cuestión:

```
$ git checkout 5d3d50f 
```

Al hacer un checkout a un *commit*, el **HEAD** queda **detached**.
Para solucionarlo creo la rama *title*:

```
$ git checkout -b title
```

Y vuelvo a hacer el mismo merge del punto 26 desde la rama **master**.

```
$ git merge --no-ff title
```

### 12. ¿Qué comando o comandos usaste en el paso 32?

Volvemos al primer commit, cuando se creó el poema, con el siguiente comando:

```
$ git checkout e36a8e7
```
En este caso tenemos HEAD suelto (detached HEAD) ya que no hay ninguna ramma en ese commit.

### 13. ¿Qué comando o comandos usaste en el paso 33?
Al conservar la rama **master** en el commit final, solo tenemos que dirigirnos a dicha rama:

```
$ git checkout master
```
