# Channels in Go

**Channels** are:

- a typed
- thread-safe queue

Channels allow different **goroutines** to communicate with each other.

```go
ch := make(chan int)

// Send a value to the channel
ch <- 69

// Receive a value from the channel
v := <- ch
```

The `<-` operator is called the **channel operator**.
Data flows in the direction of the arrow.
This operation will block until another **goroutine** is ready to receive the value.

`v := <- ch` reads and removes a value from the channel and saves it into the variable v.
This operation will block until there is a value in the channel to be read.

Careful:

- Reading from an empty channel will block the goroutine until a value is sent.
- Reading from a nil channel will block forever.
- Sending to a channel will block until another goroutine is ready to receive the value.
- Sending to a closed channel will panic.

## Empty Structs

Empty structs are often used as a unary value.
Sometimes, we don't care what is passed through a channel. We care when and if it is passed.

We can block and wait until something is sent on a channel using the following syntax

```go
package main

import "fmt"

func waitForDBs(numDBs int, dbChan chan struct{}) {
	for i := 0; i < numDBs; i++ {
		<-dbChan
	}
}

func getDBsChannel(numDBs int) (chan struct{}, *int) {
	count := 0
	ch := make(chan struct{})

	go func() {
		for i := 0; i < numDBs; i++ {
			ch <- struct{}{}
			fmt.Printf("Database %v is online\n", i+1)
			count++
		}
	}()

	return ch, &count
}
```

## Buffered Channels

You can provide a buffer length as the second argument to make() to create a buffered channel:

```go
ch := make(chan int, 100)
```

A buffer allows the channel to hold a fixed number of values before sending blocks.
This means sending on a buffered channel only blocks when the buffer is full, and receiving blocks only when the buffer is empty.

## Closing Channels

You can close a channel using the `close()` function.

```go
close(ch)
```

You can check if a channel is closed using the following syntax:

```go
v, ok := <-ch
```

ok is `false` if the channel is empty and closed.

Sending on a closed channel will cause a panic. A panic on the main goroutine will cause the entire program to crash, and a panic in any other goroutine will cause that goroutine to crash.

Closing isn't necessary. There's nothing wrong with leaving channels open, they'll still be garbage collected if they're unused. You should close channels to indicate explicitly to a receiver that nothing else is going to come across.

## Range Over Channels

Similar to slices and maps, channels can be ranged over.

```go
for item := range ch {
    // item is the next value received from the channel
}
```

This example will receive values over the channel (blocking at each iteration if nothing new is there) and will exit only when the channel is closed.

## Select

Sometimes we have a single goroutine listening to multiple channels and want to process data in the order it comes through each channel.

A select statement is used to listen to multiple channels at the same time. It is similar to a switch statement but for channels.

```go
select {
    case i, ok := <- chInts:
	fmt.Println(i)
    case s, ok := <- chStrings:
	fmt.Println(s)
    default:
	fmt.Println("No value ready, moving on.")
}
```

The first channel with a value ready to be received will fire and its body will execute.
If multiple channels are ready at the same time one is chosen randomly.
The ok variable in the example above refers to whether or not the channel has been closed by the sender yet.

The default case in a select statement executes immediately if no other channel has a value ready.
A default case stops the select statement from blocking.

## Read-only Channels

A channel can be marked as read-only by casting it from a chan to a <-chan type. For example:

```go
func main() {
    ch := make(chan int)
    readCh(ch)
}

func readCh(ch <-chan int) {
    // ch can only be read from in this function
}
```

## Write-only Channels

The same goes for write-only channels, but the arrow's position moves.

```go
func writeCh(ch chan<- int) {
    // ch can only be written to in this function
}
```
