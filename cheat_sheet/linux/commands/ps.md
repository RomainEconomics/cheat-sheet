# PS

## Description

A process is an instance of a program that is being executed. The `ps` command is used to list the currently running processes on a system.

A process is an independent execution unit with its own resources (CPU, memory, opened files, network connections ...)

It is manage by the kernel

Each process has:

- process id (pid)
- a user under which the process runs
- a state
- possibly a parent pid

## Process Status (PS)

```bash
ps              # only display the process of the terminal
ps aux          # BSD style params (a: all users, u: user friendly, x: process without a tty i.e. process outside of a terminal)
ps --forest     # display tree process
ps -A           # display all process
ps -ef          # display process and the executable path
ps -f           # show extended information (about user, parent pid ...)
ps -l           # show also state process
ps -p 1234,1235 # display info about specific processes
ps 1234 1235    # same
ps | fzf
ps | less
```
