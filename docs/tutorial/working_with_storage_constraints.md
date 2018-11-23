---
---

# Working with storage constraints

## Knowing how much space disk is available

`df` reports disk space usage in bytes:

```bash
$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
udev             4053992       0   4053992   0% /dev
tmpfs             816852    1508    815344   1% /run
/dev/sda1       10253588 5194736   4518284  54% /
tmpfs            4084244       0   4084244   0% /dev/shm
tmpfs               5120       4      5116   1% /run/lock
tmpfs            4084244       0   4084244   0% /sys/fs/cgroup
/dev/loop1         35584   35584         0 100% /snap/gtk-common-themes/319
/dev/loop2        144384  144384         0 100% /snap/gnome-3-26-1604/70
/dev/loop3         14976   14976         0 100% /snap/gnome-logs/45
/dev/loop0         89088   89088         0 100% /snap/core/4917
/dev/loop4         35456   35456         0 100% /snap/gtk-common-themes/818
/dev/loop6          3840    3840         0 100% /snap/gnome-system-monitor/51
/dev/loop9         14848   14848         0 100% /snap/gnome-logs/37
/dev/loop11        90368   90368         0 100% /snap/core/5897
/dev/loop13         3840    3840         0 100% /snap/gnome-system-monitor/57
/dev/loop12        13312   13312         0 100% /snap/gnome-characters/139
/dev/loop7         13312   13312         0 100% /snap/gnome-characters/103
/dev/loop8        144128  144128         0 100% /snap/gnome-3-26-1604/74
/dev/loop14        89984   89984         0 100% /snap/core/5742
/dev/loop10         2304    2304         0 100% /snap/gnome-calculator/260
/dev/loop5          2432    2432         0 100% /snap/gnome-calculator/180
tmpfs             816848      28    816820   1% /run/user/121
tmpfs             816848      24    816824   1% /run/user/1000
```

As for `ls` and other commands, the `-h` option allows to display the sizes
in a human-readable way:

```bash
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            3.9G     0  3.9G   0% /dev
tmpfs           798M  1.5M  797M   1% /run
/dev/sda1       9.8G  5.0G  4.4G  54% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           3.9G     0  3.9G   0% /sys/fs/cgroup
/dev/loop1       35M   35M     0 100% /snap/gtk-common-themes/319
/dev/loop2      141M  141M     0 100% /snap/gnome-3-26-1604/70
/dev/loop3       15M   15M     0 100% /snap/gnome-logs/45
/dev/loop0       87M   87M     0 100% /snap/core/4917
/dev/loop4       35M   35M     0 100% /snap/gtk-common-themes/818
/dev/loop6      3.8M  3.8M     0 100% /snap/gnome-system-monitor/51
/dev/loop9       15M   15M     0 100% /snap/gnome-logs/37
/dev/loop11      89M   89M     0 100% /snap/core/5897
/dev/loop13     3.8M  3.8M     0 100% /snap/gnome-system-monitor/57
/dev/loop12      13M   13M     0 100% /snap/gnome-characters/139
/dev/loop7       13M   13M     0 100% /snap/gnome-characters/103
/dev/loop8      141M  141M     0 100% /snap/gnome-3-26-1604/74
/dev/loop14      88M   88M     0 100% /snap/core/5742
/dev/loop10     2.3M  2.3M     0 100% /snap/gnome-calculator/260
/dev/loop5      2.4M  2.4M     0 100% /snap/gnome-calculator/180
tmpfs           798M   28K  798M   1% /run/user/121
tmpfs           798M   24K  798M   1% /run/user/1000
```


## Finding bulky files/directories

`ls -lh` allows to list files along with their size, while `du -h` allows to
list directories size (in both programs, the `-h` option stands for
*human readable*).

Examples:

```bash
$ ls -lh
-rw-r--r-- 1 fish fish   40 Nov 21 14:01 animals2.txt
-rw-r--r-- 1 fish fish   40 Nov 21 14:01 animals3.txt
-rw-r--r-- 1 fish fish   40 Nov 21 10:41 animals.txt
drwxr-xr-x 2 fish fish 4.0K Nov 14 15:31 creatures
-rw-r--r-- 1 fish fish 3.7K Nov 14 15:35 iris.csv
drwxr-xr-x 2 fish fish 4.0K Nov 13 13:58 molecules
-rw-r--r-- 1 fish fish 1.9K Nov 20 16:07 tooth.csv

$ du -h
28K ./molecules
12K ./creatures
64K
```

