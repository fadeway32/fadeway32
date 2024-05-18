
---

layout: K8S部署dashboard

title: K8S部署dashboard


tags: Kubernetes

categories: Kubernetes

top: 35

path: /article/1715610102

abbrlink: 1715610102



date: 2024-05-13 22:21:48


---


# K8S部署dashboard 









单机搭建dashboard



https://cloud.tencent.com/developer/article/1797416



~~~shell
PS C:\Users\Administrator> kubectl create serviceaccount dashboard-admin -n kube-system
serviceaccount/dashboard-admin created
PS C:\Users\Administrator> kubectl create clusterrolebinding dashboard-admin --clusterrole=cluster-admin --serviceaccount=kube-system:dashboard
clusterrolebinding.rbac.authorization.k8s.io/dashboard-admin created
PS C:\Users\Administrator> kubectl -n kube-system create token dashboard-admin
eyJhbGciOiJSUzI1NiIsImtpZCI6ImtGdnBVbkIyRlpqRVE2OWdncXpkSERHcHYweDRjWVU1MDUxdTFndHN4dzgifQ.eyJhdWQiOlsiaHR0cHM6Ly9rdWJlcm5ldGVzLmRlZmF1bHQuc3ZjLmNsdXN0ZXIubG9jYWwiXSwiZXhwIjoxNzE1NjEyNTMxLCJpYXQiOjE3MTU2MDg5MzEsImlzcyI6Imh0dHBzOi8va3ViZXJuZXRlcy5kZWZhdWx0LnN2Yy5jbHVzdGVyLmxvY2FsIiwia3ViZXJuZXRlcy5pbyI6eyJuYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsInNlcnZpY2VhY2NvdW50Ijp7Im5hbWUiOiJkYXNoYm9hcmQtYWRtaW4iLCJ1aWQiOiIxNTI5MWFmMC05YzhjLTRhZjMtYjIwMy1hMGU1ZDc0YTA3ZWEifX0sIm5iZiI6MTcxNTYwODkzMSwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmUtc3lzdGVtOmRhc2hib2FyZC1hZG1pbiJ9.NE28iISr87ib3z-dwfalCGay1gu-GjrSLKjGaxbh6g43vB8NL7VgKMPhLJWYqjRTyXrSFp_2YuytD1R3f5AYEg5BlsV5qAW5TgwfF7-9iWSnsM-4EKfHSzDI7b-ScUmspjhXGVp-f-xw7FF5D1DHVSyMXgYpqbxxU_gbfaQA-TuJsWbPj3RRAiKEb8N_YGE1WDxm7Rl4runKgU99jVN3TJHyd02fCCrZM0A4aBmKFx3sPivSOdlcydIzuXQywe9VZK7r-H3NJa6AlzuSUFIHaA-_Pq2XFjWDR0JNbaBXrzLo--sgFPagUShYo8tEKrBABj70oB6ROFY32JN0_0WBBA
~~~



常见命令

## 基本命令

### create

根据文件或标准输入（stdin）创建资源。

**创建资源**

> kubectl create -f ./nginx.yaml

**创建当前目录下的所有yaml资源**

> kubectl create -f .

**使用多个文件创建资源**

> kubectl create -f ./nginx1.yaml -f ./mysql2.yaml

**使用目录下的所有清单文件来创建资源**

> kubectl create -f ./dir

**使用 url 来创建资源**

> kubectl create -f [xxx.git.io/vxxzso.yaml](https://link.juejin.cn/?target=https%3A%2F%2Fxxx.git.io%2Fvxxzso.yaml)

### run

在集群中运行特定镜像。

**创建带有终端的pod**

> kubectl run -i --tty busybox --image=busybox

**启动一个 nginx 实例**

> kubectl run nginx --image=nginx

**启动多个pod实例**

> kubectl run mybusybox --image=busybox --replicas=5

### explain

获取资源的文档。

**获取 pod 和 svc 的文档**

> kubectl explain pods,svc



### get

获取所有的resources，包括`node`、`pod` 、`namespace`、`service` 、`deployment`等，可以展示一个或者多个资源。

**查看nodes节点**

> kubectl get nodes

**通过yaml文件查询资源**

> kubectl get -f xxx.yaml

**查询资源**

> kubectl get resourcequota

**查询endpoints**

> kubectl get endpoints

#### 查看pods

**查看指定空间`kube-system`的pods**

> kubectl get po -n kube-system

查看所有空间的pods的详细信息

> kubectl get pods -o wide --all-namespaces

查看指定空间`kube-system`的pods的详细信息

> kubectl get pod -o wide --namespace=kube-system

#### 获取指定namespace信息

```bash
bash复制代码kubectl get namespaces

# 获取指定namespace的yaml格式和json格式信息
kubectl get namespaces kube-system -o yaml 
kubectl get namespaces kube-system -o json
```

#### 获取service(svc)

**查看所有命令空间的service**

> kubectl get svc --all-namespaces

**查看所有命令空间的service的其他写法**

> kubectl get services --all-namespaces

```bash
bash复制代码# 通过 yaml 方式导出所有 service
kubectl get service -o yaml > backup.yaml

# 通过 yaml 方式导出单个 service
kubectl get service serviceName -o yaml > backup.yaml
```

#### 查询事件(Event)

> kubectl get events --all-namespaces

**查看某个命名空间下的事件**

> kubectl get events -n kube-system

**查看某个命名空间下的事件，并根据关键字过滤**

> kubectl get events -n kube-system | grep "name"

#### 通过lable查询

> kubectl get pods -l app=nginx -o yaml|grep podIP

### delete

根据文件、标准输入（stdin）、资源名或者资源标签删除资源。

**删除 pod.json 文件中定义的类型和名称的pod**

> kubectl delete -f ./pod.json

**删除名为“baz”的 pod 和名为“foo”的 service**

> kubectl delete pod,service baz foo

**删除具有 name=myLabel 标签的 pod 和 serivce**

> kubectl delete pods,services -l name=myLabel

**删除具有 name=myLabel 标签的 pod 和 service，包括尚未初始化的**

> kubectl delete pods,services -l name=myLabel --include-uninitialized

**删除 my-ns 命名空间下的所有 pod 和 serivce，包括尚未初始化的**

> kubectl -n my-ns delete po,svc --all

**强制删除pod(如，prometheus-7fcfcb9f89-qkkf7)**

> kubectl delete pods prometheus-7fcfcb9f89-qkkf7 --grace-period=0 --force

## 集群管理命令

### cluster-info

**查看集群信息**

> kubectl cluster-info

**查看更详细的集群信息。**

> kubectl cluster-info dump

### top

显示CPU、内存、存储资源的使用情况。

**显示节点（k8s-node）资源的使用情况**

> kubectl top node k8s-node

**显示集群所有节点的资源的使用情况**

> kubectl top node

**显示指定命名空间（如，logging）的pod的资源的使用情况**

> kubectl top pod -n logging

### cordon

标记节点不可调度。

**标记k8s-node节点不可调度**

> kubectl cordon k8s-node

### uncordon

标记节点可调度。

**标记k8s-node节点可调度**

> kubectl uncordon k8s-node

### drain

排除某节点，准备进行维护

**排除k8s-node节点，准备进行维护**

> kubectl drain k8s-node