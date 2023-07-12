Fluid는 GooseFS와 [Fuse](https://github.com/libfuse/libfuse)를 통해 사용자에게 보다 간단한 파일 액세스 인터페이스를 제공하여, Kubernetes 클러스터에서 실행되는 모든 프로그램이 로컬 파일에 액세스하는 것처럼 편리하게 원격 파일 시스템의 파일에 액세스할 수 있도록 합니다. Fluid는 데이터 세트의 전체 라이프사이클을 관리 및 격리하며, 특히 라이프사이클이 짧은 애플리케이션(예: 데이터 분석 작업, 머신 러닝 작업)의 경우, 사용자는 클러스터에서 대규모 배포를 진행할 수 있습니다.


## 전제 조건

이 예시를 실행하기 전에, [설치](https://intl.cloud.tencent.com/document/product/436/42230) 문서를 참고하여 설치를 완료하고, Fluid 각 컴포넌트의 정상 실행 여부를 확인해야 합니다.
```shell
$ kubectl get pod -n fluid-system
NAME                                  READY   STATUS    RESTARTS   AGE
goosefsruntime-controller-5b64fdbbb-84pc6   1/1     Running   0          8h
csi-nodeplugin-fluid-fwgjh                  2/2     Running   0          8h
csi-nodeplugin-fluid-ll8bq                  2/2     Running   0          8h
dataset-controller-5b7848dbbb-n44dj         1/1     Running   0          8h
```

일반적으로 'dataset-controller'라는 이름의 Pod, 'goosefsruntime-controller'라는 이름의 Pod, 그리고 'csi-nodeplugin'이라는 이름의 여러 Pod가 실행 중인 것을 볼 수 있습니다. 이 중 `csi-nodeplugin`과 같은 Pod 수량은 Kubernetes 클러스터 노드 수량에 따라 결정됩니다.


## 실행 예시
**특정 노드에 태그 달기**

```shell
$ kubectl  label node 192.168.0.199 fluid=multi-dataset
```

>? 다음 단계부터는 'NodeSelector'를 사용하여 Dataset 스케쥴링 노드를 관리합니다. 본문에서는 테스트용으로 진행합니다.
>

**생성 대기 중인 Dataset 리소스 객체 조회**

- dataset.yaml
<dx-codeblock>
::: yaml yaml
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
            - key: fluid
              operator: In
              values:
                - "multi-dataset"
  placement: "Shared" //Exclusive 또는 공란으로 설정된 경우, 배타적 노드 데이터 세트입니다.
:::
</dx-codeblock>
- dataset1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: spark
spec:
  mounts:
    - mountPoint: https://mirrors.bit.edu.cn/apache/spark/
      name: spark
  nodeAffinity:
      required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: fluid
              operator: In
              values:
                - "multi-dataset"
  placement: "Shared" 
:::
</dx-codeblock>

>? 사용자의 테스트 편의를 위해, 본 예시 중 mountPoint는 Web UFS를, UFS는 COS를 사용합니다. [GooseFS를 통한 COS(COSN) 마운트](https://intl.cloud.tencent.com/document/product/436/41024)를 참고하시기 바랍니다.
>

**Dataset 리소스 객체 생성**

```shell
$ kubectl apply -f dataset.yaml
dataset.data.fluid.io/hbase created
$ kubectl apply -f dataset1.yaml
dataset.data.fluid.io/spark created
```


** Dataset 리소스 객체 상태 조회**

```shell
$ kubectl get dataset
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE      AGE
hbase                                                                  NotBound   6s
spark                                                                  NotBound   4s
```
상기와 같이, 'status'의 'phase' 속성 값은 'NotBound'이며, 이는 'Dataset' 리소스 객체가 아직 'GooseFSRuntime' 리소스 객체와 바인딩되지 않았음을 의미합니다. 다음은 ` GooseFSRuntime' `리소스 객체 생성 관련 내용입니다.


**생성 대기 중인 GooseFSRuntime 리소스 객체 조회**

- runtime.yaml
<dx-codeblock>
::: yaml yaml
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
        high: "0.8"
        low: "0.7"
:::
</dx-codeblock>
- runtime-1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: spark
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk2/
        quota: 4G
        high: "0.8"
        low: "0.7"
:::
</dx-codeblock>

**GooseFSRuntime 리소스 객체 생성**
```shell
$ kubectl create -f runtime.yaml
goosefsruntime.data.fluid.io/hbase created


# Dataset hbase 실행의 모든 컴포넌트 Running 대기 
$ kubectl get pod -o wide | grep hbase
NAME                              READY   STATUS    RESTARTS   AGE   IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-jl2g2           1/1     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>
hbase-master-0             2/2     Running   0          2m55s   192.168.0.200   192.168.0.200   <none>           <none>
hbase-worker-g89p8         2/2     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>

$ kubectl create -f runtime1.yaml
goosefsruntime.data.fluid.io/spark created
```

**GooseFSRuntime 리소스 객체 생성 여부 확인**

```shell
$ kubectl get goosefsruntime
NAME    MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
hbase   Ready          Ready          Ready        2m14s
spark   Ready          Ready          Ready        58s
```

'GooseFSRuntime'은 Fluid가 정의한 또 다른 CRD입니다. 'GooseFSRuntime' 리소스 객체는 Kubernetes 클러스터에서 GooseFS 인스턴스를 실행하는 데 필요한 구성 정보를 설명합니다.


GooseFSRuntime 리소스 객체의 각 컴포넌트가 성공적으로 실행될 때까지 일정 시간 기다리면 다음과 유사한 상태를 확인할 수 있습니다.


```shell
$ kubectl get pod -o wide
NAME                        READY   STATUS    RESTARTS   AGE     IP              NODE                       NOMINATED NODE   READINESS GATES
hbase-fuse-jl2g2     1/1     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>
hbase-master-0       2/2     Running   0          2m55s   192.168.0.200   192.168.0.200   <none>           <none>
hbase-worker-g89p8   2/2     Running   0          2m24s   192.168.0.199   192.168.0.199   <none>           <none>
spark-fuse-5z49p     1/1     Running   0          19s     192.168.0.199   192.168.0.199   <none>           <none>
spark-master-0       2/2     Running   0          50s     192.168.0.200   192.168.0.200   <none>           <none>
spark-worker-96ksn   2/2     Running   0          19s     192.168.0.199   192.168.0.199   <none>           <none>
```
상기와 다른 Dataset의 worker 및 fuse 컴포넌트는 정상적으로 동일한 노드 '192.168.0.199'에 스케줄링될 수 있습니다.

**Dataset 리소스 객체 상태 재확인**

```shell
$ kubectl get dataset 
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   443.89MiB        0.00B    2.00GiB          0.0%                Bound   11m
spark   1.92GiB          0.00B    4.00GiB          0.0%                Bound   9m38s
```

성공적으로 실행된 GooseFSRuntime과 바인딩되었기 때문에, Dataset 리소스 객체 상태가 업데이트되었으며, 'PHASE' 속성 값이 'Bound' 상태로 변경되었습니다. 리소스 객체에 대한 기본 정보는 상기 명령어를 통해 얻을 수 있습니다.


**GooseFSRuntime 상태 조회**

```shell
$ kubectl get goosefsruntime -o wide
NAME    READY MASTERS   DESIRED MASTERS   MASTER PHASE   READY WORKERS   DESIRED WORKERS   WORKER PHASE   READY FUSES   DESIRED FUSES   FUSE PHASE   AGE
hbase   1               1                 Ready          1               1                 Ready          1             1               Ready        11m
spark   1               1                 Ready          1               1                 Ready          1             1               Ready        9m52s
```

>? 'GooseFSRuntime' 리소스 객체의 'status'에 더 자세한 정보가 포함되어 있습니다.
>

**원격 파일과 연결된 PersistentVolume 및 PersistentVolumeClaim 조회**

```shell
$ kubectl get pv
NAME    CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM           STORAGECLASS   REASON   AGE
hbase   100Gi      RWX            Retain           Bound    default/hbase                           4m55s
spark   100Gi      RWX            Retain           Bound    default/spark                           51s
```

```shell
$ kubectl get pvc
NAME    STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
hbase   Bound    hbase    100Gi      RWX                           4m57s
spark   Bound    spark    100Gi      RWX                           53s
```

'Dataset' 리소스 객체 준비 완료 후(즉, GooseFS 인스턴스에 바인딩된 후), 리소스 객체와 연결된 PV 및 PVC가 Fluid에 의해 생성되었습니다. 애플리케이션은 이 PVC를 통해 원격 파일의 Pod 마운트를 완료할 수 있으며, 디렉터리 마운트를 통해 원격 파일 액세스를 구현할 수 있습니다.

## 원격 파일 액세스

**생성 대기 중인 애플리케이션 조회**

- nginx.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-hbase
spec:
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
  nodeName: 192.168.0.199
:::
</dx-codeblock>
- nginx1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-spark
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
        - mountPath: /data
          name: hbase-vol
  volumes:
    - name: hbase-vol
      persistentVolumeClaim:
        claimName: spark
  nodeName: 192.168.0.199
:::
</dx-codeblock>

**애플리케이션을 실행하여 원격 파일 액세스 진행**
```shell
$ kubectl create -f nginx.yaml
$ kubectl create -f nginx1.yaml
```

Nginx hbase Pod 로그인:

```shell
$ kubectl exec -it nginx-hbase -- bash
```

원격 파일 마운트 상황 조회:

```shell
$ ls -lh /data/hbase
total 444M
-r--r----- 1 root root 193K Sep 16 00:53 CHANGES.md
-r--r----- 1 root root 112K Sep 16 00:53 RELEASENOTES.md
-r--r----- 1 root root  26K Sep 16 00:53 api_compare_2.2.6RC2_to_2.2.5.html
-r--r----- 1 root root 211M Sep 16 00:53 hbase-2.2.6-bin.tar.gz
-r--r----- 1 root root 200M Sep 16 00:53 hbase-2.2.6-client-bin.tar.gz
-r--r----- 1 root root  34M Sep 16 00:53 hbase-2.2.6-src.tar.gz
```

Nginx spark Pod 로그인:
```shell
$ kubectl exec -it nginx-spark -- bash
```

원격 파일 마운트 상황 조회:

```shell
$ ls -lh /data/spark/
total 1.0K
dr--r----- 1 root root 7 Oct 22 12:21 spark-2.4.7
dr--r----- 1 root root 7 Oct 22 12:21 spark-3.0.1
$ du -h /data/spark/
999M	/data/spark/spark-3.0.1
968M	/data/spark/spark-2.4.7
2.0G	/data/spark/
```

Nginx Pod 로그아웃:

```shell
$ exit
```

보시다시피 WebUFS에 저장된 모든 파일은 로컬 파일과 다름 없이 Pod에 존재하며, Pod에서 쉽게 액세스할 수 있습니다.

## 원격 파일 액세스 가속

원격 파일에 액세스할 때 얻을 수 있는 가속 효과를 나타내기 위해, 테스트 작업 예시를 제공합니다.

**생성 대기 중인 테스트 작업 조회**

- app.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: fluid-copy-test-hbase
spec:
  template:
    spec:
      restartPolicy: OnFailure
      containers:
        - name: busybox
          image: busybox
          command: ["/bin/sh"]
          args: ["-c", "set -x; time cp -r /data/hbase ./"]
          volumeMounts:
            - mountPath: /data
              name: hbase-vol
      volumes:
        - name: hbase-vol
          persistentVolumeClaim:
            claimName: hbase
      nodeName: 192.168.0.199
:::
</dx-codeblock>
- app1.yaml
<dx-codeblock>
::: yaml yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: fluid-copy-test-spark
spec:
  template:
    spec:
      restartPolicy: OnFailure
      containers:
        - name: busybox
          image: busybox
          command: ["/bin/sh"]
          args: ["-c", "set -x; time cp -r /data/spark ./"]
          volumeMounts:
            - mountPath: /data
              name: spark-vol
      volumes:
        - name: spark-vol
          persistentVolumeClaim:
            claimName: spark
      nodeName: 192.168.0.199
:::
</dx-codeblock>


**테스트 작업 실행**

```shell
$ kubectl create -f app.yaml
job.batch/fluid-copy-test-hbase created
$ kubectl create -f app1.yaml
job.batch/fluid-copy-test-spark created
```

hbase 작업 프로그램은 `time cp -r /data/hbase ./`의 shell 명령을 실행합니다. 이 중 `/data/hbase`는 원격 파일이 Pod에 마운트된 위치입니다. 명령이 완료된 후, 명령 실행 소요시간은 디바이스에 표시됩니다.

spark 작업 프로그램은 `time cp -r /data/spark ./`의 shell 명령을 실행합니다. 여기서 `/data/spark`는 원격 파일이 Pod에 마운트된 위치입니다. 명령이 완료된 후, 명령이 완료된 후, 명령 실행 소요시간은 디바이스에 표시됩니다.

작업 완료까지 일정 시간 동안 기다린 후, 다음 명령으로 작업의 실행 상태를 확인할 수 있습니다.

```shell
$ kubectl get pod -o wide | grep copy 
fluid-copy-test-hbase-r8gxp   0/1     Completed   0          4m16s   172.29.0.135    192.168.0.199   <none>           <none>
fluid-copy-test-spark-54q8m   0/1     Completed   0          4m14s   172.29.0.136    192.168.0.199   <none>           <none>
```

상기와 같은 결과가 보이면 작업이 완료된 것입니다.

>!  `fluid-copy-test-hbase-r8gxp`의 `r8gxp`는 작업에 의해 생성된 식별입니다. 사용자의 환경에 따라 이 식별은 다를 수 있습니다. 하기 내용 중 이 식별과 관련된 내용은 사용자의 환경을 기준으로 참고하시기 바랍니다.
>

**테스트 작업 완료 시간 확인**


```shell
$ kubectl  logs fluid-copy-test-hbase-r8gxp
+ time cp -r /data/hbase ./
real    3m 34.08s
user    0m 0.00s
sys     0m 1.24s
$ kubectl  logs fluid-copy-test-spark-54q8m
+ time cp -r /data/spark ./
real    3m 25.47s
user    0m 0.00s
sys     0m 5.48s
```


hbase에서 첫 번째 원격 파일 읽기는 약 3분 34초가 소요되었고, spark 읽기는 약 3분 25초가 소요되었습니다.


**Dataset 리소스 객체 상태 조회**


```shell
$ kubectl get dataset
NAME    UFS TOTAL SIZE   CACHED      CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
hbase   443.89MiB        443.89MiB   2.00GiB          100.0%              Bound   30m
spark   1.92GiB          1.92GiB     4.00GiB          100.0%              Bound   28m
```

이제 모든 원격 파일이 GooseFS에 캐시되었습니다.

**테스트 작업 재실행**

```shell
$ kubectl delete -f app.yaml
$ kubectl create -f app.yaml
$ kubectl delete -f app1.yaml
$ kubectl create -f app1.yaml
```

원격 파일이 캐시되었으므로 테스트 작업을 빠르게 완료할 수 있습니다.

```shell
$ kubectl get pod -o wide| grep fluid
fluid-copy-test-hbase-sf5md   0/1     Completed   0          53s   172.29.0.137    192.168.0.199   <none>           <none>
fluid-copy-test-spark-fwp57   0/1     Completed   0          51s   172.29.0.138    192.168.0.199   <none>           <none>
```

```shell
$ kubectl  logs fluid-copy-test-hbase-sf5md
+ time cp -r /data/hbase ./
real    0m 0.36s
user    0m 0.00s
sys     0m 0.36s
$ kubectl  logs fluid-copy-test-spark-fwp57
+ time cp -r /data/spark ./
real    0m 1.57s
user    0m 0.00s
sys     0m 1.57s
```

동일한 파일 액세스 작업에 hbase는 단 0.36초, spark는 단 1.57초가 소요되었습니다.

이렇게 큰 가속 효과는 GooseFS가 제공하는 강력한 캐싱 기능에 기인합니다. 이 캐싱 기능은 원격 파일에 한 번 액세스하기만 하면, 해당 파일이 GooseFS에 캐시됨을 의미합니다. 반복 액세스 시 원격 파일을 읽어올 필요 없이 GooseFS에서 데이터를 직접 가져오기 합니다.

## 환경 정리
```shell
$ kubectl delete -f .
$ kubectl label node 192.168.0.199 fluid-
```
