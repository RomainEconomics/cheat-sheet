# Jq

## Links

- [jq Manual](https://stedolan.github.io/jq/manual/)

## Examples

```
URL="https://api.github.com/repos/jqlang/jq/issues\?per_page\=2"

```

### Selecting by array index and a specific field

```bash
curl URL | jq '.[0].title'
```

### Selecting multiple fields and constructing a new object

```bash
curl URL | jq '.[] | {title: .title, url: .url}'
curl URL | jq '.[] | {title, url}'
```

### Creating a new array object and sorting it

```bash
curl URL | jq '[ .[] | {title, url, number} ]' | jq 'sort'
curl URL | jq '[ .[] | {title, url, number} ]' | jq 'sort_by(.number)'
```

### Get the length of a field in an array

We can also use the pipe inside the object to create a new field, here using the length function.

```bash
curl URL | jq '[ .[] | {title, url} ]' | jq '.[].title | length'
curl URL | jq '[ .[] | {title, url, number, count: .title | length} ]'
```

### Selecting by field value

```bash
curl URL | jq '.[] | select(.number == 1)'
curl URL | jq '.[] | select(.title == "Title")'
curl URL | jq '.[] | select(.title == "Title" and .number == 1)'
curl URL | jq '.[] | select(.title | contains("Title"))'
```

### Read Json line format

```bash
cat file.json | jq -s
```

