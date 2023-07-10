Fluid에서 'Dataset' 리소스 객체에 정의된 원격 파일은 스케쥴링 가능합니다. 즉, Pod를 관리하는 것처럼 원격 파일 캐시의 Kubernetes 클러스터 저장 위치를 관리할 수 있습니다. 또한 Fluid는 애플리케이션에 대한 데이터 캐시 친화성 스케줄링도 지원합니다. 이 스케줄링 방법은 추가적인 부하를 최소화하기 위해 애플리케이션(예: 데이트 분석 작업, 머신러닝 작업 등)과 필요한 데이터 캐시를 함께 배치합니다.


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

**전체 노드 조회**

```shell
$ kubectl get nodes
NAME                       STATUS   ROLES    AGE     VERSION
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```


**태그를 통한 노드 식별**

```shell
$ kubectl label nodes 192.168.1.146 hbase-cache=true
```

다음 단계부터는 'NodeSelector'를 사용하여 클러스터에서 데이터가 저장되는 위치를 관리하므로, 여기에서 원하는 노드를 표시합니다.


**노드 재확인**


```shell
$ kubectl get node -L hbase-cache
NAME                       STATUS   ROLES    AGE     VERSION            HBASE-CACHE
192.168.1.146   Ready    <none>   7d14h   v1.18.4-tke.13   true
192.168.1.147   Ready    <none>   7d14h   v1.18.4-tke.13
```

현재 2개의 노드 모두에서 'hbase-cache=true'라는 태그가 추가된 노드는 하나뿐입니다. 다음 단계부터 이 노드에만 데이터 캐시가 배치되도록 합니다.


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
            - key: hbase-cache
              operator: In
              values:
                - "true"
```

>? 사용자의 테스트 편의를 위해, 본 예시 중 mountPoint는 Web UFS를, UFS는 COS를 사용합니다. [GooseFS를 통한 COS(COSN) 마운트](https://intl.cloud.tencent.com/document/product/436/41024)를 참고하시기 바랍니다.
>

'Dataset' 리소스 객체의 'spec' 속성에서 'nodeSelectorTerm' 하위 속성을 정의합니다. 데이터 캐시는 'hbase-cache=true' 태그가 있는 노드에 배치되어야 합니다.


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
  replicas: 2
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1
        quota: 2G
        high: "0.8"
        low: "0.7"
```

프로파일 스니펫에는 GooseFS의 인스턴스 활성화를 위해 Fluid가 사용하는 GooseFS 관련 많은 구성 정보가 포함되어 있습니다. 상기 파일 스니펫의 `spec.replicas` 속성은 2로 설정되어 있으며, 이는 Fluid가 GooseFS Master 1개와 GooseFS Worker 2개가 포함된 GooseFS 인스턴스가 실행될 것임을 나타냅니다. 

**GooseFSRuntime 리소스 생성 및 상태 조회**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          3m3s   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          104s   192.168.1.146   192.168.1.146   <none>           <none>
```

GooseFS Worker 2개가 실행되기를 원했지만, GooseFS Worker가 하나만 실행되었고, 지정된 태그(예: `cache-node=true`)가 있는 노드에서 실행되고 있음을 확인할 수 있습니다.

**GooseFSRuntime 상태 확인**

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE     AGE
hbase   1               1                 Ready          1               2                 PartialReady   1             2               PartialReady   4m3s
```

예상대로 'Worker Phase'의 상태는 이제 'PartialReady'이고 'Ready Workers: 1'은 'Desired Workers: 2'보다 작습니다.

**생성 대기 중인 애플리케이션 조회**

Fluid가 데이터 캐시 친화성 스케줄링을 수행하는 방법을 보여주는 애플리케이션 샘플을 제공합니다. 먼저 애플리케이션을 살펴봅니다.

**app.yaml**
```yaml
apiVersion: apps/v1beta1
kind: StatefulSet
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  replicas: 2
  serviceName: "nginx"
  podManagementPolicy: "Parallel"
  selector: # define how the deployment finds the pods it manages
    matchLabels:
      app: nginx
  template: # define the pods specifications
    metadata:
      labels:
        app: nginx
    spec:
      affinity:
        # prevent two Nginx Pod from being scheduled at the same Node
        # just for demonstrating co-locality demo
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - nginx
            topologyKey: "kubernetes.io/hostname"
      containers:
        - name: nginx
          image: nginx
          volumeMounts:
            - mountPath: /data
              name: hbase-vol
      volumes:
        - name: hbase-vol
          persistentVolumeClaim:
            claimName: hbase
```
'podAntiAffinity' 속성은 동일한 애플리케이션에 속한 여러 Pod가 여러 다른 노드에 배포되도록 하며, 이 구성을 통해 Fluid의 데이터 캐시 친화성 스케줄링이 수행되는 방식을 보다 명확하게 관찰할 수 있습니다. 'podAntiAffinity'는 데모 전용 속성이므로 크게 주의하지 않아도 됩니다.


