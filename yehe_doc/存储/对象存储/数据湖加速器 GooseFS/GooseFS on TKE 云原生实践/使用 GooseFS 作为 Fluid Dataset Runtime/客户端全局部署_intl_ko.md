Fluid에서 'Dataset' 리소스 객체에 정의된 원격 파일은 스케쥴링 가능합니다. 즉, Pod를 관리하는 것처럼 원격 파일 캐시의 Kubernetes 클러스터 저장 위치를 ​​관리할 수 있습니다. 계산을 수행하는 Pod는 Fuse 클라이언트를 통해 데이터 파일에 액세스할 수 있습니다.

Fuse 클라이언트는 2가지 모드를 지원합니다.
-global false 모드. Fuse 클라이언트와 캐시된 데이터 사이의 친화성을 강제하는 모드로, 이 때 Fuse 클라이언트의 수량은 Runtime Replica의 수량과 동일합니다. 이 구성의 기본 모드는 명시적 선언이 필요하지 않으며, 데이터의 친화성의 장점을 활용할 수 있지만 Fuse 클라이언트의 배포가 상대적으로 고정적입니다.
- global true 모드. 이 모드는 Kubernetes 클러스터에 전역적으로 배포할 수 있는 Fuse 클라이언트로, 데이터와 Fuse 클라이언트 간의 친화성이 강제적이지 않습니다. 이 때 Fuse 클라이언트 수량이 Runtime Replica의 수량보다 훨씬 많을 수 있습니다. nodeSelector를 사용한 Fuse 클라이언트의 배포 범위 지정을 권장합니다.


## 전제 조건

