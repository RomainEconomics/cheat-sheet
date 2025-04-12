

# Lifetime

Lifetime is a concept in Rust to ensure that references are valid. It is a way to prevent dangling references.

Lifetimes are named regions of code that a reference is valid for.


References have two properties:

- when they must be valid (in which scope/region of the code)
- what they can point to

Reference is a special case of pointer.
The `'` symbol is used to denote lifetimes, which ensures that references are valid, and that the data they point to is not deallocated while the reference is still in use.



## Examples

### 