If your disk is close to being full, you may want to free some space disk.

A more comprehensive way to use `du` would be to use it with the `-a` option
which write counts for all files, not just directories:

```bash
$ # Find the 5 most bulky files and directories
$ du -ah|sort -rh|head -n 5
64K .
28K ./molecules
12K ./creatures
4.0K    ./tooth.csv
4.0K    ./molecules/propane.pdb
```

What is happening here is

- `du -ah` lists files and directories human readable size
- `sort -rh` reverse sorts (`-r`) human sizes (`-h`)
- `head -n 5` displays the first 5 results

You may also want to find only bulky files:

```bash
$ # Find files larger than 100 M
$ find / -size '+100M'
```

Combined with other options (`-name`, `mtime`, etc.), this tool is a great to
to list files you may want to move to a backup drive or even delete in
order to free some space disk.


## Finding directories containing numerous files

Without going into technical details, it is important to being aware that
a single directory containing a large number of files considerably slows
down the system.

The best way to avoid those situations is to be careful when coding
automatisation scripts.

However, it could be necessary to locate directories that contain numerous files
in order to clean them up and/or archive them.

To locate those directories:

```bash
$ # Find the 5 directories that contain the most files.
$ du / --inodes -S 2> /dev/null | sort -rh | head -5
5863    /var/lib/dpkg/info
1954    /var/lib/app-info/icons/ubuntu-bionic-universe/64x64
1602    /usr/share/man/man1
1497    /usr/bin
1214    /usr/lib/x86_64-linux-gnu
```

In this example, the directory that contains the most files is `/var/lib/dpkg/info`,
which contains 5863 files, which is totally acceptable.


## Archiving and compressing files/directories

Archiving files and directories means "creating an archive", i.e. a single
file that contains a subtree.
Under Windows, `zip` is probably the most well know archiving tool.

Under unix, the most `tool` used to create archives is `tar`, which allow to
create archives as well as compress them:

```bash
$ # Create a compressed archive of the creatures directory
$ tar cvzf creatures.tar.gz creatures
# [...]

$ # Unarchive the file we've just created
$ tar xvzf creatures.tar.gz
# [...]
```

**Question**: create a compressed archive of the directory `molecules`. What
is archive size? How does it compare to the directory's size?

```bash
$ tar cvzf molecules.tar.gz molecules
molecules/
molecules/octane.pdb
molecules/propane.pdb
molecules/cubane.pdb
molecules/methane.pdb
molecules/ethane.pdb
molecules/pentane.pdb

$ ls -lh molecules.tar.gz
-rw-rw-r-- 1 fish fish 1.6K Nov 23 11:42 molecules.tar.gz

$ du -h molecules
28K molecules

$ # The archive is only 1.6K compared to the 28K of the directory.
```
{:#answer}

## Using links

Another way to space space disk is to use so-called "links", which allows
not to copy a file in different directory.

There are two kinds of links, symbolic links and hard links.

### Symbolic links

The easiest way to think about symbolic links is to consider them as shortcuts.
Like you would do for a program for example: you might want to create a shortcut
on the desktop to access it faster.

The symbolic link is exactly that: a special file that points the another on
the system.

The benefice being that symbolic link is very lightweight compared to copying
the source file.

Importantly, if a link source is deleted, the link is broken.

The command to create a symbolic link is: `ln -s <SOURCE> [TARGET]`, the `-s`
option standing for 'symbolic'. 


### Hard links.

Hard links are also special files which point to a source file.
Technically, a hard link is assigned the same inode as the original file.
This difference is crucial, considering that a file is never deleted until there
is no more reference to the inode it is assigned.

In other word, when a file is hard linked, removing the source file does not
actually remove the file has the hard link stays alive.

The command to create a hard link is: `ln <SOURCE> [TARGET]`.
