

# Grep


## Examples

### Display 2 line above and below using JQ and Grep

```bash
bat file.json | jq | grep -A 2 -B "PATTERN"
```
