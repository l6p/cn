---
sort: 1
title: 初始化测试脚本
---

# 初始化测试脚本

Lollipop 的测试脚本本质上是一个 Go module。可以将 Go module 中的指定方法输出给 Lollipop 作为测试用例使用。
所以 Lollipop 可以理解为一个利用 K8s 平台资源编排并高效运行您创建的 Go module 中的指定方法的工具。
同时 Lollipop 提供了方便的工具和报表，帮助您完成不同的测试目的。

创建测试脚本的第一步是，首先创建一个空的文件夹，例如名叫 `script`。

在这个新创建的文件夹中运行 `go mod init` 命令，使其成为一个 Go module。

```shell
mkdir script
cd script
go mod init script
```

请注意您要使用 **go 1.13** 版本。下面是通过 `go mod init` 命令创建的 `go.mod` 文件中的内容示例：

```go
module script

go 1.13
```
