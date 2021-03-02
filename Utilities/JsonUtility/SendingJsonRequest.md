---
sort: 1
title: Sending JSON Request
---

# Sending JSON Request

Add a dependency on `github.com/l6p/utils` for the script, and add a `*json.Client` type parameter to the test case function, 
then the test framework will automatically inject the JSON client for the test case to use.

`json.Client` encapsulates [Go Resty](https://github.com/go-resty/resty){:target="_blank"}, making the operation of handling JSON data more convenient.

## Getting A JSON Response

The `R()` of `json.Client` is used to create a JSON request. Using the `Get(...)` of the request, 
you can directly request a JSON API and use the `D()` to get the data you need in the response.

The type of `D()` is `json.Data`, which provides some methods to easily handle JSON data:
- [Reading data by path](/Utilities/JsonUtility/ReadingDataByPath.html)
- [Filtering elements in array](/Utilities/JsonUtility/FilteringElementsInArray.html)
- [Modifying data](/Utilities/JsonUtility/ModifyingData.html)
- [Merging JSON data](/Utilities/JsonUtility/MergingJsonData.html)

## Posting JSON Data

Using the `Post(...)` of the request to send a Post request. Before sending the Post request, 
you can use the `J(...)` to set the JSON string to be sent, for example:

```go
client.R().J(`
{
    "title": "foo",
    "body": "bar",
    "userId": 1
}
`).Post("https://jsonplaceholder.typicode.com/posts")
```

If you already have `json.Data` then you can use `D(...)` of `json.Request` instead of `J(...)` to set the data to be posted.
