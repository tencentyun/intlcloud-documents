## 전제 조건

- [Fluid](https://github.com/fluid-cloudnative/fluid)(version >= 0.6.0)다운로드 및 설치가 완료되어야 합니다.
>! [fluid-0.6.0.tgz](https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/fluid.tgz)를 클릭하여 설치 패키지를 다운로드합니다.
>
- [설치](https://intl.cloud.tencent.com/document/product/436/42230) 문서를 참고하여 Fluid를 설치합니다.

## Dataset 및 GooseFSRuntime 생성

1. 다음 내용을 포함한 resource.yaml 파일을 생성합니다.
 - 데이터세트와 ufs를 포함하는 dataset 정보.
 - 예시의 test-bucket과 같은 데이터 세트 소스를 설명하는 Dataset CRD 객체 생성.
 - GooseFS 클러스터를 실행하여 캐싱 서비스를 제공하는 것과 같이, GooseFSRuntime 생성.

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
AK 등 키 정보의 보안을 위해, secret 사용을 통한 관련 키 정보 저장을 권장하며, secret 사용은 <a href="https://intl.cloud.tencent.com/document/product/436/42239">매개변수를 사용하여 암호화하기</a>를 참고하시기 바랍니다.
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

 - Dataset：
    - mountPoint: UFS 마운트 경로를 나타내며, endpoint 정보를 포함할 필요가 없습니다.
    - options: options에서 버킷에 필요한 정보를 지정해야 하며, 자세한 내용은 [API 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
    - fs.cosn.userinfo.secretId/fs.cosn.userinfo.secretKey：COS 버킷에 대한 액세스 권한이 있는 키 정보입니다.
 - GooseFSRuntime: 더 많은 API는 [api_doc.md](https://github.com/fluid-cloudnative/fluid/blob/master/docs/en/dev/api_doc.md)를 참고하십시오.
    - replicas: 생성된 GooseFS 클러스터 노드 수량을 나타냅니다.
    - mediumtype: GooseFS는 HDD/SSD/MEM 세 가지 유형의 캐시 매체를 지원하여 다단계 캐시 구성을 제공합니다.
    - path: 저장 경로.
    - quota: 캐시 최대 용량.
    - high: 수위의 상한값.
    - low: 수위의 하한값.
2.  다음 명령을 실행하여 GooseFSRuntime을 생성합니다.
```shell
$ kubectl create -f resource.yaml
```
3.  GooseFSRuntime 배포 상황을 확인합니다. 모두 Ready 상태이면 배포에 성공한 것입니다.
```shell
$ kubectl get goosefsruntime hadoop
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hadoop    Ready           Ready           Ready     62m
```
4. dataset의 상태를 확인합니다. Bound가 표시되면 dataset가 성공적으로 바인딩되었음을 나타냅니다.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop       210.00MiB       0.00B    180.00GiB              0.0%          Bound   1h
```
5. PV 및 PVC 생성 상태를 확인합니다. GooseFSRuntime 배포 과정 중 PV 및 PVC가 자동으로 생성됩니다.
```shell
$ kubectl get pv,pvc
NAME                      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM            STORAGECLASS   REASON   AGE
persistentvolume/hadoop   100Gi      RWX            Retain           Bound    default/hadoop                           58m

NAME                           STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/hadoop   Bound    hadoop   100Gi      RWX                           58m
```

## 서비스 정상 여부 확인

1. master/worker pod에 로그인합니다. 파일을 정상적으로 list할 수 있는지 관찰합니다.
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
2. fuse pod에 로그인합니다. 파일을 정상적으로 list할 수 있는지 관찰합니다.
```shell
$ kubectl exec -ti hadoop-goosefs-fuse-svz4s bash
cd /runtime-mnt/goosefs/<namespace>/<DatasetName>/goosefs-fuse/<DatasetName>
```

## 애플리케이션 컨테이너 생성을 통한 가속 효과 체험

애플리케이션 컨테이너를 생성하여 GooseFS 가속 서비스를 사용하거나, 머신러닝 작업을 제출하여 관련 기능을 경험할 수 있습니다. 다음과 같이 이 데이터 세트 사용에 사용될 애플리케이션 컨테이너 app.yaml을 생성합니다. 동일한 데이터에 여러 번 액세스하고, 액세스 소요 시간을 비교하여 GooseFSRuntime의 가속 효과를 확인합니다.
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

1. kubectl을 사용하여 애플리케이션 생성을 완료합니다.
```shell
$ kubectl create -f app.yaml
```
2. 파일 크기를 확인합니다.
```shell
$ kubectl exec -it demo-app -- bash
$ du -sh /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
210M	/data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
```
3. 관찰 결과, 파일의 cp 소요 시간은 18s입니다.
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 /dev/null

real0m18.386s
user	0m0.002s
sys	  0m0.105s
```
4. 이 때 dataset 의 캐시 상황을 확인한 결과, 로컬에 210MB의 데이터가 캐시되어 있습니다.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop   210.00MiB       210.00MiB    180.00GiB        100.0%           Bound   1h
```
5. 다른 요소(예: page cache)가 결과에 영향을 미치지 않도록 하기 위해, 이전 컨테이너를 삭제하고 동일한 애플리케이션을 생성하여 동일 파일에 대한 액세스를 시도합니다. 이때 파일은 이미 GooseFS에 의해 캐싱되었기 때문에, 두 번째 액세스 소요 시간이 첫 번째보다 훨씬 짧은 것을 확인할 수 있습니다.
```shell
$ kubectl delete -f app.yaml && kubectl create -f app.yaml
```
6. 관찰 결과, 파일 복사 소요 시간은 48ms이며, 전체 복사 시간은 300배 단축되었습니다.
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2  /dev/null

real	0m0.048s
user	0m0.001s
sys	  0m0.046s
```

## 환경 정리

```shell
$ kubectl delete -f resource.yaml
```
