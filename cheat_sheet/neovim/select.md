# Select from a table

```lua
local models = { "LLM", "OpenAI", "Machine" }
vim.ui.select(models, { prompt = "Model:" }, function(item)
	Snacks.debug(item)
end)

```
