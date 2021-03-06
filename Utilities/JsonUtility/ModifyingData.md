---
sort: 4
title: 更改数据
---

# 更改数据

`json.Data` 对象提供了修改它所封装的数据的功能，例如基于下面的 JSON 数据：

```go
d := json.D(`
    {
        "key1": "value1",
        "key2": {
            "key21": 0
        },
        "key3": [10, 20]
    }
`)
```

## 重新赋值

当下面代码执行以后：

```go
d.SetString("key1", "foo")
d.SetInt("key2.key21", 10)
```

示例中的 JSON 数据会改变成：

```json
{
    "key1": "foo",
    "key2": {
        "key21": 10
    },
    "key3": [10, 20]
}
```

## 在数组后增加数据

进一步的执行下面代码后：

```go
d.AppendInt("key3", 30)
```

JSON 数据会进一步改变成：

```json
{
    "key1": "foo",
    "key2": {
        "key21": 10
    },
    "key3": [10, 20, 30]
}
```

## 删除数据

然后继续执行下面的代码：

```go
d.Delete("key2")
```

JSON 数据会最终改变成：

```json
{
    "key1": "foo",
    "key3": [10, 20, 30]
}
```
