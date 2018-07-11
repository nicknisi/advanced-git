# Exercise 01 - Multiple Commits

### Overview

The purpose of this exercise is to become just a little bit familiar with Git objects and how Git stores information about your repository. In this exercise you will go through the exercises of creating an empty repository, adding a file, staging and committing it, then modifying the existing file and adding a new file. Then, you'll use `git cat-file` to answer a few questions about the Git objects created.



### Steps

1. Create a new repository in an empty folder
2. Create a new file called `hello.txt` with the contents `hello, world`
3.  Stage and commit it
4. Modify the file created in step 2 by adding a new line `hola, mundo` and stage it
5. Create a new directory called `lib` 
6. Create another new file called `lib/goodbye.txt` with the contents `goodbye, world` and stage it
7. Commit the changes from steps 4 through 6 in a new commit
8. Verify that you now have two commits by running `git log --oneline`
9. Log out the contents of the `commit` object from step 7
10. Log out the contents of the `tree` object for this commit
11. Log out the contents of the `blob` object found in the `tree` from step 10

### Questions

Use `git log` or `git log --oneline` and `git cat-file` to answer the following questions.

1. What is the main reference missing from the initial commit object (from step 3)?
2. Use `git cat-file` on the second commit (from step 6) to find the associated top-level `tree` object.
   1. What is listed in the `tree` object? Why?
   2. What is surprising about the `blob` object referenced in this commit for `hello.txt`?

## Solution

### Steps

#### 1. Create a new repository in an empty folder

```shell
> mkdir git-test

> git init
```

#### 2. Create a new file called `hello.txt` with the contents `hello, world`

```shell
> echo "hello, world" > hello.txt
```

#### 3. Stage and commit it

```shell
> git add hello.txt

> git commit -m "initial commit"
```

#### 4. Modify the file created in step 2 by adding a new line `hola, mundo` and stage it

```shell
> echo "hola, mundo" >> hello.txt

> git add hello.txt
```

#### 5. Create a new directory called `lib` 

```shell
> mkdir lib
```

#### 6. Create another new file called `lib/goodbye.txt` with the contents `goodbye, world` and stage it

```shell
> echo "goodbye, world" > lib/goodbye.txt

> git add lib/goodbye.txt
```

#### 7. Commit the changes from steps 4 through 6 in a new commit

```shell
> git commit -m "add spanish hello, goodbye"
```

#### 8. Verify that you now have two commits by running `git log --oneline`

```shell
> git log --oneline
6fb33c0 add spanish hello, goodbye
2fcf070 initial commit
```

_Note: your commit SHAs will differ_

#### 9. Log out the contents of the `commit` object from step 7

```shell
> git cat-file -p 6fb33c0
tree aa315a0e37901ad1deb49448151643e0cc878446
parent 2fcf070118eafc860bb87aa933d7a3cbea1c027b
author Nick Nisi <nick@nisi.org> 1530498966 -0500
committer Nick Nisi <nick@nisi.org> 1530498966 -0500

add spanish hello, goodbye
```



#### 10. Log out the contents of the `tree` object for this commit

```shell
> git cat-file -p aa315a0e37901ad1deb49448151643e0cc878446
100644 blob 419b8794955e9caa5632242821cdd0a358fc20c1	hello.txt
040000 tree 72b7de1f2e7825d1578985c1519800cd1bfd33dc	lib

```



#### 11. Log out the contents of the `blob` object found in the `tree` from step 10

```shell
> git cat-file -p 419b8794955e9caa5632242821cdd0a358fc20c1
hello, world
hola, mundo
```



### Questions

Use `git log` or `git log --oneline` and `git cat-file` to answer the following questions.

1. What is the main reference missing from the initial commit object (from step 3)? **There is no parent commit**
2. Use `git cat-file` on the second commit (from step 6) to find the associated top-level `tree` object.
   1. What is listed in the `tree` object? Why? **The `tree` references another tree**
   2. What is surprising about the `blob` object referenced in this commit for `hello.txt`? **It contains the entire file contents**
