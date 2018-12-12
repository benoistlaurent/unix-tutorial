---
---

# Installing a software

## Using the package manager


## From sources

A major step when installing software from sources is finding a program
dependencies on your system, i.e. other programs and libraries that are required
to install the particular piece of software you are trying to install.

Most well-made software will have a configuration step which aims to find
all dependencies and set everything up before building and installing the
software.

There are mainly two ways of configuring a program installation:

- the configure script
- the cmake script

### The configure script

The most widely used method for configuring a package installation.
The idea is to run the *configure script* which will find all dependencies
needed for the compilation.
It will most likely display error messages and crash if some require
ddependencies are not found.

The simplest way to run the configure script is:

```bash
$ ./configure
```

This script has options which allow to customize the compilation and installation
processes.
A very common option is the ``--prefix`` option which allows to define the
installation prefix:

```bash
$ # The package will be installed in $HOME/local
$ ./configure --prefix=$HOME/local
```


### The CMake script

`cmake` is a tool which development started in 2000 and which aimed a replacing
the configure script.
The objective was to make a simpler tool from the developers point of view.

The standard procedure to configure a compilation/installation using `cmake` 
would be:

```bash
$ # Create and go to the build directory
$ mkdir build
$ cd build
$ # Configuration itself
$ cmake ..
# [...]
```

`cmake` allows so-called *out-of-source compiling* meaning that you can build
the software in a directory separate from the sources.
This is a very healthy way to proceed: in this fashion, all configuration/build
files can be removed simply by deleting the build directory.

To tell `cmake` to install the package in a different directory than the default
one, the command would be:

```bash
$ # The package will be installed in $HOME/local
$ cmake .. -DCMAKE_INSTALL_PREFIX=$HOME/local
# [...]
```


### Compilation

After configuring the compilation and installation running either `cmake` or
the configure script, it is time to compile the package:

```bash
$ # Compilation time!
$ make
# [...]
```

### Installation

The installation prefix default value is `/usr/local` (in most cases).
This is a protected directory meaning that only administrators can write to
this directory.

If you are not administrator on this particular machine, you have to install
the package for example in you home directory (see sections [The configure script](#the-configure-script)
and [The CMake script](#the-cmake-script)).

The command to actually install the package is:

```bash
$ # Unprivileged installation (e.g. in $HOME/local)
$ make install
# [...]
```

If you are administrator on this particular machine, you have to use
those administrator privileges using the `sudo` command:

```bash
$ # Privileged installation (e.g. in /usr/local)
$ sudo make install
# [...]
```
