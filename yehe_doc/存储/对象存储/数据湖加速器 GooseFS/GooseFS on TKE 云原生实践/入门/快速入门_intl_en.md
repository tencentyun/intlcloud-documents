## Getting Started with GooseFSRuntime

The process of using GooseFSRuntime is simple. It takes only about 10 minutes to deploy the required GooseFSRuntime environment after you prepare the basic Kubernetes and Cloud Object Storage (COS) environment. The following describes the process.

## Prerequisites

- You have installed Git.
- You have installed the Kubernetes cluster (version 1.14 or later) and it supports the Container Storage Interface (CSI). To get the best practice, you can deploy it by referring to [Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457/30635).
- You have installed kubectl (version 1.14 or later). For kubectl installation and configuration details, see [Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
- You have installed Helm (version 3.0 or later). For Helm 3 installation and configuration details, see [Helm documentation](https://v3.helm.sh/docs/intro/install/).
- If the local installation package `fluid.tgz` is available, you can directly install it:
```shell
$ helm install fluid fluid.tgz
NAME: fluid
LAST DEPLOYED: Mon Mar 29 11:21:46 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

>? The general format of the `helm install` command is `helm install <RELEASE_NAME> <SOURCE>`. In the command, the first `fluid` specifies the name (customizable) of the release installed, and the second `fluid.tgz` specifies the path to Helm charts.
>

## Directions

### 1. Create a namespace
```shell
kubectl create ns fluid-system
```
### 2. Download Fluid

Click to download the [fluid-0.6.0.tgz](https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/fluid.tgz) installation package.

>! You can also go to [Fluid Releases](https://github.com/fluid-cloudnative/fluid/releases) to download the latest version. However, certain machines may have problems accessing the website from inside China.
>

### 3. Install Fluid with Helm

```shell
helm install --set runtime.goosefs.enabled=true fluid fluid-0.6.0.tgz
```

### 4. Check the running status of Fluid

```shell
$ kubectl get pod -n fluid-system
NAME                                         READY   STATUS    RESTARTS   AGE
csi-nodeplugin-fluid-2mfcr                   2/2     Running   0          108s
csi-nodeplugin-fluid-l7lv6                   2/2     Running   0          108s
dataset-controller-5465c4bbf9-5ds5p          1/1     Running   0          108s
goosefsruntime-controller-564f59bdd7-49tkc    1/1     Running   0          108s
```
The number of `csi-nodeplugin-fluid-xx` must be the same as the number of nodes in the Kubernetes cluster.

### 5. Prepare the GooseFS cache environment

#### a. Prepare the COS service

You need to enable COS and create a COS bucket. For creation instructions, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

#### b. Prepare test sample data

We can use Spark related resource files on the Apache image site as the remote files used in the demo. In practice, you can also change these remote files to any of your remote files.

- Download the remote resource files to your local host
```shell
mkdir tmp
cd tmp
wget https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-2.4.8/spark-2.4.8-bin-hadoop2.7.tgz 
wget https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz 
```
- Upload the local files to COS
You can use the [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) client or [COS SDK](https://intl.cloud.tencent.com/document/product/436/6474) provided by the Tencent Cloud COS team to upload the files downloaded to the local host to the COS bucket according to their respective use instructions.

#### c. Create a dataset and a GooseFSRuntime

i. Create a file named `resource.yaml`, which contains the following:
- Data storage location and UFS dataset information
- Create a dataset CRD object, describing the source of the dataset, such as `test-bucket` in this example
- Create a GooseFSRuntime, equivalent to starting a GooseFS cluster to provide the caching service

<dx-codeblock>
::: yaml yaml
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
        low: "0.8"
:::
</dx-codeblock>

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

ii. Run the following command to create GooseFSRuntime:
```shell
kubectl create -f resource.yaml
```
iii. Check the status of the GooseFSRuntime deployed. If all states are `Ready`, GooseFSRuntime is deployed successfully.
```shell
kubectl get goosefsruntime hadoop
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hadoop    Ready           Ready           Ready     62m
```
iv. Check the dataset status. If the state is `Bound`, the dataset is bound successfully.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop        511MiB       0.00B    180.00GiB              0.0%          Bound   1h
```
v. Check the PV and PVC creation results. PV and PVC are automatically created during GooseFSRuntime deployment.
```shell
kubectl get pv,pvc
NAME                      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM            STORAGECLASS   REASON   AGE
persistentvolume/hadoop   100Gi      RWX            Retain           Bound    default/hadoop                           58m


NAME                           STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/hadoop   Bound    hadoop   100Gi      RWX                           58m
```

### 6. Create an application container to try out the acceleration effect

You can create an application container to use the GooseFS acceleration service or submit a machine learning job to try out related features.

In the following example, we create an application container `app.yaml` to use the dataset. We will access the same data multiple times and compare access times to demonstrate the acceleration effect of GooseFS.
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

i. Use kubectl to create an application.
```shell
kubectl create -f app.yaml
```
ii. Check the file size.
```shell
$ kubectl exec -it demo-app -- bash
$ du -sh /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
210M/data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
```
iii. Check the file copy time (18 seconds in this example).
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2  /dev/null

real    0m18.386s
user    0m0.002s
sys      0m0.105s
```
iv. Now check the dataset cache status. You can find that 210 MB data is all cached locally.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop   210.00MiB       210.00MiB    180.00GiB        100.0%           Bound   1h
```
v. To prevent other factors (such as page cache) affecting the results, we delete the previous container, create the same application, and try to access the same file. Since the file is already cached by GooseFS at this point, you can see that the second access takes much less time than the first.
```shell
kubectl delete -f app.yaml && kubectl create -f app.yaml
```
vi. Check the file copy time (48 ms in this example). The entire copy duration is reduced by 300 times.
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2  /dev/null

real    0m0.048s
user    0m0.001s
sys      0m0.046s
```

### 7. Clean up the environment

- Delete the application and the application container.
- Delete GooseFSRuntime.
```shell
kubectl delete goosefsruntime hadoop
```
- Delete the dataset.
```shell
kubectl delete dataset hadoop
```

For more information about Fluid GooseFSRuntime, see the [feature list](https://intl.cloud.tencent.com/document/product/436/42233). 
