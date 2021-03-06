---
sort: 3
title: 在数组中过滤数据
---

# 在数组中过滤数据

基于下面的 JSON 数据：

```go
d := json.D(`
    {
        "records": [
            {
                "key": "k1",
                "value": "v1"
            },
            {
                "key": "k2",
                "value": "v2"
            }
        ]
    }
`)
```

如果想要获取键值为 `k2` 的数据项并且读取 `value` 字段的值，可以这样做：

```go
d.Filter("records", func(data *json.Data) bool {
    return data.GetString("key") == "k2"
}).GetString("records[0].value")
```

在上面的示例中，数组的数据在过滤之后只剩下一条数据符合条件。
所以可以用 `records[0]` 定位到这条数据，然后用 `.value` 作为路径来读取 value 字段的数值。
