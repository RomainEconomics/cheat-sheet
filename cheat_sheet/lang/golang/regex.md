# Regex in Go

```go
package main

import (
    "bytes"
    "fmt"
    "regexp"
)

func main() {

    match, _ := regexp.MatchString("p([a-z]+)ch", "peach")
    match // true

    r, _ := regexp.Compile("p([a-z]+)ch")

    r.MatchString("peach") // true

    r.FindString("peach punch") // peach

    r.FindStringIndex("peach punch") // [0 5]

    r.FindStringSubmatch("peach punch") // [peach ea]

    r.FindStringSubmatchIndex("peach punch") // [0 5 1 3]

    r.FindAllString("peach punch pinch", -1) // [peach punch pinch]

    r.FindAllStringSubmatchIndex("peach punch pinch", -1) // [[0 5 1 3] [6 11 7 9] [12 17 13 15]]

    r.FindAllString("peach punch pinch", 2)) // [peach punch]

    r = regexp.MustCompile("p([a-z]+)ch")

    r.ReplaceAllString("a peach", "<fruit>") // a <fruit>

    in := []byte("a peach")
    out := r.ReplaceAllFunc(in, bytes.ToUpper)
    string(out) // a PEACH
}
```
