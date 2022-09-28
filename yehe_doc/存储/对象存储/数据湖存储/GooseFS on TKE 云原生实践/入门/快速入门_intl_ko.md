## GooseFSRuntime 빠르게 사용하기

GooseFSRuntime 사용 과정은 간단합니다. 기본 k8s 및 오브젝트 스토리지(Cloud Object Storage, COS) 환경을 준비한 후, GooseFSRuntime 환경을 배포하는 데 약 10분 정도 투자하면 됩니다. 다음 순서에 따라 배포할 수 있습니다.

## 전제 조건

- Git 설치 완료.
- Kubernetes 클러스터(version >= 1.14) 설치 완료 및 CSI 기능 지원. 최선의 적용 효과를 위해서는, [Tencent Kubernetes Engine(TKE)](https://intl.cloud.tencent.com/document/product/457/30635)에서 직접 배포할 수 있습니다.
- kubectl 설치 완료(버전 >= 1.14). `kubectl` 설치 및 설정에 대한 자세한 내용은 [Kubernetes 문서](https://kubernetes.io/docs/tasks/tools/install-kubectl/)를 참고하십시오.
- Helm 설치 완료(버전 >= 3.0). Helm 3 설치 및 구성에 대한 자세한 내용은 [HELM 문서](https://v3.helm.sh/docs/intro/install/)를 참고하십시오.
- 로컬 설치 패키지 `fluid.tgz`는 다음과 같이 제공되며, 직접 설치하여 사용할 수 있습니다.
```shell
$ helm install fluid fluid.tgz
NAME: fluid
LAST DEPLOYED: Mon Mar 29 11:21:46 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

>? `helm install` 명령어의 일반적인 형식은 `helm install <RELEASE_NAME> <SOURCE>`입니다. 상기 명령어에서 첫 번째 `fluid`는 설치된 release 이름(직접 변경 가능)을 지정하고, 두 번째는 'fluid.tgz'는 helm chart가 있는 경로를 지정합니다.
>

## 작업 단계

### 1. 네임스페이스 생성
```shell
kubectl create ns fluid-system
```
### 2. fluid 다운로드

[fluid-0.6.0.tgz](https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/fluid.tgz) 설치 패키지를 클릭하여 다운로드합니다.

>! [Fluid Releases](https://github.com/fluid-cloudnative/fluid/releases)로 이동하여 최신 버전을 다운로드할 수도 있지만, 일부 중국 내 컴퓨터를 통한 웹사이트 접속은 네트워크 문제가 발생할 수 있습니다.
>

### 3. Helm을 사용한 Fluid 설치

```shell
helm install --set runtime.goosefs.enabled=true fluid fluid-0.6.0.tgz
```

### 4. Fluid의 실행 상태 확인

```shell
$ kubectl get pod -n fluid-system
NAME                                         READY   STATUS    RESTARTS   AGE
csi-nodeplugin-fluid-2mfcr                   2/2     Running   0          108s
csi-nodeplugin-fluid-l7lv6                   2/2     Running   0          108s
dataset-controller-5465c4bbf9-5ds5p          1/1     Running   0          108s
goosefsruntime-controller-564f59bdd7-49tkc    1/1     Running   0          108s
```
이 중 csi-nodeplugin-fluid-xx의 수량은 k8s 클러스터의 노드 node 수량과 같아야 합니다.

### 5. GooseFS 캐시 환경 준비

#### (1) COS 서비스 준비 

COS 버킷을 활성화하여 버킷 생성을 완료합니다. [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참고하십시오.

####(2) 테스트 샘플 데이터 준비

Apache 미러 이미지 사이트의 Spark 관련 리소스 파일을 데모에 사용할 원격 파일로 사용할 수 있습니다. 실제 사용 시, 이 원격 파일을 임의의 원격 파일로 변경할 수도 있습니다.

- 원격 리소스 파일을 로컬로 다운로드합니다.
```shell
mkdir tmp
cd tmp
wget https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-2.4.8/spark-2.4.8-bin-hadoop2.7.tgz 
wget https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz 
```
- COS에 로컬 파일 업로드
Tencent Cloud COS팀에서 제공하는 클라이언트 [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) 또는 [COS SDK](https://intl.cloud .tencent.com/document/product/436/6474)를 사용하여, 로컬로 다운로드한 파일을 COS 버킷에 업로드합니다.

#### (3) dataset 및 GooseFSRuntime 생성

i. 다음 내용을 포함한 resource.yaml 파일을 생성합니다.
- 데이터세트와 ufs를 포함하는 dataset 정보.
- 예시의 test-bucket과 같은 데이터 세트 소스를 설명하는 Dataset CRD 객체 생성.
- 캐싱 서비스를 제공하기 위해 GooseFS 클러스터를 실행하는 것과 같이, GooseFSRuntime 생성.

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

- Dataset：
 - mountPoint: UFS 마운트 경로를 나타내며, endpoint 정보를 포함할 필요가 없습니다.
 - options: options에서 버킷에 필요한 정보를 지정해야 하며, 자세한 내용은 [API 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
 - fs.cosn.userinfo.secretId/fs.cosn.userinfo.secretKey: COS 버킷의 키 정보에 접근할 수 있는 권한이 있습니다.
- GooseFSRuntime: 더 많은 API는 [api_doc.md](https://github.com/fluid-cloudnative/fluid/blob/master/docs/en/dev/api_doc.md)를 참고하십시오.
 - replicas: 생성된 GooseFS 클러스터 노드 수량을 나타냅니다.
 - mediumtype: GooseFS는 HDD/SSD/MEM 세 가지 유형의 캐시 매체를 지원하여 다단계 캐시 구성을 제공합니다.
 - path: 저장 경로.
 - quota: 캐시 최대 용량.
 - high: 수위의 상한값.
 - low: 수위의 하한값.

ii. 다음 명령을 실행하여 GooseFSRuntime을 생성합니다.
```shell
kubectl create -f resource.yaml
```
iii. GooseFSRuntime 배포 상황을 확인합니다. 모두 Ready 상태이면 배포에 성공한 것입니다.
```shell
kubectl get goosefsruntime hadoop
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hadoop    Ready           Ready           Ready     62m
```
iv. dataset의 상태를 확인합니다. Bound가 표시되면 dataset가 성공적으로 바인딩되었음을 나타냅니다.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop        511MiB       0.00B    180.00GiB              0.0%          Bound   1h
```
v. PV 및 PVC 생성 상태를 확인합니다. GooseFSRuntime 배포 과정 중 PV 및 PVC가 자동으로 생성됩니다.
```shell
kubectl get pv,pvc
NAME                      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM            STORAGECLASS   REASON   AGE
persistentvolume/hadoop   100Gi      RWX            Retain           Bound    default/hadoop                           58m


NAME                           STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/hadoop   Bound    hadoop   100Gi      RWX                           58m
```

### 6. 애플리케이션 컨테이너 생성을 통한 가속 효과 체험

애플리케이션 컨테이너를 생성하여 GooseFS 가속 서비스를 사용하거나, 머신러닝 작업을 제출하여 관련 기능을 경험할 수 있습니다. 

다음과 같이 이 데이터 세트 사용에 사용될 애플리케이션 컨테이너 app.yaml을 생성합니다. 동일한 데이터에 여러 번 액세스하고, 액세스 소요 시간을 비교하여 GooseFSRuntime의 가속 효과를 확인합니다.
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

i. kubectl을 사용하여 애플리케이션 생성을 완료합니다.
```shell
kubectl create -f app.yaml
```
ii. 파일 크기를 확인합니다.
```shell
$ kubectl exec -it demo-app -- bash
$ du -sh /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
210M    /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2 
```
iii. 관찰 결과, 파일의 cp 소요 시간은 18s입니다.
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2  /dev/null

real    0m18.386s
user    0m0.002s
sys      0m0.105s
```
iv. 4. 이 때 dataset 의 캐시 상황을 확인한 결과, 로컬에 210MB의 데이터가 캐시되어 있습니다.
```shell
$ kubectl get dataset hadoop
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hadoop   210.00MiB       210.00MiB    180.00GiB        100.0%           Bound   1h
```
v. 다른 요소(예: page cache)가 결과에 영향을 미치지 않도록 하기 위해, 이전 컨테이너를 삭제하고 동일한 애플리케이션을 생성하여 동일 파일에 대한 액세스를 시도합니다. 이때 파일은 이미 GooseFS에 의해 캐싱되었기 때문에, 두 번째 액세스 소요 시간이 첫 번째보다 훨씬 짧은 것을 확인할 수 있습니다.
```shell
kubectl delete -f app.yaml && kubectl create -f app.yaml
```
vi. 관찰 결과, 파일 복사 소요 시간은 48ms이며, 전체 복사 시간은 300배 단축되었습니다.
```shell
$ time cp /data/hadoop/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2  /dev/null

real    0m0.048s
user    0m0.001s
sys      0m0.046s
```

### 7. 환경 정리

- 애플리케이션 및 애플리케이션 컨테이너 삭제
- GooseFSRuntime 삭제
```shell
kubectl delete goosefsruntime hadoop
```
- dataset 삭제
```shell
kubectl delete dataset hadoop
```

상기와 같이 간단한 예시를 통해 GooseFS on Fluid 기본 체험 및 학습을 완료하였습니다. 마지막으로 환경 정리를 진행합니다. Fluid GooseFSRuntime의 기능에 대한 자세한 내용은 [기능 리스트](https://intl.cloud.tencent.com/document/product/436/42233)를 참고하십시오.
