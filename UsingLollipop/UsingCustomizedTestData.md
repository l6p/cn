---
sort: 2
title: Using Customized Test Data
---

# Using Customized Test Data

For more flexibility in running tests, the system allows custom data to be passed into the test script.

The first step is to define the fields in the **Context** where the data needs to be provided dynamically.
You need to tag the custom fields, such as `l6p:"sleepSeconds"`.

```tip
Note that `l6p:"sync"` is reserved and cannot be used to pass data.
```

```go
package main

import (
	"fmt"
	"github.com/l6p/utils/client/json"
	"math/rand"
	"time"
)

type Context struct {
	BaseUrl      string
	SubPaths     []string `l6p:"sync"`
	SleepSeconds int      `l6p:"sleepSeconds"`
}

func SetUp(ctx *Context) {
	ctx.SubPaths = []string{
		"/users",
		"/todos",
		"/posts",
	}
}

func SimpleCase(ctx *Context, client *json.Client) {
	subPath := ctx.SubPaths[rand.Intn(len(ctx.SubPaths))]
	_ = client.R().Get(fmt.Sprintf("%s%s", ctx.BaseUrl, subPath))
	time.Sleep(time.Duration(ctx.SleepSeconds) * time.Second)
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"context": Context{
			BaseUrl: "https://jsonplaceholder.typicode.com",
		},
		"setUp":      SetUp,
		"SimpleCase": SimpleCase,
	}
}
```

In the above example `SleepSeconds` is a custom field defined in the **Context**.
When creating a test, the system prompts the user to assign a value to this field, 
which currently only supports `int`, `string` and `float`.

<style>
    img[alt=pic00000002] { 
        display: block;
        width: 660px; 
    }
</style>
![pic00000002](/assets/images/pic00000002.png)

## Reference

* [Learn more about the test context](/ScriptGuides/UsingContext.html)
