---
---

# Manipulating data

## Displaying the content of a file

There are several tools aiming to display the content of a file, each of
them whith a different purpose.

### Displaying the entire file

`cat` display the whole content of a file:

```bash
$ cat molecules/methane.pdb
COMPND      METHANE
AUTHOR      DAVE WOODCOCK  95 12 18
ATOM      1  C           1       0.257  -0.363   0.000  1.00  0.00
ATOM      2  H           1       0.257   0.727   0.000  1.00  0.00
ATOM      3  H           1       0.771  -0.727   0.890  1.00  0.00
ATOM      4  H           1       0.771  -0.727  -0.890  1.00  0.00
ATOM      5  H           1      -0.771  -0.727   0.000  1.00  0.00
TER       6              1
END
```

Actually, `cat`'s primary purpose is to concatenate files.
Meaning that a way of using it would actually be to give several files as
input in order to get the concatenation of the files:

```bash
$ cat molecules/methane.pdb molecules/ethane.pdb
COMPND      METHANE
AUTHOR      DAVE WOODCOCK  95 12 18
ATOM      1  C           1       0.257  -0.363   0.000  1.00  0.00
ATOM      2  H           1       0.257   0.727   0.000  1.00  0.00
ATOM      3  H           1       0.771  -0.727   0.890  1.00  0.00
ATOM      4  H           1       0.771  -0.727  -0.890  1.00  0.00
ATOM      5  H           1      -0.771  -0.727   0.000  1.00  0.00
TER       6              1
END
COMPND      ETHANE
AUTHOR      DAVE WOODCOCK  95 12 18
ATOM      1  C           1      -0.752   0.001  -0.141  1.00  0.00
ATOM      2  C           1       0.752  -0.001   0.141  1.00  0.00
ATOM      3  H           1      -1.158   0.991   0.070  1.00  0.00
ATOM      4  H           1      -1.240  -0.737   0.496  1.00  0.00
ATOM      5  H           1      -0.924  -0.249  -1.188  1.00  0.00
ATOM      6  H           1       1.158  -0.991  -0.070  1.00  0.00
ATOM      7  H           1       0.924   0.249   1.188  1.00  0.00
ATOM      8  H           1       1.240   0.737  -0.496  1.00  0.00
TER       9              1
END
```


### Displaying files screen by screen

There are two utilities, `more` and `less`, that allows to display files
screen by screen, which is very usefull when reading large files.

**Question**: try `more` and `less` to display `iris.csv`.

**Question**: in both programs, use `/` to find the occurences of 'virginica'.


### Displaying only the beginning of the file

Displaying the beginning of the file, or *head*, is done thanks to the
`head` command.

**Question**: use `head` to display the first 5 lines of `iris.csv`.

> **Solution**:
> > ```bash
> > $ head -n5 iris.csv
> > sepal_length,sepal_width,petal_length,petal_width,species
> > 5.1,3.5,1.4,0.2,setosa
> > 4.9,3,1.4,0.2,setosa
> > 4.7,3.2,1.3,0.2,setosa
> > 4.6,3.1,1.5,0.2,setosa
> > ```
{:.answer}


### Displaying only the end of the file

Displaying the beginning of the file, or *tail*, is done thanks to the
`tail` command.

**Question**: use `tail` to display the last 5 lines of `iris.csv`.

> **Solution**:
> > ```bash
> > $ tail -n5 iris.csv
> > 6.7,3,5.2,2.3,virginica
> > 6.3,2.5,5,1.9,virginica
> > 6.5,3,5.2,2,virginica
> > 6.2,3.4,5.4,2.3,virginica
> > 5.9,3,5.1,1.8,virginica
> > ```
{:.answer}


## Saving the output of a command to a file

Most standard unix tools do not have an option for naming an output file.
It is because the standard way to store a command output is by **redirecting**
it to a file.
This is done by using the greather-than sign `>`:

