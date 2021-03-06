---
sort: 6
title: 使用 Chrome 引擎
---

# 使用 Chrome 引擎

在测试用例的入参中声明一个为 `*web.Client` 类型的参数，系统就会自动将 Chrome Headless 引擎注入该参数。

`web.Client` 使用了 [chromedp](https://github.com/chromedp/chromedp){:target="_blank"} 项目并使其使用更加方便。

`web.Client` 使用如下参数初始化了 Chrome Headless 引擎：

| 参数 | 描述 |
| --------- | ----------- |
| --disable-gpu | 禁用 GPU 硬件加速 |
| --no-default-browser-check | 禁用默认浏览器检查 |
| --no-first-run | 跳过浏览器第一次运行的任务 |
| --no-sandbox | 禁用沙箱 |
| --headless | 使用 Headless 模式运行 |
| --hide-scrollbars | 在截屏中隐藏滚动条 |
| --mute-audio | 静音 |

浏览器窗口的大小可以在 Web 管理平台中调整，默认为 **1920 * 1080**。

## 代码示例

```go
package main

import (
	"github.com/l6p/utils/client/web"
	"log"
	"time"
)

func SimpleCase(client *web.Client, logger *log.Logger) error {
	var example string
	client.Go(`https://golang.org/pkg/time/`).
		WaitVisible(`body > footer`).
		Click(`#pkg-examples > div`).
		Value(`#example_After .play .input textarea`, &example).
		Do()

	logger.Printf("Go's time.After example:\n%s", example)
	time.Sleep(10 * time.Second)
	return nil
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"SimpleCase": SimpleCase,
	}
}
```

## 源代码参考

* [使用 Chrome 引擎的测试脚本](https://github.com/l6p/helm/tree/master/examples/using-chrome){:target="_blank"}
* [本地调试 Chrome 引擎的测试脚本](https://github.com/l6p/helm/tree/master/examples/using-chrome-with-local-debug){:target="_blank"}
