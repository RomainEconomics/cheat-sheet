# Variables in Go

```go
var intVar int
var floatVar float64
var boolVar bool
var stringVar string

s := "Happy birthday! You are now"
a := 21
s2 := "years old!"
```

## Types

The size (8, 16, 32, 64, 128, etc) represents how many bits in memory will be used to store the variable. The "default" int and uint types refer to their respective 32 or 64-bit sizes depending on the environment of the user.

```go
// Whole numbers
int  int8  int16  int32  int64

// Positive whole numbers
uint uint8 uint16 uint32 uint64 uintptr

// Signed decimal numbers
float32 float64

// Imaginary numbers
complex64 complex128
```

## Conversion

```go
temperatureFloat := 88.26
temperatureInt := int64(temperatureFloat)
```
