---
---

# Manipulating files and directories

## Where am I?

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


## Listing the content of a directory

To display the content of a directory, use the `ls` command (which stands
for "listing").

Use the `ls` command to list files and directories present in your current
working directory.

```bash
$ ls
Desktop Downloads list.txt
```

As you can see, based on this result, there is no way to distinguish files from
directories.
`Desktop` and `Downloads`, which have no extension, are probably directories
and `list.txt`, which extension is `.txt`  is probably a file.
But this is only a convention and we need a better way to make sure of it.


### Identifying files and directories

The command `ls -l` runs the command `ls` with the option `-l` (which stands
for "long"):

```bash
ls -l
total 8
drwxr-xr-x 2 laurent laurent 4096 May 23 11:06 Desktop
drwxr-xr-x 2 laurent laurent 4096 Jul  3 11:01 Downloads
```

The character `d` starting each path line indicates that this path is
a directory.

### Knowing files size

<div class="important">
    The `man` command allows to get some help on a particular command.
</div>

**Question**: use `man ls` to find how to print human readable file sizes.

<div class="answer">
```bash
$ ls -lh
```
</div>


### Knowing directories size

`du -h`
`du --max-depth=1`

### Displaying the tree structure

`tree`


## Changing directory

`cd`
`cd ..`


## Copying files and directories

`cp`
`cp -r`
`rsync -a`


## Moving files and directories

`mv`


## Creating a directory

`mkdir`


## Delete files and directories

`rm`
`rmdir`
`rm -r`


## Autocompletion

`tab`


## Searching files and directories

`find`


