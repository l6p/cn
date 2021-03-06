---
sort: 2
title: 使用自定义的测试数据
---

# 使用自定义的测试数据

为了更加灵活的运行测试，Lollipop 提供了动态地把自定义参数注入到测试脚本中的功能。

首先在**测试上下文**中定义用来接收动态参数的字段。您需要用 `l6p` 的标签来标注这些字段。
例如在下面的示例中 `SleepSeconds` 这个字段是用于接收自定义参数的。

```tip
注意 "sync" 是保留关键字，用于在 Worker 之间同步数据，不可用于标注字段。
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

当创建性能测试时，系统如果发现测试脚本中有自定义参数，则会提供单独的对话窗口供您填写参数。
当前参数只支持 `int`、 `string` 和 `float` 类型。

<style>
    img[alt=pic00000002] { 
        display: block;
        width: 660px; 
    }
</style>
![pic00000002](/assets/images/pic00000002.png)

从界面上输入的数值，例如给 `sleepSeconds` 赋值10秒，会在测试开始时自动注入到测试中。
以上面的脚本为例，通过动态参数我们可以自由的选择 `SimpleCase` 这个测试用例在单个 Worker 上运行的时间间隔，从而防止给予被测系统太高的负载。

## 进一步阅读

* [关于测试上下文](/cn/ScriptGuides/UsingContext.html)
