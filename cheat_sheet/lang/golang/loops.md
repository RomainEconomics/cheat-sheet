# Loops in Go

```go
for INITIAL; CONDITION; AFTER{
  // do something
}

for i := 0; i < 10; i++ {
  fmt.Println(i)
}

// While loop
i := 1
for i < 5 {
  i++
}
```

## Loop over a slice

```go
for INDEX, ELEMENT := range SLICE {
}
```
