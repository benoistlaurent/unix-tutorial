---
---

# Environment

## Environment variables

Environment variables are a set of variables which can be used internaly
in some programs, or just as shortcuts in the terminal.

### Listing environment variables

To get the list of all environment variables with their values, type `env`.

**Question**: what's the value of the variable `HOME`


### Displaying a variable's value

To display a single variable's value, use `echo`, which basically prints
a message.
So `echo coucou` will simply print "coucou", while `echo $HOME` prints
the value of the `HOME` variable (`$HOME` refers to the value for the 
`HOME` variable):

```bash
$ echo $HOME
/home/fish
$ echo "This is the value of HOME: $HOME"
This is the value of HOME: /home/fish
```

Importantly, trying to use a environment variable that hasn't been defined
is equivalent to using a variable set to empty string:

```bash
$ echo "hello: '$SOME_UNDEFINED_ENVIRONMENT_VARIABLE'"
hello: ''
```


### Setting/unsetting a variable value

To set an envionement varible:

```bash
$ export MY_VARIABLE=12
$ # Check the result
$ echo $MY_VARIABLE
12
```

To unset this environment variable, use the command `unset`:

```bash
$ export FOO="I am Groot"
$ echo "FOO is: '$FOO'"
FOO is: 'I am Groot'
$ unset FOO
$ echo "FOO is: '$FOO'"
FOO is: ''
```


### Important environment variables

The most important environment variable would be

- `HOME`, path to your home directory which is the place were numerous hidden files are stored
- `PS1`, defines the look of your command-line prompt
- `PATH`, stores the list of directories where executables are to be found.

For example, a current practice is to store some executables in your home
directory, more precisely in `HOME/.local/bin`.
To append this directory to the list of directories where executable should
be looked for, type: `export PATH=$HOME/.local/bin:$PATH`


## Configuring the environment

### The `$HOME/.bashrc` file

A file is often used to configure the environment.
This file, `$HOME/.bashrc`, is read by `bash`, the terminal interpreter upon
start.

### aliases

Aliases are pseudo-commands you defined as shortcuts for other commands.
As an example, you'll probably want to list a directory's content and getting
file sizes quite often.
We saw in chapter [Manipulating files and directories](./manipulating_files_and_directories#knowing-files-size) 
that the command for that is `ls -lh`.
A way to get faster at typing this command is by creating an *alias*, i.e. a
shorter pseudo-command that will do the same thing.

The command to create an alias is...`alias`:

```bash
$ # Create an alias for ls -lh
$ alias ll='ls -lh'
$ # Now, typing 'll' as the same effect as 'ls -lh'
```


### exports
