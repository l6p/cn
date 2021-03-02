---
sort: 3
title: Getting JSON Data
---

# Getting JSON Data

In the following code example, the `SimpleCase` parameters `client` and `logger` are automatically injected by the test framework at runtime.
Call `client.R().Get(...)` to make a GET request, and the returned JSON data is:

```json
{
    "userId": 1,
    "id": 1,
    "title": "delectus aut autem",
    "completed": false
}
```

You can use `resp.D()` to extract the content of JSON data in the test case, for example, `GetInt(...)` for integers, `GetString(...)` for strings.
The parameter of a function like `GetInt` or `GetString` is a path to the value's key.

```tip
`logger.Print(...)` is used to write custom messages in the log, unlike direct printing, `logger.Print(...)` will output the log information asynchronously as JSON format to improve performance.
```

```tip
`time.Sleep(...)` is used to reduce the frequency of test case execution and does not need to be added when actually performing performance tests.
```

## Code example

```go
import (
	"github.com/l6p/utils/client/json"
	"time"
)

func SimpleCase(client *json.Client, logger *log.Logger) {
	resp := client.R().Get("https://jsonplaceholder.typicode.com/todos/1")
	logger.Print("id: ", resp.D().GetInt("id"))
	logger.Print("title: ", resp.D().GetString("title"))
	time.Sleep(5 * time.Second)
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"SimpleCase": SimpleCase,
	}
}
```

## Reference

* [Learn more about how to write JSON path](/Utilities/JsonUtility/SendingJsonRequest.html)
