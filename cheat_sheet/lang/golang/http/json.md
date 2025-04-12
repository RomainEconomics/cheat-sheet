# Working with JSON in Go

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

## Marshall

```go
type Board struct {
	Id       int    `json:"id"`
	Name     string `json:"name"`
	TeamId   int    `json:"team"`
	TeamName string `json:"team_name"`
}

board := Board{
	Id:       1,
	Name:     "API",
	TeamId:   9001,
	TeamName: "Backend",
}

data, err := json.Marshal(board)
if err != nil {
	log.Fatal(err)
}
fmt.Println(string(data))
// {
```

```go
package main

import (
	"encoding/json"
)

func marshalAll[T any](items []T) ([][]byte, error) {
	var res [][]byte
	for _, item := range items {
		data, err := json.Marshal(item)
		if err != nil {
			return res, err
		}
		res = append(res, data)
	}
	return res, nil
}

```

When you don't want to create a struct, use an interface (equivalent to `any`).

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	var data map[string]interface{}
	jsonString := `{"name": "Alice", "age": 30, "address": {"city": "Wonderland"}}`
	json.Unmarshal([]byte(jsonString), &data)
	fmt.Println(data["name"]) // Output: Alice
	fmt.Println(data["address"].(map[string]interface{})["city"])

}
```
