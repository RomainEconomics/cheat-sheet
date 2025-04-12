# Arrays in Go

```go
// Array of 10 int
var myInts [10]int

primes := [6]int{2, 3, 5, 7, 11, 13}
```

## Slices

But in Go, we mosltly use slices, which reference arrays:

```go
primes := [6]int{2, 3, 5, 7, 11, 13}
mySlice := primes[1:4]
```

```go
arrayname[lowIndex:highIndex]
arrayname[lowIndex:]
arrayname[:highIndex]
arrayname[:]
```

Slices hold references to an underlying array, and if you assign one slice to another, both refer to the same array.

Like maps, slices are also passed by reference into functions. This means that when a slice is passed into a function we write, we can make changes to the original, we don't have a copy.

## Create a Slice

```go
mySlice := []string{"I", "love", "go"}
```

Or using `map`:

```go
// func make([]T, len, cap) []T
mySlice := make([]int, 5, 10)

// the capacity argument is usually omitted and defaults to the length
mySlice := make([]int, 5)
```

## Variadic

The spread operator, `...`, allows function to take an arbitrary number of final arguments.

```go
func concat(strs ...string) string {
    final := ""
    // strs is just a slice of strings
    for i := 0; i < len(strs); i++ {
        final += strs[i]
    }
    return final
}

func main() {
    final := concat("Hello ", "there ", "friend!")
    // Output: Hello there friend!
}
```

The familiar fmt.Println() and fmt.Sprintf() are variadic! fmt.Println() prints each element with space delimiters and a newline at the end.

## Append

To dynamically add elements to a slice:

```go
func append(slice []Type, elems ...Type) []Type
```

The append() function changes the underlying array of its parameter AND returns a new slice. This means that using append() on anything other than itself is usually a BAD idea.

```go
// dont do this!
someSlice = append(otherSlice, element)
```

## Slices of slice

Slices can hold other slices, effectively creating a matrix, or a 2D slice.

```go
rows := [][]int{}
```

```go
package main

func createMatrix(rows, cols int) [][]int {
	matrix := make([][]int, rows)

	for i := 0; i < rows; i++ {
		matrix[i] = make([]int, cols)
		for j := 0; j < cols; j++ {
			matrix[i][j] = i * j
		}
	}
	return matrix
}
```

## Loop over a slice - Range

```go
for INDEX, ELEMENT := range SLICE {
}
```
