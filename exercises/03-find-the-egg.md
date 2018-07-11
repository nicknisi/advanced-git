# Exercise 03 - Find the Egg

### Overview

The purpose of this exercise is to get acquainted with `git bisect`. To do this, Type up the `randomegg.sh` script, run it, and then use `git bisect` to find the commit that added the egg.

### Steps

1. Create a new repository
2. Create an empty egg.txt file and commit it
3. Create an empty noegg.txt file and commit it
4. Add the `randomegg.sh` script to the project and commit it
```bash
#!/usr/bin/env bash

RAND=$(( ( RANDOM % 10 ) + 1 ))
for i in {1..20}; do
	if [ "$i" -eq "$RAND" ]; then
		echo "HERE'S THE EGG" >| egg.txt
	else
		echo "NO EGG" >> noegg.txt
	fi
	git commit --allow-empty -am "random commit $i"
done
```
5. Run `randomegg.sh`
6. Use `git bisect` to find the random commit that added the egg. Get creative

## Solution

1. Create a new repository
```shell
> git init
```
2. Create an empty egg.txt file and commit it
```shell
> touch egg.txt
> git add egg.txt
> git commit -m "add egg.txt"
```
3. Create an empty noegg.txt file and commit it
```shell
> touch noegg.txt
> git add noegg.txt
> git commit -m "add noegg.txt"
```
4. Add the `randomegg.sh` script to the project and commit it
```bash
#!/usr/bin/env bash

RAND=$(( ( RANDOM % 10 ) + 1 ))
for i in {1..20}; do
	if [ "$i" -eq "$RAND" ]; then
		echo "HERE'S THE EGG" >| egg.txt
	else
		echo "NO EGG" >> noegg.txt
	fi
	git commit --allow-empty -am "random commit $i"
done
```
5. Run `randomegg.sh`
```shell
> chmod +x randomegg.sh
> ./randomegg.sh
```
6. Use `git bisect` to find the random commit that added the egg. Get creative

```shell
➜ ./randomegg.sh
[master bb5ca8f] random commit 1
 1 file changed, 1 insertion(+)
[master 43dd705] random commit 2
 1 file changed, 1 insertion(+)
[master cad3986] random commit 3
 1 file changed, 1 insertion(+)
[master c173293] random commit 4
 1 file changed, 1 insertion(+)
[master 99722dc] random commit 5
 1 file changed, 1 insertion(+)
[master 35a0b25] random commit 6
 1 file changed, 1 insertion(+)
[master 7008e63] random commit 7
 1 file changed, 1 insertion(+)
[master 35331a2] random commit 8
 1 file changed, 1 insertion(+)
[master e885a26] random commit 9
 1 file changed, 1 insertion(+), 1 deletion(-)
[master 4eab98d] random commit 10
 1 file changed, 1 insertion(+)
[master b23efa3] random commit 11
 1 file changed, 1 insertion(+)
[master 9bc3b89] random commit 12
 1 file changed, 1 insertion(+)
[master d4f978c] random commit 13
 1 file changed, 1 insertion(+)
[master c6dbce2] random commit 14
 1 file changed, 1 insertion(+)
[master 0cf152b] random commit 15
 1 file changed, 1 insertion(+)
[master 68eaf42] random commit 16
 1 file changed, 1 insertion(+)
[master b2562f9] random commit 17
 1 file changed, 1 insertion(+)
[master e399e03] random commit 18
 1 file changed, 1 insertion(+)
[master 0158f2b] random commit 19
 1 file changed, 1 insertion(+)
[master 6962087] random commit 20
 1 file changed, 1 insertion(+)

➜ git log --oneline --graph
* 6962087 (HEAD -> master) random commit 20
* 0158f2b random commit 19
* e399e03 random commit 18
* b2562f9 random commit 17
* 68eaf42 random commit 16
* 0cf152b random commit 15
* c6dbce2 random commit 14
* d4f978c random commit 13
* 9bc3b89 random commit 12
* b23efa3 random commit 11
* 4eab98d random commit 10
* e885a26 random commit 9
* 35331a2 random commit 8
* 7008e63 random commit 7
* 35a0b25 random commit 6
* 99722dc random commit 5
* c173293 random commit 4
* cad3986 random commit 3
* 43dd705 random commit 2
* bb5ca8f random commit 1
* 8cc5d6a initial commit

➜ git bisect start --term-old noegg --term-new egg

➜ git bisect noegg 8cc5d6a

➜ git biect egg HEAD
git: 'biect' is not a git command. See 'git --help'.

The most similar command is
        bisect

➜ git bisect egg HEAD
Bisecting: 9 revisions left to test after this (roughly 3 steps)
[4eab98db42a0a4875689b2d390bc5314cfe8ac5c] random commit 10

➜ cat egg.txt
HERE'S THE EGG

➜ git bisect egg
Bisecting: 4 revisions left to test after this (roughly 2 steps)
[99722dc0c9b6c0ea865c3fd3b06829a3d9547db0] random commit 5

➜ cat egg.txt
there is no egg.

➜ git bisect noegg
Bisecting: 2 revisions left to test after this (roughly 1 step)
[7008e633682151a47d0c949682f9051b26e30a1b] random commit 7

➜ cat egg.txt
there is no egg.

➜ git bisect noegg
Bisecting: 0 revisions left to test after this (roughly 1 step)
[e885a26b178471750c286b5fb02fe5b511e68afd] random commit 9

➜ cat egg.txt
HERE'S THE EGG

➜ git bisect egg
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[35331a25aa3cd2f90e40fc88f0e297e668d933a9] random commit 8

➜ cat egg.txt
there is no egg.

➜ git bisect noegg
e885a26b178471750c286b5fb02fe5b511e68afd is the first egg commit
commit e885a26b178471750c286b5fb02fe5b511e68afd
Author: Nick Nisi <nick@nisi.org>
Date:   Wed Jul 11 03:25:23 2018 -0500

    random commit 9

:100644 100644 8f0174ba5b657d0fa26a5a3f67b153a885b0eaa5 84337fe8021dede703bdf196d1960815edd0f377 M       egg.txt
```
