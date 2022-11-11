노드 친화성은 Kubernetes Pod의 속성으로, Pod가 특정 유형의 노드에 이끌리게 합니다. 이것은 선호도 때문일 수도 있고 강제적인 요구 사항일 수도 있습니다. Taint(테인트)는 반대의 개념이며, 노드로 하여금 특정 유형의 Pod를 거부하도록 합니다.

Toleration은 Pod에 적용되어 Pod가 매칭되는 테인트가 있는 노드에 스케줄링되도록 허용하지만 강제적이지는 않습니다.

테인트와 톨러레이션(Toleration)은 함께 작동하여 Pod가 부적절한 노드에 할당되는 것을 방지합니다. 각 노드에는 하나 이상의 테인트가 적용될 수 있으며, 이러한 테인트에 대한 톨러레이션이 없는 Pod는 노드에서 허용되지 않습니다.

Fluid에서는 'Dataset'의 스케줄링 가능성을 고려하여 리소스 객체에도 toleration을 정의해야 합니다. 즉, Pod를 스케줄링하는 것처럼 Kubernetes 클러스터에서 캐시의 저장 위치를 ​​스케줄링할 수 있습니다.


## 작업 환경 생성
```shell
$ mkdir <any-path>/tolerations
$ cd <any-path>/tolerations
```

## 실행 예시

**전체 노드 조회**
```shell
$ kubectl get no
NAME            STATUS   ROLES    AGE    VERSION
192.168.1.146   Ready    <none>   200d   v1.18.4-tke.13
```


**노드에 테인트(taint) 구성**

```shell
$ kubectl taint nodes 192.168.1.146 hbase=true:NoSchedule
```

다음 단계에서는 노드의 테인트 구성을 진행합니다.


**노드 재조회**
```shell
$ kubectl get node 192.168.1.146 -o yaml | grep taints -A3
  taints:
  - effect: NoSchedule
    key: hbase
    value: "true"
```

현재 노드에 taints NoSchedule 구성을 추가하였으므로 기본 데이터 세트를 노드에 배치할 수 없습니다.

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
  tolerations:
    - key: hbase 
      operator: Equal 
      value: "true" 
```

>? 사용자의 테스트 편의를 위해, 본 예시 중 mountPoint는 Web UFS를, UFS는 COS를 사용합니다. [GooseFS를 통한 COS(COSN) 마운트](https://intl.cloud.tencent.com/document/product/436/41024)를 참고하시기 바랍니다.
>

'Dataset' 리소스 객체의 'spec' 속성에서 'tolerations' 하위 속성을 정의합니다. 이 하위 속성은 데이터 캐시가 테인트가 구성되어있는 노드에 배치될 수 있도록 합니다.


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
        path: /mnt/disk1
        quota: 2G
        high: "0.95"
        low: "0.7"
```


프로파일 스니펫에는 GooseFS의 인스턴스 활성화를 위해 Fluid가 사용하는 GooseFS 관련 많은 구성 정보가 포함되어 있습니다. 상기 파일 스니펫의 `spec.replicas` 속성은 1로 설정되어 있으며, 이는 Fluid가 GooseFS Master 1개와 GooseFS Worker 1개가 포함된 GooseFS 인스턴스를 실행할 것임을 나타냅니다. 


**GooseFSRuntime 리소스 생성 및 상태 조회**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


$ kubectl get pod -o wide
NAME                 READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-n4tnc     1/1     Running   0          63m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-master-0       2/2     Running   0          85m   192.168.1.146   192.168.1.146   <none>           <none>
hbase-worker-qs26l   2/2     Running   0          63m   192.168.1.146   192.168.1.146   <none>           <none>
```

GooseFS Worker가 실행되었으며, 테인트가 있는 노드에서 실행되고 있음을 확인할 수 있습니다.

**GooseFSRuntime 상태 확인**

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE     AGE
hbase   1               1                 Ready          1               1                 Ready   1             1               Ready   4m3s
```


**생성 대기 중인 애플리케이션 조회**

Fluid가 데이터 캐시 친화성 스케줄링을 수행하는 방법을 보여주는 애플리케이션 샘플을 제공합니다. 먼저 애플리케이션을 살펴봅니다.
- app.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: apps/v1beta1
kind: StatefulSet
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  replicas: 1
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
      tolerations:
      - key: hbase 
        operator: Equal 
        value: "true" 
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
:::
</dx-codeblock>

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
```

Nginx Pod가 성공적으로 실행되었으며, taint가 구성된 노드에서 실행되는 것을 볼 수 있습니다.


## 환경 정리

```shell
$ kubectl delete -f .

$ kubectl taint nodes 192.168.1.146 hbase=true:NoSchedule-
```
