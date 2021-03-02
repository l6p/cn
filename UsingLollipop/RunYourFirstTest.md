---
sort: 1
title: Run Your First Test
---

# Run Your First Test

## Write Your First Test Case

The first step is to create a new directory `script`, and perform the following actions:

```shell
mkdir script
cd script
go mod init script
go get github.com/l6p/utils
```

Copy the code below, paste it into your favourite editor, and save it as `main.go` in this folder:

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

Compress this folder into a zip file:

```shell
zip -r script.zip ./script
```

## Upload Script

Choose **Script** from the left menu and click **UPLOAD** button and fill in the form:

```text
| Item    | Value                             |
|---------|-----------------------------------|
| Name    | script                            |
| Version | 0.1.0                             |
| File    | Choose the "script.zip" to upload |
```

Waiting for a moment until script's status is ready.

## Create A Test Plan

Choose **Plan** from the left menu and click **CREATE** button and fill in the form:

```text
| Item           | Value  |
|----------------|--------|
| Name           | plan   |
| Script Name    | script |
| Script Version | 0.1.0  |
```

Click **NEXT** and continue to fill in the form:

```text
| Item         | Value      |
|--------------|------------|
| VUser Type   | tester     |
| VUser Weight | 100%       |
| Max Sessions | 1          |
| Case Name    | SimpleCase |
| Case Weight  | 100%       |
```

Click **DONE** and **SAVE**

## Run Test

Choose **Test** from the left menu and click **CREATE** button and fill in the form:

```text
| Item     | Value |
|----------|-------|
| Name     | test  |
| Plan     | plan  |
| Warm Up  | 1m    |
| Duration | 1m    |
```

Click **NEXT** and continue to fill in the form:

```text
| Item              | Value |
|-------------------|-------|
| Total Workers     | 1     |
| VUsers per Worker | 1     |
```

Click **NEXT** and **RUN**

## Check Report

While the test is running you can slide the mouse over the right side trigger points of the test to slide out the functional buttons.

<style>
    img[alt=pic00000001] { 
        display: block;
        width: 280px; 
    }
</style>
![pic00000001](/assets/images/pic00000001.png)

Then click the **Dashboard** button to view the test report.
Or even simpler, just click on the test item in the list to view the test report.

## Further Reading

* [Learn more about creating test scripts](/ScriptGuides)
* [Learn more about the test details](/TestingGuides)
