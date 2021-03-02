---
sort: 2
title: Creating Test Cases
---

# Creating Test Cases

In a test script project, you need to declare an `Export` function, 
which is used to provide the necessary information for the test framework, 
so the `Export` function is the interface between the test script and the framework.

The return value of the `Export` function is of type `map`, 
and there are some reserved strings as the key of the map to play some special role.

In addition to the reserved strings, the **key** is the name of the test case output to the framework, 
and the **value** is the function that executes the test case.

The following code example defines an empty test case and outputs it to the framework with the name `SimpleCase`.

## Code example

```go
func SimpleCase() {
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"SimpleCase": SimpleCase,
	}
}
```

## Reference

* [An example of a simple test script](https://github.com/l6p/helm/tree/master/examples/getting-json-data){:target="_blank"}
* [An example of local debugging test script](https://github.com/l6p/helm/tree/master/examples/getting-json-data-with-local-debug){:target="_blank"}
