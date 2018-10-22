---
---

# Working with storage constraints

## Knowing how much space disk is available

`df -h`


## Listing bulky files/directories

`ls -lh`
`du -h`


## Finding bulky files/directories

`find -size`
`du -ah|sort -rn|head -n 20`


## Finding directories containing numerous files

`du --inodes -S | sort -rh | head -20`


## Archiving and compressing files/directories

`tar cvzf`
`tar xvzf`


## Using links

`ln`
`ln -s`

