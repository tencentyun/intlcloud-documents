Node affinity is an attribute of pods that attracts them to a set of nodes (either as a preference or a mandatory requirement). Taints are the opposite: they allow a node to repel a set of pods.

Tolerations are applied to pods, and they allow (but do not require) the pods to be scheduled to nodes with matching taints.

Taints and tolerations work together to ensure that pods are not scheduled to inappropriate nodes. One or more taints are applied to a node, and the node should not accept any pods that do not tolerate the taints.

In Fluid, considering the schedulability of 'Dataset', tolerations also need to be defined in the resource object. In this way, you can schedule the storage locations of caches on Kubernetes clusters like scheduling your pods.


## Setting Up an Environment
```shell
$ mkdir <any-path>/tolerations
$ cd <any-path>/tolerations
```

## Demo Run Example

**Check all nodes**
```shell
$ kubectl get no
NAME            STATUS   ROLES    AGE    VERSION
192.168.1.146   Ready    <none>   200d   v1.18.4-tke.13
```


**Configure a taint for a node**

```shell
$ kubectl taint nodes 192.168.1.146 hbase=true:NoSchedule
```

In the following step, we shall see the taint configuration of this node.


**Check the node again**
```shell
$ kubectl get node 192.168.1.146 -o yaml | grep taints -A3
  taints:
  - effect: NoSchedule
    key: hbase
    value: "true"
```

Now, the taint configuration `NoSchedule` is added to the node, and no dataset can be placed on this node by default.

**Check the `Dataset` resource object to be created**
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

>? To facilitate testing, `mountPoint` is set to WebUFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

In the `spec` attribute of the `Dataset` resource object, we define a `tolerations` sub-attribute to specify that data caches can be placed on the tainted node.


**Create the `Dataset` resource object**


```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
```


**Check the `GooseFSRuntime` resource object to be created**
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


The above snippet of the configuration file contains a lot of GooseFS related configuration, and Fluid will start a GooseFS instance based on the configuration. Among the configuration, the `spec.replicas` attribute is set to `1`, indicating that Fluid will start a GooseFS instance containing 1 GooseFS master and 1 GooseFS worker.


**Create the GooseFSRuntime resource object and check its status**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-n4tnc     1/1     Running   0          63m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          85m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-worker-qs26l   2/2     Running   0          63m   192.168.1.146   192.168.1.146   <none>           <none>
```

As shown above, the GooseFS worker is started and is running on the tainted node.

**Check the status of the `GooseFSRuntime` object**

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE     AGE
hbase   1               1                 Ready          1               1                 Ready   1             1               Ready   4m3s
```


**Check the application to be created**

A sample application is provided to demonstrate how data cache affinity scheduling is implemented in Fluid. First, you need to check the application:
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

**Run the application**

```shell
$ kubectl create -f app.yaml
statefulset.apps/nginx created
```

**Check the application running status**

```shell
$ kubectl get pod -o wide -l app=nginx
NAME      READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
nginx-0   1/1     Running   0          2m5s   192.168.1.146   192.168.1.146   <none>           <none>
```

As shown above, the Nginx Pod is started successfully and is running on the tainted node.


## Cleaning Up the Environment

```shell
$ kubectl delete -f .

$ kubectl taint nodes 192.168.1.146 hbase=true:NoSchedule-
```
