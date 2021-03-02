---
sort: 2
title: Reading Data By Path
---

# Reading Data By Path

The simple path consists of JSON keys and dots. For example, based on the following JSON data:

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

Use `key1` as path to get `value1`:

```go
d.GetString("key1")
```

Use `key2.key21` as path to get `value2`:

```go
d.GetString("key2.key21")
```

## Reading Data From Array

Based on the following JSON data:

```go
d := json.D(`
    {
        "key1": [10, 20, 30]
    }
`)
```

Use `key1[1]` as path to get `20`:

```go
d.GetInt("key1[1]")
```
