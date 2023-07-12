Fluid에서 Dataset 를 생성할 때 'mounts'에서 일부 키 정보를 구성해야 하는 경우가 있습니다. 보안을 위해 Fluid는 Secret을 사용하여 이러한 키 정보를 구성하는 기능을 제공합니다.

다음은 [Cloud Object Storage(COS)](https://intl.cloud.tencent.com/product/cos) 데이터 세트 액세스를 예시로 구성 방법을 설명하는 내용입니다.

## 키 정보를 포함하는 Dataset 생성

### Secret 조회

생성할 Secret에는 Dataset 생성 시 설정해야 하는 키 정보를 입력해야 합니다.
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
stringData:
  fs.cosn.userinfo.secretId: <COS_SECRET_ID>
  fs.cosn.userinfo.secretKey: <COS_SECRET_KEY>
```

보시다시피 `fs.cosn.userinfo.secretKey`와 `fs.cosn.userinfo.secretId`의 구체적인 내용은 Secret에 작성되어 있으며, Dataset은 직접 작성하는 대신, 동일 이름의 Secret과 key를 찾아 해당 값을 읽어옵니다. 이를 통해 일부 데이터의 보안성을 보장합니다.

### secret 생성
```shell
$ kubectl apply -f secret.yaml 
secret/mysecret created

$ kubectl get secret
NAME        TYPE     DATA   AGE
mysecret   Opaque    2      57s
```

### Dataset와 Runtime 조회
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

보시다시피 보안성을 보장하기 위해, 상기 구성에서는 `fs.cos.endpoint`를 직접 구성하는 것과 달리, Secret에서 `fs.cosn.userinfo.secretId`와 `fs.cosn.userinfo.secretKey`의 구성을 읽어왔습니다. 

>! 'options'와 'encryptOptions'에 동일한 이름의 키가 구성된 경우(예: 모두 다 'fs.cosn.userinfo.secretId'가 구성됨), `encryptOptions`의 값이 `options`의 해당 값의 내용을 덮어씁니다.
>

###  Dataset와 Runtime 생성

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/mydata created
goosefsruntime.data.fluid.io/mydata created
```

배포된 GooseFSRuntime의 Ready 상태로 표시되면 배포 성공을 나타냅니다.

```shell
$ kubectl get goosefsruntime mydata
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
mydata    Ready           Ready           Ready     62m
```

dataset의 상태를 확인합니다. Bound가 표시되면 dataset가 성공적으로 바인딩되었음을 나타냅니다.

```shell
$ kubectl get dataset mydata
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
mydata       210.00MiB       0.00B    2GiB              0.0%          Bound   1h
```

이 때 Secret Dataset을 사용하여 원격 파일을 가져올 수 있습니다.

