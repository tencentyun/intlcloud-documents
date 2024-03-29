节点亲和性是 Kubernetes Pod 的一种属性，它使得 Pod 被吸引到一类特定的节点。这可能出于一种偏好，也可能是硬性要求。Taint（污点）则相反，它使节点能够排斥一类特定的 Pod。

容忍度（Tolerations）是应用于 Pod 上的，允许（但并不要求）Pod 调度到带有与之匹配的污点的节点上。

污点和容忍度（Toleration）相互配合，可以用来避免 Pod 被分配到不合适的节点上。每个节点上都可以应用一个或多个污点，这表示对于那些不能容忍这些污点的 Pod，是不会被该节点接受的。

而在 Fluid 中，考虑到 `Dataset` 的可调度性，资源对象中也需要定义 toleration，这意味着您能够像调度您的 Pod 一样调度缓存在 Kubernetes 集群上的存放位置。


## 新建工作环境
```shell
$ mkdir <any-path>/tolerations
$ cd <any-path>/tolerations
```

## 运行示例

**查看全部节点**
```shell
$ kubectl get no
NAME            STATUS   ROLES    AGE    VERSION
192.168.1.146   Ready    <none>   200d   v1.18.4-tke.13
```


**为节点配置污点（taint）**

```shell
$ kubectl taint nodes 192.168.1.146 hbase=true:NoSchedule
```

在接下来的步骤中，我们将看到节点上的污点配置。


**再次查看节点**
```shell
$ kubectl get node 192.168.1.146 -o yaml | grep taints -A3
  taints:
  - effect: NoSchedule
    key: hbase
    value: "true"
```

目前，节点增加了 taints 配置 NoSchedule，这样默认数据集就无法放置到该节点上。

**检查待创建的 Dataset 资源对象**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hbase
spec:
  mounts:
    - mountPoint: https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/stable/
      name: hbase
  tolerations:
    - key: hbase 
      operator: Equal 
      value: "true" 
```

>? 为了方便用户进行测试，mountPoint 这里使用的是 Web UFS，使用 COS 作为 UFS 可见 [使用 GooseFS 挂载 COS（COSN）](https://intl.cloud.tencent.com/document/product/436/41024)。
>

在该`Dataset`资源对象的`spec`属性中，我们定义了一个`tolerations`的属性，该子属性要求数据缓存可以放置到配置污点的节点。


**创建 Dataset 资源对象**


```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
```


**检查待创建的 GooseFSRuntime 资源对象**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hbase
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1
        quota: 2G
        high: "0.95"
        low: "0.7"
```


该配置文件片段中，包含了许多与 GooseFS 相关的配置信息，这些信息将被 Fluid 用来启动一个 GooseFS 实例。上述配置片段中的 `spec.replicas` 属性被设置为1，这表明 Fluid 将会启动一个包含1个 GooseFS Master 和1个 GooseFS Worker 的 GooseFS 实例。


**创建 GooseFSRuntime 资源并查看状态**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-n4tnc     1/1     Running   0          63m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          85m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-worker-qs26l   2/2     Running   0          63m   192.168.1.146   192.168.1.146   <none>           <none>
```

在此处可以看到，GooseFS Worker 被启动，并且运行在具有污点的节点之上。

**检查 GooseFSRuntime 状态**

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE     AGE
hbase   1               1                 Ready          1               1                 Ready   1             1               Ready   4m3s
```


**查看待创建的应用**

我们提供了一个样例应用来演示 Fluid 是如何进行数据缓存亲和性调度的，首先查看该应用：
- app.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: apps/v1beta1
kind: StatefulSet
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  replicas: 1
  serviceName: "nginx"
  podManagementPolicy: "Parallel"
  selector: # define how the deployment finds the pods it manages
    matchLabels:
      app: nginx
  template: # define the pods specifications
    metadata:
      labels:
        app: nginx
    spec:
      tolerations:
      - key: hbase 
        operator: Equal 
        value: "true" 
      containers:
        - name: nginx
          image: nginx
          volumeMounts:
            - mountPath: /data
              name: hbase-vol
      volumes:
        - name: hbase-vol
          persistentVolumeClaim:
            claimName: hbase
:::
</dx-codeblock>

**运行应用**

```shell
$ kubectl create -f app.yaml
statefulset.apps/nginx created
```

**查看应用运行状态**

```shell
$ kubectl get pod -o wide -l app=nginx
NAME      READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
nginx-0   1/1     Running   0          2m5s   192.168.1.146   192.168.1.146   <none>           <none>
```

可以看到 Nginx Pod 成功启动，并且运行在配置 taint 的节点之上。


## 环境清理

```shell
$ kubectl delete -f .

$ kubectl taint nodes 192.168.1.146 hbase=true:NoSchedule-
```
