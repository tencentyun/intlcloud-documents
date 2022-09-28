When creating a dataset in Fluid, sometimes we need to configure some key information in `mounts`. To ensure security, Fluid provides the capability to configure these key information using Secret.

The following takes access to the [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/product/cos) Dataset as an example to illustrate how to configure key information.

## Creating a Dataset with Key Information

### Checking the Secret

In the Secret to be created, you need to specify the key information that needs to be configured in the above dataset.
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
stringData:
  fs.cosn.userinfo.secretId: <COS_SECRET_ID>
  fs.cosn.userinfo.secretKey: <COS_SECRET_KEY>
```

As shown above, the specific contents of `fs.cosn.userinfo.secretKey` and `fs.cosn.userinfo.secretId` are written in the Secret, and the dataset needs to read the corresponding values by looking for the same Secret and key. Key information is no longer directly written in the dataset, and thus the security of some data is guaranteed.

### Create Secret
```shell
$ kubectl apply -f secret.yaml 
secret/mysecret created

$ kubectl get secret
NAME        TYPE     DATA   AGE
mysecret   Opaque    2      57s
```

### Check the dataset and runtime
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: mydata
spec:
  mounts:
    - mountPoint: cosn://<COS_BUCKET>/<COS_DIRECTORY>/
      name: mydata
      options:
        fs.cosn.bucket.region: <COS_REGION>
        fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
        fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
        fs.cosn.userinfo.appid: <COS_APP_ID>
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
  name: mydata
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
```

In the above configuration, unlike the direct configuration of `fs.cos.endpoint`, we changed the configuration of `fs.cosn.userinfo.secretId` and `fs.cosn.userinfo.secretKey` to read from Secret to ensure security.

>! If the same key is configured both in `options` and `encryptOptions`, the value in `encryptOptions` will override the corresponding value in `options`.
>

### Create a dataset and a runtime

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/mydata created
goosefsruntime.data.fluid.io/mydata created
```

Check the status of the GooseFSRuntime deployed. If all states are `Ready`, GooseFSRuntime is deployed successfully.

```shell
$ kubectl get goosefsruntime mydata
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
mydata    Ready           Ready           Ready     62m
```

Check the dataset status. If the state is `Bound`, the dataset is bound successfully.

```shell
$ kubectl get dataset mydata
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
mydata       210.00MiB       0.00B    2GiB              0.0%          Bound   1h
```

Now, the dataset that uses the Secret can obtain the remote file.

