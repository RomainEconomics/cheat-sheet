
# Jq-kubernetes

## Examples

### Get all pods names

```bash
k get pods -o json | jq '.items[].metadata.name' -r
```