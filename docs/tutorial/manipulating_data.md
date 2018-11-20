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
input in order to get the concatenation of the two files:

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


### Displaying only beginning of the file

Displaying the beginning of the file, or *head*, is done thanks to the
`head` command.

**Question**: use `head` to display the first 5 lines of `iris.csv`.

```bash
$ head -n5 iris.csv
sepal_length,sepal_width,petal_length,petal_width,species
5.1,3.5,1.4,0.2,setosa
4.9,3,1.4,0.2,setosa
4.7,3.2,1.3,0.2,setosa
4.6,3.1,1.5,0.2,setosa
```
{:.answer}


### Displaying only end of the file

Displaying the beginning of the file, or *tail*, is done thanks to the
`tail` command.

**Question**: use `tail` to display the last 5 lines of `iris.csv`.

```bash
$ tail -n5 iris.csv
tail -n5 iris.csv
6.7,3,5.2,2.3,virginica
6.3,2.5,5,1.9,virginica
6.5,3,5.2,2,virginica
6.2,3.4,5.4,2.3,virginica
5.9,3,5.1,1.8,virginicafish@ocean:/data$
```
{:.answer}


## File editors

There are a number of terminal file editors.
The winner in the category "easy hands-on" is probably `nano`, which has
the advantage that keyboard shortcut are display at the bottom of the screen.

**Question**: use `nano` to create a file `animals.txt` with 3 lines: "dog",
"cat", "rabbit".

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

```bash
$ # display only the number of lines
$ wc -l creatures/basilisk.fasta
28 creatures/basilisk.fasta
$ # display only the number of words
$ wc -w creatures/basilisk.fasta
34 creatures/basilisk.fasta
$ # display only the number of characters
$ wc -c creatures/basilisk.fasta
1708 creatures/basilisk.fasta
```
{:.answer}

**Question**: how to display the number of lines in pdb files located in `molecules`?

```bash
$ wc -l molecules/*.pdb
  20 molecules/cubane.pdb
  12 molecules/ethane.pdb
   9 molecules/methane.pdb
  30 molecules/octane.pdb
  21 molecules/pentane.pdb
  15 molecules/propane.pdb
 107 total
```
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

```bash
$ grep -vc canine tooth.csv
81
```

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

Similarly, to extract the teeth column:

```bash
$ # Extract characters 12 to end-of-line
$ cut -c 12- tooth.csv
molar
molar
molar
premolar
canine
incisor
premolar
incisor
incisor
# [...]
$ # Extract second column using "," as column separator
$ cut -d "," -f 2 tooth.csv
molar
molar
molar
premolar
canine
incisor
premolar
incisor
incisor
```


## Sorting a file

`sort`
`sort -r`
`sort -f`
`sort -n`


## Removing duplicate lines

`uniq`
`uniq -c`
`uniq -d`
`uniq -u`


## Concatenating files

`cat`
`paste`
`paste -d`


## Comparing files

`cmp`
`diff`
`diff -y`
`meld`


## Substituting text

`sed`
`awk`

