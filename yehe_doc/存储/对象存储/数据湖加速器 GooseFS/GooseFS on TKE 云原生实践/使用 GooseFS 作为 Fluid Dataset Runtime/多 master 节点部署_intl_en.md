## Overview

A system with a single master may be less stable, and in some online service scenarios, multiple masters are required to ensure fault tolerance. To implement fault tolerance, GooseFSRuntime provides 3 masters, which are elected using Raft, a highly consistent, decentralized, highly available distributed protocol that is widely used in engineering.

The feature is introduced as follows.

## Prerequisites

Before running the sample code provided in this document, install Fluid by referring to [Installation](https://intl.cloud.tencent.com/document/product/436/42230) and check that all the components used by Fluid are running properly.

```shell
$ kubectl get pod -n fluid-system
goosefsruntime-controller-5b64fdbbb-84pc6   1/1     Running   0          8h
csi-nodeplugin-fluid-fwgjh                  2/2     Running   0          8h
csi-nodeplugin-fluid-ll8bq                  2/2     Running   0          8h
csi-nodeplugin-fluid-dhz7d                  2/2     Running   0          8h
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
192.168.1.145   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```


### Check the `Dataset` resource object to be created
```shell
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
```shell
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hbase
spec:
  replicas: 3
  tieredstore:
    levels:
      - mediumtype: HDD
        path: /mnt/disk1
        quota: 2G
        high: "0.8"
        low: "0.7"
  master:
    replicas: 3
```

Specify `spec.master.replicas=3` to enable the Raft 3-master mode. The parameter must be set to a positive odd number.

### Create the GooseFSRuntime resource object and check its status

```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created



$ kubectl get pod
NAME                          READY   STATUS    RESTARTS   AGE
hbase-fuse-4v9mq     1/1     Running   0          84s
hbase-fuse-5kjbj     1/1     Running   0          84s
hbase-fuse-tp2q2     1/1     Running   0          84s
hbase-master-0       1/1     Running   0          104s
hbase-master-1       1/1     Running   0          102s
hbase-master-2       1/1     Running   0          100s
hbase-worker-cx8x7   1/1     Running   0          84s
hbase-worker-fjsr6   1/1     Running   0          84s
hbase-worker-fvpgc   1/1     Running   0          84s
```

### Check the status of the `GooseFSRuntime` object

```shell
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hbase   Ready           Ready            Ready     15m
```

Check that all `PHASE` values are `Ready`.

### Check the Raft status (leader/follower)

Log in to the pod of one master:

```shell
$ kubectl exec -ti hbase-master-0 bash
$ goosefs fs masterInfo
```

You can see that the one node is `leader`, and the other two are `follower`:

```shell
current leader master: hbase-master-0:26000
All masters: [hbase-master-0:26000, hbase-master-1:26000, hbase-master-2:26000]
```
