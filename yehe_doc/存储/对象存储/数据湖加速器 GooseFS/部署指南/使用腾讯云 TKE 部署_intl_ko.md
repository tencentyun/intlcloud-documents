TKE를 이용한 GooseFS 배포는 [오픈소스 모듈 Fluid](https://github.com/fluid-cloudnative/fluid) 배포가 필요하며, TKE 애플리케이션은 이미 런칭되었습니다. 배포에는 다음 두 단계가 포함됩니다.

1. [Fluid helm chart](https://console.cloud.tencent.com/tke2/market/detail?chart=fluid&project=qcloud-stable&clusterType=tke)를 통한 controller 배포.
2. kubectl를 통한 Dataset와 GooseFS runtime 생성. 


## 준비 사항
1. Tencent Cloud TKE 클러스터가 있어야 합니다. 
2. kubectl v1.18 이상 버전이 설치되어 있어야 합니다. 

## 설치 방법

1. [TKE 애플리케이션 마켓](https://console.cloud.tencent.com/tke2/market)에서 fluid 애플리케이션을 찾습니다. 

2. Fluid Controller를 설치합니다. 

3. controller 모듈을 검사합니다. 좌측 [클러스터]에서 해당 클러스터를 찾고 2개의 controller가 확인되었다면 fluid 모듈이 성공적으로 설치가 되었음을 의미합니다. 



## 작업 예시

### 1. 클러스터 액세스 권한

```shell
[root@master01 run]# export KUBECONFIG=xxx/cls-xxx-config (tke 콘솔 페이지에서 클러스터 증명을 특정 디렉터리에 다운로드합니다.）
```

>! 클러스터 API Server의 외부 네트워크 액세스 권한을 활성화해야 합니다. 
>

### 2. UFS 데이터 세트 Dataset 생성 (예시: COS)

암호화를 위한 secret.yaml을 생성합니다. 템플릿은 다음과 같습니다.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
stringData:
  fs.cosn.userinfo.secretKey: xxx
  fs.cosn.userinfo.secretId:xxx
```

secret 생성:
```shell
[root@master01 ~]# kubectl apply  -f secret.yaml
secret/mysecret created
```

dataset.yaml 템플릿은 아래와 같습니다. 
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

dataset 생성
```shell
[root@master01 run]# kubectl apply -f dataset.yaml 
dataset.data.fluid.io/slice1 created
```

Dataset 상태 조회, NotBond 상태.
```shell
[root@master01 run]# kubectl get dataset
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE      AGE
slice1 
                                                                 NotBound   11s
```

### 3. runtime 생성

runtime.yaml 템플릿은 아래와 같습니다.

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

runtime 생성.
```shell
[root@master01 run]# kubectl apply -f runtime.yaml 
goosefsruntime.data.fluid.io/slice1 created
```

goosefs 모듈 상태 확인.

```shell
[root@master01 run]# kubectl get pods
NAME                  READY   STATUS    RESTARTS   AGE
slice1-fuse-xsvwj     1/1     Running   0          37s
slice1-master-0       2/2     Running   0          118s
slice1-worker-fzpdw   2/2     Running   0          37s
```

### 4. 프리패치 데이터

dataload.yaml 프리패치 모듈은 아래와 같습니다.

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

이때 Dataset는 Bond 상태이며 Cached 비율은 0%입니다. 

```shell
[root@master01 run]# kubectl get dataset
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
slice1   97.67MiB         0.00B    4.00GiB          0.0%                Bound   31m
```

데이터 프리패치 실행.

```shell
[root@master01 run]# kubectl apply -f dataload.yaml 
dataload.data.fluid.io/slice1-dataload created
```

데이터 프리패치 진행률 확인.

```shell
[root@master01 run]# kubectl get dataset --watch
NAME     UFS TOTAL SIZE   CACHED     CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
slice1   97.67MiB         52.86MiB   4.00GiB          54.1%               Bound   39m
slice1   97.67MiB         53.36MiB   4.00GiB          54.6%               Bound   39m
slice1   97.67MiB         53.36MiB   4.00GiB          54.6%               Bound   39m
slice1   97.67MiB         53.87MiB   4.00GiB          55.2%               Bound   39m
slice1   97.67MiB         53.87MiB   4.00GiB          55.2%               Bound   39m
```

데이터 프리패치 100% 완료.

```shell
[root@master01 run]# kubectl get dataset --watch
NAME     UFS TOTAL SIZE   CACHED     CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
slice1   97.67MiB         97.67MiB   4.00GiB          100.0%              Bound   44m
```


### 5. 데이터 검사

```shell
[root@master01 run]# kubectl get pods
NAME                               READY   STATUS      RESTARTS   AGE
slice1-dataload-loader-job-km6mg   0/1     Completed   0          12m
slice1-fuse-xsvwj                  1/1     Running     0          17m
slice1-master-0                    2/2     Running     0          19m
slice1-worker-fzpdw                2/2     Running     0          17m
```

goosefs master 컨테이너로 이동

```shell
[root@master01 run]# kubectl exec -it slice1-master-0 -- /bin/bash
Defaulting container name to goosefs-master.
```

goosefe 디렉터리 나열.

```shell
[root@VM-2-40-tlinux goosefs-1.0.0-SNAPSHOT-noUI-noHelm]# goosefs fs ls /slice1
          10240       PERSISTED 06-25-2021 16:45:11:809 100% /slice1/p1
              1       PERSISTED 05-24-2021 16:07:37:000  DIR /slice1/a
          10000       PERSISTED 05-26-2021 19:29:05:000  DIR /slice1/p2
```

특정 파일 보기.
```shell
[root@VM-2-40-tlinux goosefs-1.0.0-SNAPSHOT-noUI-noHelm]# goosefs fs ls /slice1/a/
             12       PERSISTED 06-25-2021 16:45:11:809 100% /slice1/a/1.xt
```

