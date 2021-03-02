---
sort: 3
title: Filtering Elements In Array
---

# Filtering Elements In Array

Based on the following JSON data:

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

If you want to find a record with key equal to `k2` and read the value of `value`, you can do this:

```go
d.Filter("records", func(data *json.Data) bool {
    return data.GetString("key") == "k2"
}).GetString("records[0].value")
```

In the above example, after the records are filtered, there is only one record that matches the criteria, 
so you can locate the record by `records[0]` and get the value of the record by `.value`.
