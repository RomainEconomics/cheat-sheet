
# Commit

## Overview


Write changes, from staging area to a git repository.


## Examples

### Commit changes to the repository

```bash
git commit -m "Add a new file"
```



## In Depth

It is an object that contains the history of changes to a tree. 

It contains:

- metadata (author, committer, and commit message)
- a pointer to the tree object
- a sha1 hash (since it is a git object)
- a hash of the parent commit(s)

It allows to get a snapshot of the changes to the tree.


### Display the commit object

```bash
git log --oneline
git cat-file -p COMMIT_HASH
```

```
tree 9436f7a306ff05a3381b839a1783d8d44f204ee4
parent c4ebef51f56641fb0daf078e261ebf16a791e38c
author JR <romain.jouhameau@icebergdatalab.com> 1708072729 +0100
committer JR <romain.jouhameau@icebergdatalab.com> 1708072729 +0100

Update TAG to 0.0.36 in .gitlab-ci.yml
```
