---
sort: 4
title: SetUp 和 TearDown
---

# SetUp 和 TearDown

创建两个函数 **SetUp** 和 **TearDown**，分别用于定义在 **SetUp** 阶段和 **TearDown** 阶段需要执行的过程。
并且把这两个函数的引用通过 **Export** 函数输出给框架。

```tip
在 **Export** 函数输出的 **map** 中的键值 `setUp` 和 `tearDown` 是**保留字**，不能用于输出测试用例。
```

**SetUp** 和 **TearDown** 函数只会在测试开始之前和完全结束之前被一个 Worker 节点运行一次。

## 代码示例

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

## 源代码参考

* [使用 SetUp 和 TearDown 的测试脚本](https://github.com/l6p/helm/tree/master/examples/setUp-and-tearDown){:target="_blank"}
