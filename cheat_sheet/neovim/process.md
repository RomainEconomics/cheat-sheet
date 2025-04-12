# Working with external tools

| Method                     | Description                              | Async ? |
| -------------------------- | ---------------------------------------- | ------- |
| `:! {cmd}`                 | Run {cmd} in shell connected to pipe     | No      |
| `:%! {cmd}`                | Run {cmd} with output in current buffer  | No      |
| `io.popen()`               | Execute shell cmd (Lua stdlib)           | No      |
| `uv.spawn`                 | Async spawn process (part of luv)        | Yes     |
| `vim.system()`             | Run {cmd} sync or async                  | Both    |
| `fn.termopen({cmd})`       | Spawn {cmd} in a new pseudo term session | Yes     |
| `vim.api.nvim_open_term()` | Creates a new terminal without a process | Yes     |
| vim.system()               | Run {cmd}                                | Item3.1 |

`vim.api.nvim_open_term()` only useful for tools like distant.nvim for proying
process

## Vim System

```lua
-- Async
vim.system({ 'echo', 'hello' }, { text = true }, function(obj)
  Snacks.debug(obj.code)
  Snacks.debug(obj.stdout)
  Snacks.debug(obj.stderr)
end)

-- Sync
local res = vim.system({ 'echo', 'hello' }, { text = true }):wait()
Snacks.debug(res)
```

## IO Open

```lua
-- List all files in cwd
local handle = io.popen("fd . --type file")

if handle then
	for line in handle:lines() do
		Snacks.debug(line)
	end
	handle:close()
else
	Snacks.debug("Doesn't work")
end
```
