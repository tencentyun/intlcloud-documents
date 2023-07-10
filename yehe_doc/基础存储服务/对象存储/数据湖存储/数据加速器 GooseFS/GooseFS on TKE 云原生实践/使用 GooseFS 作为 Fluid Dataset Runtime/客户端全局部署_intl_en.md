In Fluid, remote files defined in the 'Dataset' resource object are schedulable, which means you can manage the location for caching remote files on a Kubernetes cluster as you manage your pods. The pod that performs the computing can access the data files through the Fuse client.

The Fuse client supports two modes:
- `global` is `false`: In this mode, affinity is enforced between Fuse clients and cache data, and the number of Fuse clients is equal to the number of Runtime replicas. This is the default mode and does not need to be explicitly declared. The advantage of this mode is that it takes advantage of data affinity, but the deployment of Fuse clients becomes more rigid.
- `global` is `true`: In this mode, Fuse clients can be deployed globally in a Kubernetes cluster. There is no mandatory affinity between data and Fuse clients. In this case, the number of Fuse clients may far exceed the number of Runtime replicas. It is recommended that `nodeSelector` be used to specify the deployment scope of Fuse clients.


## Prerequisites

Before running the sample code provided in this document, install Fluid by referring to [Installation](https://intl.cloud.tencent.com/document/product/436/42230). Be sure to run the `helm` command to add the parameter `--set webhook.enable=true` to enable `webhook` and check that all the components used by Fluid are running properly.

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
$ mkdir <any-path>/fuse-global-deployment
$ cd <any-path>/fuse-global-deployment
```

## Demo Run Example


### Example 1: Set `global` to `true`

**Check all nodes in your cluster**
```shell
$ kubectl get nodes
NAME            STATUS   ROLES    AGE     VERSION
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```

**Label one of the nodes**
```shell
$ kubectl label nodes 192.168.1.146 cache-node=true
```

In the following steps, we will use `NodeSelector` to manage where to store data, and therefore we add a label to a desired node.

**Check all nodes again**
```shell
$ kubectl get node -L cache-node
NAME         STATUS   ROLES    AGE     VERSION            cache-node
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13   true
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```

Currently, among all the 2 nodes, only one node holds the `cache-node=true` label, indicating that data will only be cached on this node.

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
            - key: cache-node
              operator: In
              values:
                - "true"
```

>? To facilitate testing, `mountPoint` is set to Web UFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

In the `spec` attribute of the `Dataset` resource object, we defined the `nodeSelectorTerms` sub-attribute to specify that data caches must be placed on the node with the `cache-node=true` label.

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
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
  fuse:
    global: true
```

The above snippet of the configuration file contains a lot of GooseFS related configuration, and Fluid will start a GooseFS instance based on the configuration. Among the configuration, the `spec.replicas` attribute is set to `1`, indicating that Fluid will start a GooseFS instance containing 1 GooseFS master and 1 GooseFS worker. It is also worth noting that Fuse contains `global: true', which means that Fuse can be deployed globally, independent of the location of the data cache.

**Create the GooseFSRuntime resource object and check its status**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get po -owide
NAME                 READY   STATUS    RESTARTS   AGE     IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-gfq7z     1/1     Running   0          3m47s   192.168.1.147   192.168.1.147   <none>           <none>
hbase-fuse-lmk5p     1/1     Running   0          3m47s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m47s   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-hvbp2   2/2     Running   0          3m1s    192.168.1.146   192.168.1.146   <none>           <none>
```

As shown above, one GooseFS worker is started successfully and runs on the node with the `cache-node=true` label. There are two GooseFS Fuse clients, running on all sub-nodes.

**Check the status of the `GooseFSRuntime` object**

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          2             2               Ready        12m
```

As shown above, there is one GooseFS worker and two GooseFS Fuse clients.

**Delete GooseFSRuntime**

```shell
kubectl delete goosefsruntime hbase
```



### Example 2: Set `global` to `true` and use `nodeSelector` to configure the Fuse client

In this example, we use `nodeSelector` to configure the Fuse client to place it to a certain node in the cluster. Now that we have selected the `192.168.1.146` node as the cache node, for comparison, we select the `192.168.1.147` node to run GooseFS Fuse.
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
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
  fuse:
    global: true
    nodeSelector:
      kubernetes.io/hostname: 192.168.1.147
```


In this configuration file snippet, compared with `runtime.yaml`, `nodeSelector` is added and points to the `192.168.1.147` node while Fuse contains 'global: true'.


**Create the GooseFSRuntime resource object and check its status**
```shell
$ kubectl create -f runtime-node-selector.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get po -owide
NAME                 READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-xzbww     1/1     Running   0          1h   192.168.1.147   192.168.1.147   <none>           <none>
hbase-master-0       2/2     Running   0          1h   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-vdxd5   2/2     Running   0          1h   192.168.1.146   192.168.1.146   <none>           <none>
```

As shown above, one GooseFS worker is started successfully and runs on the node with the `cache-node=true` label. There is one GooseFS Fuse client, running on the sub-node `192.168.1.147`.


**Check the status of the `GooseFSRuntime` object**

```shell
$ kubectl get goosefsruntimes.data.fluid.io -owide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        1h
```

As shown above, there is one GooseFS worker and one GooseFS Fuse client. This is because GooseFSRuntime specifies `nodeSelector` and only one node meets the specification.

This example shows that Fluid supports separate scheduling policies for Fuse clients, providing users with more flexible Fuse client scheduling policies.

## Cleaning Up the Environment

```shell
$ kubectl delete -f .

$ kubectl label node 192.168.1.146 cache-node-
```
