---
---

# Installing a software

## Using the package manager

The package manager installs pre-compiled packages on a system.
Under debian-like systems (e.g. Ubuntu), the package manager name is `apt-get`.

To install a package, the command is `apt-get install <PACKAGE_NAME>`.

With the package manager, you are forced to install the package on a system
level.
This means that all user will be able to use the package.
It also means that the files will be installed in privileged locations, meaning
only administrators can write there.

To tell the system you want to use your administrator privileges, use the
command `sudo`.

**Question**: install the `cmake` software and the package `build-essential`
which contains several software and libraries.

> **Solution**:
> > ```bash
> > $ sudo apt-get install cmake build-essential
> > # [...]
> > Do you want to continue? [Y/n] y
> > # [...]
> > ```
{:.answer}


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

## Application: hello world

**Question**: install the program "hello" which is in `/data/software` using
both strategies: the configure script and `cmake`. You will be installing the
software in the directory `$HOME/local`.

> **Solution using the configure script**:
> > ```bash
> > $ cd /data/software
> > $ # Extract the archive
> > $ tar xvzf hello-1.0.0.tar.gz
> > x hello-1.0.0/
> > x hello-1.0.0/install-sh
> > x hello-1.0.0/configure.ac
> > x hello-1.0.0/CMakeLists.txt
> > x hello-1.0.0/configure
> > x hello-1.0.0/config.h.in
> > x hello-1.0.0/depcomp
> > x hello-1.0.0/missing
> > x hello-1.0.0/README
> > x hello-1.0.0/Makefile.am
> > x hello-1.0.0/Makefile.in
> > x hello-1.0.0/aclocal.m4
> > x hello-1.0.0/src/
> > x hello-1.0.0/src/Makefile.am
> > x hello-1.0.0/src/main.c
> > x hello-1.0.0/src/Makefile.in
> > $ cd hello-1.0.0
> > $ # Configuration
> > $ ./configure --prefix=$HOME/local
> > checking for a BSD-compatible install... /usr/bin/install -c
> > checking whether build environment is sane... yes
> > checking for a thread-safe mkdir -p... /bin/mkdir -p
> > checking for gawk... no
> > checking for mawk... mawk
> > checking whether make sets $(MAKE)... yes
> > checking for gcc... gcc
> > checking whether the C compiler works... yes
> > checking for C compiler default output file name... a.out
> > checking for suffix of executables...
> > checking whether we are cross compiling... no
> > checking for suffix of object files... o
> > checking whether we are using the GNU C compiler... yes
> > checking whether gcc accepts -g... yes
> > checking for gcc option to accept ISO C89... none needed
> > checking for style of include used by make... GNU
> > checking dependency style of gcc... gcc3
> > checking that generated files are newer than configure... done
> > configure: creating ./config.status
> > config.status: creating Makefile
> > config.status: creating src/Makefile
> > config.status: creating config.h
> > config.status: executing depfiles commands
> > $ # Compilation
> > $ make
> > make  all-recursive
> > make[1]: Entering directory '/data/software/hello-1.0.0'
> > Making all in src
> > make[2]: Entering directory '/data/software/hello-1.0.0/src'
> > gcc -DHAVE_CONFIG_H -I. -I..     -g -O2 -MT main.o -MD -MP -MF .deps/main.Tpo -c -o main.o main.c
> > mv -f .deps/main.Tpo .deps/main.Po
> > gcc  -g -O2   -o hello main.o
> > make[2]: Leaving directory '/data/software/hello-1.0.0/src'
> > make[2]: Entering directory '/data/software/hello-1.0.0'
> > make[2]: Nothing to be done for 'all-am'.
> > make[2]: Leaving directory '/data/software/hello-1.0.0'
> > make[1]: Leaving directory '/data/software/hello-1.0.0'
> > $ # Installation
> > $ make install
> > Making install in src
> > make[1]: Entering directory '/data/software/hello-1.0.0/src'
> > make[2]: Entering directory '/data/software/hello-1.0.0/src'
> >  /bin/mkdir -p '/home/fish/local/bin'
> >   /usr/bin/install -c hello '/home/fish/local/bin'
> > make[2]: Nothing to be done for 'install-data-am'.
> > make[2]: Leaving directory '/data/software/hello-1.0.0/src'
> > make[1]: Leaving directory '/data/software/hello-1.0.0/src'
> > make[1]: Entering directory '/data/software/hello-1.0.0'
> > make[2]: Entering directory '/data/software/hello-1.0.0'
> > make[2]: Nothing to be done for 'install-exec-am'.
> >  /bin/mkdir -p '/home/fish/local/share/doc/amhello'
> >  /usr/bin/install -c -m 644 README '/home/fish/local/share/doc/amhello'
> > make[2]: Leaving directory '/data/software/hello-1.0.0'
> > make[1]: Leaving directory '/data/software/hello-1.0.0'
> > $ # Run the program to make sure it works
> > $ $HOME/local/bin/hello
> > Hello world (version 1.0.0)
> > ```
{:.answer}

> **Solution using cmake**:
> > ```bash
> > $ # Assuming we are already in /data/software/hello-1.0.0
> > $ # Create a directory for out-of-source build
> > $ mkdir build
> > $ cd build
> > $ # Configuration
> > $ cmake .. -DCMAKE_INSTALL_PREFIX=$HOME/local
> > -- The C compiler identification is GNU 7.3.0
> > -- The CXX compiler identification is GNU 7.3.0
> > -- Check for working C compiler: /usr/bin/cc
> > -- Check for working C compiler: /usr/bin/cc -- works
> > -- Detecting C compiler ABI info
> > -- Detecting C compiler ABI info - done
> > -- Detecting C compile features
> > -- Detecting C compile features - done
> > -- Check for working CXX compiler: /usr/bin/c++
> > -- Check for working CXX compiler: /usr/bin/c++ -- works
> > -- Detecting CXX compiler ABI info
> > -- Detecting CXX compiler ABI info - done
> > -- Detecting CXX compile features
> > -- Detecting CXX compile features - done
> > -- Configuring done
> > -- Generating done
> > -- Build files have been written to: /data/software/hello-1.0.0/build
> > $ # Compilation
> > $ make
> > Scanning dependencies of target hello
> > [ 50%] Building C object CMakeFiles/hello.dir/src/main.c.o
> > [100%] Linking C executable hello
> > [100%] Built target hello
> > $ # Installation
> > $ make install
> > [100%] Built target hello
> > Install the project...
> > -- Install configuration: ""
> > -- Installing: /home/fish/local/bin/hello
> > $ # Run the program to make sure it works
> > $ $HOME/local/bin/hello
> > Hello world (version 1.0.0)
> > ```
{:.answer}
