---
sort: 1
title: Initializing The Script Project
---

# Initializing The Script Project

Lollipop script is technically a Go module. Dedicated functions in the Go module can be exported to Lollipop as test cases. 
So Lollipop is actually a framework by using K8s's resources to schedule and run functions in the Go module and providing 
some conveniences in order to fulfill different test purposes.

The first step to create a script is to create a new, empty directory, e.g., script. 
Run `go mod init` in that directory to make the directory as the root of a Go module.

```shell
mkdir script
cd script
go mod init script
```

Please make sure you are using **go 1.13**.

```go
module script

go 1.13
```
