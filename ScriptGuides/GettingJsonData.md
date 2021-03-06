---
sort: 3
title: 在测试用例中发送 API 请求
---

# 在测试用例中发送 API 请求

在下面的代码示例中，`SimpleCase` 方法的参数 `client` 和 `logger` 是由测试框架自动注入，以便帮助您发送 API 请求和输出自定义日志信息。
调用 `client.R().Get(...)` 来发送一个 **GET** 请求。假设该请求返回的 JSON 数据为：

```json
{
    "userId": 1,
    "id": 1,
    "title": "delectus aut autem",
    "completed": false
}
```

您可以在测试用例中使用 `resp.D()` 来获得该 JSON 数据，并且使用例如：`GetInt(...)` 获取整数值，`GetString(...)` 获取字符串值。
`GetInt` 或 `GetString` 方法的入参为一个定位要获取值的所在位置的路径。

```tip
使用 `logger.Print(...)` 用于在测试用例中输出自定义日志，输出的内容会被异步地以 JSON 格式输出到 Worker 节点的日志中。
```

```tip
使用 `time.Sleep(...)` 的目的是在运行的时候减缓测试用例的执行频率。
```

## 代码示例

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

## 进一步阅读

* [如何书写 JSON 路径](/cn/Utilities/JsonUtility/SendingJsonRequest.html)
