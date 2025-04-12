---
title: My first presentation
sub_title: (in presenterm!)
author: Me, Myself and I
---

# Welcome to Slides

A terminal based presentation tool

<!-- end_slide -->

Slide title
===

## Everything is markdown

In fact, this entire presentation is a markdown file.

<!-- end_slide -->

## Everything happens in your terminal

Create slides and present them without ever leaving your terminal.

```bash +exec
tmux display-popup
```

<!-- end_slide -->

<!-- column_layout: [3, 2] -->

<!-- column: 0 -->

## Code execution with Go

```go
package main

import "fmt"

func main() {
  fmt.Println("Execute code directly inside the slides")
}
```

<!-- column: 1 -->

```go
package main

import "fmt"

func main() {
  fmt.Println("Execute code directly inside the slides")
}
```


<!-- new_lines: 10 -->

mom

<!-- new_line -->

bye

<!-- end_slide -->

## Pre-process slides

<!-- incremental_lists: true -->

- this
- appears
- one after
- the other

<!-- incremental_lists: false -->

- this appears
- all at once