이 예시를 실행하기 전에, [설치](https://intl.cloud.tencent.com/document/product/436/42230) 문서를 참고하여 설치를 완료해야 합니다. 또한, helm 명령어에 `--set webhook.enable =true` 매개변수 추가, `webhook` 활성화, Fluid 각 컴포넌트의 정상 작동 확인을 진행해야 합니다.

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
$ mkdir <any-path>/fuse-global-deployment
$ cd <any-path>/fuse-global-deployment
```

## 실행 예시


### 예시 1: global을 true로 설정

**전체 노드 조회**
```shell
$ kubectl get nodes
NAME            STATUS   ROLES    AGE     VERSION
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```

**태그를 통한 노드 식별**
```shell
$ kubectl label nodes 192.168.1.146 cache-node=true
```

다음 단계부터는 'NodeSelector'를 사용하여 클러스터에서 데이터가 저장되는 위치를 관리하므로, 여기에서 원하는 노드를 표시합니다.

**노드 재확인**
```shell
$ kubectl get node -L cache-node
NAME         STATUS   ROLES    AGE     VERSION            cache-node
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13   true
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```

현재 2개의 노드 모두에서 'cache-node=true'라는 태그가 추가된 노드는 하나뿐입니다. 다음 단계부터 이 노드에만 데이터 캐시가 배치되도록 합니다.

**생성 대기 중인 Dataset 리소스 객체 확인**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hbase
spec:
  mounts:
    - mountPoint: https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/stable/
      name: hbase
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: cache-node
              operator: In
              values:
                - "true"
```

>? 사용자의 테스트 편의를 위해, 본 예시 중 mountPoint는 Web UFS를, UFS는 COS를 사용합니다. [GooseFS를 통한 COS(COSN) 마운트](https://intl.cloud.tencent.com/document/product/436/41024)를 참고하시기 바랍니다.
>

'Dataset' 리소스 객체의 'spec' 속성에서 'nodeSelectorTerm' 하위 속성을 정의합니다. 데이터 캐시는 'cache-node=true' 태그가 있는 노드에 배치되어야 합니다.

**Dataset 리소스 객체 생성**

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
```

**생성 대기 중인 GooseFSRuntime 리소스 객체 확인**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hbase
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
  fuse:
    global: true
```

프로파일 스니펫에는 GooseFS의 인스턴스 활성화를 위해 Fluid가 사용하는 GooseFS 관련 많은 구성 정보가 포함되어 있습니다. 상기 파일 스니펫의 `spec.replicas` 속성은 1로 설정되어 있으며, 이는 Fluid가 GooseFS Master 1개와 GooseFS Worker 1개가 포함된 GooseFS 인스턴스가 실행될 것임을 나타냅니다. 또한, Fuse에 `global: true`가 포함되어 있으며, 이는 Fuse가 데이터 캐시의 위치에 의존하지 않고 전역적으로 배포될 수 있음을 나타냅니다.

**GooseFSRuntime 리소스 생성 및 상태 조회**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get po -owide
NAME                 READY   STATUS    RESTARTS   AGE     IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-gfq7z     1/1     Running   0          3m47s   192.168.1.147   192.168.1.147   <none>           <none>
hbase-fuse-lmk5p     1/1     Running   0          3m47s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m47s   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-hvbp2   2/2     Running   0          3m1s    192.168.1.146   192.168.1.146   <none>           <none>
```

GooseFS Worker가 성공적으로 실행되었고, 지정된 태그(예: `cache-node=true`)가 있는 노드에서 실행되고 있음을 알 수 있습니다. 모든 하위 노드에서 실행되는 GooseFS Fuse 수량은 2입니다.

**GooseFSRuntime 상태 확인**

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          2             2               Ready        12m
```

GooseFS Worker의 수량은 1이고, GooseFS Fuse의 수량은 2임을 확인할 수 있습니다.

**GooseFSRuntime 삭제**

```shell
kubectl delete goosefsruntime hbase
```



### 예시 2: global을 true로 설정 및 fuse의 nodeSelector 설정

다음으로 node selector 구성을 통해 Fuse 클라이언트를 구성하고, 이를 클러스터 노드에 지정합니다. 본 예시에서 192.168.1.146 노드를 캐시 노드로 선택했으므로, 비교를 위해 192.168.1.147을 GooseFS Fuse를 실행할 노드로 선택합니다.
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hbase
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
  fuse:
    global: true
    nodeSelector:
      kubernetes.io/hostname: 192.168.1.147
```


이전 runtime.yaml과 비교하였을 때, 이 프로파일 스니펫은 Fuse에 `global: true`가 포함되어 있다는 전제 하에 nodeSelector가 추가되었으며, 192.168.1.147 노드가 지정되어있습니다.


**GooseFSRuntime 리소스 생성 및 상태 조회**
```shell
$ kubectl create -f runtime-node-selector.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get po -owide
NAME                 READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-xzbww     1/1     Running   0          1h   192.168.1.147   192.168.1.147   <none>           <none>
hbase-master-0       2/2     Running   0          1h   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-vdxd5   2/2     Running   0          1h   192.168.1.146   192.168.1.146   <none>           <none>
```

GooseFS Worker가 성공적으로 실행되었고, 지정된 태그(`cache-node=true`)가 있는 노드에서 실행되고 있음을 확인할 수 있습니다. 192.168.1.147 노드에서 실행되는 GooseFS Fuse 수량은 1입니다. 


**GooseFSRuntime 상태 확인**

```shell
$ kubectl get goosefsruntimes.data.fluid.io -owide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        1h
```

GooseFS Worker 수량은 1이고, GooseFS Fuse의 수량도 1임을 확인할 수 있습니다. 이는 GooseFSRuntime이 nodeSelector를 지정하였고, 조건을 충족하는 노드가 한 개이기 때문입니다.

Fluid는 Fuse 클라이언트에 대해 별도의 스케줄링 정책을 지원하며, 이러한 스케줄링 정책은 사용자에게 보다 유연한 Fuse 클라이언트 스케줄링 정책을 제공함을 알 수 있습니다.

## 환경 정리

```shell
$ kubectl delete -f .

$ kubectl label node 192.168.1.146 cache-node-
```
