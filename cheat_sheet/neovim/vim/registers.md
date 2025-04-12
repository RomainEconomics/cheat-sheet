# Vim Registers

```vim
# List all registers

"        # Normal Mode
<CTRL-r> # Insert Mode
```

# Examples

## When Trying to replace a same word multiple times

Goal: Replace all `something` with `else`.

- **Normal Mode**: `:%s/something/else/g` (but we won't use this, as we use registers here)
- **Normal Mode**: `yiw` (copy the word `else`), replace first 'something', but then the second it won't work
  - To solve this, we use registers.
  - `viw` (select the word `something`) and `"0p`

```python
s = 'else'
s = 'something'
s = 'something'
```
