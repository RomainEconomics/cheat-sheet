
# Branch

Branch is a pointer to a commit.


## Examples

### List all branches

```bash
git branch
```

### Create a new branch

```bash
git branch NEW_BRANCH
git checkout -b NEW_BRANCH
```

### Checkout a branch

```bash
git checkout BRANCH
```

### Delete a branch

```bash
git branch -d BRANCH
```

### Merge a branch

```bash
git merge BRANCH
```

### Rename a branch

```bash
git branch -m OLD_BRANCH NEW_BRANCH
```

## In Depth

A branch is a pointer to a commit. When a new branch is created, it points to the current commit. When a commit is made, the branch pointer moves to the new commit. This is why the branch is said to be a pointer to a commit.

- Default branch: `master` or `main`
- Multiple branches can exist in a repository
- Pointers for branches are stored in `.git/refs/heads/`
- Current branch tracks new commits
- Branch pointer moves to the new commit when a commit is made