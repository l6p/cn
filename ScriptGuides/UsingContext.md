---
sort: 5
title: Using Context
---

# Using Context In Testing

Use context to exchange data between test cases or use context to pass the dynamic data needed for testing.

First declare a structure to hold the data in the context.
For example, in the following example, a structure called `Context` is declared,
and a field called `BaseUrl` is declared in it to store the base url of the back-end API.

```go
type Context struct {
	BaseUrl string
}
```

Initialize the `Context` in the `Export` function, and export it to the test framework with the `context` key.

```go
func Export() map[string]interface{} {
	return map[string]interface{}{
		"context": Context{
			BaseUrl: "https://jsonplaceholder.typicode.com",
		},
		"SimpleCase": SimpleCase,
	}
}
```

Using context in a test case simply requires defining a parameter of the `Context` pointer type on the test case:

```go
func SimpleCase(ctx *Context, client *json.Client) {
	_ = client.R().Get(fmt.Sprintf("%s/todos/1", ctx.BaseUrl))
	time.Sleep(5 * time.Second)
}
```

In the above example the API base url will be taken from the `Context` instead of being hardcoded in the test case.

## Code example

```go
import (
	"fmt"
	"github.com/l6p/utils/client/json"
	"time"
)

type Context struct {
	BaseUrl string
}

func SimpleCase(ctx *Context, client *json.Client) {
	_ = client.R().Get(fmt.Sprintf("%s/todos/1", ctx.BaseUrl))
	time.Sleep(5 * time.Second)
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"context": Context{
			BaseUrl: "https://jsonplaceholder.typicode.com",
		},
		"SimpleCase": SimpleCase,
	}
}
```

## Reference

* [An example of a test script that uses Context](https://github.com/l6p/helm/tree/master/examples/simple-context){:target="_blank"}
* [An example of synchronizing Context data](https://github.com/l6p/helm/tree/master/examples/sync-context){:target="_blank"}
* [An example of using Context to pass parameters](https://github.com/l6p/helm/tree/master/examples/context-parameter){:target="_blank"}
