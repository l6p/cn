---
sort: 2
title: Installing Lollipop
---

# Installing Lollipop

Download or clone [this project](https://github.com/l6p/helm){:target="_blank"} and go to the `charts/lollipop` directory.
Open and edit the **values.yaml** file and modify the configuration as required.

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| global.mongodb.host | MongoDB address and port in the K8s cluster | mongodb.l6p-system.svc.cluster.local:27017 |
| global.mongodb.user | MongoDB username | root |
| global.mongodb.pass | MongoDB password | rootpassword |
| global.kafka.endpoint | Kafka endpoint | kafka.l6p-system.svc.cluster.local:9092 |
| global.kafka.topic | Kafka topic | l6p.log |
| server.storageClass | storage class of backing PVC | hostpath |
| server.service.port | port of the API server | 80 |
| server.ingress.hosts[0].host | hostname of the API server | local.l6p.io |
| server.ingress.hosts[0].path | path within the API url structure | "/api/v1" |
| web.apiBaseUrl | base URL of API | "http://local.l6p.io/api/v1" |
| web.service.port | port of the Web server | 80 |
| web.ingress.hosts[0].host | hostname of the Web server | local.l6p.io |
| web.ingress.hosts[0].path | root path of the Web server | "/" |

```warning
Please change `local.l6p.io` in the configuration to your actual domain name, such as `l6p.mycompany.com`, 
and resolve the domain name to the external IP address of Ingress Controller. The external IP address of 
Ingress Controller can be retrieved by using the command `kubectl get service -n ingress-nginx`. 
If you are only running on desktop, you can add a record in `/etc/hosts` to point `local.l6p.io` to the 
external IP address of Ingress Controller.
```

After modifying the configuration, please go back to the **root directory** and run:

```shell
helm install l6p ./charts/lollipop -n l6p-system
```

To check if the Lollipop pods have started, run the following command:

```shell
kubectl get pods -n l6p-system --watch
```

When all pods are running and ready it means that the system has installed successfully.

## Login Lollipop

Open the Chrome browser and access the home page of the Lollipop web console.
For example, according to the default configuration, the home page address is `http://local.l6p.io`.

By default, the system will create an administrator account with the username `admin` and the password `password`.
