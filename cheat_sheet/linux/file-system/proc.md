# Proc

## Proc files

Allowing access to kernel data structures and system information.

Some of the most common files are:

```bash
# Contains info about system cpu (vendor, model, speed, cache, flags, etc.)
cat /proc/cpuinfo

# Contains info about system memory (usage of the system, physical memory, swap, etc.)
cat /proc/meminfo

# Contains info about system kernel version
cat /proc/version

# Contains info about system uptime (running time since last boot, idle time)
cat /proc/uptime

# Contains info about system load average (1, 5, 15 minutes) for running, waiting and blocked processes
cat /proc/loadavg
```
