---
sort: 5
title: 使用测试上下文
---

# 使用测试上下文

**测试上下文**可用于在测试用例之间传递数据和存放自定义参数。

首先要在测试脚本中声明一个用于测试上下文使用的结构体。
例如在下面的代码示例中，声明了一个命名为 `Context` 的结构体类型，并且在该类型中定义了一个字段叫 `BaseUrl` 用于存放请求的API的基础 URL。

```go
type Context struct {
	BaseUrl string
}
```

在 **Export** 方法输出的 **map** 中的键值 `context` 是**保留字**，用于向系统输出测试上下文的初始值。

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

在测试用例的入参中声明一个为 `Context` 指针类型的参数，系统就会自动将测试上下文注入该参数：

```go
func SimpleCase(ctx *Context, client *json.Client) {
	_ = client.R().Get(fmt.Sprintf("%s/todos/1", ctx.BaseUrl))
	time.Sleep(5 * time.Second)
}
```

在上面的代码片段中调用 API 的URL将基于测试上下文中保存的基础 URL 生成。

## 代码示例

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

## 源代码参考

* [使用测试上下文的测试脚本](https://github.com/l6p/helm/tree/master/examples/simple-context){:target="_blank"}
* [使用测试上下文在 Worker 节点间同步数据](https://github.com/l6p/helm/tree/master/examples/sync-context){:target="_blank"}
* [使用测试上下文保存自定义参数](https://github.com/l6p/helm/tree/master/examples/context-parameter){:target="_blank"}