```bash
$ # Output is displayed on screen
$ head -n5 iris.csv
sepal_length,sepal_width,petal_length,petal_width,species
5.1,3.5,1.4,0.2,setosa
4.9,3,1.4,0.2,setosa
4.7,3.2,1.3,0.2,setosa
4.6,3.1,1.5,0.2,setosa

$ # Output is redicted to tmp.csv, therefore not displayed on screen
$ head -n5 iris.csv > tmp.csv

$ # Display the content of tmp.csv
$ cat tmp.csv
sepal_length,sepal_width,petal_length,petal_width,species
5.1,3.5,1.4,0.2,setosa
4.9,3,1.4,0.2,setosa
4.7,3.2,1.3,0.2,setosa
4.6,3.1,1.5,0.2,setosa

$ # Remove temporary file.
$ rm tmp.csv
```

Importantly, `>` creates a new file, whether or not the command output
contains something.
**If the output file already exists, it is erased then created again.**

**Question**: how to store the first 2 lines of `iris.csv` to `output.csv`?
Once done, store the last 2 lines of `iris.csv` to `output.csv`. See
by yourself that `output.csv` only contains the output of your last command.
Remove `output.csv` when done.

> **Solution**:
> > ```bash
> > $ head -2 iris.csv > output.csv
> > $ cat output.csv
> > sepal_length,sepal_width,petal_length,petal_width,species
> > 5.1,3.5,1.4,0.2,setosa
> > $ tail -2 iris.csv > output.csv
> > $ cat output.csv
> > 6.2,3.4,5.4,2.3,virginica
> > 5.9,3,5.1,1.8,virginica
> > $ # The output contains only the last two lines of iris.csv, as
> > $ # the system erased output.csv prior to writing the tail command output.
> > $ rm output.csv  # cleaning
> > ```
{:.answer}


There is a second operator, made of two greater-than signs ('`>>`'), which
allows to append output to an already existing file (note: if the file does not
exist, it will be created).

**Question**: how to store the first 2 and last 2 lines of `iris.csv`
to `output.csv`? Once done, display it and remove `output.csv`

> **Solution**:
> > ```bash
> > $ head -2 iris.csv > output.csv
> > $ tail -2 iris.csv >> output.csv
> > $ cat output.csv
> > sepal_length,sepal_width,petal_length,petal_width,species
> > 5.1,3.5,1.4,0.2,setosa
> > 6.2,3.4,5.4,2.3,virginica
> > 5.9,3,5.1,1.8,virginica
> > $ rm output.csv  # cleaning
> > ```
{:.answer}


## File editors

There are a number of terminal file editors.
The winner in the category "easy hands-on" is probably `nano`, which has
the advantage that keyboard shortcut are display at the bottom of the screen.

**Question**: use `nano` to create a file `animals.txt` with 3 lines: "dog",
"cat", "rabbit".

> **Solution**:
> To open a new or existing file, the command whould be `nano <FILENAME>`.
> In our case `nano animals.txt`.
> 
> Then, just enter the 3 lines and hit Ctrl+X to exit.
> `nano` prompts whether or not you want to save the changes you made.
> So hit `Y` to save the changes.
{:.answer}

Other historical and still widely used editors are `vi` and `emacs`, which
are both very powerful.
I would personnaly recommand using `vi` as it uses keyboard shortcuts which
are common to other unix programs.


## Counting the number of lines/words/characters in a file

To count lines, words or characters in a file, we use `wc` (**w**ord **c**ount).

```bash
$ wc creatures/basilisk.fasta
  28   34 1708 creatures/basilisk.fasta
```

By default, `wc` displays three numbers, namely the number of lines, words
and characters in a file.

**Question**: how to display only the number of lines in a file? of words? of characters?

