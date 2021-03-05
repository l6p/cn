---
sort: 2
title: 安装 Lollipop
---

# 安装 Lollipop

请首先[下载这个项目](https://github.com/l6p/helm){:target="_blank"}，然后进入 `charts/lollipop` 目录.

请首先按照您自身的要求更改其中的 **values.yaml** 文件中的设置，下面是对于配置信息的描述：

| 参数 | 描述 | 默认值 |
| --------- | ----------- | ------- |
| global.mongodb.host | MongoDB 在 K8s 集群中的地址和端口 | mongodb.l6p-system.svc.cluster.local:27017 |
| global.mongodb.user | MongoDB 的用户名 | root |
| global.mongodb.pass | MongoDB 的密码 | rootpassword |
| global.kafka.endpoint | Kafka 在集群中的地址和端口 | kafka.l6p-system.svc.cluster.local:9092 |
| global.kafka.topic | Kafka 的主题名称 | l6p.log |
| server.storageClass | PVC 的存储类型 | hostpath |
| server.service.port | API 服务的端口 | 80 |
| server.ingress.hosts[0].host | API 服务的域名 | local.l6p.io |
| server.ingress.hosts[0].path | API 的基础 URL | "/api/v1" |
| web.apiBaseUrl | API 服务的基础 URL | "http://local.l6p.io/api/v1" |
| web.service.port | WEB 服务的端口 | 80 |
| web.ingress.hosts[0].host | WEB 服务的域名 | local.l6p.io |
| web.ingress.hosts[0].path | WEB 服务的根路径 | "/" |

```warning
请按照实际需要将 `local.l6p.io` 更改为您部署和使用的实际域名，例如 `l6p.mycompany.com`，
并且要把域名指向 Ingress Controller 的外网IP。Ingress Controller 的外网IP可通过 `kubectl get service -n ingress-nginx` 命令
获得。如果运行在个人笔记本上，可在本机的 `/etc/hosts` 文件中将 `local.l6p.io` 指向 Ingress Controller 的外网IP。
```

在更改完配置后请回到**根目录**然后运行：

```shell
helm install l6p ./charts/lollipop -n l6p-system
```

可以使用下面的命令来查看 Pod 的启动情况：

```shell
kubectl get pods -n l6p-system --watch
```

当所有 Pod 成功启动以后部署完毕。

## 登陆 Lollipop

打开 Lollipop Web 管理平台的页面，例如按照默认的配置，管理平台的地址为 `http://local.l6p.io`。

默认的管理员的用户名为 `admin` 密码为 `password`。

