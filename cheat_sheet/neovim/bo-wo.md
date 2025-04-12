# Buffer and Windows Options

Key differences:

• `bo` affects how the buffer content is stored and interpreted
• `wo` affects how the content is displayed in a window

Let me explain the bo and wo options in Neovim:

1. bo (Buffer Options):

• bo is used to set or get options that are local to a specific buffer
• These options apply only to the current buffer being edited
• Syntax: vim.bo[buffer_number].option_name

Common examples:

```lua
-- Set file type for current buffer
vim.bo.filetype = "lua"

-- Set tab settings for current buffer
vim.bo.expandtab = true
vim.bo.shiftwidth = 2

-- Set file format
vim.bo.fileformat = "unix"

-- Set buffer-specific options
vim.bo.modifiable = true
vim.bo.readonly = false
```

2 wo (Window Options):

• wo is used to set or get options that are local to a specific window
• These options apply to how the content is displayed in a particular window
• Syntax: `vim.wo[window_number]`.option_name

Common examples:

```lua
-- Set line numbers in current window
vim.wo.number = true
vim.wo.relativenumber = true

-- Set fold settings for current window
vim.wo.fold = true
vim.wo.foldmethod = "indent"

-- Set cursor line highlighting
vim.wo.cursorline = true

-- Set window-specific wrap settings
vim.wo.wrap = false
vim.wo.linebreak = true
```

You can also use these in combination:

```lua
-- Configure a specific buffer and its window
local buf = vim.api.nvim_create_buf(false, true)
local win = vim.api.nvim_open_win(buf, true, {
	relative = "editor",
	width = 80,
	height = 24,
	row = 2,
	col = 2
})

vim.bo[buf].filetype = "markdown"
vim.wo[win].number = true
```

```lua
-- File and Buffer Related
vim.bo.fileformat     -- File format (unix, dos, mac)
vim.bo.filetype       -- Type of file
vim.bo.buftype        -- Type of buffer
vim.bo.modified       -- Whether buffer has been modified
vim.bo.modifiable     -- Whether buffer can be modified
vim.bo.readonly       -- Whether buffer is read-only

-- Indentation and Formatting
vim.bo.expandtab      -- Convert tabs to spaces
vim.bo.shiftwidth     -- Number of spaces for indentation
vim.bo.tabstop        -- Number of spaces a tab counts for
vim.bo.softtabstop    -- Number of spaces for a tab in editing
vim.bo.textwidth      -- Maximum width of text
vim.bo.cindent        -- C-style indentation
vim.bo.smartindent    -- Smart autoindenting
vim.bo.autoindent     -- Copy indent from current line

-- Syntax and Search
vim.bo.syntax         -- Syntax highlighting
vim.bo.swapfile       -- Whether to use a swapfile
vim.bo.undofile       -- Whether to use an undo file
vim.bo.spelllang      -- Language(s) for spell checking
vim.bo.spellfile      -- File containing spell checking words

-- File Encoding
vim.bo.fileencoding   -- File encoding for current buffer
vim.bo.bomb           -- Prepend BOM to file
```

```lua
-- Display Numbers
vim.wo.number         -- Show line numbers
vim.wo.relativenumber -- Show relative line numbers
vim.wo.signcolumn     -- Show sign column ("yes", "no", "auto")

-- Folding
vim.wo.fold           -- Enable folding
vim.wo.foldmethod     -- Folding method (manual, indent, syntax, etc.)
vim.wo.foldlevel      -- Folds with level higher than this are closed
vim.wo.foldcolumn     -- Width of fold column
vim.wo.foldenable     -- Enable folding

-- Display and Visual
vim.wo.wrap           -- Line wrapping
vim.wo.linebreak      -- Wrap lines at convenient points
vim.wo.list           -- Show invisible characters
vim.wo.cursorline     -- Highlight current line
vim.wo.cursorcolumn   -- Highlight current column
vim.wo.colorcolumn    -- Highlight specific column(s)
vim.wo.conceallevel   -- How concealed text is shown

-- Scrolling
vim.wo.scroll         -- Number of lines to scroll
vim.wo.scrolloff      -- Min number of lines above/below cursor
vim.wo.sidescrolloff  -- Min number of columns left/right of cursor

-- Window Specific
vim.wo.winfixheight   -- Keep window height
vim.wo.winfixwidth    -- Keep window width
vim.wo.winhl         -- Window-local highlights
vim.wo.preview        -- Identify preview window

-- Diff Mode
vim.wo.diff           -- Show differences
vim.wo.diffopt        -- Options for diff mode

-- Status
vim.wo.statusline     -- Custom status line
vim.wo.winbar         -- Custom window bar
```

```lua
-- Set up a buffer for Python development
vim.bo.expandtab = true
vim.bo.shiftwidth = 4
vim.bo.tabstop = 4
vim.bo.filetype = "python"

-- Configure window display
vim.wo.number = true
vim.wo.relativenumber = true
vim.wo.signcolumn = "yes"
vim.wo.cursorline = true

-- Set up folding
vim.wo.foldmethod = "indent"
vim.wo.foldlevel = 99
vim.wo.foldenable = true

-- Configure wrapping
vim.wo.wrap = false
vim.wo.linebreak = true
vim.wo.colorcolumn = "80"
```
