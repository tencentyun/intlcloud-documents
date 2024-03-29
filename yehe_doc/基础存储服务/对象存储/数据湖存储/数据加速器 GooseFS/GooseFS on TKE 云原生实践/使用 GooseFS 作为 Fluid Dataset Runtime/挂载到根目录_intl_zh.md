## 概述

在 Fluid 中默认的数据源 mount 路径是 `/<ns>/dir`，中间默认会有一层 ns 的路径。如果您只有一个数据源的情况下，可以将该数据源 mount 到 GooseFS 协议的根目录下，这样的好处是用户的程序完全无需改变，即可使用该功能。

下面将向您简单地介绍上述特性。

## 前提条件

在运行该示例之前，请参考 [安装](https://intl.cloud.tencent.com/document/product/436/42230) 文档完成安装，并检查 Fluid 各组件正常运行：

```shell
$ kubectl get pod -n fluid-system
goosefsruntime-controller-5b64fdbbb-84pc6   1/1     Running   0          8h
csi-nodeplugin-fluid-fwgjh                  2/2     Running   0          8h
csi-nodeplugin-fluid-ll8bq                  2/2     Running   0          8h
dataset-controller-5b7848dbbb-n44dj         1/1     Running   0          8h
```

通常来说，您会看到一个名为 `dataset-controller` 的 Pod、一个名为 `goosefsruntime-controller` 的 Pod 和多个名为 `csi-nodeplugin` 的 Pod 正在运行。其中 `csi-nodeplugin` 这些 Pod 的数量取决于您的 Kubernetes 集群中结点的数量。

## 新建工作环境

```shell
$ mkdir <any-path>/co-locality
$ cd <any-path>/co-locality
```

## 示例

### 检查待创建的 Dataset 资源对象
```shell
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hbase
spec:
  mounts:
    - mountPoint: https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/stable/
      name: hbase
      path: /
```


>? 为了方便用户进行实验，mountPoint 这里使用的是 Web UFS，使用 COS 作为 UFS 可参见 [使用 GooseFS 挂载 COS（COSN）](https://intl.cloud.tencent.com/document/product/436/41024)。
>

在该 `Dataset` 资源对象的 `spec` 属性中，我们定义了一个 `path` 的子属性，该子属性要求数据源 mount 到根目录下。

### 创建 Dataset 资源对象

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
```

### 检查待创建的 GooseFSRuntime 资源对象
```shell
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hbase
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: MEM
        path: /dev/shm
        quota: 2Gi
        high: "0.95"
        low: "0.7"
```
该配置文件片段中，包含了许多与 GooseFS 相关的配置信息，这些信息将被 Fluid 用来启动一个 GooseFS 实例。上述配置片段中的`spec.replicas`属性被设置为1，这表明 Fluid 将会启动一个包含1个 GooseFS Master 和1个 GooseFS Worker 的 GooseFS 实例。


### 创建 GooseFSRuntime 资源并查看状态

```shell
$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m3s   192.168.1.147   192.168.1.146   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
```


### 创建 fuse 节点并查看 mount 信息路径

```shell
$ kubectl exec -ti hbase-fuse-42csf bash
$ ls /runtime-mnt/goosefs/<namespace>/<DatasetName>/goosefs-fuse/
drwxrwx--x 2 message   99  4096 Apr 23 16:39 /user
drwxr-xr-x 2 message root  4096 Apr 23 16:38 /data
```
