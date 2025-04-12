# Kill

In Linux, signals are used to communicate with processes. Here is a list of some common kill signals, their signal  
codes, and descriptions:

| Signal               | Code       | Description                                                                                                                            |
| -------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| SIGHUP               | (1)        | Hangup detected on controlling terminal or death of controlling process. Often used to reload configuration files.                     |
| SIGINT               | (2)        | Interrupt from keyboard (Ctrl+C). Used to interrupt a process.                                                                         |
| SIGQUIT              | (3)        | Quit from keyboard (Ctrl+). Generates a core dump and terminates the process.                                                          |
| SIGILL               | (4)        | Illegal Instruction. Indicates that the process has attempted to execute an illegal, malformed, unknown privileged instruction.        |
| SIGABRT              | (6)        | Abort signal from abort(3). Used by the abort function to signal abnormal termination.                                                 |
| SIGFPE               | (8)        | Floating-point exception. Indicates an erroneous arithmetic operation, such as division by zero or an operation resulting in overflow. |
| SIGKILL              | (9)        | Kill signal. Forces the process to terminate immediately. Cannot be caught, blocked, or ignored.                                       |
| SIGSEGV              | (11)       | Invalid memory reference (segmentation fault). Indicates an attempt to access memory that the process does not have rights to.         |
| SIGPIPE              | (13)       | Broken pipe: write to pipe with no readers. Sent to a process when it attempts to write to a pipe without a reader.                    |
| SIGALRM              | (14)       | Timer signal from alarm(2). Used to signal that a timer set by the alarm function has expired.                                         |
| SIGTERM              | (15)       | Termination signal. Requests a process to terminate. Unlike SIGKILL, it can be caught and interpreted or ignored by the process.       |
| SIGUSR1              | (10)       | User-defined signal 1. Available for application-specific purposes.                                                                    |
| SIGUSR2              | (12)       | User-defined signal 2. Available for application-specific purposes.                                                                    |
| SIGCHLD              | (17)       | Child stopped or terminated. Sent to a parent process when a child process terminates or stops.                                        |
| SIGCONT              | (18)       | Continue if stopped. Resumes a process that has been stopped.                                                                          |
| SIGSTOP              | (19)       | Stop process. Stops (pauses) a process. Cannot be caught, blocked, or ignored.                                                         |
| SIGTSTP              | (20)       | Stop typed at terminal (Ctrl+Z). Stops a process and can be resumed later.                                                             |
| SIGTTIN              | (21)       | Background process attempting read. Sent to a process when it tries to read from the terminal while in the background.                 |
| SIGTTOU              | (22)       | Background process attempting write. Sent to a process when it tries to write to the terminal while in the background.                 |
| SIGBUS               | (7)        | Bus error. Indicates an access to an invalid address.                                                                                  |
| SIGPOLL              | (29)       | Pollable event (Sys V). Synonym for SIGIO.                                                                                             |
| SIGPROF              | (27)       | Profiling timer expired. Indicates expiration of a profiling timer.                                                                    |
| SIGSYS               | (31)       | Bad system call. Indicates a bad argument to a system call.                                                                            |
| SIGTRAP              | (5)        | Trace/breakpoint trap. Used by debuggers.                                                                                              |
| SIGURG               | (23)       | Urgent condition on socket (4.2BSD).                                                                                                   |
| SIGVTALRM            | (26)       | Virtual alarm clock. Indicates expiration of a virtual timer.                                                                          |
| SIGXCPU              | (24)       | CPU time limit exceeded. Sent when a process exceeds its CPU time limit.                                                               |
| SIGXFSZ              | (25)       | File size limit exceeded. Sent when a process exceeds its file size limit.                                                             |
| SIGWINCH             | (28)       | Window resize signal (4.3BSD, Sun).                                                                                                    |
| SIGIO                | (29)       | I/O now possible (4.2BSD).                                                                                                             |
| SIGPWR               | (30)       | Power failure (System V).                                                                                                              |
| SIGSTKFLT            | (16)       | Stack fault on coprocessor (unused).                                                                                                   |
| SIGRTMIN to SIGRTMAX | (34 to 64) | Real-time signals. Used for real-time application needs.                                                                               |

These signals can be sent using the kill command or programmatically using functions like kill(2), raise(3), or sigqueue(3).

## Examples

```bash
kill [signal] PID
kill 1234              # SIGTERM is the default signal
kill 1234 1235         # Can pass many pid at the same time
kill -9 1234           # SIGKILL by code
kill -s SIGKILL 1234   # SIGKILL by name
kill -9 $(pgrep PNAME) # SIGKILL by code and with getting the pid from process name
```

## Other tools

For convenience, you can use `pkill` or `killall` to send signals to processes by name:

```bash
pkill -9 myprocess
```

This sends the SIGKILL signal to all processes named myprocess.

```bash
killall -15 myprocess
```

This sends the SIGTERM signal to all processes named myprocess.
