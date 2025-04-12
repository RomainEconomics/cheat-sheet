# Tables in Lua/Neovim

| Command                                 | Description                                                                |
| --------------------------------------- | -------------------------------------------------------------------------- |
| `local tbl = {}`                        | Create an empty table                                                      |
| `local tbl = {1, 2, 3}`                 | Create and initialize an array-like table                                  |
| `local tbl = {name = "john", age = 25}` | Create and initialize a dictionary-like table                              |
| `table.insert(tbl, value)`              | Insert value at the end of table                                           |
| `table.insert(tbl, pos, value)`         | Insert value at specific position                                          |
| `table.remove(tbl, pos)`                | Remove element at position (defaults to last element if pos not specified) |
| `#tbl`                                  | Get length of sequence-like table                                          |
| `vim.tbl_keys(tbl)`                     | Get all keys from table (Neovim specific)                                  |
| `vim.tbl_values(tbl)`                   | Get all values from table (Neovim specific)                                |
| `vim.tbl_extend("force", tbl1, tbl2)`   | Merge tables (Neovim specific)                                             |
| `vim.deep_equal(tbl1, tbl2)`            | Compare tables deeply (Neovim specific)                                    |

Here are some practical examples:

```lua
-- Creating tables
local array_like = {1, 2, 3, 4, 5}
local dict_like = {
    name = "john",
    age = 25,
    languages = {"lua", "python"}
}
local mixed = {
    1,
    2,
    name = "mixed",
    nested = {x = 1, y = 2}
}

-- Inserting elements
table.insert(array_like, 6)        -- adds to end
table.insert(array_like, 1, 0)     -- adds at position 1

-- Removing elements
table.remove(array_like, 1)        -- removes first element
table.remove(array_like)           -- removes last element

-- Looping through tables
-- For array-like tables:
for i, value in ipairs(array_like) do
    print(i, value)
end

-- For dictionary-like tables:
for key, value in pairs(dict_like) do
    print(key, value)
end

-- Table length
print(#array_like)  -- prints length of array-like table

-- Merging tables (Neovim specific)
local tbl1 = {a = 1, b = 2}
local tbl2 = {b = 3, c = 4}
local merged = vim.tbl_extend("force", tbl1, tbl2)  -- {a = 1, b = 3, c = 4}

-- Checking if key exists
if dict_like.name then
    print("Name exists!")
end

-- Adding/updating values
dict_like.new_key = "new value"    -- Adding new key-value
dict_like.age = 26                 -- Updating existing value

-- Nested tables
local nested = {
    level1 = {
        level2 = {
            value = "deep"
        }
    }
}
print(nested.level1.level2.value)  -- accessing nested values
```

Some Neovim-specific table utilities:

```lua
-- Get all keys
local keys = vim.tbl_keys(dict_like)

-- Get all values
local values = vim.tbl_values(dict_like)

-- Deep copy a table
local copy = vim.deepcopy(dict_like)

-- Check if tables are equal
local is_equal = vim.deep_equal(tbl1, tbl2)

-- Filter a table
local filtered = vim.tbl_filter(function(value)
    return value > 2
end, {1, 2, 3, 4, 5})

-- Map a table
local mapped = vim.tbl_map(function(value)
    return value * 2
end, {1, 2, 3, 4, 5})
```
