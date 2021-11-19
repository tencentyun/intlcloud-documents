## Overview

In Fluid, you can use `nodeselector` to specify master node deployment. For example, you can choose to deploy a master to a Kubernetes server with higher performance.

The feature is introduced as follows.

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

### Check all nodes in your cluster
```shell
$ kubectl get nodes
NAME                       STATUS   ROLES    AGE     VERSION
192.168.1.146   Ready    <none>   7d14h  v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h  v1.18.4-tke.13
```

### Label one of the nodes

```shell
$ kubectl label nodes 192.168.1.146 hbase-cache=true
```

### Check all nodes again

```shell
$ kubectl get node -L hbase-cache
NAME                       STATUS   ROLES    AGE     VERSION            HBASE-CACHE
192.168.1.146   Ready    <none>   7d14h  v1.18.4-tke.13   true
192.168.1.147   Ready    <none>   7d14h  v1.18.4-tke.13
```

### Check the `Dataset` resource object to be created
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hbase
spec:
  mounts:
    - mountPoint: https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/stable/
      name: hbase
```

>? To facilitate testing, `mountPoint` is set to Web UFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

### Create the `Dataset` resource object

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
```

### Check the `GooseFSRuntime` resource object to be created
```yaml
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
        quota: 2G
        high: "0.8"
        low: "0.7"
  master:
    nodeSelector:
      hbase-cache: "true"
```
The above snippet of the configuration file contains a lot of GooseFS related configuration, and Fluid will start a GooseFS instance based on the configuration. Among the configuration, the `spec.replicas` attribute is set to `1`, indicating that Fluid will start a GooseFS instance containing 1 GooseFS master and 1 GooseFS worker.

### Create the GooseFSRuntime resource object and check its status

```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created



$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m3s   192.168.1.147   192.168.1.146   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
```

As shown above, the master is started successfully and runs on the node with the `hbase-cache=true` label.
