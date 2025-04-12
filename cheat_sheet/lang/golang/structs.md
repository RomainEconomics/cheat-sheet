# Structs in Go

## Struct

```go
type car struct {
  brand string
  model string
}
```

## Anonymous Struct

May be useful when processing JSON for ex

```go
myCar := struct {
  brand string
  model string
} {
  brand: "tesla",
  model: "model 3",
}
```

## Methods

```go
package main

type authenticationInfo struct {
	username string
	password string
}

func (info authenticationInfo) getBasicAuth() string {
	return "Authorization: Basic " + info.username + ":" + info.password
}
```

## Memory layout

```go
type stats struct {
	Reach    uint16
	NumPosts uint8
	NumLikes uint8
}
```

Each `stats` struct would use 4 bytes:

- uint16: 2 bytes
- uint8: 1 bytes

Field ordering impact the memory layout:

```go
type stats struct {
	NumPosts uint8
	Reach    uint16
	NumLikes uint8
}
```

Each `stats` struct would use 6 bytes:

- uint8: 1 bytes + wasted 1 byte
- uint16: 2 bytes
- uint8: 1 bytes + wasted 1 byte

## Empty Struct

```go
// anonymous empty struct type
empty := struct{}{}

// named empty struct type
type emptyStruct struct{}
empty := emptyStruct{}
```

Use 0 bytes of memory.
Useful for channels and maps.
