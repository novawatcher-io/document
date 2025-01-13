# 快速上手：采集Kubernetes Pod日志

下面将带你演示在一个Kubernetes集群中，通过创建LogConfig CRD快速采集Pod的日志。

## 1. 准备Kubernetes环境

可以使用现有Kubernetes集群，或者[部署Kubernetes](https://kubernetes.io/zh/docs/tasks/tools/)。本地推荐使用[Kind](https://kind.sigs.k8s.io/)搭建Kubernetes集群。  

本文的操作需要在本地使用:

- kubectl（[下载](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG)）
- helm（[下载](https://helm.sh/docs/intro/install/)）

请确保本地有kubectl和helm可执行命令。

## 2. 创建存储类

以nfs为例

### 1、安装nfs-subdir-external-provisioner

```
helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner  --set nfs.server=192.168.2.104  --set nfs.path=/nfs/node_01/
```

### 2、创建StorageClass

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: default
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: cluster.local/nfs-subdir-external-provisioner
parameters:
  server: 192.168.2.104
  path: /nfs/node_01/
  readOnly: "false"
  archiveOnDelete: "true"
reclaimPolicy: Delete
volumeBindingMode: Immediate 
```

## 3. 部署Nova

你可以在 [installation](https://github.com/novawatcher-io/installation/releases) 页面查看所有发布的部署chart。

可以选择：

#### 下载chart再部署

```bash
helm pull https://github.com/novawatcher-io/installation/releases/download/v1.2.0/nova-v1.2.0.tgz && tar xvzf nova-v1.2.0.tgz
```
尝试修改一下其中的values.yaml。


然后部署安装：

```bash
helm install nova ./nova -nnova --create-namespace
```

当然你也可以：
#### 直接部署：

```bash
helm install nova -nnova --create-namespace https://github.com/novawatcher-io/installation/releases/download/v1.2.0/nova-v1.2.0.tgz
```

!!! node "想使用其他版本镜像？"

    为了方便体验最新的Fix和特性，我们提供了main分支每次合并后的镜像版本，可通过 [这里](https://hub.docker.com/r/novaio/nova/tags) 进行选择。  
    同时你可以在helm install命令中增加`--set image=novaio/nova:vX.Y.Z`来指定具体的nova镜像。


!!! caution "部署有问题？"

    如果尝试部署后出现问题，或者在你的环境中以下演示操作未成功，请参考[Kubernetes下部署nova](../install/kubernetes.md)，修改相关配置。



## 4. 查看日志


然后我们找到该节点的nova：
```bash
kubectl -nnova get po -owide |grep ${node}
```
可以通过：
```bash
kubectl -nnova logs -f ${nova-pod}
```
查看nova打印出的日志，里面展示了采集到的nginx标准输出日志。  

## 更多

上文只是一个简单的快速演示，部署出现问题或者想了解更多Kubernetes下nova如何使用？

- 更全面的部署介绍：[Kubernetes下部署nova](../install/kubernetes.md)
