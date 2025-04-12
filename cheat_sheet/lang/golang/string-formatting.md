# Working with Strings in Go

- `fmt.Printf` - Prints a formatted string to standard out.
- `fmt.Sprintf()` - Returns the formatted string
  - use `v` for value as default

```go
s := fmt.Sprintf("I am %v years old", 10)
// I am 10 years old

s := fmt.Sprintf("I am %v years old", "way too many")
// I am way too many years old

s := fmt.Sprintf("I am %s years old", "way too many")
s := fmt.Sprintf("I am %d years old", 10)
s := fmt.Sprintf("I am %f years old", 10.523)
s := fmt.Sprintf("I am %.2f years old", 10.523)

```

## Runes and String Encoding

In many programming languages (cough, C, cough), a "character" is a single byte. Using ASCII encoding, the standard for the C programming language, we can represent 128 characters with 7 bits. This is enough for the English alphabet, numbers, and some special characters.

In Go, strings are just sequences of bytes: they can hold arbitrary data. However, Go also has a special type, rune, which is an alias for int32. This means that a rune is a 32-bit integer, which is large enough to hold any Unicode code point.

When you're working with strings, you need to be aware of the encoding (bytes -> representation). Go uses UTF-8 encoding, which is a variable-length encoding.

1. When you need to work with individual characters in a string, you should use the rune type. It breaks strings up into their individual characters, which can be more than one byte long.
2. We can use zany characters like emojis and Chinese characters in our strings, and Go will handle them just fine.