**애플리케이션 실행**
```shell
$ kubectl create -f app.yaml
statefulset.apps/nginx created
```

**애플리케이션 실행 상태 조회**
```shell
$ kubectl get pod -o wide -l app=nginx
NAME      READY   STATUS    RESTARTS   AGE    IP              NODE                       NOMINATED NODE   READINESS GATES
nginx-0   1/1     Running   0          2m5s   192.168.1.146   192.168.1.146   <none>           <none>
nginx-1   0/1     Pending   0          2m5s   <none>          <none>                     <none>           <none>
```

하나의 Nginx Pod만 성공적으로 실행되었으며, `nodeSelectorTerm`을 충족하는 노드에서 실행 중입니다.


**애플리케이션 실행 실패 원인 확인**
```shell
$ kubectl describe pod nginx-1
...
Events:
  Type     Reason            Age        From               Message
  ----     ------            ----       ----               -------
  Warning  FailedScheduling  <unknown>  default-scheduler  0/2 nodes are available: 1 node(s) didn't match pod affinity/anti-affinity, 1 node(s) didn't satisfy existing pods anti-affinity rules, 1 node(s) had volume node affinity conflict.
  Warning  FailedScheduling  <unknown>  default-scheduler  0/2 nodes are available: 1 node(s) didn't match pod affinity/anti-affinity, 1 node(s) didn't satisfy existing pods anti-affinity rules, 1 node(s) had volume node affinity conflict.
```


상기와 같이, 한편으로는 'PodAntiAffinity' 속성의 요구 사항을 충족하기 위해 두 개의 Nginx Pod를 동일한 노드에 스케줄링할 수 없습니다. 반면 현재 Dataset 리소스 객체의 친화성 요구 사항을 충족하는 노드는 하나뿐이므로, Nginx Pod가 하나만 성공적으로 스케줄링됩니다.


**다른 노드에 태그 추가**

```shell
$ kubectl label node 192.168.1.147 hbase-cache=true
```

두 노드의 태그가 모두 같으므로 각 컴포넌트의 실행 상태를 재확인합니다.

```shell
$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-42csf     1/1     Running   0          44m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-fuse-kth4g     1/1     Running   0          10m   192.168.1.147   192.168.1.147   <none>           <none>
hbase-master-0       2/2     Running   0          46m   192.168.1.147   192.168.1.147   <none>           <none>
hbase-worker-l62m4   2/2     Running   0          44m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-worker-rvncl   2/2     Running   0          10m   192.168.1.147   192.168.1.147   <none>           <none>
```

두 GooseFS Worker가 성공적으로 실행되고, 개별적으로 두 노드에서 실행됩니다.

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          2               2                 Ready          2             2               Ready        46m43s
```

```shell
$ kubectl get pod -l app=nginx -o wide
NAME      READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
nginx-0   1/1     Running   0          21m   192.168.1.146   192.168.1.146   <none>           <none>
nginx-1   1/1     Running   0          21m   192.168.1.147   192.168.1.147   <none>           <none>
```

다른 nginx Pod는 더 이상 'Pending' 상태가 아니며 다른 노드에서 성공적으로 실행되었습니다.

스케줄링 가능한 데이터 캐시와 애플리케이션 데이터 캐시의 친화성 스케줄링은 모두 Fluid에서 지원하는 기능임을 알 수 있습니다. 대부분의 경우, 이 두 기능은 함께 작동하여 사용자에게 Kubernetes 클러스터의 데이터를 보다 유연하고 편리하게 관리할 수 있는 방법을 제공합니다. 

요약하면, Fluid는 사용자에게 보다 유연한 데이터 캐시 관리 기능을 제공하는 데이터 캐시 스케줄링 정책을 지원합니다.

## 환경 정리
```shell
$ kubectl delete -f .


$ kubectl label node 192.168.1.146 hbase-cache-
$ kubectl label node 192.168.1.147 hbase-cache-
```
