## 개요

Fluid에서 nodeselector를 사용하여 master 노드의 배포를 지정할 수 있습니다. 예를 들어 master를 성능이 더 나은 k8s 머신에 배포하도록 선택할 수 있습니다.

다음은 상기 기능에 대한 간략한 소개입니다.

## 전제 조건

이 예시를 실행하기 전에 먼저 [설치](https://intl.cloud.tencent.com/document/product/436/42230) 문서를 참고하여 설치를 완료하고, Fluid 컴포넌트의 정상 작동 여부를 확인하십시오.

```shell
$ kubectl get pod -n fluid-system
goosefsruntime-controller-5b64fdbbb-84pc6   1/1     Running   0          8h
csi-nodeplugin-fluid-fwgjh                  2/2     Running   0          8h
csi-nodeplugin-fluid-ll8bq                  2/2     Running   0          8h
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
192.168.1.146   Ready    <none>   7d14h  v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h  v1.18.4-tke.13
```

### 태그를 통한 노드 식별

```shell
$ kubectl label nodes 192.168.1.146 hbase-cache=true
```

### 노드 재확인

```shell
$ kubectl get node -L hbase-cache
NAME                       STATUS   ROLES    AGE     VERSION            HBASE-CACHE
192.168.1.146   Ready    <none>   7d14h  v1.18.4-tke.13   true
192.168.1.147   Ready    <none>   7d14h  v1.18.4-tke.13
```

### 생성 대기 중인 Dataset 리소스 객체 확인
```yaml
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
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hbase
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: MEM
        path: /dev/shm
        quota: 2G
        high: "0.8"
        low: "0.7"
  master:
    nodeSelector:
      hbase-cache: "true"
```
프로파일 스니펫에는 GooseFS의 인스턴스 활성화를 위해 Fluid가 사용하는 GooseFS 관련 많은 구성 정보가 포함되어 있습니다. 상기 파일 스니펫의 `spec.replicas` 속성은 1로 설정되어 있으며, 이는 Fluid가 GooseFS Master 1개와 GooseFS Worker 1개가 포함된 GooseFS 인스턴스가 실행될 것임을 나타냅니다.

### GooseFSRuntime 리소스 생성 및 상태 조회

```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created



$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m3s   192.168.1.147   192.168.1.146   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
```

master가 성공적으로 실행되고, 지정된 태그(예: `hbase-cache=true`)가 있는 노드에서 실행되는 것을 볼 수 있습니다.
