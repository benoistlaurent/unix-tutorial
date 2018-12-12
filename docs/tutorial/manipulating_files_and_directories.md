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
/data
```


## Listing the content of a directory

To display the content of a directory, use the `ls` command (which stands
for "listing").

Use the `ls` command to list files and directories present in your current
working directory.

```bash
$ ls
animals  creatures  iris.csv  molecules  tooth.csv
```

As you can see, based on this result, there is no way to distinguish files from
directories.
`creatures` and `molecules`, which have no extension, are probably directories
and `iris.csv`, which extension is `.csv`  is probably a file.
But this is only a convention and we need a better way to make sure of it.


### Identifying files and directories

The command `ls -l` runs the command `ls` with the option `-l` (which stands
for "long")

```bash
$ ls -l
total 20
drwxr-xr-x 2 fish fish 4096 Nov 23 15:11 animals
drwxr-xr-x 2 fish fish 4096 Nov 14 15:31 creatures
-rw-r--r-- 1 fish fish 3715 Nov 14 15:35 iris.csv
drwxr-xr-x 2 fish fish 4096 Nov 13 13:58 molecules
-rw-r--r-- 1 fish fish 1855 Nov 20 16:07 tooth.csv
```

The character `d` starting each path line indicates that this path is
a directory.

### Knowing files size

**Question**: use `man ls` to find how to print human readable file sizes.

> **Solution**:
> > The `-h` option allows to print human readable sizes.
> > ```bash
> > total 20K
> > drwxr-xr-x 2 fish fish 4.0K Nov 23 15:11 animals
> > drwxr-xr-x 2 fish fish 4.0K Nov 14 15:31 creatures
> > -rw-r--r-- 1 fish fish 3.7K Nov 14 15:35 iris.csv
> > drwxr-xr-x 2 fish fish 4.0K Nov 13 13:58 molecules
> > -rw-r--r-- 1 fish fish 1.9K Nov 20 16:07 tooth.csv
> > ```
{:.answer}

**Question**: list the content of the directory named `molecules`.

> **Solution**:
> > ```bash
> > $ ls molecules
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > ```
{:.answer}


**Question**: list the content of the directory named `molecules` with the
element size.

> **Solution**:
> > ```bash
> > $ ls -lh molecules
> > total 24K
> > -rw-r--r-- 1 fish fish 1.2K Nov 13 13:58 cubane.pdb
> > -rw-r--r-- 1 fish fish  622 Nov 13 13:58 ethane.pdb
> > -rw-r--r-- 1 fish fish  422 Nov 13 13:58 methane.pdb
> > -rw-r--r-- 1 fish fish 1.8K Nov 13 13:58 octane.pdb
> > -rw-r--r-- 1 fish fish 1.2K Nov 13 13:58 pentane.pdb
> > -rw-r--r-- 1 fish fish  825 Nov 13 13:58 propane.pdb
> > ```
{:.answer}


**Question**: list the content of the root directory.

> **Solution**:
> > ```bash
> > $ ls /
> > bin   dev   initrd.img      lib64       mnt   root  srv       tmp  vmlinuz
> > boot  etc   initrd.img.old  lost+found  opt   run   swapfile  usr  vmlinuz.old
> > data  home  lib             media       proc  sbin  sys       var
> > ```
{:.answer}


**Question**: list the content of directory `home/fish` which is located
in the parent directory of `/data`.

> **Solution**:
> > ```bash
> > $ ls ../home/fish/
> > ```
> > `..` is the shortcut for the parent directory of the current directory.
> > In the same fashion, `../..` would be the parent of the parent.
> > 
> > In this example, there is no output to the `ls` command, which basically
> > means that the directory is empty.
{:.answer}


### Knowing directories size

Importantly, the `ls` command won't display the actual disk usage for directories.
To convince us, let's list the content of the `molecules` directory:

```bash
$ ls -lh molecules
total 24K
-rw-r--r-- 1 fish fish 1.2K Nov 13 13:58 cubane.pdb
-rw-r--r-- 1 fish fish  622 Nov 13 13:58 ethane.pdb
-rw-r--r-- 1 fish fish  422 Nov 13 13:58 methane.pdb
-rw-r--r-- 1 fish fish 1.8K Nov 13 13:58 octane.pdb
-rw-r--r-- 1 fish fish 1.2K Nov 13 13:58 pentane.pdb
-rw-r--r-- 1 fish fish  825 Nov 13 13:58 propane.pdb
```

The first line of this output tells us that the total file size is 24K.
However, a moment ago, `ls -l` displayed 4K for the `molecules` directory size.
This is because the `ls` command won't recurse into subdirectories to get file
sizes and, more importantly, won't sum file and subdirectories sizes to get
the actual disk usage for a directory.

The command `du` (**d**isk **u**sage) will give us this information:

```bash
$ du
12  ./creatures
28  ./molecules
20  ./animals
72  .
```

As for `ls`, the `-h` option allows to display human readable sizes:

```bash
$ du -h
12K ./creatures
28K ./molecules
20K ./animals
72K .
```

**Question**: use the manual to find `du`'s option that will limit recursion
to a single subdirectory, then get the disk usage for `/usr`.

> **Solution**:
> > ```bash
> > $ du -h --max-depth=1 /usr
> > 136M    /usr/src
> > 60K /usr/local
> > 131M    /usr/lib
> > 157M    /usr/share
> > 200K    /usr/include
> > 41M /usr/bin
> > 4.0K    /usr/games
> > 8.1M    /usr/sbin
> > 473M    /usr
> > ```
{:.answer}


### Displaying the tree structure

Being able to see a directory tree structure can be very useful.
`ls -R` allow to recurse into subdirectories:

```bash
$ ls -R
.:
animals  creatures  iris.csv  molecules  tooth.csv

