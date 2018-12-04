---
---

# Processes

## Displaying alive processes

`ps`
`top`
`htop`


## Stopping a process

When running a series of analyses which take some time, it may be useful
to stop it if, for example, we notice an mistake in the script.

If the job is running in foreground, you can stop it by hitting `Ctrl-C`.

If the job is in background or runs in another terminal, you will have to 
*kill* it with the command `kill [options] PID`, with `PID` the process id.

Example:


You can also kill a process using its name with `killall [options] PROCNAME`.
Importantly, and as its name suggests, this tool will kill **all** processes
named `PROCNAME`.
Meaning that you cannot use this tools to kill only one instance of a program
if you have multiple instances running (you have to use `kill` instead).

Example:

```bash
```

## Pausing a job

`Ctrl-Z`


## Putting a job in background

`bg`
`fg`
