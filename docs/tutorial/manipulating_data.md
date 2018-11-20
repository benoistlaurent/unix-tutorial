---
---

# Manipulating data

## Displaying the content of a file


`cat`
`more`
`less`
`head`
`less`


## File editors

There are a number of terminal file editors.
The winner in the category "easy hands-on" is probably `nano`, which has
the advantage that keyboard shortcut are display at the bottom of the screen.

**Question**: use `nano` to create a file `animals.txt` with 3 lines: 'dog',
'cat', 'rabbit'.

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

`grep`
`grep -v`
`grep -i`
`grep -n`
`grep -c`
`grep -r`


## Extracting a file columns

`cut -c`
`cut -d -f`


## Concatenating files

`cat`
`paste`
`paste -d`


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


## Comparing files

`cmp`
`diff`
`diff -y`
`meld`


## Substituting text

`sed`
`awk`

