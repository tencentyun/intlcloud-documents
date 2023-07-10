## 전제 조건

[Fluid](https://github.com/fluid-cloudnative/fluid)(version >= 0.5.0)가 설치되어 있어야 합니다.

>? [설치](https://intl.cloud.tencent.com/document/product/436/10865) 문서를 참고하여 설치하십시오.
>

## 작업 환경 생성

```shell
$ mkdir <any-path>/dataset_scale
$ cd <any-path>/dataset_scale
```

## 실행 예시

**Dataset와 GooseFSRuntime의 리소스 객체 생성**
```yaml
$ cat << EOF > dataset.yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: hbase
spec:
  mounts:
    - mountPoint: https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/stable/
  name: hbase
---
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
        high: "0.95"
        low: "0.7"
EOF
```
>? 사용자의 테스트 편의를 위해, 본 예시 중 mountPoint는 Web UFS를, UFS는 COS를 사용합니다. [GooseFS를 통한 COS(COSN) 마운트](https://intl.cloud.tencent.com/document/product/436/41024)를 참고하시기 바랍니다.
>

상기 예시에서 `GooseFSRuntime.spec.replicas`를 1로 설정했습니다. 즉, Worker 노드가 있는 GooseFS 클러스터를 실행하여 데이터 세트의 데이터를 캐시합니다.

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/hbase created
goosefsruntime.data.fluid.io/hbase created
```

GooseFS 클러스터가 정상적으로 실행될 때까지 기다리면 생성된 Dataset와 GooseFSRuntime이 다음과 같은 상태임을 확인할 수 있습니다.

GooseFS 각 컴포넌트의 실행 상태:

```shell
$ kubectl get pod
NAME                 READY   STATUS    RESTARTS   AGE
hbase-fuse-6pcnc     1/1     Running   0          3m15s
hbase-master-0       2/2     Running   0          3m50s
hbase-worker-w9wxh   2/2     Running   0          3m15s
```

Dataset 상태:

```shell
$ kubectl get dataset hbase
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   544.77MiB        0.00B    2.00GiB          0.0%                Bound   3m28s
```

GooseFSRuntime 상태:

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        4m55s
```

**Dataset 스케일 업**

```shell
$ kubectl scale goosefsruntime hbase --replicas=2
goosefsruntime.data.fluid.io/hbase scaled
```

'kubectl scale' 명령을 직접 사용하여 Dataset 스케일 업을 완료합니다. 상기 명령을 성공적으로 실행하고 일정 시간 동안 기다리면 Dataset 및 GooseFSRuntime 상태가 변경된 것을 확인할 수 있습니다.

새 GooseFS Worker 및 해당 GooseFS Fuse 컴포넌트가 성공적으로 실행되었습니다.

```shell
$ kubectl get pod
NAME                 READY   STATUS    RESTARTS   AGE
hbase-fuse-6pcnc     1/1     Running   0          13m
hbase-fuse-8qgww     1/1     Running   0          6m49s
hbase-master-0       2/2     Running   0          13m
hbase-worker-l4c8n   2/2     Running   0          6m49s
hbase-worker-w9wxh   2/2     Running   0          13m
```

Dataset  'Cache Capacity'이 기존 '2.00GiB'에서 '4.00GiB'로 변경됩니다. 이는 이 Dataset의 가용 캐시 용량이 증가했음을 나타냅니다.

```shell
$ kubectl get dataset hbase
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   544.77MiB        0.00B    4.00GiB          0.0%                Bound   15m
```

GooseFSRuntime의 'Ready Workers' 및 'Ready Fuses' 속성이 모두 2로 변경되었습니다.

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          2               2                 Ready          2             2               Ready        17m
```

최신 스케일링 정보에 대해 알아보려면 GooseFSRuntime의 구체적인 설명 정보를 확인합니다.
```shell
$ kubectl describe goosefsruntime hbase
...
  Conditions:
    ...
    Last Probe Time:                2021-04-23T07:54:03Z
    Last Transition Time:           2021-04-23T07:54:03Z
    Message:                        The workers are scale out.
    Reason:                         Workers scaled out
    Status:                         True
    Type:                           Workers scaled out
    Last Probe Time:                2021-04-23T07:54:03Z
    Last Transition Time:           2021-04-23T07:54:03Z
    Message:                        The fuses are scale out.
    Reason:                         Fuses scaled out
    Status:                         True
    Type:                           FusesScaledOut
...
Events:
  Type    Reason   Age   From            Message
  ----    ------   ----  ----            -------
  Normal  Succeed  2m2s  GooseFSRuntime  GooseFS runtime scaled out. current replicas: 2, desired replicas: 2.
```

**Dataset 스케일 다운**

스케일 업과 유사하게, 스케일 다운도 `kubectl scale`을 사용하여 Runtime의 Worker 수량을 조정할 수 있습니다.

```shell
$ kubectl scale goosefsruntime hbase --replicas=1
goosefsruntime.data.fluid.io/hbase scaled
```

상기 명령을 성공적으로 실행한 후, **현재 환경에서 데이터 세트에 액세스를 시도하는 애플리케이션이 없는 경우** Runtime 스케일 다운이 트리거됩니다.

지정된 'replicas`' 수량을 초과하는 Runtime Worker는 중지됩니다.

```shell
NAME                 READY   STATUS        RESTARTS   AGE
hbase-fuse-8qgww     1/1     Running       0          21m
hbase-fuse-zql96     1/1     Terminating   0          17m32s
hbase-master-0       2/2     Running       0          22m
hbase-worker-f92vv   2/2     Terminating   0          17m32s
hbase-worker-l4c8n   2/2     Running       0          21m
```

Dataset의 캐시 용량 'Cache Capacity'이 '2.00GiB'로 복구됩니다.

```shell
$ kubectl get dataset hbase
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   544.77MiB        0.00B    2.00GiB          0.0%                Bound   30m
```

>! 현재 Fluid 버전에서는 스케일 다운 시 Dataset의 'Cache Capacity' 속성 필드 변경에 몇 분의 딜레이가 발생하므로, 이 속성의 변경을 빠르게 관찰하지 못할 수 있습니다.
>

GooseFSRuntime의 'Ready Workers' 및 'Ready Fuses' 필드도 '1'이 됩니다.

```shell
$ kubectl get goosefsruntime hbase -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        30m
```

최신 스케일링 정보에 대해 알아보려면 GooseFSRuntime의 구체적인 설명 정보를 확인하십시오.
```shell
$ kubectl describe goosefsruntime hbase
...
  Conditions:
    ...
    Last Probe Time:                2021-04-23T08:00:55Z
    Last Transition Time:           2021-04-23T08:00:55Z
    Message:                        The workers scaled in.
    Reason:                         Workers scaled in
    Status:                         True
    Type:                           WorkersScaledIn
    Last Probe Time:                2021-04-23T08:00:55Z
    Last Transition Time:           2021-04-23T08:00:55Z
    Message:                        The fuses scaled in.
    Reason:                         Fuses scaled in
    Status:                         True
    Type:                           FusesScaledIn
...
Events:
  Type     Reason               Age    From            Message
  ----     ------               ----   ----            -------
  Normal   Succeed              6m56s  GooseFSRuntime  GooseFS runtime scaled out. current replicas: 2, desired replicas: 2.
  Normal   Succeed              4s     GooseFSRuntime  GooseFS runtime scaled in. current replicas: 1, desired replicas: 1.
```

Fluid가 제공하는 스케일링 기능은 사용자 또는 클러스터 관리자가 데이터 세트 캐시가 차지하는 클러스터 리소스를 제 때에 조정하거나, 자주 사용하지 않는 데이터 세트의 캐시 용량을 줄이거나(스케일 다운), 필요에 따라 캐시 용량을 늘리는 데(스케일업) 도움이 됩니다. 이를 통해 보다 정교한 리소스 할당을 구현하고 리소스 활용도를 향상시킬 수 있습니다.

## 환경 정리

```shell
$ kubectl delete -f dataset.yaml
```
