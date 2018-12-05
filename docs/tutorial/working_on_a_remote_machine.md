---
---

# Working on a remote machine

## Connecting to a distant machine

The command to connect to a distance machine is `ssh` (*Secure Shell*):
`ssh <login>@<host>`.


## Sending/getting files to/from a distance machine

Two options here, `scp` or `rsync`.

`rsync` has this advantage over `scp` that, if you are sending several files and
the process is interrupted for some reason, when you start the transfert again,
rsync starts again from where it stopped, saving lots of time.

The typical rsync command would be `rsync -av SOURCE login@host:TARGET`.

Importantly, those two commands can also be used to copy files on the same
machine.
