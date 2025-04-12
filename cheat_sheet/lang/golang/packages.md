# Packages in Go

Every Go program is made up of packages.

- A package named `main` has an entrypoint at the main() function. A main package is compiled into an **executable program**.
- A package by any other name is a **library package**. Libraries have no entry point. Libraries simply export functionality that can be used by other packages.

For example:

```go
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("My favorite number is", rand.Intn(10))
}
```

## Package Naming

By convention, a package's name is the same as the last element of its import path. For instance, the `math/rand` package comprises files that begin with:

```go
package rand
```

**A directory of Go code can have at most one package.**

All .go files in a single directory must all belong to the same package.

If they don't, an error will be thrown by the compiler. This is true for main and library packages alike.

## Modules

Go programs are organized into packages.

A package is a directory of Go code that's all compiled together.

Functions, types, variables, and constants defined in one source file are visible to all other source files within the same package (directory).

A **repository** contains one or more modules.
A **module** is a collection of Go packages that are released together.

A file named `go.mod` at the root of a project declares the module.

It contains:

- The module path
- The version of the Go language your project requires
- Optionally, any external package dependencies your project has

The module path is just the import path prefix for all packages within the module.

Here's an example of a go.mod file:

```go
module github.com/bootdotdev/exampleproject

go 1.23.0

require github.com/google/examplepackage v1.3.0
```
