---
sort: 4
title: SetUp And TearDown
---

# SetUp And TearDown

Add **SetUp** and **TearDown** functions to the test script, and passes the references to the framework via the **Export** function.

```tip
**setUp** and **tearDown** are reserved keywords for registering the SetUp and TearDown functions with the framework.
```

**SetUp** and **TearDown** will only be run once by a worker during the entire test, before the test starts and before it ends, respectively.

## Code example

```go
package main

import (
	"github.com/l6p/utils/client/json"
	"log"
	"time"
)

func SetUp(logger *log.Logger) {
	logger.Print("SetUp has been executed.")
}

func TearDown(logger *log.Logger) {
	logger.Print("TearDown has been executed.")
}

func SimpleCase(client *json.Client) {
	_ = client.R().Get("https://jsonplaceholder.typicode.com/todos/1")
	time.Sleep(5 * time.Second)
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"setUp": SetUp,
		"tearDown": TearDown,
		"SimpleCase": SimpleCase,
	}
}
```

## Reference

* [An example of a test script with SetUp and TearDown](https://github.com/l6p/helm/tree/master/examples/setUp-and-tearDown){:target="_blank"}
