# Nvim FS Api

| Command                                | Description                                                            |
| -------------------------------------- | ---------------------------------------------------------------------- |
| `vim.fn.glob(pattern)`                 | Returns a list of files matching the given pattern                     |
| `vim.fn.mkdir(path, [parents], )`      | Creates a directory. Set `parents` to "p" to create parent directories |
| `vim.fn.readfile(filename)`            | Reads a file and returns its contents as a list of lines               |
| `vim.fn.writefile(lines, filename)`    | Writes a list of lines to a file                                       |
| `vim.fn.filereadable(filename)`        | Checks if a file exists and is readable                                |
| `vim.fn.filewritable(filename)`        | Checks if a file is writable                                           |
| `vim.fn.isdirectory(path)`             | Checks if a path is a directory                                        |
| `vim.fn.delete(filename)`              | Deletes a file                                                         |
| `vim.fn.rename(src, dst)`              | Renames/moves a file from src to dst                                   |
| `vim.loop.fs_stat(path)`               | Gets file/directory statistics (size, permissions, etc.)               |
| `vim.loop.fs_open(path, flags, mode)`  | Opens a file with specified flags and permissions                      |
| `vim.loop.fs_read(fd, length, offset)` | Reads from an opened file descriptor                                   |
| `vim.loop.fs_write(fd, data, offset)`  | Writes to an opened file descriptor                                    |
| `vim.loop.fs_close(fd)`                | Closes an opened file descriptor                                       |
| `vim.loop.fs_scandir(path)`            | Scans a directory for entries                                          |
| `vim.loop.fs_realpath(path)`           | Returns the resolved absolute path                                     |
| `vim.fn.getcwd()`                      | Gets the current working directory                                     |
| `vim.fn.chdir(path)`                   | Changes the current working directory                                  |
| `vim.fn.expand(expr)`                  | Expands wildcards and special file patterns                            |
| `vim.fn.fnamemodify(filename, mods)`   | Modifies a filename according to specified modifications               |

## Examples

### Reading / Writing files

```lua
-- Reading files
-- 1. Simple file read
local content = vim.fn.readfile("/path/to/file.txt")
-- 2. Read file line by line
local lines = vim.fn.readfile("/path/to/file.txt", "b") -- 'b' for binary mode
-- 3.
local f = io.open(file, 'r')
while true do
  line = f:read()
  if line == nil then
    break
  end
  Snacks.debug(line)
end

-- Writing files
local lines = {"line1", "line2", "line3"}
vim.fn.writefile(lines, "/path/to/file.txt")

```

```lua
-- Directory operations
-- Create directory
vim.fn.mkdir("/path/to/newdir", "p") -- 'p' creates parent directories if needed

-- Check if directory exists
local is_dir = vim.fn.isdirectory("/path/to/dir") -- returns 1 if exists, 0 if not

-- File existence checks
local can_read = vim.fn.filereadable("/path/to/file.txt") -- returns 1 if readable
local can_write = vim.fn.filewritable("/path/to/file.txt") -- returns 1 if writable

-- Get list of files
local files = vim.fn.glob("/path/to/*.lua", false, true) -- returns table of matches

-- Working with paths
-- Get current directory
local cwd = vim.fn.getcwd()
-- Change directory
vim.fn.chdir("/new/path")

-- Using vim.loop (async) functions
-- Get file stats
vim.loop.fs_stat("/path/to/file.txt", function(err, stats)
    if err then
        print("Error:", err)
        return
    end
    print("File size:", stats.size)
    print("Last modified:", stats.mtime.sec)
end)

-- Reading directory contents
local handle = vim.loop.fs_scandir("/path/to/dir")
if handle then
    local name, type = vim.loop.fs_scandir_next(handle)
    while name do
        print(name, type)
        name, type = vim.loop.fs_scandir_next(handle)
    end
end

-- Async file read example
local function read_file_async(path)
    vim.loop.fs_open(path, "r", 438, function(err, fd)
        if err then
            print("Error opening file:", err)
            return
        end

        vim.loop.fs_fstat(fd, function(err, stat)
            if err then
                print("Error getting file stats:", err)
                return
            end

            vim.loop.fs_read(fd, stat.size, 0, function(err, data)
                if err then
                    print("Error reading file:", err)
                    return
                end

                vim.loop.fs_close(fd, function(err)
                    if err then
                        print("Error closing file:", err)
                        return
                    end
                    print("File contents:", data)
                end)
            end)
        end)
    end)
end

-- Path manipulation
local expanded_path = vim.fn.expand("%:p") -- expands current buffer's path
local modified_path = vim.fn.fnamemodify("file.txt", ":p") -- converts to full path
```

### Wrapper

For plugin development, you might want to wrap these in more convenient functions:

```lua
-- Example wrapper for common file operations
local M = {}

M.file_exists = function(path)
    return vim.fn.filereadable(path) == 1
end

M.read_file = function(path)
    if M.file_exists(path) then
        return vim.fn.readfile(path)
    end
    return nil
end

M.write_file = function(path, lines)
    return vim.fn.writefile(lines, path) == 0
end

M.ensure_directory = function(path)
    if not vim.fn.isdirectory(path) then
        vim.fn.mkdir(path, "p")
    end
end

return M
```

### Is Directory ?

`vim.fs.dir(i)` can take an optional `type` field

```lua
for i in vim.fs.dir '.' do
  if vim.fn.isdirectory(i) == 1 then
    print 'is dir'
  end
end

for i, type in vim.fs.dir '.' do
  if type == 'directory' then
    print(i, 'is dir')
  end
end
```
