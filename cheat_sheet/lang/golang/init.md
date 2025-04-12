# Start a Go Project

```go
go mod init {REMOTE}/{USERNAME}/{PROJECTNAME}
```

The `go run` command quickly compiles and runs a Go package.
The compiled binary is not saved in your working directory.

```go
package main

import "fmt"

func main() {
	fmt.Println("hello world")
}
```

```sh
go run main.go
```

or build and run the binary:

```sh
go build
./PROJECTNAME
```

## Install a Package

```sh
go install
```

The go install command compiles and installs a package or packages on your local machine for your personal usage. It installs the package's compiled binary in the GOBIN directory.
