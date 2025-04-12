
# Object types

## Blob

Git stores files as blobs. A blob is a binary file with no metadata. It is a snapshot of a file.

```bash
git hash-object file.txt # Create a blob object in ".git/objects/"
```


## Tree

Git stores the file structure as a tree. A tree is a list of blobs and other trees. It is a snapshot of a directory.

```bash
git mktree # Create a tree object
```


## Commit

Git stores the history of changes as a commit. A commit is a snapshot of the changes to the tree. It contains metadata such as the author, committer, and commit message.

```bash
git commit-tree # Create a commit object
```

## Annotated Tag

Git stores tags as a reference to a commit. A tag is a snapshot of a commit. It contains metadata such as the tagger, tag message, and the commit it points to.