> **Solution**:
> > ```bash
> > $ # display only the number of lines
> > $ wc -l creatures/basilisk.fasta
> > 28 creatures/basilisk.fasta
> > $ # display only the number of words
> > $ wc -w creatures/basilisk.fasta
> > 34 creatures/basilisk.fasta
> > $ # display only the number of characters
> > $ wc -c creatures/basilisk.fasta
> > 1708 creatures/basilisk.fasta
> > ```
{:.answer}

**Question**: how to display the number of lines in pdb files located in `molecules`?

> **Solution**:
> > ```bash
> > $ wc -l molecules/*.pdb
> >   20 molecules/cubane.pdb
> >   12 molecules/ethane.pdb
> >    9 molecules/methane.pdb
> >   30 molecules/octane.pdb
> >   21 molecules/pentane.pdb
> >   15 molecules/propane.pdb
> >  107 total
> > ```
{:.answer}


## Searching a pattern in a file

`grep` prints lines matching a pattern.

For example, to get the "canine" lines from tooth.csv, just type

```bash
$ grep canine tooth.csv
2015-05-27,canine
2016-12-09,canine
2015-10-18,canine
2016-06-13,canine
2015-05-10,canine
2016-05-07,canine
2015-10-26,canine
2016-07-08,canine
2015-02-14,canine
2016-08-12,canine
2016-09-17,canine
2016-02-07,canine
2017-11-12,canine
2016-08-17,canine
2015-10-23,canine
2015-12-09,canine
2015-12-03,canine
2016-03-07,canine
2017-03-04,canine
2015-03-05,canine
```

`grep` has a lot of useful options:

- `-v`, reverse search
- `-i`, ignore case
- `-n`, prefix each line with the line number
- `-c`, count the number of occurences of the pattern
- `-r`, recursively explore files

**Question**: how to get the number of non-canine line?

> **Solution**:
> > ```bash
> > $ grep -vc canine tooth.csv
> > 80
> > ```
{:.answer}


## Extracting a file columns

The command `cut` allows to extract columns from a file in various ways.

For example, to extract the date column from `tooth.csv`, several approches
can be used:

```bash
$ # Extract each line first 10 characters
$ cut -c 1-10 tooth.csv
2015-08-03
2015-06-21
2015-10-26
2017-01-30
2015-05-27
2016-07-14
2016-01-21
2015-05-14
2016-03-07
# [...]
$ # Extract the first column using "," as a separator
$ cut -d "," -f 1 tooth.csv
2015-08-03
2015-06-21
2015-10-26
2017-01-30
2015-05-27
2016-07-14
2016-01-21
2015-05-14
2016-03-07
# [...]
```

**Question**: find two ways to extract the teeth column from `tooth.csv`.

> **Solution**:
> > ```bash
> > $ # Extract characters 12 to end-of-line
> > $ cut -c 12- tooth.csv
> > molar
> > molar
> > molar
> > premolar
> > canine
> > incisor
> > premolar
> > incisor
> > incisor
> > # [...]
> > $ # Extract the second column using "," as column separator
> > $ cut -d "," -f 2 tooth.csv
> > molar
> > molar
> > molar
> > premolar
> > canine
> > incisor
> > premolar
> > incisor
> > incisor
> > ```
{:.answer}


## Sorting a file

Quite intuitively, `sort` allows to sort a file lines:

```bash
$ sort tooth.csv
2015-01-16,incisor
2015-02-14,canine
2015-02-22,molar
2015-02-25,incisor
2015-03-05,canine
2015-03-20,premolar
2015-03-31,premolar
2015-04-16,molar
2015-04-23,premolar
2015-05-10,canine
# [...]
```

Importantly, by default, the sort is not a numeric sort but rather a sort by
ASCII code.

So when sorting `animals/animals.txt`, this is what happens:

```bash
$ sort animals/animals.txt
11 cat
1 dog
23 bird
2 rabbit
3 chicken
```

**Question**: how to sort `animals/animals.txt` properly? How to sort it in decreasing order?

