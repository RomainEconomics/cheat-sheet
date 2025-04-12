# Maps in Go

```go
ages := make(map[string]int)
ages["John"] = 37
ages["Mary"] = 24
ages["Mary"] = 21 // overwrites 24
```

or

```go
ages = map[string]int{
  "John": 37,
  "Mary": 21,
}
```

## Different methods available on Maps

```go
// Insert an element
m[key] = elem

// Get an element
elem = m[key]

// Delete an element
delete(m, key)

// Check if a key exist
elem, ok := m[key]
```

If key is in m, then ok is true and elem is the value as expected.

If key is not in the map, then ok is false and elem is the zero value for the map's element type.

Like slices, maps are also passed by reference into functions. This means that when a map is passed into a function we write, we can make changes to the original, we don't have a copy.

## Keys

Any type can be used as the value in a map, but keys are more restrictive.
Map keys may be of any type that is comparable

Can also use Struct

```go
hits := make(map[string]map[string]int)

map[string]map[string]int
map[rune]map[string]int
map[int]map[string]map[string]int
```
