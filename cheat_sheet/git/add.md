
# Add

Add files, from working directory to staging area.

Different cases are possible:

- Add an untracked file to the staging area
- Add a modified file to the staging area

## Examples

### Add an untracked or a modified file to the staging area

```bash
git add FILE
```

### Remove a file from the staging area

```bash
git reset HEAD FILE
git rm --cached FILE # Remove file from staging area and working directory
```

## In Depth

