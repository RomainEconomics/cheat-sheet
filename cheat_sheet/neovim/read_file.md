# Read files in Neovim

See also `fs.md`

```lua
-- Method 1: Using vim.fn.readfile()
local lines = vim.fn.readfile('path/to/your/file.txt')
-- Now 'lines' is a table where each element is a line from the file
```

```lua
-- Method 2: Using vim.api.nvim_buf_get_lines()
-- This works on an existing buffer
local bufnr = vim.fn.bufnr('path/to/your/file.txt')
local lines = vim.api.nvim_buf_get_lines(bufnr, 0, -1, false)
```

2 Using pure Lua:

```lua
-- Method 3: Using io.lines()
local lines = {}
for line in io.lines('path/to/your/file.txt') do
    table.insert(lines, line)
end

-- Method 4: Using io.open()
local function read_file(path)
    local file = io.open(path, "r")
    if not file then return nil end

    local lines = {}
    for line in file:lines() do
        table.insert(lines, line)
    end

    file:close()
    return lines
end

local lines = read_file('path/to/your/file.txt')
```
