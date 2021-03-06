---
sort: 2
title: 创建测试用例
---

# 创建测试用例

在测试脚本的文件中，您需要声明一个名叫 `Export` 的方法。
这个方法用以向测试框架输出必要信息，所以 `Export` 方法可以被视为一个框架与测试脚本沟通的接口。

`Export` 方法的返回值必须是 `map` 类型，某些键的名称是作为**保留字**有特定的含义。

除了保留字之外的其它的键的名称将被视为**测试用例的名称**，键所对应的值被视为该**测试用例的执行方法**。

下面的代码定义了一个空的测试用例方法 `SimpleCase`，并且通过 `Export` 方法以 `SimpleCase` 作为测试用例的名称输出给测试框架。

## 代码示例

```go
func SimpleCase() {
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"SimpleCase": SimpleCase,
	}
}
```

## 源代码参考

* [一个简单的测试脚本](https://github.com/l6p/helm/tree/master/examples/getting-json-data){:target="_blank"}
* [测试脚本的本地调试](https://github.com/l6p/helm/tree/master/examples/getting-json-data-with-local-debug){:target="_blank"}
