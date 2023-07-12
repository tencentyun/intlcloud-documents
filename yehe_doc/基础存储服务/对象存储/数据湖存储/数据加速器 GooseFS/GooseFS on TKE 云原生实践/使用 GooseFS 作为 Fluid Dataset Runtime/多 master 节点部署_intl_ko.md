## 개요

단일 마스터의 안정성은 비교적 낮을 수 있습니다. 일부 온라인 서비스 시나리오에서는 내결함성을 보장하기 위해 여러 master를 사용해야 합니다. GooseFSRuntime은 내결함성을 3개의 master 형태로 제공하며, Raft 프로토콜을 통해 선택합니다. Raft는 강력한 일관성, 탈중앙성 및 고가용성을 갖추고 있어, 널리 사용되는 분산 프로토콜입니다.

다음은 상기 기능에 대한 간략한 소개입니다.

## 전제 조건

이 예시를 실행하기 전에 먼저 [설치](https://intl.cloud.tencent.com/document/product/436/42230) 문서를 참고하여 설치를 완료하고, Fluid 컴포넌트의 정상 작동 여부를 확인하십시오.

```shell
$ kubectl get pod -n fluid-system
goosefsruntime-controller-5b64fdbbb-84pc6   1/1     Running   0          8h
csi-nodeplugin-fluid-fwgjh                  2/2     Running   0          8h
csi-nodeplugin-fluid-ll8bq                  2/2     Running   0          8h
csi-nodeplugin-fluid-dhz7d                  2/2     Running   0          8h
dataset-controller-5b7848dbbb-n44dj         1/1     Running   0          8h
```

일반적으로 'dataset-controller'라는 이름의 Pod, 'goosefsruntime-controller'라는 이름의 Pod, 그리고 'csi-nodeplugin'이라는 이름의 여러 Pod가 실행 중인 것을 볼 수 있습니다. 이 중 `csi-nodeplugin`과 같은 Pod 수량은 Kubernetes 클러스터 노드 수량에 따라 결정됩니다.

## 작업 환경 생성

```shell
$ mkdir <any-path>/co-locality
$ cd <any-path>/co-locality
```

## 예시


### 전체 노드 조회


```shell
$ kubectl get nodes
NAME                       STATUS   ROLES    AGE     VERSION
192.168.1.145   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```


### 생성 대기 중인 Dataset 리소스 객체 확인
```shell
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hbase
spec:
  mounts:
    - mountPoint: https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/stable/
      name: hbase
```

>?사용자의 테스트 편의를 위해, 본 예시 중 mountPoint는 Web UFS를, UFS는 COS를 사용합니다. [GooseFS를 통한 COS(COSN) 마운트](https://intl.cloud.tencent.com/document/product/436/41024)를 참고하시기 바랍니다.
>

### Dataset 리소스 객체 생성

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
```

### 생성 대기 중인 GooseFSRuntime 리소스 객체 확인
```shell
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hbase
spec:
  replicas: 3
  tieredstore:
    levels:
      - mediumtype: HDD
        path: /mnt/disk1
        quota: 2G
        high: "0.8"
        low: "0.7"
  master:
    replicas: 3
```

`spec.master.replicas=3`을 지정하여 Raft 3 master 모드를 활성화합니다. 이 매개변수는 양의 홀수이어야 합니다.

### GooseFSRuntime 리소스 생성 및 상태 조회

```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created



$ kubectl get pod
NAME                          READY   STATUS    RESTARTS   AGE
hbase-fuse-4v9mq     1/1     Running   0          84s
hbase-fuse-5kjbj     1/1     Running   0          84s
hbase-fuse-tp2q2     1/1     Running   0          84s
hbase-master-0       1/1     Running   0          104s
hbase-master-1       1/1     Running   0          102s
hbase-master-2       1/1     Running   0          100s
hbase-worker-cx8x7   1/1     Running   0          84s
hbase-worker-fjsr6   1/1     Running   0          84s
hbase-worker-fvpgc   1/1     Running   0          84s
```

### GooseFSRuntime 상태 조회

```shell
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hbase   Ready           Ready            Ready     15m
```

`PHASE`가 전부 Ready 상태임을 확인합니다.

### Raft leader/follower상태 조회

이 중 하나의 master pod에 로그인합니다.

```shell
$ kubectl exec -ti hbase-master-0 bash
$ goosefs fs masterInfo
```

하나의 노드는 `LEADER`, 나머지 두 개는 `FOLLOWER`임을 볼 수 있습니다.

```shell
current leader master: hbase-master-0:26000
All masters: [hbase-master-0:26000, hbase-master-1:26000, hbase-master-2:26000]
```
