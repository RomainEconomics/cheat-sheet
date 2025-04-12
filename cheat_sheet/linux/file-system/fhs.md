# File System Hierarchy Standard (FHS)

Defines the directory structure and directory contents in Unix-like operating systems.

It provides a way to organize files and directories on a Unix-like system.

- `/`: root directory
- `/bin`: essential command binaries required by all users
  - nowadays, it is a symbolic link to `/usr/bin`
- `/boot`: static files of the boot loader
- `/dev`: device files
- `/etc`: host-specific system-wide configuration files
- `/home`: home directories for users
- `/lib`: libraries essential for binaries in `/bin` and `/sbin`
  - nowadays, it is a symbolic link to `/usr/lib`
- `/media`: mount points for removable media (e.g., CD-ROMs, USB)
- `/mnt`: temporarily mounted filesystems (e.g., NFS, second hard drive)
- `/opt`: add-on application software packages
- `/proc`: virtual filesystem providing process and kernel information
- `/root`: home directory for the root user
- `/run`: system runtime data (files that are created and removed automatically during boot or shutdown)
- `/sbin`: essential system binaries usually run by the root user
  - nowadays, it is a symbolic link to `/usr/sbin`
- `/srv`: data for services provided by the system (e.g., websites)
- `/sys`: contains information about devices, drivers, and some kernel features
- `/tmp`: temporary files
  - files in this directory are deleted when the system is rebooted
- `/usr`: secondary hierarchy for shareable, read-only user data, not unique to our system
  - `/usr/local`: tertiary hierarchy for local data
- `/var`: variable data files containing files such as databases, mail, and logs
  - important for backups
  - `/var/log`: log files
  - `/var/mail`: mailboxes
  - `/var/spool`: spool for tasks waiting to be processed (e.g., print queues)
  - `/var/tmp`: temporary files that should be preserved between system reboots
