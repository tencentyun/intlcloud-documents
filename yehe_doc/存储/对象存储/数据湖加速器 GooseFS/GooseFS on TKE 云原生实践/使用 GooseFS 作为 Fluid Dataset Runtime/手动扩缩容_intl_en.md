## Prerequisites

You have installed [Fluid](https://github.com/fluid-cloudnative/fluid) (version 0.5.0 or later).

>? For Fluid installation details, please see [Installation](https://intl.cloud.tencent.com/document/product/436/42230).
>

## Setting Up an Environment

```shell
$ mkdir <any-path>/dataset_scale
$ cd <any-path>/dataset_scale
```

## Demo Run Example

**Create a dataset and a GooseFSRuntime**
```yaml
$ cat << EOF > dataset.yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hbase
spec:
  mounts:
    - mountPoint: https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/stable/
  name: hbase
---
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
        high: "0.95"
        low: "0.7"
EOF
```
>? To facilitate testing, `mountPoint` is set to WebUFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

In the above example, we set `GooseFSRuntime.spec.replicas` to `1`, indicating that Fluid will launch a GooseFS cluster containing one GooseFS worker to cache data in the dataset.

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
goosefsruntime.data.fluid.io/hbase created
```

After the GooseFS cluster is started properly, you can see that the completed dataset and GooseFSRuntime are in the following states:

GooseFS component status:

```shell
$ kubectl get pod
NAME                 READY   STATUS    RESTARTS   AGE
hbase-fuse-6pcnc     1/1     Running   0          3m15s
hbase-master-0       2/2     Running   0          3m50s
hbase-worker-w9wxh   2/2     Running   0          3m15s
```

Dataset status:

```shell
$ kubectl get dataset hbase
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   544.77MiB        0.00B    2.00GiB          0.0%                Bound   3m28s
```

GooseFSRuntime status:

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        4m55s
```

**Dataset scale-out**

```shell
$ kubectl scale goosefsruntime hbase --replicas=2
goosefsruntime.data.fluid.io/hbase scaled
```

Directly use the 'kubectl scale' command to scale out the dataset. After executing the above command successfully and waiting for some time, you can see that the states of the dataset and GooseFSRuntime have changed:

A new GooseFS worker and the corresponding GooseFS Fuse component are started successfully:

```shell
$ kubectl get pod
NAME                 READY   STATUS    RESTARTS   AGE
hbase-fuse-6pcnc     1/1     Running   0          13m
hbase-fuse-8qgww     1/1     Running   0          6m49s
hbase-master-0       2/2     Running   0          13m
hbase-worker-l4c8n   2/2     Running   0          6m49s
hbase-worker-w9wxh   2/2     Running   0          13m
```

For the dataset, the value of `Cache Capacity` is changed from `2.00GiB` to `4.00GiB`, indicating that the available cache capacity of the dataset increases:

```shell
$ kubectl get dataset hbase
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   544.77MiB        0.00B    4.00GiB          0.0%                Bound   15m
```

For GooseFSRuntime, the values of `Ready Workers` and `Ready Fuses` are changed to `2`:

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          2               2                 Ready          2             2               Ready        17m
```

Check the description of GooseFSRuntime and you can learn the latest scaling information:
```shell
$ kubectl describe goosefsruntime hbase
...
  Conditions:
    ...
    Last Probe Time:                2021-04-23T07:54:03Z
    Last Transition Time:           2021-04-23T07:54:03Z
    Message:                        The workers are scale out.
    Reason:                         Workers scaled out
    Status:                         True
    Type:                           Workers scaled out
    Last Probe Time:                2021-04-23T07:54:03Z
    Last Transition Time:           2021-04-23T07:54:03Z
    Message:                        The fuses are scale out.
    Reason:                         Fuses scaled out
    Status:                         True
    Type:                           FusesScaledOut
...
Events:
  Type    Reason   Age   From            Message
  ----    ------   ----  ----            -------
  Normal  Succeed  2m2s  GooseFSRuntime  GooseFS runtime scaled out. current replicas: 2, desired replicas: 2.
```

**Dataset scale-in**

Similar to scale-out, you can use the `kubectl scale` command to adjust the number of workers of the GooseFSRuntime:

```shell
$ kubectl scale goosefsruntime hbase --replicas=1
goosefsruntime.data.fluid.io/hbase scaled
```

After the preceding command is run, **if no application in the current environment is attempting to access the dataset**, GooseFSRuntime scale-in will be triggered.

GooseFSRuntime workers exceeding the specified number of replicas will be terminated:

```shell
NAME                 READY   STATUS        RESTARTS   AGE
hbase-fuse-8qgww     1/1     Running       0          21m
hbase-fuse-zql96     1/1     Terminating   0          17m32s
hbase-master-0       2/2     Running       0          22m
hbase-worker-f92vv   2/2     Terminating   0          17m32s
hbase-worker-l4c8n   2/2     Running       0          21m
```

The value of `Cache Capacity` of the dataset is restored to `2.00GiB`:

```shell
$ kubectl get dataset hbase
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   544.77MiB        0.00B    2.00GiB          0.0%                Bound   30m
```

>! In the current version of Fluid, there is a delay of several minutes in changing the 'Cache Capacity' attribute during dataset scale-in, so you may not notice the change of this attribute quickly.
>

For GooseFSRuntime, the values of `Ready Workers` and `Ready Fuses` are changed to `1`:

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        30m
```

Check the description of GooseFSRuntime and you can learn the latest scaling information:
```shell
$ kubectl describe goosefsruntime hbase
...
  Conditions:
    ...
    Last Probe Time:                2021-04-23T08:00:55Z
    Last Transition Time:           2021-04-23T08:00:55Z
    Message:                        The workers scaled in.
    Reason:                         Workers scaled in
    Status:                         True
    Type:                           WorkersScaledIn
    Last Probe Time:                2021-04-23T08:00:55Z
    Last Transition Time:           2021-04-23T08:00:55Z
    Message:                        The fuses scaled in.
    Reason:                         Fuses scaled in
    Status:                         True
    Type:                           FusesScaledIn
...
Events:
  Type     Reason               Age    From            Message
  ----     ------               ----   ----            -------
  Normal   Succeed              6m56s  GooseFSRuntime  GooseFS runtime scaled out. current replicas: 2, desired replicas: 2.
  Normal   Succeed              4s     GooseFSRuntime  GooseFS runtime scaled in. current replicas: 1, desired replicas: 1.
```

Fluid provides the scaling capability to help users or cluster admins timely adjust the cluster resources occupied by dataset cache to reduce the cache capacity of any infrequently used dataset (scale-in) or increase the cache capacity of any dataset as needed (scale-out), achieving more fine grained resource allocation to maximize resource utilization.

## Cleaning Up the Environment

```shell
$ kubectl delete -f dataset.yaml
```
