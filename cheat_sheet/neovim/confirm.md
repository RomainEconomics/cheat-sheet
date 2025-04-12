# Confirm in Neovim

```lua
local choice = vim.fn.confirm("Delete ?", "&Yes\n&No")

Snacks.debug(choice)
if choice == 1 then
	Snacks.debug("Deleting")
else
	Snacks.debug("Not deleting")
end

```
