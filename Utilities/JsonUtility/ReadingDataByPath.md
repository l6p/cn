---
sort: 2
title: 按照路径获取数据
---

# 按照路径获取数据

最基本的路径只包括**键值**和**逗点**，例如基于下面的 JSON 数据：

```go
d := json.D(`
    {
        "key1": "value1",
        "key2": {
            "key21": "value2"
        }
    }
`)
```

使用 `key1` 作为路径来得到 `value1`，例如： 

```go
d.GetString("key1")
```

使用 `key2.key21` 作为路径来得到 `value2`，例如：

```go
d.GetString("key2.key21")
```

## 从数组中读取数据

基于下面的 JSON 数据：

```go
d := json.D(`
    {
        "key1": [10, 20, 30]
    }
`)
```

使用 `key1[1]` 作为路径来得到 `20`，例如：

```go
d.GetInt("key1[1]")
```
