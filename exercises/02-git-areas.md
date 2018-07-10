# Exercise 02 - Git Areas



### Overview

The purpose of this exercise is to become a bit more familiar with Git's Areas. In this exercise, you will make some changes to a file, use the power of the staging area to craft the perfect commit, and using the stash to dismiss and bring back some parts of a file.



### Steps

1. Create a new repository in an empty folder

2. Create a new file called `utils.js` and add the following code to it. 

   ```js
   export function logc(message, color = 'blue') {
   	console.log(`%c${message}`, `font-weight:bold;color:${color};`);
   }
   ```

3. Commit `utils.js`

4. Modify `utils.js`, changing the default color to `'purple'`

5. Also add a new utility function of your choosing.

6. Commit each change as a separate commit using the staging area and `git add -p`.

7. Add a `debugger;` somewhere in `utils.js`

8. Stash this change with an error message using `git stash`

9. List the contents of the stash using `git stash list` and verify the stash contains your changes

10. Reapply the stash to your working directory

11. Clear the stash list

## Solution

1. Create a new repository in an empty folder

```shell
mkdir git-areas
cd git-areas
git init
```

2. Create a new file called `utils.js` and add the following code to it. 

```js
export function logc(message, color = 'blue') {
      console.log(`%c${message}`, `font-weight:bold;color:${color};`);
}
```

3. Commit `utils.js`

```shell
git add utils.js
git commit -m "initial commit of utils.js"
```

4. Modify `utils.js`, changing the default color to `'purple'`

Make modifications in the editor

5. Also add a new utility function of your choosing.

```js
export function bigAlert(message) {
   console.log(`%c${message}`, 'font-size:3em;');
}
```

6. Commit each change as a separate commit using the staging area and `git add -p`.


```shell
~/code/git-exercise-02
➜ git add -p utils.js
diff --git a/utils.js b/utils.js
index 70eb8b9..e147219 100644
--- a/utils.js
+++ b/utils.js
@@ -1,3 +1,7 @@
-export function logc(message, color = 'blue') {
+export function logc(message, color = 'purple') {
        console.log(`%c${message}`, `font-weight:bold;color:${color};`);
 }
+
+export function bigAlert(message) {
+       console.log(`%c${message}`, 'font-size:3ewm;');
+}
Stage this hunk [y,n,q,a,d,s,e,?]? s
Split into 2 hunks.
@@ -1,3 +1,3 @@
-export function logc(message, color = 'blue') {
+export function logc(message, color = 'purple') {
        console.log(`%c${message}`, `font-weight:bold;color:${color};`);
 }
Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? y
@@ -2,2 +2,6 @@
        console.log(`%c${message}`, `font-weight:bold;color:${color};`);
 }
+
+export function bigAlert(message) {
+       console.log(`%c${message}`, 'font-size:3ewm;');
+}
Stage this hunk [y,n,q,a,d,K,g,/,e,?]? n


~/code/git-exercise-02
➜ git commit -m "change default color"
[master 0ba65ad] change default color
 1 file changed, 1 insertion(+), 1 deletion(-)

~/code/git-exercise-02
➜ git commit -am "add another function"
[master 50f2995] add another function
 1 file changed, 4 insertions(+)
```

7. Add a `debugger;` somewhere in `utils.js`

Make modifications in your editor

8. Stash this change with an error message using `git stash`

```shell
~/code/git-exercise-02
➜ git stash push -m "debugger statement"
Saved working directory and index state On master: debugger statement
```

9. List the contents of the stash using `git stash list` and verify the stash contains your changes

```shell
~/code/git-exercise-02
➜ git stash list
stash@{0}: On master: debugger statement
```

10. Reapply the stash to your working directory

```shell
~/code/git-exercise-02
➜ git stash pop
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   utils.js

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (2b20c9460b80124eb9429f85bcf390555fffc030)

~/code/git-exercise-02
➜ git stash list
```

11. Clear the stash list

If you used `git stash pop`, the stash will be cleared as `pop` removes the next item from the list. If not, you can clear with `git stash clear`
