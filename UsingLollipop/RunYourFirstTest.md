---
sort: 1
title: 运行您的第一个测试
---

# 运行您的第一个测试

## 创建您的第一个测试脚本

首先创建一个新的文件夹，例如命名成 `script`，然后执行下面的操作：

```shell
mkdir script
cd script
go mod init script
go get github.com/l6p/utils
```

然后把下面的代码拷贝到文本编辑器中，命名成 `main.go` 并保存在新创建的文件夹下：

```go
package main

import (
	"github.com/l6p/utils/client/json"
	"log"
	"time"
)

func SimpleCase(client *json.Client, logger *log.Logger) {
	data := client.R().Get("https://jsonplaceholder.typicode.com/todos/1").D()
	logger.Printf("Todo title: %s", data.GetString("title"))
	time.Sleep(5 * time.Second)
}

func Export() map[string]interface{} {
	return map[string]interface{}{
		"SimpleCase": SimpleCase,
	}
}
```

把新创建的 `script` 文件夹压缩成一个 zip 文件：

```shell
zip -r script.zip ./script
```

## 上传测试脚本

在 Lollipop Web 管理平台的左侧菜单上选择 **Script** 菜单，并点击 **UPLOAD** 按钮：

在弹出对话框中输入如下信息：

```text
| 表单项目 | 输入值                             |
|---------|-----------------------------------|
| Name    | script                            |
| Version | 0.1.0                             |
| File    | Choose the "script.zip" to upload |
```

输入完毕并确认后等待一会，等上传的测试脚本变为 `ready` 的状态。

## 创建测试计划

在 Lollipop Web 管理平台的左侧菜单上选择 **Plan** 菜单，并点击 **CREATE** 按钮：

```text
| 表单项目        | 输入值  |
|----------------|--------|
| Name           | plan   |
| Script Name    | script |
| Script Version | 0.1.0  |
```

点击 **NEXT** 按钮并继续输入下面的信息：

```text
| 表单项目      | 输入值      |
|--------------|------------|
| VUser Type   | tester     |
| VUser Weight | 100%       |
| Max Sessions | 1          |
| Case Name    | SimpleCase |
| Case Weight  | 100%       |
```

点击 **DONE** 和 **SAVE**

## 运行测试

在 Lollipop Web 管理平台的左侧菜单上选择 **Test** 菜单，并点击 **CREATE** 按钮：

```text
| 表单项目  | 输入值 |
|----------|-------|
| Name     | test  |
| Plan     | plan  |
| Warm Up  | 1m    |
| Duration | 1m    |
```

点击 **NEXT** 并继续在对话框里填写：

```text
| 表单项目           | 输入值 |
|-------------------|-------|
| Total Workers     | 1     |
| VUsers per Worker | 1     |
```

点击 **NEXT** 和 **RUN**

## 查看测试报表

将鼠标移动到测试项目右侧的功能区展开选项：

<style>
    img[alt=pic00000001] { 
        display: block;
        width: 280px; 
    }
</style>
![pic00000001](/assets/images/pic00000001.png)

点击 **Dashboard** 按钮来查看测试报表。或者直接点击测试项目本身也可以查看测试报表。

## 进一步阅读

* [进一步了解如何创建测试用例](/cn/ScriptGuides)
* [进一步了解关于性能测试的细节](/cn/TestingGuides)
