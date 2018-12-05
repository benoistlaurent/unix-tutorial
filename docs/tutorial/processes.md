---
---

# Processes

## Displaying alive processes

The simplest way to get the list of running processes is to use the `ps`
command:

```bash
$ ps
  PID TTY          TIME CMD
 1866 pts/0    00:00:00 bash
 2247 pts/0    00:00:00 ps
```

In this example, there are only 2 processes running:

- bash (the shell interpreter)
- ps

Importantly, the first column is the process id (or PID), which is be useful
when it comes to kill the process (see next section).

The `top` command displays all running processes with associate resources.
Similarly, `htop` does the same thing in a prettier fashion.


## Stopping a process

When running a series of analyses which take some time, it may be useful
to stop it if, for example, we notice an mistake in the script.

If the job is running in foreground, you can stop it by hitting `Ctrl-C`.

If the job is in background or runs in another terminal, you will have to 
*kill* it with the command `kill [options] PID`, with `PID` the process id.

You can also kill a process using its name with `killall [options] PROCNAME`.
Importantly, and as its name suggests, this tool will kill **all** processes
named `PROCNAME`.
Meaning that you cannot use this tools to kill only one instance of a program
if you have multiple instances running (you have to use `kill` instead).
