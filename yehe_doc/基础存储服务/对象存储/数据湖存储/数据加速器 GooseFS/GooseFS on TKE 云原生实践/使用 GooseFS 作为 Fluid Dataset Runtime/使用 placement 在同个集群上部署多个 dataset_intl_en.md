Through GooseFS and [Fuse](https://github.com/libfuse/libfuse), Fluid provides users with a type of simple file access APIs to enable any applications running on Kubernetes to access files stored in remote file systems, just like accessing files in local file systems. Fluid manages and isolates the entire lifecycle of datasets, especially for short lifecycle applications (such as data analysis tasks and machine learning tasks), and users can deploy such applications on a large scale in a cluster.


## Prerequisites

Before running the sample code provided in this document, install Fluid by referring to [Installation](https://intl.cloud.tencent.com/document/product/436/42230) and check that all the components used by Fluid are running properly.
```shell
$ kubectl get pod -n fluid-system
NAME                                  READY   STATUS    RESTARTS   AGE
goosefsruntime-controller-5b64fdbbb-84pc6   1/1     Running   0          8h
csi-nodeplugin-fluid-fwgjh                  2/2     Running   0          8h
csi-nodeplugin-fluid-ll8bq                  2/2     Running   0          8h
dataset-controller-5b7848dbbb-n44dj         1/1     Running   0          8h
```

Normally, you shall see a pod named `dataset-controller`, a pod named `goosefsruntime-controller`, and multiple pods named `csi-nodeplugin`. The number of `csi-nodeplugin` pods depends on the number of nodes in your Kubernetes cluster.


## Demo Run Example
**Label a node**

```shell
$ kubectl  label node 192.168.0.199 fluid=multi-dataset
```

>? In the following steps, we will use `NodeSelector` to manage the nodes scheduled by the `Dataset` resource object. The setting here is only for testing.
>

**Check the `Dataset` resource object to be created**

- dataset.yaml
<dx-codeblock>
::: yaml yaml
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
            - key: fluid
              operator: In
              values:
                - "multi-dataset"
  placement: "Shared" // Setting the parameter to `Exclusive` or empty means dataset exclusive
:::
</dx-codeblock>
- dataset1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: spark
spec:
  mounts:
    - mountPoint: https://mirrors.bit.edu.cn/apache/spark/
      name: spark
  nodeAffinity:
      required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: fluid
              operator: In
              values:
                - "multi-dataset"
  placement: "Shared" 
:::
</dx-codeblock>

>? To facilitate testing, `mountPoint` is set to WebUFS in this example. If you want to mount COS, see [Mounting COS (COSN) to GooseFS](https://intl.cloud.tencent.com/document/product/436/41024).
>

**Create the `Dataset` resource object**

```shell
$ kubectl apply -f dataset.yaml
dataset.data.fluid.io/hbase created
$ kubectl apply -f dataset1.yaml
dataset.data.fluid.io/spark created
```


**Check the status of the `Dataset` resource object**

```shell
$ kubectl get dataset
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE      AGE
hbase                                                                  NotBound   6s
spark                                                                  NotBound   4s
```
As shown above, the value of the `phase` attribute in `status` is `NotBound`, indicating that the `Dataset` resource object is not yet bound with any `GooseFSRuntime` resource object. Next, we will create a `GooseFSRuntime` resource object.


**Check the `GooseFSRuntime` resource object to be created**

- runtime.yaml
<dx-codeblock>
::: yaml yaml
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
        high: "0.8"
        low: "0.7"
:::
</dx-codeblock>
- runtime-1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: spark
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk2/
        quota: 4G
        high: "0.8"
        low: "0.7"
:::
</dx-codeblock>

**Create the `GooseFSRuntime` resource object**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


# Wait for the status of all dataset HBase components to change to Running 
$ kubectl get pod -o wide | grep hbase
NAME                              READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-jl2g2           1/1     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>
hbase-master-0             2/2     Running   0          2m55s   192.168.0.200   192.168.0.200   <none>           <none>
hbase-worker-g89p8         2/2     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>

$ kubectl create -f runtime1.yaml
goosefsruntime.data.fluid.io/spark created
```

**Check whether the `GooseFSRuntime` resource object is created**

```shell
$ kubectl get goosefsruntime
NAME    MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hbase   Ready          Ready          Ready        2m14s
spark   Ready          Ready          Ready        58s
```

`GooseFSRuntime` is another CRD defined by Fluid. A `GooseFSRuntime` resource object describes the configuration information required to run a GooseFS instance in a Kubernetes cluster.


Wait for a while, and make sure all components defined in the `GooseFSRuntime` resource object are successfully started. You shall see information similar to the following:


```shell
$ kubectl get pod -o wide
NAME                        READY   STATUS    RESTARTS   AGE     IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-jl2g2     1/1     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>
hbase-master-0       2/2     Running   0          2m55s   192.168.0.200   192.168.0.200   <none>           <none>
hbase-worker-g89p8   2/2     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>
spark-fuse-5z49p     1/1     Running   0          19s     192.168.0.199   192.168.0.199   <none>           <none>
spark-master-0       2/2     Running   0          50s     192.168.0.200   192.168.0.200   <none>           <none>
spark-worker-96ksn   2/2     Running   0          19s     192.168.0.199   192.168.0.199   <none>           <none>
```
Note that the worker and Fuse components of the different datasets above can be scheduled to the same node `192.168.0.199`.

**Check the status of the `Dataset` resource object again**

```shell
$ kubectl get dataset 
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   443.89MiB        0.00B    2.00GiB          0.0%                Bound   11m
spark   1.92GiB          0.00B    4.00GiB          0.0%                Bound   9m38s
```

Because the `Dataset` resource object has been bound to a successfully started `GooseFSRuntime`, the state of the `Dataset` resource object has been updated, and the value of the `PHASE` attribute has changed to `Bound`. The basic information about the resource object can be obtained through the above command.


**Check the status of the `GooseFSRuntime` object**

```shell
$ kubectl get goosefsruntime -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        11m
spark   1               1                 Ready          1               1                 Ready          1             1               Ready        9m52s
```

>? The `status` attribute of the `GooseFSRuntime` resource object contains more detailed information.
>

**Check `PersistentVolume` and `PersistentVolumeClaim` related to the remote files**

```shell
$ kubectl get pv
NAME    CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM           STORAGECLASS   REASON   AGE
hbase   100Gi      RWX            Retain           Bound    default/hbase                           4m55s
spark   100Gi      RWX            Retain           Bound    default/spark                           51s
```

```shell
$ kubectl get pvc
NAME    STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
hbase   Bound    hbase    100Gi      RWX                           4m57s
spark   Bound    spark    100Gi      RWX                           53s
```

After the `Dataset` resource object is ready (bound with the GooseFS instance), the PV and PVC associated with the resource object are generated by Fluid. Applications now can mount remote files to the pod via the PVC and access the remote files via the mount directory.

## Remote File Access

**Check the application to be created**

- nginx.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-hbase
spec:
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
  nodeName: 192.168.0.199
:::
</dx-codeblock>
- nginx1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-spark
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
        - mountPath: /data
          name: hbase-vol
  volumes:
    - name: hbase-vol
      persistentVolumeClaim:
        claimName: spark
  nodeName: 192.168.0.199
:::
</dx-codeblock>

**Run the application to access remote files**
```shell
$ kubectl create -f nginx.yaml
$ kubectl create -f nginx1.yaml
```

Log in to the Nginx HBase pod:

```shell
$ kubectl exec -it nginx-hbase -- bash
```

Check the mounting status of the remote files:

```shell
$ ls -lh /data/hbase
total 444M
-r--r----- 1 root root 193K Sep 16 00:53 CHANGES.md
-r--r----- 1 root root 112K Sep 16 00:53 RELEASENOTES.md
-r--r----- 1 root root  26K Sep 16 00:53 api_compare_2.2.6RC2_to_2.2.5.html
-r--r----- 1 root root 211M Sep 16 00:53 hbase-2.2.6-bin.tar.gz
-r--r----- 1 root root 200M Sep 16 00:53 hbase-2.2.6-client-bin.tar.gz
-r--r----- 1 root root  34M Sep 16 00:53 hbase-2.2.6-src.tar.gz
```

Log in to an Nginx Spark pod:
```shell
$ kubectl exec -it nginx-spark -- bash
```

Check the mounting status of the remote files:

```shell
$ ls -lh /data/spark/
total 1.0K
dr--r----- 1 root root 7 Oct 22 12:21 spark-2.4.7
dr--r----- 1 root root 7 Oct 22 12:21 spark-3.0.1
$ du -h /data/spark/
999M/data/spark/spark-3.0.1
968M/data/spark/spark-2.4.7
2.0G/data/spark/
```

Log out of the Nginx pod:

```shell
$ exit
```

As shown above, all the files stored on the WebUFS show no differences from any other file stored in the local file system of any pod and they can be easily accessed by the pod.

## Accelerating Access to Remote Files

To demonstrate how great speedup you may enjoy when accessing remote files, we provide a test job demo:

**Check the test job to be launched**

- app.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: fluid-copy-test-hbase
spec:
  template:
    spec:
      restartPolicy: OnFailure
      containers:
        - name: busybox
          image: busybox
          command: ["/bin/sh"]
          args: ["-c", "set -x; time cp -r /data/hbase ./"]
          volumeMounts:
            - mountPath: /data
              name: hbase-vol
      volumes:
        - name: hbase-vol
          persistentVolumeClaim:
            claimName: hbase
      nodeName: 192.168.0.199
:::
</dx-codeblock>
- app1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: fluid-copy-test-spark
spec:
  template:
    spec:
      restartPolicy: OnFailure
      containers:
        - name: busybox
          image: busybox
          command: ["/bin/sh"]
          args: ["-c", "set -x; time cp -r /data/spark ./"]
          volumeMounts:
            - mountPath: /data
              name: spark-vol
      volumes:
        - name: spark-vol
          persistentVolumeClaim:
            claimName: spark
      nodeName: 192.168.0.199
:::
</dx-codeblock>


**Launch the test job**

```shell
$ kubectl create -f app.yaml
job.batch/fluid-copy-test-hbase created
$ kubectl create -f app1.yaml
job.batch/fluid-copy-test-spark created
```

The HBase task program executes a shell command `time cp -r /data/hbase ./`, and `/data/hbase` is the location where the remote file is mounted in the pod. After the command is completed, the execution duration of the command will be displayed on the terminal.

The Spark task program executes a shell command `time cp -r /data/spark ./`, and `/data/spark` is the location where the remote file is mounted in the pod. After the command is completed, the execution duration of the command will be displayed on the terminal.

Wait for a while and make sure the test job is completed. You can check its running status by using the following command:

```shell
$ kubectl get pod -o wide | grep copy 
fluid-copy-test-hbase-r8gxp   0/1     Completed   0          4m16s   172.29.0.135    192.168.0.199   <none>           <none>
fluid-copy-test-spark-54q8m   0/1     Completed   0          4m14s   172.29.0.136    192.168.0.199   <none>           <none>
```

If the above result is displayed, the jobs have been completed.

>!  `r8gxp` in `fluid-copy-test-hbase-r8gxp` is an identifier generated by the test job we created. You may have a different identifier in your environment. Please remember to replace it with your own identifier in the commands in the following steps.
>

**Check the running duration of the test job**


```shell
$ kubectl  logs fluid-copy-test-hbase-r8gxp
+ time cp -r /data/hbase ./
real    3m 34.08s
user    0m 0.00s
sys     0m 1.24s
$ kubectl  logs fluid-copy-test-spark-54q8m
+ time cp -r /data/spark ./
real    3m 25.47s
user    0m 0.00s
sys     0m 5.48s
```


As shown above, reading the first remote file, HBase took nearly 3 minutes and 34 seconds, and Spark nearly 3 minutes and 25 seconds.


**Check the status of the `Dataset` resource object**


```shell
$ kubectl get dataset
NAME    UFS TOTAL SIZE   CACHED      CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   443.89MiB        443.89MiB   2.00GiB          100.0%              Bound   30m
spark   1.92GiB          1.92GiB     4.00GiB          100.0%              Bound   28m
```

Now, all the remote files have been cached in GooseFS.

**Re-launch the test job**

```shell
$ kubectl delete -f app.yaml
$ kubectl create -f app.yaml
$ kubectl delete -f app1.yaml
$ kubectl create -f app1.yaml
```

Since the remote files have been cached, the test job can be completed quickly:

```shell
$ kubectl get pod -o wide| grep fluid
fluid-copy-test-hbase-sf5md   0/1     Completed   0          53s   172.29.0.137    192.168.0.199   <none>           <none>
fluid-copy-test-spark-fwp57   0/1     Completed   0          51s   172.29.0.138    192.168.0.199   <none>           <none>
```

```shell
$ kubectl  logs fluid-copy-test-hbase-sf5md
+ time cp -r /data/hbase ./
real    0m 0.36s
user    0m 0.00s
sys     0m 0.36s
$ kubectl  logs fluid-copy-test-spark-fwp57
+ time cp -r /data/spark ./
real    0m 1.57s
user    0m 0.00s
sys     0m 1.57s
```

Now, accessing the same file, HBase took only 0.36 seconds and Spark took only 1.57 seconds.

The great speedup is attributed to the powerful caching capability provided by GooseFS. With the capability, once you access a remote file, it will be cached in GooseFS. Whenever you access the same file again in the future, you will enjoy local access via GooseFS.

## Cleaning Up the Environment
```shell
$ kubectl delete -f .
$ kubectl label node 192.168.0.199 fluid-
```
