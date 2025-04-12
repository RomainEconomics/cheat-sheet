# Requests in Go

We can decode JSON bytes (or strings) into a Go struct using json.Unmarshal or a json.Decoder.

The Decode method of `json.Decoder` streams data from an io.Reader into a Go struct, while `json.Unmarshal` works with data that's already in []byte format.

Using a json.Decoder can be more memory-efficient because it doesn't load all the data into memory at once.
json.Unmarshal is ideal for small JSON data you already have in memory.

When dealing with HTTP requests and responses, you will likely use json.Decoder since it works directly with an io.Reader.

## Using Decoder

```go
package main

import (
	"fmt"
	"net/http"
	"encoding/json"
)

type Issue struct {
	Title    string `json:"title"`
	Estimate int    `json:"estimate"`
}


func getIssues(url string) ([]Issue, error) {
	res, err := http.Get(url)
	if err != nil {
		return nil, fmt.Errorf("error creating request: %w", err)
	}
	defer res.Body.Close()

	var issues []Issue
	decoder := json.NewDecoder(res.Body)
	if err := decoder.Decode(&issues); err != nil {
		return nil, err
	}
	return issues, nil
}

```

## Using Unmarshal

```go
package main

import (
	"encoding/json"
	"fmt"
	"io"
	"net/http"
)

type Issue struct {
	Title    string `json:"title"`
	Estimate int    `json:"estimate"`
}

func getIssues(url string) ([]Issue, error) {
	res, err := http.Get(url)
	if err != nil {
		return nil, fmt.Errorf("error creating request: %w", err)
	}
	defer res.Body.Close()

	data, err := io.ReadAll(res.Body)
	if err != nil {
		return nil, err
	}

	var issues []Issue
	if err = json.Unmarshal(data, &issues); err != nil {
		return nil, err
	}

	return issues, nil
}

```

## Http Client

This allows to modify the headers, timeouts, and other settings of the request.

```go
client := &http.Client{
	Timeout: time.Second * 10,
}

req, err := http.NewRequest("GET", "https://jsonplaceholder.typicode.com/users", nil)
if err != nil {
	log.Fatal(err)
}

resp, err := client.Do(req)
```
