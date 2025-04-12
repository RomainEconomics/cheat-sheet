# IO Redirection

- `&0`: file descriptor 0 (stdin)
- `&1`: file descriptor 1 (stdout)
- `&2`: file descriptor 2 (stderr)
- `/dev/null`: special file that discards all data written to it
- `>`: redirect stdout to a file
- `2>`: redirect stderr to a file
- `&>`: redirect both stdout and stderr to a file
- `<`: redirect a file to stdin
- `|`: pipe stdout of one command to stdin of another

## Examples

```bash
echo hi                   # redirect to stdout - print to terminal
echo hi >/dev/null        # redirect to /dev/null - discard output

echo h1 >&2 | grep foo    # redirect stdout to stderr - print "hi"

./script 2>/dev/null      # redirect stderr to /dev/null - discard errors
./script 2>&1 1>/dev/null # redirect stderr to stdout, then stdout to /dev/null
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
