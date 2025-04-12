

# System


## Examples

### Display all space used by Docker

```bash
docker system df
docker system df -v
```

### Remove all unused containers, networks, images (both dangling and unreferenced), and build cache

```bash
docker system prune
```

### Remove unused images

```bash
docker image prune
docker image prune --all
```