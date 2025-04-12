# Working with strings in Neovim

| Command                     | Description                                | Example                                                          |
| --------------------------- | ------------------------------------------ | ---------------------------------------------------------------- |
| `string.format()`           | Formats a string using placeholders        | `local msg = string.format("Hello %s!", "John")` → "Hello John!" |
| `string.sub()`              | Extracts substring from start to end index | `string.sub("Hello", 1, 3)` → "Hel"                              |
| `string.gsub()`             | Global string replacement                  | `string.gsub("hello world", "world", "lua")` → "hello lua"       |
| `string.match()`            | Finds first pattern match in string        | `string.match("hello 123", "%d+")` → "123"                       |
| `string.gmatch()`           | Iterator for pattern matches               | `for num in string.gmatch("123 456", "%d+") do print(num) end`   |
| `string.find()`             | Finds pattern position in string           | `string.find("hello", "ll")` → 3, 4                              |
| `string.len()`              | Returns string length                      | `string.len("hello")` → 5                                        |
| `string.lower()`            | Converts string to lowercase               | `string.lower("HELLO")` → "hello"                                |
| `string.upper()`            | Converts string to uppercase               | `string.upper("hello")` → "HELLO"                                |
| `string.reverse()`          | Reverses a string                          | `string.reverse("hello")` → "olleh"                              |
| `..`                        | String concatenation operator              | `"hello " .. "world"` → "hello world"                            |
| `#`                         | String length operator                     | `#"hello"` → 5                                                   |
| `vim.endswith(s, suffix)`   | Checks if string ends with suffix          | `vim.endswith("test.lua", ".lua")` → `true`                      |
| `vim.startswith(s, prefix)` | Checks if string starts with prefix        | `vim.startswith("test.lua", "test")` → `true`                    |
| `vim.split(s, sep[, opts])` | Splits string by separator                 | `vim.split("a,b,c", ",")` → `{"a", "b", "c"}`                    |
| `vim.trim(s)`               | Removes leading/trailing whitespace        | `vim.trim("  hello  ")` → `"hello"`                              |
| `vim.join(tbl[, sep])`      | Joins table elements with separator        | `vim.join({"a", "b"}, ", ")` → `"a, b"`                          |

Common pattern characters for matching:

- `%d`: digits
- `%s`: whitespace
- `%a`: letters
- `%w`: alphanumeric
- `%p`: punctuation
- `%l`: lowercase letters
- `%u`: uppercase letters
- `+`: one or more occurrences
- `*`: zero or more occurrences
- `?`: zero or one occurrence

Example usage in Neovim configuration:

```lua
-- Replace text in current line
local line = vim.api.nvim_get_current_line()
local new_line = string.gsub(line, "old", "new")
vim.api.nvim_set_current_line(new_line)

-- Format a status message
local filename = vim.fn.expand("%:t")
local msg = string.format("Editing file: %s", filename)
vim.notify(msg)

-- Extract file extension
local fname = "test.lua"
local ext = string.match(fname, "%.(%w+)$")
```

```lua
-- Check file extensions
local function is_lua_file(filename)
    return vim.endswith(filename, ".lua")
end

-- Check file prefixes
local function is_temp_file(filename)
    return vim.startswith(filename, "temp_")
end

-- Split path components
local path = "/home/user/file.txt"
local parts = vim.split(path, "/")
-- parts = {"", "home", "user", "file.txt"}

-- Clean up user input
local user_input = "   some text   "
local cleaned = vim.trim(user_input)
-- cleaned = "some text"

-- Join file extensions
local extensions = {".txt", ".lua", ".md"}
local ext_string = vim.join(extensions, ", ")
-- ext_string = ".txt, .lua, .md"

-- Practical use in a configuration
local function setup_file_types()
    local file_patterns = {
        lua = {"*.lua"},
        python = {"*.py", "*.pyw"},
        markdown = {"*.md", "*.markdown"}
    }

    for ft, patterns in pairs(file_patterns) do
        vim.filetype.add({
            pattern = {
                [".*"] = {
                    priority = -math.huge,
                    function(path)
                        for _, pattern in ipairs(patterns) do
                            if vim.endswith(path, pattern:sub(2)) then
                                return ft
                            end
                        end
                    end,
                },
            },
        })
    end
end

-- Using split for path manipulation
local function get_parent_directory(path)
    local parts = vim.split(path, "/")
    table.remove(parts) -- Remove last element
    return vim.join(parts, "/")
end

-- Using trim in a command
vim.api.nvim_create_user_command("SaveTrimmed", function()
    local lines = vim.api.nvim_buf_get_lines(0, 0, -1, false)
    local trimmed_lines = {}
    for _, line in ipairs(lines) do
        table.insert(trimmed_lines, vim.trim(line))
    end
    vim.api.nvim_buf_set_lines(0, 0, -1, false, trimmed_lines)
end, {})
```

Additional tips:

- The `vim.split()` function accepts an optional table of options:

  ```lua
  local opts = {
    plain = true,    -- Treat separator as plain string, not pattern
    trimempty = true -- Remove empty strings from result
  }
  local parts = vim.split("a,,b", ",", opts)
  -- With trimempty=true: {"a", "b"}
  -- Without trimempty: {"a", "", "b"}
  ```

- You can combine these functions for more complex operations:
  ```lua
  local function get_file_extension(filename)
    if not filename then return nil end
    local parts = vim.split(vim.trim(filename), ".")
    return #parts > 1 and parts[#parts] or nil
  end
  `
  ```
