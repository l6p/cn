---
sort: 1
title: 发送 JSON 请求
---

# 发送 JSON 请求

首先在测试脚本的根目录中运行：

```shell
go get github.com/l6p/utils
```

在为测试脚本添加了 `github.com/l6p/utils` 的依赖之后，在测试用例的入参中声明一个为 `*json.Client` 类型的参数，系统就会自动将工具库注入该参数：

`json.Client` 封装了 [Go Resty](https://github.com/go-resty/resty){:target="_blank"} 项目并使处理 JSON 的方式变得更加方便。

## 请求并处理 JSON 数据

使用 `json.Client` 的 `R()` 方法来创建一个 JSON 请求对象，再使用请求的 `Get(...)` 方法可以执行 GET 请求并获取返回对象。
通过返回对象的 `D()` 方法来获取 API 返回的 JSON 数据对象。

JSON 数据对象是 `json.Data` 类型，这个对象提供了一些方法可以让我们方便的处理 JSON 数据：
- [按照路径获取数据](/cn/Utilities/JsonUtility/ReadingDataByPath.html)
- [在数组中过滤数据](/cn/Utilities/JsonUtility/FilteringElementsInArray.html)
- [更改数据](/cn/Utilities/JsonUtility/ModifyingData.html)
- [合并 JSON 数据](/cn/Utilities/JsonUtility/MergingJsonData.html)

## 提交 JSON 数据

使用 JSON 请求对象的 `Post(...)` 方法来执行 POST 请求并获取返回对象。
在调用 `Post(...)` 方法之前可以使用 `J(...)` 方法来设置需要提交的 JSON 数据，例如：

```go
client.R().J(`
{
    "title": "foo",
    "body": "bar",
    "userId": 1
}
`).Post("https://jsonplaceholder.typicode.com/posts")
```

如果已经具有 `json.Data` 类型的数据对象则可以使用 `json.Request` 的 `D(...)` 方法代替 `J(...)` 方法来设置提交数据。
