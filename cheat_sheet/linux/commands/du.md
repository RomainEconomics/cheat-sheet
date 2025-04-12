

# Du

Disk Usage (du) is a standard Unix program used to estimate file space usage—space used under a particular directory or files on a file system.

## Examples

### Show disk usage of a directory

```bash
du -sh /path/to/directory
du -sh ~/.local/share/Trash # Show disk usage of trash directory
``` 

### Show disk usage of a directory and its subdirectories

```bash
du -sh /path/to/directory/*
du -sh /path/to/directory/* | sort -h # Sort by size
```

### Show disk usage of a directory and its subdirectories, including hidden files

```bash
du -sh /path/to/directory/.*
```
