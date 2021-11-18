In Fluid, remote files defined in the 'Dataset' resource object are schedulable, which means you can manage the location for caching remote files on a Kubernetes cluster as you manage your pods. Fluid also supports data cache affinity scheduling for applications. This scheduling method places applications (such as data analysis tasks and machine learning tasks) together with the required data cache to minimize additional overhead.


## Prerequisites

Before running the sample code provided in this document, install Fluid by referring to [Installation](https://intl.cloud.tencent.com/document/product/436/42230) and check that all the components used by Fluid are running properly.

```shell
$ kubectl get pod -n fluid-system
goosefsruntime-controller-5b64fdbbb-84pc6   1/1     Running   0          8h
csi-nodeplugin-fluid-fwgjh                  2/2     Running   0          8h
csi-nodeplugin-fluid-ll8bq                  2/2     Running   0          8h
dataset-controller-5b7848dbbb-n44dj         1/1     Running   0          8h
```

Normally, you shall see a pod named `dataset-controller`, a pod named `goosefsruntime-controller`, and multiple pods named `csi-nodeplugin`. The number of `csi-nodeplugin` pods depends on the number of nodes in your Kubernetes cluster.

## Setting Up an Environment
```shell
$ mkdir <any-path>/co-locality
$ cd <any-path>/co-locality
```

## Example

**Check all nodes in your cluster**

```shell
$ kubectl get nodes
NAME                       STATUS   ROLES    AGE     VERSION
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```


**Label one of the nodes**

```shell
$ kubectl label nodes 192.168.1.146 hbase-cache=true
```

In the following steps, we will use `NodeSelector` to manage where to store data, and therefore we add a label to a desired node.


**Check all nodes again**


```shell
$ kubectl get node -L hbase-cache
NAME                       STATUS   ROLES    AGE     VERSION            HBASE-CACHE
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13   true
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```

Currently, among all the 2 nodes, only one node holds the `hbase-cache=true` label, indicating that data will only be cached on this node.


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
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: hbase-cache
              operator: In
              values:
                - "true"
```

>? To facilitate testing, `mountPoint` is set to WebUFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

In the `spec` attribute of the `Dataset` resource object, we defined the `nodeSelectorTerms` sub-attribute to specify that data caches must be placed on the node with the `hbase-cache=true` label.


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
  replicas: 2
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1
        quota: 2G
        high: "0.8"
        low: "0.7"
```

This segment of the configuration file contains GooseFS configuration, which will be used by Fluid to launch a GooseFS instance. In the configuration, the `spec.replicas` attribute is set to `2`, indicating that Fluid will launch a GooseFS instance containing one GooseFS master and two GooseFS workers.

**Create the GooseFSRuntime resource object and check its status**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m3s   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
```

As shown above, though two GooseFS workers are expected, only one GooseFS worker is started successfully and runs on the node with the `hbase-cache=true` label.

**Check the status of the `GooseFSRuntime` object**

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE     AGE
hbase   1               1                 Ready          1               2                 PartialReady   1             2               PartialReady   4m3s
```

As expected, `Worker Phase` is `PartialReady`, and `Ready Workers` is `1`, which is less than the value `2` of `Desired Workers`.

**Check the application to be created**

A sample application is provided to demonstrate how data cache affinity scheduling is implemented in Fluid. First, you need to check the application:

**app.yaml**
```yaml
apiVersion: apps/v1beta1
kind: StatefulSet
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  replicas: 2
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
      affinity:
        # prevent two Nginx Pod from being scheduled at the same Node
        # just for demonstrating co-locality demo
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - nginx
            topologyKey: "kubernetes.io/hostname"
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
```
The `podAntiAffinity` attribute, solely designed for demonstration, is configured to ensure that all the pods of the same application are distributed to different nodes, for better demonstration effect.


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
nginx-1   0/1     Pending   0          2m5s   <none>          <none>                     <none>           <none>
```

Only one Nginx pod is started successfully and it runs on the node that matches `nodeSelectorTerms`.


**Check the causes of the application startup failure**
```shell
$ kubectl describe pod nginx-1
...
Events:
  Type     Reason            Age        From               Message
  ----     ------            ----       ----               -------
  Warning  FailedScheduling  <unknown>  default-scheduler  0/2 nodes are available: 1 node(s) didn't match pod affinity/anti-affinity, 1 node(s) didn't satisfy existing pods anti-affinity rules, 1 node(s) had volume node affinity conflict.
  Warning  FailedScheduling  <unknown>  default-scheduler  0/2 nodes are available: 1 node(s) didn't match pod affinity/anti-affinity, 1 node(s) didn't satisfy existing pods anti-affinity rules, 1 node(s) had volume node affinity conflict.
```


As shown above, there are two causes: on the one hand, according to the settings of the `PodAntiAffinity` attribute, two Nginx pods cannot be scheduled to the same node. On the other hand, there is currently only one node that meets the affinity requirements of the `Dataset` resource object and therefore only one Nginx pod is successfully scheduled.


**Label the other node**

```shell
$ kubectl label node 192.168.1.147 hbase-cache=true
```

Now the two nodes have the same label. Check the running status of all the components again.

```shell
$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          44m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-fuse-kth4g     1/1     Running   0          10m   192.168.1.147   192.168.1.147   <none>           <none>
hbase-master-0       2/2     Running   0          46m   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          44m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-worker-rvncl   2/2     Running   0          10m   192.168.1.147   192.168.1.147   <none>           <none>
```

Now, the two GooseFS workers are started successfully and they run on two different nodes:

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          2               2                 Ready          2             2               Ready        46m43s
```

```shell
$ kubectl get pod -l app=nginx -o wide
NAME      READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
nginx-0   1/1     Running   0          21m   192.168.1.146   192.168.1.146   <none>           <none>
nginx-1   1/1     Running   0          21m   192.168.1.147   192.168.1.147   <none>           <none>
```

The other Nginx pod is no longer in the `Pending` state. It is now successfully started and is running on another node.

The above example shows that both schedulable data cache and data cache affinity scheduling for applications are supported by Fluid. In most cases, these two features work together to provide users with a more flexible and convenient way to manage data on Kubernetes clusters.

To sum up, Fluid supports data cache scheduling policies, which provide users with more flexible data cache management capabilities.

## Cleaning Up the Environment
```shell
$ kubectl delete -f .


$ kubectl label node 192.168.1.146 hbase-cache-
$ kubectl label node 192.168.1.147 hbase-cache-
```
