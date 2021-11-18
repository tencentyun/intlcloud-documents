## Overview

In Fluid, the default data source mount path is '/<ns>/dir', with a layer of the `ns` path in between by default. If you have only one data source, you can mount the data source to the root directory of the GooseFS protocol. By doing so, you can use this feature without changing your programs at all.

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
      path: /
```


>? To facilitate testing, `mountPoint` is set to Web UFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

In the `spec` attribute of the `Dataset` resource object, we defined the `path` sub-attribute to specify that data sources must be mounted to the root directory.

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
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: MEM
        path: /dev/shm
        quota: 2Gi
        high: "0.95"
        low: "0.7"
```
The above snippet of the configuration file contains a lot of GooseFS related configuration, and Fluid will start a GooseFS instance based on the configuration. Among the configuration, the `spec.replicas` attribute is set to `1`, indicating that Fluid will start a GooseFS instance containing 1 GooseFS master and 1 GooseFS worker.


### Create the GooseFSRuntime resource object and check its status

```shell
$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m3s   192.168.1.147   192.168.1.146   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
```


### Create a Fuse node and check the mount path information

```shell
$ kubectl exec -ti hbase-fuse-42csf bash
$ ls /runtime-mnt/goosefs/<namespace>/<DatasetName>/goosefs-fuse/
drwxrwx--x 2 message   99  4096 Apr 23 16:39 /user
drwxr-xr-x 2 message root  4096 Apr 23 16:38 /data
```
