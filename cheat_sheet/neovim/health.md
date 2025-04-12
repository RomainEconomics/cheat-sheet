# Write Health Check for plugins

## Does `X` exists ?

```lua
if vim.fn.executable('curl') == 0 then
	vim.health.error("Curl not installed")
end
```

## Is right version ?

```lua
local res = vim.system({ 'curl', '--version' }, { text = true }):wait()
local version = (vim.version.parse(res.stdout))

if version.major < 8 then
  vim.health.error('curl needs to be x.x.x. Got: ', tostring(version))
end
```

## Is external service accessible ?

```lua
local res = vim.system({ 'curl', 'wttr.in' }, { text = true }):wait()
if res.code ~= 0 then
  vim.health.error('website not accessible')
end
```
