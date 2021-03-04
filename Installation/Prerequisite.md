---
sort: 1
title: 预先的准备
---

# 预先的准备

## 安装 Kubernetes

```warning
如果您已经有了 K8s 集群或者不打算在个人电脑上运行请忽略此步。
```

下面介绍的是如何在个人电脑上安装 K8s。最简单的方法是安装 Docker Desktop，可以打开这个[页面](https://www.docker.com/products/docker-desktop){:target="_blank"}下载这个应用并进行安装。

安装好 Docker Desktop 以后，如果您使用的是 Mac 电脑就按照[这上面的步骤](https://docs.docker.com/docker-for-mac/#kubernetes){:target="_blank"}来打开 K8s 功能。
如果您使用的是 Windows 电脑则按照[这上面的步骤](https://docs.docker.com/docker-for-windows/#kubernetes){:target="_blank"}来打开 K8s 功能。

K8s 功能一旦开启后，您可以使用这个命令：

```shell
kubectl version --short
``` 

来查看 K8s 的版本，如果命令执行成功则 K8s 安装成功。

## 安装 Helm

Helm 是用于安装 Lollipop 及其组件用的。如果您还没有安装 Helm 那么可以[打开这个页面](https://helm.sh/docs/intro/install){:target="_blank"}按照上面的步骤来进行安装。

一旦安装完毕，您可以使用这个命令：

```shell
helm version --short
``` 

来查看 Helm 的版本，如果命令执行成功则 Helm 安装成功。

## 创建 K8s 命名空间

下面需要在 K8s 集群中创建两个命名空间，执行如下命令：

```shell
kubectl create ns l6p-system 
kubectl create ns l6p-space
```

## 安装 MongoDB

Lollipop 使用 MongoDB 存储数据，如果没有安装 MongoDB 请首先[下载这个项目](https://github.com/l6p/helm){:target="_blank"}，然后进入 `utils/mongodb` 目录。

请首先按照您自身的要求更改其中的 **values.yaml** 文件中的设置，然后在当前目录中运行下面的命令进行安装：

```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install mongodb -n l6p-system -f ./values.yaml bitnami/mongodb
```

## 安装 Kafka

Lollipop 使用 Kafka 作为消息队列来临时存储性能测试时临时产生的日志，如果没有安装请首先[下载这个项目](https://github.com/l6p/helm){:target="_blank"}，然后进入 `utils/kafka` 目录。

请首先按照您自身的要求更改其中的 **values.yaml** 文件中的设置，然后在当前目录中运行下面的命令进行安装：

```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install kafka -n l6p-system -f ./values.yaml bitnami/kafka
```

## 安装 K8s Ingress Controller

Lollipop 提供了基于 Web 的管理平台。如果在本地使用管理平台就需要安装 Ingress Controller。

首先要为 Ingress controller 创建一个 K8s 的命名空间：

```shell
kubectl create ns ingress-nginx
```

使用下面的命令来安装 NGINX Ingress controller：

```shell
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx/
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx
```

使用下面的命令来检查是否启动成功：

```shell
kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
```
