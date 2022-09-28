To ensure the performance of the application when accessing data, the data in a remote storage system can be pulled to the distributed cache engine that is close to the computing node through **data preloading** before the application starts. Then the application that consumes the data can enjoy the acceleration effect brought by distributed cache even at the first run.

We provide DataLoad CRD to help you easily implement and control data preloading with simple configuration.

This document provides two examples to demonstrate how to use DataLoad CRD:

- DataLoad Quick Usage
- DataLoad Advanced Configuration


## Prerequisites

You have installed [Fluid](https://github.com/fluid-cloudnative/fluid) (version 0.6.0 or later).

>? For Fluid installation details, please see [Installation](https://intl.cloud.tencent.com/document/product/436/42230).
>

## Setting Up an Environment

```yaml
$ mkdir <any-path>/warmup
$ cd <any-path>/warmup
```

## DataLoad Quick Usage

**Configure the `Dataset` and `Runtime` objects to be created**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: spark
spec:
  mounts:
    - mountPoint: https://mirrors.bit.edu.cn/apache/spark/
      name: spark 
---
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: spark
spec:
  replicas: 2
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
```

>? To facilitate testing, `mountPoint` is set to WebUFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

Here, we'd like to create a resource object whose `kind` is `Dataset`. `Dataset` is a Custom Resource Definition (CRD) defined by Fluid and is used to tell Fluid where to find data desired. Fluid mounts the `mountPoint` attribute defined in this CRD object to GooseFS.

In this example, for simplicity, we use COS for demonstration.

**Create the `Dataset` and `Runtime` objects**

```shell
$ kubectl create -f dataset.yaml
```

**Wait for `Dataset` and `Runtime` to be ready**

```shell
$ kubectl get datasets spark
```

If information similar to the following is displayed, `Dataset` and `Runtime` are ready:

```shell
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
spark   1.92GiB          0.00B    4.00GiB          0.0%                Bound   4m4s
```

**Configure the `DataLoad` object to be created**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  loadMetadata: true
  dataset:
    name: spark
    namespace: default
```

`spec.dataset` specifies the target dataset that needs to be preloaded. In this example, our target is the dataset named `spark` under the `default` namespace. You can modify the configuration above if it doesn't match your actual environment.

**By default, according to the above `DataLoad` configuration, the system will attempt to load all the data in the entire dataset.** If you want to control the data preloading behaviors in a more fine-grained way (e.g. preload data under a specified path only), please see [DataLoad Advanced Configurations](https://github.com/fluid-cloudnative/fluid/blob/master/docs/en/dev/api_doc.md).

**Create the `DataLoad` object**

```shell
$ kubectl create -f dataload.yaml
```

**Check the status of the created `DataLoad` object**

```shell
$ kubectl get dataload spark-dataload
```

Information similar to the following will be displayed:

```shell
NAME             DATASET   PHASE     AGE
spark-dataload   spark     Loading   2m13s
```

You can also use `kubectl describe` to get more details about the `DataLoad`:

```shell
$ kubectl describe dataload spark-dataload
```

Information similar to the following will be displayed:
```
Name:         spark-dataload
Namespace:    default
Labels:       <none>
Annotations:  <none>
API Version:  data.fluid.io/v1alpha1
Kind:         DataLoad
...
Spec:
  Dataset:
    Name:       spark
    Namespace:  default
Status:
  Conditions:
  Phase:  Loading
Events:
  Type    Reason              Age   From      Message
  ----    ------              ----  ----      -------
  Normal  DataLoadJobStarted  80s   DataLoad  The DataLoad job spark-dataload-loader-job started
```

The data preloading process may take several minutes depending on your network environment.

**Wait for the data preloading to complete**

```shell
$ kubectl get dataload spark-dataload
```

If the data preloading is completed, the value of `Phase` of the `DataLoad` changes from `Loading` to `Complete`.

```shell
NAME             DATASET   PHASE      AGE
$ spark-dataload   spark     Complete   5m17s
```

Now, check the cache status of the `Dataset` object:

```shell
$ kubectl get dataset spark
```

You'll find that all data in the remote file storage system has already been preloaded into the distributed cache engine:

```shell
NAME    UFS TOTAL SIZE   CACHED    CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
spark   1.92GiB          1.92GiB   4.00GiB          100.0%              Bound   7m41s
```

**Clean up the environment**

```shell
$ kubectl delete -f .
```

## DataLoad Advanced Configuration

Besides the basic data preloading feature demonstrated in the above example, with simple configuration, you can enable some advanced data preloading features, including:

- Preload data under one or more specified dataset subdirectories only
- Set cache replicas when preloading data
- Sync metadata before preloading data

### Preload data under one or more specified dataset subdirectories only

Preload data under some specified subdirectories (or files) instead of the whole dataset. For example:
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  dataset:
    name: spark
    namespace: default
  loadMetadata: true
  target:
    - path: /spark/spark-2.4.8
    - path: /spark/spark-3.0.1/pyspark-3.0.1.tar.gz
```

The above DataLoad will only preload all files in `/spark/spark-2.4.8` and the `/spark/spark-3.0.1/pyspark-3.0.1.tar.gz` file.

In `spec.target.path`, all values are relative paths under the mount point specified by `mountpoint`. Assume that the current mount point is `cos://test/` and the original path contains the following files:

```shell
cos://test/user/sample.txt
cos://test/data/fluid.tgz
```

Then, you can define `target.path` as follows:
```yaml
target:
  - path: /user
  - path: /data
```

### Set cache replicas when preloading data

When preloading data, you can set cache replicas by simple configuration. For example:
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  dataset:
    name: spark
    namespace: default
  loadMetadata: true
  target:
    - path: /spark/spark-2.4.8
      replicas: 1
    - path: /spark/spark-3.0.1/pyspark-3.0.1.tar.gz
      replicas: 2
```

The above DataLoad will preload all the files in the `/spark/spark-2.4.8` directory with only **1** cache replica in the distributed cache engine, and preload the `/spark/spark-3.0.1/pyspark-3.0.1.tar.gz` file with **2** cache replicas in the distributed cache engine.

### Sync metadata before preloading data (recommended)

In many scenarios, files in the remote storage system may have changed, and the distributed cache engine needs to sync the metadata of the files to perceive the changes in the underlying storage system. Therefore, before data preloading, you can configure `spec.loadMetadata` of the `DataLoad` object to sync metadata in advance. For example:
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  dataset:
    name: spark
    namespace: default
  loadMetadata: true
  target:
    - path: /
      replicas: 1
```
