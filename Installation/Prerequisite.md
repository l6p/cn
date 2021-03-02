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

## Installing MongoDB

Download or clone [this project](https://github.com/l6p/helm){:target="_blank"} and go to the `utils/mongodb` directory.
Please change the **values.yaml** file according to your requirements, and run the command:

```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install mongodb -n l6p-system -f ./values.yaml bitnami/mongodb
```

## Installing Kafka

Lollipop uses Kafka as a message queue to store the logs generated during testing.

Download or clone [this project](https://github.com/l6p/helm){:target="_blank"} and go to the `utils/kafka` directory.
Please change the **values.yaml** file according to your requirements, and run the command:

```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install kafka -n l6p-system -f ./values.yaml bitnami/kafka
```

## Installing K8s Ingress Controller

```warning
Ignore this step if your K8s cluster already has an Ingress controller.
```

Lollipop provides a web-based management platform. In order to use this feature, the Ingress controller must be installed on k8s.

First create a K8s namespace for NGINX Ingress controller:

```shell
kubectl create ns ingress-nginx
```

NGINX Ingress controller can be installed via Helm:

```shell
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx/
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx
```

To check if the ingress controller pods have started, run the following command:

```shell
kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
```