./animals:
animals2.txt  animals3.txt  animals4.txt  animals.txt

./creatures:
basilisk.fasta  unicorn.fasta

./molecules:
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

Unfortunately, the output may be quite unreadable.
For this reason, the `tree` program may be useful:

```bash
$ tree
.
├── animals
│   ├── animals2.txt
│   ├── animals3.txt
│   ├── animals4.txt
│   └── animals.txt
├── creatures
│   ├── basilisk.fasta
│   └── unicorn.fasta
├── iris.csv
├── molecules
│   ├── cubane.pdb
│   ├── ethane.pdb
│   ├── methane.pdb
│   ├── octane.pdb
│   ├── pentane.pdb
│   └── propane.pdb
└── tooth.csv

3 directories, 14 files
```


## Changing directory

The command to change the current working directory is `cd` (**c**hange **d**irectory).

```bash
$ pwd
/data
$ cd creatures
$ pwd
/data/creatures
```

**Question**: now that you are in the `creatures` directory, how to go back
to the parent directory?

> **Solution**:
> > ```bash
> > $ cd ..
> > ```
{:.answer}


## Copying files and directories

The command `cp` (**c**o**p**y) usage is `cp [options] <SOURCE> <TARGET>`,
meaning that, appart from options, it takes two arguments, meaning the source
and the target:

```bash
$ cp iris.csv iris-copy.csv
$ ls
animals  creatures  iris-copy.csv  iris.csv  molecules  tooth.csv
```

If the target name is a directory, the file will be copied to the directory
with the same name:

```bash
$ cp iris.csv /home/fish
$ ls /home/fish/
iris.csv
```

**Question**: find in the manual how to copy a whole directory (recursive copy),
then copy `creatures` to `tmp`.

> **Solution**:
> > ```bash
> > $ cp -r creatures /tmp
> > $ ls /tmp/creatures
> > basilisk.fasta  unicorn.fasta
> > ```
{:.answer}

## Moving files and directories

In unix, "moving" a file and renaming a file is actually the same thing and
we use the command `mv` (**m**o**v**e):

```bash
# Rename iris-copy.csv to iris2.csv
$ mv iris-copy.csv iris2.csv

# Moves iris2.csv to the /tmp directory
$ mv iris2.csv /tmp
```


## Creating a directory

To create a directory, use the command ``mkdir`` (**m**a**k**e **dir**ectory):

```bash
$ mkdir tempdir
```


## Delete files and directories

To remove a file, use the command `rm` (**r**e**m**ove):

```bash
$ rm /tmp/iris2.csv
```

To remove a directory, use can either use `rm -r` (**r**ecursive) or the
``rmdir`` command which will only work if the target directory is empty:

**Question**: remove the directory `tempdir` we just created.

> **Solution**:
> > ```bash
> > $ rmdir tempdir  # Alternatively (rm -r tempdir)
> > ```
{:.answer}


## Searching files and directories

The command `find`, which quite intuitively searches and finds files and directories,
is a very powerful and this tutorial will not cover 10% of its capacities.

So this is a very short list of examples


## By name

```bash
$ # find files and directories named "ethane.pdb"
$ find . -name ethane.pdb
./molecules/ethane.pdb

$ # find files and directories named "ethane.pdb" and located in /home/fish
$ find /home/fish -name ethane.pdb
$ # no result found
```


### By extension

```bash
$ # find files and directories with extension ".pdb"
$ find . -name *.pdb
./molecules/octane.pdb
./molecules/propane.pdb
./molecules/cubane.pdb
./molecules/methane.pdb
./molecules/ethane.pdb
./molecules/pentane.pdb
```


### By prefix

```bash
$ # find files and directories starting with "c"
$ find . -name 'c*'
./molecules/cubane.pdb
./creatures
```


### By size

```bash
$ # find files and directories larger than 2K
$ find . -size '+2k'
.
./molecules
./iris.csv
./creatures
```


### By modification date

```bash
$ # find files and directories modified in the last 60 days
$ find . -mtime -60
# [...]
$ # find files and directories modified in more than 60 days ago
$ find . -mtime +60
# [...]
```


### Find only files/directories

```bash
$ # find files and directories starting with "c"
$ find . -name 'c*'
./molecules/cubane.pdb
./creatures

$ # find only files starting with "c"
$ find . -type f -name 'c*'
./molecules/cubane.pdb

$ # find only directories starting with "c"
$ find . -type d -name 'c*'
./creatures
```

