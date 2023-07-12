To deploy GooseFS using TKE, the [open source Fluid component](https://github.com/fluid-cloudnative/fluid) is required, which is available in the TKE application market. You can deploy as follows:

1. Use [Fluid helm chart](https://console.cloud.tencent.com/tke2/market/detail?chart=fluid&project=qcloud-stable&clusterType=tke) to deploy controllers.
2. Use kubectl to create the dataset and GooseFS runtime.


## Preparations
1.  Have a Tencent Cloud TKE cluster.
2.  Have installed kubectl of v1.18 or a later version.

## Installation

1. Find Fluid from the [TKE Application Market](https://console.cloud.tencent.com/tke2/market).

2. Install Fluid controllers.

3. Check the controllers. You can click **Cluster** in the left sidebar and find the desired cluster. If there are two controllers, Fluid has been installed successfully.



## Operation Example

### 1. Authorize cluster access

```shell
[root@master01 run]# export KUBECONFIG=xxx/cls-xxx-config (Download the cluster credential to a directory from the TKE console.)
```

>! You need to grant the cluster’s API Server access to the public network.
>

### 2. Create a UFS dataset (using COS as an example)

Create `secret.yaml` for encryption. The template is as follows:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
stringData:
  fs.cosn.userinfo.secretKey: xxx
  fs.cosn.userinfo.secretId:xxx
```

Create `secret`:
```shell
[root@master01 ~]# kubectl apply  -f secret.yaml
secret/mysecret created
```

`dataset.yaml` template:
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: slice1
spec:
  mounts:
  - mountPoint: cosn://{your bucket}
    name: slice1
    options:
      fs.cosn.bucket.region: ap-beijing
      fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
      fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
      fs.cosn.userinfo.appid: "${your appid}"
    encryptOptions:
      - name: fs.cosn.userinfo.secretKey
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: fs.cosn.userinfo.secretKey
      - name: fs.cosn.userinfo.secretId
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: fs.cosn.userinfo.secretId
```

Create a dataset:
```shell
[root@master01 run]# kubectl apply -f dataset.yaml 
dataset.data.fluid.io/slice1 created
```

Query the dataset status (NotBond):
```shell
[root@master01 run]# kubectl get dataset
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE      AGE
slice1 
                                                                 NotBound   11s
```

### 3. Create runtime

`untime.yaml` template:

```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: slice1
spec:
  replicas: 1
  data:
    replicas: 1
  goosefsVersion:
    imagePullPolicy: Always
    image: ${img_uri}
    imageTag: ${tag}
  tieredstore:
    levels:
      - mediumtype: MEM
        path: /dev/shm
        quota: 1Gi
        high: "0.95"
        low: "0.7"
  properties:
    # goosefs user
    goosefs.user.file.writetype.default: MUST_CACHE
  master:
    replicas: 1
    journal:
      volumeType: hostpath
    jvmOptions:
      - "-Xmx40G"
      - "-XX:+UnlockExperimentalVMOptions"
      - "-XX:ActiveProcessorCount=8"
  worker:
    jvmOptions:
      - "-Xmx12G"
      - "-XX:+UnlockExperimentalVMOptions"
      - "-XX:MaxDirectMemorySize=32g"
      - "-XX:ActiveProcessorCount=8"
    resources:
      limits:
        cpu: 8
  fuse:
    imagePullPolicy: Always
    image: ${fuse_uri}
    imageTag: ${tag_num}
    env:
      MAX_IDLE_THREADS: "32"
    jvmOptions:
      - "-Xmx16G"
      - "-Xms16G"
      - "-XX:+UseG1GC"
      - "-XX:MaxDirectMemorySize=32g"
      - "-XX:+UnlockExperimentalVMOptions"
      - "-XX:ActiveProcessorCount=24"
    resources:
      limits:
        cpu: 16
    args:
      - fuse
      - --fuse-opts=kernel_cache,ro,max_read=131072,attr_timeout=7200,entry_timeout=7200,nonempty
```

Create runtime:
```shell
[root@master01 run]# kubectl apply -f runtime.yaml 
goosefsruntime.data.fluid.io/slice1 created
```

Check the GooseFS component status:

```shell
[root@master01 run]# kubectl get pods
NAME                  READY   STATUS    RESTARTS   AGE
slice1-fuse-xsvwj     1/1     Running   0          37s
slice1-master-0       2/2     Running   0          118s
slice1-worker-fzpdw   2/2     Running   0          37s
```

### 4. Load data

`dataload.yaml` data loading component:

```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: slice1-dataload
spec:
  dataset:
    name: slice1
    namespace: default
```

The dataset status is “Bond”, and 0% is cached.

```shell
[root@master01 run]# kubectl get dataset
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
slice1   97.67MiB         0.00B    4.00GiB          0.0%                Bound   31m
```

Start loading data:

```shell
[root@master01 run]# kubectl apply -f dataload.yaml 
dataload.data.fluid.io/slice1-dataload created
```

View data loading progress:

```shell
[root@master01 run]# kubectl get dataset --watch
NAME     UFS TOTAL SIZE   CACHED     CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
slice1   97.67MiB         52.86MiB   4.00GiB          54.1%               Bound   39m
slice1   97.67MiB         53.36MiB   4.00GiB          54.6%               Bound   39m
slice1   97.67MiB         53.36MiB   4.00GiB          54.6%               Bound   39m
slice1   97.67MiB         53.87MiB   4.00GiB          55.2%               Bound   39m
slice1   97.67MiB         53.87MiB   4.00GiB          55.2%               Bound   39m
```

100% of the data is cached:

```shell
[root@master01 run]# kubectl get dataset --watch
NAME     UFS TOTAL SIZE   CACHED     CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
slice1   97.67MiB         97.67MiB   4.00GiB          100.0%              Bound   44m
```


### 5. View data

```shell
[root@master01 run]# kubectl get pods
NAME                               READY   STATUS      RESTARTS   AGE
slice1-dataload-loader-job-km6mg   0/1     Completed   0          12m
slice1-fuse-xsvwj                  1/1     Running     0          17m
slice1-master-0                    2/2     Running     0          19m
slice1-worker-fzpdw                2/2     Running     0          17m
```

Go to the GooseFS master container:

```shell
[root@master01 run]# kubectl exec -it slice1-master-0 -- /bin/bash
Defaulting container name to goosefs-master.
```

List GooseFS directories:

```shell
[root@VM-2-40-tlinux goosefs-1.0.0-SNAPSHOT-noUI-noHelm]# goosefs fs ls /slice1
          10240       PERSISTED 06-25-2021 16:45:11:809 100% /slice1/p1
              1       PERSISTED 05-24-2021 16:07:37:000  DIR /slice1/a
          10000       PERSISTED 05-26-2021 19:29:05:000  DIR /slice1/p2
```

View a specific file:
```shell
[root@VM-2-40-tlinux goosefs-1.0.0-SNAPSHOT-noUI-noHelm]# goosefs fs ls /slice1/a/
             12       PERSISTED 06-25-2021 16:45:11:809 100% /slice1/a/1.xt
```

