# Errors in Go

In Go, errors are simply values of any type that implements the simple built-in error interface:

```go
type error interface {
    Error() string
}
```

Exemple:

```go
func Atoi(s string) (int, error)
```

```go
// Atoi converts a stringified number to an integer
i, err := strconv.Atoi("42b")
if err != nil {
    fmt.Println("couldn't convert:", err)
    return
}
```

## Errors builtin Go package

```go
package main

import (
	"errors"
)

func divide(x, y float64) (float64, error) {
	if y == 0 {
		return 0., errors.New("no dividing by 0")
	}
	return x / y, nil
}
```

## Implement custom Error

```go
package main

import (
	"fmt"
)

type divideError struct {
	dividend float64
}

func (e divideError) Error() string {
	return fmt.Sprintf("can not divide %v by zero", e.dividend)
}

func divide(dividend, divisor float64) (float64, error) {
	if divisor == 0 {
		return 0, divideError{dividend: dividend}
	}
	return dividend / divisor, nil
}

```
