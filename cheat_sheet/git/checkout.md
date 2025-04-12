

# Checkout


Checkout is a command used to switch branches or restore working tree files.

It changes the HEAD to the specified branch or commit.


## Examples

### 

## In Depth


### HEAD

HEAD is a reference to the currently checked out branch or commit.


- HEAD is locally significant, and it is a pointer to a commit.
- Pointer is located in `.git/HEAD`
- Change reference to a branch with `git checkout BRANCH`
- Change reference to a commit with `git checkout COMMIT_HASH`

