

# Pathlib

## Links

- [Pathlib](https://docs.python.org/3/library/pathlib.html)

## Examples

### List files in directory

```python
from pathlib import Path

for file_path in Path.cwd().iterdir():
    print(file_path)
```

### List files in directory recursively

```python
for file_path in Path.cwd().rglob("*"):
    print(file_path)
```

### List all directory in directory

```python
for file_path in Path.cwd().iterdir():
    if file_path.is_dir():
        print(file_path)
```

### Get all files in directory

```python
for file_path in Path.cwd().glob("*.txt"):
    print(file_path)
```

### Move files from cwd to another directory

```python
for file_path in Path.cwd().glob("*.txt"):
    new_path = Path("archive") / file_path.name
    file_path.replace(new_path)
```

### Decompose path

```python
p = PurePath('/usr/bin/python3')
p.parts
>>> ('/', 'usr', 'bin', 'python3')
```