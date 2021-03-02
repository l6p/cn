---
sort: 5
title: Merging JSON Data
---

# Merging JSON Data

For example, there are two sets of JSON data and they are encapsulated in `d1` and `d2` respectively:

```go
d1 := json.D(`
    {
        "key1": "value1",
        "key2": [10, 20]
    }
`)

d2 := json.D(`
    {
        "key2": {
            "key21": 0
        },
        "key3": 10
    }
`)
```

`d2` can be merged with `d1` using the following method:

```go
d1.Merge("", d2.GetJson(""))
```

The first parameter of the `Merge` function is the position in `d1` where `d2` is merged, 
and `""` indicates that the merge is performed at the root of `d1`.

`d2.GetJson("")` indicates that the data encapsulated in `d2` is converted to a JSON string.

If the key in `d2` overlaps with the key in `d1`, the data in `d2` prevails.
