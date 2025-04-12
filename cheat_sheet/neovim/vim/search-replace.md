# Vim Substitution

See: <https://vim.fandom.com/wiki/Search_and_replace>

```md
:[range]s[ubstitute]/{pattern}/{string}/[flags] [count]
|-----| |---------| |-------| |------| |-----| |----|
| | | | | |
| | | | | +-----> 6. Optional count
| | | | +------------> 5. Flags (e.g., g, i, c)
| | | +---------------------> 4. Replacement string or regex
| | +------------------------------> 3. Search pattern (string or regex, inc atoms)
| +-----------------------------------------> 2. Substitution command (s)
+-----------------------------------------------------> 1. Selection ('<,'>), line (.), file (%)
```

1. Selection: default to line (.), visual selection (<'>), or file (%)
2. Substitution command: `s`
3. Flags: `g` (global), `i` (case-insensitive), `c` (confirm). By default, only first occurrence is replaced.

| Command             | Description                                                       |
| ------------------- | ----------------------------------------------------------------- |
| `:s/foo/bar/g`      | Replace all occurrences of `foo` with `bar` in current line.      |
| `:%s/foo/bar/g`     | Replace all occurrences of `foo` with `bar` in the entire file.   |
| `:%s/foo/bar/gc`    | Same but ask for confirmation                                     |
| `:%s/\<foo\>/bar/g` | Replace all occurrences of the word `foo` with `bar` in the file. |
| `:s/some/&thing/g`  | Replace all occurrences of `some` with `something` in the line.   |

Advanced use cases:

- `\zs` pattern: find the start of the match
- `\ze` pattern: find the end of the match

## Examples

### Replace surrounding quotes with brackets

Select the lines and run: `:s/"\(.*\)"/[\1]/g`

```
[some some some]
```

### Replace single letter with zs

To replace the letter x on the three onxe, run: `:<,'>s/on\zs\w/c`

We find the start of the parttern with `\zs` and then only select a single letter with `\w`

```
onxe
onxe
onxe
```

### Append text between a word and a comma

Run: `:<,'>s/\(time\)/very long time`

```
Once upon a time, there was a little
Once upon a time, there was a little
Once upon a time, there was a little
```

### Delete empty lines

On the whole file: `:g/^$/d`
On the selection: `:'<,'>g/^$/d`

```
One

Two

Three
```

### Upper case first letter of each word

Whole is simply: `:g/^/norm gU$`

```
some more text
```

### Replace whitespace in the whole file

Case where copy paste from terminal and a lot of whitepaces are present, and the formatter does not work.

```vim
%s/\s\+ / /g
```

```vim
some
whitespace
```
