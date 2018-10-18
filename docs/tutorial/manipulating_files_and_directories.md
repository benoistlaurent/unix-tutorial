---
---

Manipulating files and directories
==================================

Where am I?
-----------

Files and directories are identified by an **absolute path**, which shows how
to reach it from the *root directory*.
The root directory is identified by `/`.

As an example, `/home/benoist` is a directory located in the `home` directory,
itself located in the root directory.

`home/benoist/list.txt` is a file located in `/home/benoist`.

Importantly, one cannot know if a path refers to a file or a directory simply
based on its name.
As a convention, most files will have an *extension*, i.e. the part following
the `.` character in a file name (e.g. `.txt` is the extension of file `foo.txt`).

In contrast to absolute path, one can refer to a file or directory thanks to its
**relative path**, which is its path relatively to the
**current working directory**.

As an example, if the current working directory is `/home/benoist`,
then `./lists.txt` is the relative path to `/home/benoist/lists.txt`.

The command `pwd` prints the absolute path of the current working directory.

```bash
$ pwd
/home/benoist
```


Listing the content of a directory
----------------------------------

The command we'll use to list the content of a directory is `ls` (which stands
for "listing").

### Identifying files and directories



`ls`
`ls -l`

### Knowing files size

`ls -lh`

### Knowing directories size

`du -h`
`du --max-depth=1`

### Displaying the tree structure

`tree`


Changing directory
------------------

`cd`
`cd ..`


Copying files and directories
-----------------------------

`cp`
`cp -r`
`rsync -a`


Moving files and directories
----------------------------

`mv`


Creating a directory
--------------------

`mkdir`


Delete files and directories
----------------------------

`rm`
`rmdir`
`rm -r`


Autocompletion
--------------

`tab`


Searching files and directories
-------------------------------

`find`


