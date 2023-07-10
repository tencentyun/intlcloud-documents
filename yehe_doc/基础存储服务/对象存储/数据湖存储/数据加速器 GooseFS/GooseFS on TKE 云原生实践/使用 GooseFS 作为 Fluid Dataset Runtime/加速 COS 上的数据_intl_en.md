## Prerequisites

- You have downloaded and installed [Fluid](https://github.com/fluid-cloudnative/fluid) (version 0.6.0 or later).
>! Click to download the [fluid-0.6.0.tgz](https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/fluid.tgz) installation package.
>
- For Fluid installation details, please see [Installation](https://intl.cloud.tencent.com/document/product/436/42230).

## Creating a Dataset and GooseFSRuntime

1. Create a file named `resource.yaml`, which contains the following:
 - Dataset and UFS dataset information
 - Create a dataset CRD object, describing the source of the dataset, such as `test-bucket` in this example
 - Create a GooseFSRuntime, equivalent to starting a GooseFS cluster to provide the caching service

```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hadoop
spec:
  mounts:
    - mountPoint: cosn://test-bucket/
      options:
        fs.cosn.userinfo.secretId: <COS_SECRET_ID>
        fs.cosn.userinfo.secretKey: <COS_SECRET_KEY>
        fs.cosn.bucket.region: <COS_REGION>
        fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
        fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
        fs.cosn.userinfo.appid: <COS_APP_ID>
  name: hadoop
	
---
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hadoop
spec:
  replicas: 2
  tieredstore:
    levels:
      - mediumtype: HDD
        path: /mnt/disk1
        quota: 100G
        high: "0.9"
        low: "0.2"
```
To ensure the security of key information such as AK, you are advised to use `secret` to save related key information. For details about how to use `secret`, see <a href="https://intl.cloud.tencent.com/document/product/436/42239">Using Parameters for Encryption</a>.
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
stringData:
  fs.cosn.userinfo.secretId: <COS_SECRET_ID>
  fs.cosn.userinfo.secretKey: <COS_SECRET_KEY>
---
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hadoop
spec:
  mounts:
    - mountPoint: cosn://yourbucket/
      options:
        fs.cosn.bucket.region: <COS_REGION>
        fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
        fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
        fs.cosn.userinfo.appid: <COS_APP_ID>
      name: hadoop
      encryptOptions:
        - name: fs.cosn.userinfo.secretId
          valueFrom:
            secretKeyRef:
              name: mysecret
              key: fs.cosn.userinfo.secretId
        - name: fs.cosn.userinfo.secretKey
          valueFrom:
            secretKeyRef:
              name: mysecret
              key: fs.cosn.userinfo.secretKey
---
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hadoop
spec:
  replicas: 2
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1
        quota: 100G
        high: "0.9"
        low: "0.2"
```


 - Dataset:
    - mountPoint: indicates the UFS mount path. This path does not need to contain endpoint information.
    - options: specifies necessary bucket information. For details, see [API glossary](https://intl.cloud.tencent.com/document/product/436/7751).
    - fs.cosn.userinfo.secretId/fs.cosn.userinfo.secretKey: information of the key with the permission to access the COS bucket.
 - GooseFSRuntime: for more APIs, see [api_doc.md](https://github.com/fluid-cloudnative/fluid/blob/master/docs/en/dev/api_doc.md).
    - replicas: indicates the number of nodes of the created GooseFS cluster.
    - mediumtype: GooseFS supports three types of cache media: HDD, SSD, and MEM, and provides multi-level cache configuration.
    - path: indicates the storage path.
    - quota: indicates the maximum cache capacity.
    - high: indicates the upper limit on disk utilization.
    - low: indicates the lower limit on disk utilization.
2. Run the following command to create GooseFSRuntime:
```shell
$ kubectl create -f resource.yaml
```
3. Check the status of the GooseFSRuntime deployed. If all states are `Ready`, GooseFSRuntime is deployed successfully.
```shell
$ kubectl get goosefsruntime hadoop
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hadoop    Ready           Ready           Ready     62m
```
4. Check the dataset status. If the state is `Bound`, the dataset is bound successfully.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop       210.00MiB       0.00B    180.00GiB              0.0%          Bound   1h
```
5. Check the PV and PVC creation results. PV and PVC are automatically created during GooseFSRuntime deployment.
```shell
$ kubectl get pv,pvc
NAME                      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM            STORAGECLASS   REASON   AGE
persistentvolume/hadoop   100Gi      RWX            Retain           Bound    default/hadoop                           58m

NAME                           STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/hadoop   Bound    hadoop   100Gi      RWX                           58m
```

## Checking Whether the Service Is Normal

1. Log in to the master and worker pods and observe whether files can be listed properly.
```shell
$ kubectl get pod
NAME                              READY   STATUS      RESTARTS   AGE
hadoop-fuse-svz4s         1/1     Running     0          23h
hadoop-master-0           1/1     Running     0          23h
hadoop-worker-2fpbk       1/1     Running     0          23h
```
 ```shell
$ kubectl exec -ti hadoop-goosefs-master-0 bash
goosefs fs ls /hadoop
 ```
2. Log in to the Fuse pod and observe whether files can be listed properly.
```shell
$ kubectl exec -ti hadoop-goosefs-fuse-svz4s bash
cd /runtime-mnt/goosefs/<namespace>/<DatasetName>/goosefs-fuse/<DatasetName>
```

## Creating an Application Container to Try Out the Acceleration Effect

You can create an application container to use the GooseFS acceleration service or submit a machine learning job to try out related features. In the following example, we create an application container `app.yaml` to use the dataset. We will access the same data multiple times and compare access times to demonstrate the acceleration effect of GooseFS.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: demo-app
spec:
  containers:
    - name: demo
      image: nginx
      volumeMounts:
        - mountPath: /data
          name: hadoop
  volumes:
    - name: hadoop
      persistentVolumeClaim:
        claimName: hadoop
```

1. Use kubectl to create an application.
```shell
$ kubectl create -f app.yaml
```
2. Check the file size.
```shell
$ kubectl exec -it demo-app -- bash
$ du -sh /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
210M/data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
```
3. Check the file copy time (18 seconds in this example).
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 /dev/null

real0m18.386s
user0m0.002s
sys  0m0.105s
```
4. Now check the dataset cache status. You can find that 210 MB data is all cached locally.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop   210.00MiB       210.00MiB    180.00GiB        100.0%           Bound   1h
```
5. To prevent other factors (such as page cache) affecting the results, we delete the previous container, create the same application, and try to access the same file. Since the file is already cached by GooseFS at this point, you can see that the second access takes much less time than the first.
```shell
$ kubectl delete -f app.yaml && kubectl create -f app.yaml
```
6. Check the file copy time (48 ms in this example). The entire copy duration is reduced by 300 times.
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2  /dev/null

real0m0.048s
user0m0.001s
sys  0m0.046s
```

## Cleaning Up the Environment

```shell
$ kubectl delete -f resource.yaml
```
