---
---

# Combining tools


## Using the output of a command as the input of another

We've already seen how to save the output of a command into a file.
Obviously, this new file can be used as input for the next command.
Example: remove canine from `tooth.csv` and then get the first 5 rows.

A prefered option would be to use a **pipe**, which meaning redirecting the
output of a command directly into the input of another one, without using any
temporary file.

The operator used for pipes is `|`.

So let's solve the above example: remove "canine" teeth from `tooth.csv`
then get the first 5 rows:

```bash
$ grep -v canine tooth.csv | head -n 5
2015-08-03,molar
2015-06-21,molar
2015-10-26,molar
2017-01-30,premolar
2016-07-14,incisor
```

The number of commands in a pipe is virtually infinite:

```bash
$ grep -v canine tooth.csv | sort | cut -d ',' -f2 | head
```

**Question**: in `tooth.csv`, what the canine count in 2017?

```bash
$ grep 2017 tooth.csv | grep -c canine
2

$ # If you're a big fan of pipes, you can use wc instead of the proper grep option
$ grep 2017 tooth.csv | grep canine | wc -l
2
```
{:.answer}


## Removing duplicate lines

`uniq` helps you report/omit repeated lines.
Importantly, the way it works is that it reports/omit **consecutive** repeated
lines:

```bash
$ # animals/animals4.txt is made of 3 concatenations of animals.txt
$ uniq animals/animals4.txt
2 rabbit
1 dog
11 cat
23 bird
3 chicken
2 rabbit
1 dog
11 cat
23 bird
3 chicken
2 rabbit
1 dog
11 cat
23 bird
3 chicken
```

We can see above that there are still repeated lines.
This is because uniq remove repeated **consecutive** lines and here 
repeated lines are not consecutive.

That's why we need to sort the input file first:

```bash
$ sort animals/animals4.txt | uniq
11 cat
1 dog
23 bird
2 rabbit
3 chicken
```

`uniq` has several useful options such has

- `-c` for counting
- `-d` for showing duplicate lines
- `-u` for showing uniq lines


