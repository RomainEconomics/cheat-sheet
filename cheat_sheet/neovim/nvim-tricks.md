# Neovim Tricks

| Command        | Description                                         |
| -------------- | --------------------------------------------------- |
| `:!{cmd}`      | Run command in shell                                |
| `:r !{cmd}`    | Run command in shell and insert output below cursor |
| `:.!{cmd}`     | Run command in shell and replace line               |
| `:%!{cmd}`     | Run command in shell and replace current buffer     |
| `:'<,'>!{cmd}` | Run command in shell and replace current selection  |

## Some Examples

### Base64 encode a string and decode it

Go on the line below and run: `:. !base64 -d`

WW91IGRlY29kZSBpdCBzdWNjZXNzaXZlbHkhCg==

### Run JQ

Select the lines and run: `:!jq`

```json
{"event": "Starting Analyzer", "level": "info", "timestamp": "2024-08-08 14:14:39"}
{"event": "postgres-connection-start", "level": "info", "timestamp": "2024-08-08 14:14:42"}
{"event": "postgres-connection-success", "level": "info", "timestamp": "2024-08-08 14:14:42"}
```

### Run a Bash Command

Select the two lines and run: `: !bash`

```bash
curl -s https://api.github.com/users/RomainEconomics |
jq -r '.login'
```

## Run command inside a buffer and insert bellow cursor

```vim
:r !ls
:r !cat SOME_FILE
```

## Write to a command

Output the contents of the buffer to a command, here cat.

```vim
:w !cat
```

Select the files with vlines, then run: `:w !xargs touch`

```vim
file_1.txt
file_2.txt
file_3.txt
file_4.txt
```

This will create the files.

## Add some keymaps

```vim
vim.keymap.set('n', '<leader>ex', ':.w !bash -e<CR>')
vim.keymap.set('n', '<leader>ex', ':%w !bash -e<CR>')
vim.keymap.set('n', '<leader>cx', ': !chmod +x %<CR>')

```
