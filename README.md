# Cheat Sheet

Simple cheat sheet for the most common commands I used in the terminal.

Also used for knowledge.

## Dependencies

- fzf (for fuzzy searching)
- glow (for viewing markdown files)
- neovim (+ snacks picker)

## Usage

```bash
# Clone the repository.
git clone

# Either use the "dark" or "tldr" theme. To use the "tldr" theme, copy the tldr.json file to the glow config directory.
cp tldr.json ~/.config/glow/tldr.json
```

### Using `zsh`

```bash
# Add the following line to your .bashrc or .zshrc file. (Replace CHEAT_SHEET_FOLDER with the path to the cheat_sheet folder.)
cheat-sheet() {
    FOLDER=~/Documents/repos/cheat-sheet/cheat_sheet/

    pushd $FOLDER > /dev/null && \
     fd . -t "file" |
     fzf --ansi --preview 'glow {1} --style dark' |
     xargs --no-run-if-empty glow --style dark
    popd > /dev/null
}

alias ch="cheat-sheet"
```

The alias above will allow you to search for commands in the cheat sheet folder (without having the full path, which allows to have a cleaner search) and preview the markdown file in the terminal.

Note that the path to the tldr.json file may be different on your system. You can use `dark` instead of the `tldr` theme if you prefer a dark theme.

### Using `nushell`

```nu
def cheat_sheet [] {
    cd ~/Documents/repos/cheat-sheet/cheat_sheet/
    let file = fd . -t "file" | fzf --ansi --preview 'bat --color=always {1}'
    glow --style dark $file
}

alias ch = cheat_sheet
```

### Using Neovim and Snacks Picker

```lua
---@module 'snacks'
return {
	'folke/snacks.nvim',
	lazy = false,
	priority = 1000,
    --- ...
	keys = {
		--
		-- ...
		--
		{
			'<leader>cH',
			function() Snacks.picker.files({ cwd = '~/Documents/repos/cheat-sheet/cheat_sheet' }) end,
			desc = 'Find Cheat Sheet',
		},
	},
}

```