> **Solution**:
> > ```bash
> > # Numeric sort
> > $ sort -n animals/animals.txt
> > 1 dog
> > 2 rabbit
> > 3 chicken
> > 11 cat
> > 23 bird
> > 
> > # Reverse numeric sort
> > $ sort -nr animals/animals.txt
> > 23 bird
> > 11 cat
> > 3 chicken
> > 2 rabbit
> > 1 dog
> > ```
{:.answer}

**Question**: how to sort `tooth.csv` by increasing day number?

> **Solution**:
> > ```bash
> > $ # We have to tell sort that the field separator we want to use is '-'
> > $ # and then that we want to sort by the 3rd field.
> > $ sort tooth.csv -t- -k3
> > 2017-11-01,premolar
> > 2017-12-02,incisor
> > 2015-12-03,canine
> > 2016-06-03,incisor
> > 2017-08-03,incisor
> > 2015-08-03,molar
> > 2016-06-03,premolar
> > 2017-03-04,canine
> > 2015-12-04,incisor
> > 2017-02-04,premolar
> > # [...]
> > ```
{:.answer}


## Concatenating files

As seen [previously](#displaying-the-entire-file), `cat` allows both to
display a single file and to concatenate several file one after the other.

`paste` allows to concatenate file column wide:

```bash
$ # Concatenate animals/animals.txt column wide
$ paste animals/animals.txt animals/animals.txt
2 rabbit    2 rabbit
1 dog   1 dog
11 cat  11 cat
23 bird 23 bird
3 chicken   3 chicken

$ # Concatenate animals/animals.txt column wide with custom separator (" - ")
$ paste -d "|" animals/animals.txt animals/animals.txt
2 rabbit|2 rabbit
1 dog|1 dog
11 cat|11 cat
23 bird|23 bird
3 chicken|3 chicken
```


## Comparing files

Comparing files can be done in numerous ways.
These are the most common tools.

`cmp` outputs the position of the difference if files are different, else nothing:

```bash
$ cmp animals/animals.txt animals/animals2.txt
animals/animals.txt animals/animals2.txt differ: byte 11, line 2
```

`diff` outputs the line number of the difference, and the difference:

```bash
diff animals/animals.txt animals/animals2.txt
2d1
< 1 dog
```

This interprets as "there is a difference on line 2 of animals.txt which translates
to line 1 of animals2.txt: the line '1 dog' has been deleted".

**Question**: what diff option allows to compare the files side-by-side?

> **Solution**:
> > ```bash
> > diff -y animals/animals.txt animals/animals2.txt
> > 2 rabbit                            2 rabbit
> > 1 dog                                 <
> > 11 cat                              11 cat
> > 23 bird                             23 bird
> > 3 chicken                           3 chicken
> > ```
{:.answer}


## Modifying file content

To make simple changes, you probably want to use a classic text editor.

But sometimes, you need to make more complicated changes, e.g. changing all
the occurences of a string in a file.


### Replacing all occurences of a word in a file

To to this, `sed` is probably the most straight-forward solution:

```bash
$ # Replace all occurences of 'rabbit' with 'bunny'
$ sed 's/rabbit/bunny/g' animals/animals.txt
2 bunny
1 dog
11 cat
23 bird
3 chicken
```

The script part of this command tells `sed`:

- `s/` stands for "substitute"
- `rabbit/bunny/` means"rabbit" with "bunny"
- the trailing `g` indicates that we want all occurences on the line to be substituted

So, in one sentence, "replace all occurences of 'rabbit' with 'bunny'".


### Removing a line

#### By line number

```bash
$ # Remove lines 1 and 2
$ sed '1,2d' animals/animals.txt
11 cat
23 bird
3 chicken
```

#### By pattern

```bash
$ # Remove all lines that contains 'chicken'
$ sed '/chicken/d' animals/animals.txt
2 rabbit
1 dog
11 cat
23 bird
```

`sed` is actually a lot more poweful than only those two simple examples.
If you want to know more about `sed` there are numerous quality tutorials
around.
