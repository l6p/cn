---
sort: 4
title: Modifying Data
---

# Modifying Data

`json.Data` provides the ability to modify its encapsulated JSON data. 
For example, based on the following JSON data:

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

## Setting New Value

When the following code is executed:

```go
d.SetString("key1", "foo")
d.SetInt("key2.key21", 10)
```

The JSON value will change to:

```json
{
    "key1": "foo",
    "key2": {
        "key21": 10
    },
    "key3": [10, 20]
}
```

## Appending Value To Array

Further, execute the following code:

```go
d.AppendInt("key3", 30)
```

The JSON value will change to:

```json
{
    "key1": "foo",
    "key2": {
        "key21": 10
    },
    "key3": [10, 20, 30]
}
```

## Deleting Item

Then proceed to execute the following code:

```go
d.Delete("key2")
```

JSON will finally become:

```json
{
    "key1": "foo",
    "key3": [10, 20, 30]
}
```
