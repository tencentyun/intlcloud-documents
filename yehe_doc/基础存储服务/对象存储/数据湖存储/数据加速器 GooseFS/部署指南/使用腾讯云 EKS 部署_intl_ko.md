 [Elastic Kubernetes Service(EKS)](https://intl.cloud.tencent.com/document/product/457/34040)는 사용자가 노드를 구매하지 않고도 워크로드를 배포할 수 있는 Tencent Kubernetes Engine입니다. EKS는 네이티브 Kubernetes와 완벽하게 호환되며, 네이티브 방식으로 리소스를 구매 및 관리할 수 있고, 컨테이너에서 사용한 실제 리소스 양에 따라 요금이 청구됩니다. EKS는 또한 Tencent Cloud의 스토리지 및 네트워크 제품을 확장 지원하는 동시에 사용자 컨테이너의 안전한 격리와 사용 편리성을 보장합니다.

Tencent Cloud EKS를 사용하여 GooseFS를 배포하면 EKS의 탄력적인 컴퓨팅 리소스를 최대한 활용할 수 있으며, 초 단위로 과금되는 주문형 Cloud Object Storage(COS) 스토리지 액세스 가속화 서비스를 구축할 수 있습니다.

## 아키텍처 설명

다음 이미지는 Tencent Cloud EKS를 사용하여 GooseFS를 배포하는 일반적인 아키텍처를 보여줍니다.
![](https://main.qcloudimg.com/raw/edccf984a806e02a53dd2f88a6fb4728.jpg)

그림에 표시된 것처럼 전체 아키텍처는 EKS 호스팅 컴포넌트, 사용자 리소스 풀 및 COS ​​스토리지 세 부분으로 구성됩니다. 그 중 사용자 리소스 풀은 주로 GooseFS 클러스터를 구축하는데 사용되고, COS 스토리지는 원격 스토리지 시스템으로 사용되며, 퍼블릭 클라우드 스토리지 서비스인 클라우드 HDFS의 대체도 지원됩니다. 구체적인 구축 과정은 다음과 같습니다.
- GooseFS Master와 Worker 모두 Kubernetes Statefulset 유형으로 리소스를 배포합니다.
- Fluid를 사용하여 GooseFS 클러스터를 풀업합니다.
- Fuse Client는 사용자 Pod의 샌드박스(Sandbox)에 통합됩니다.
- 사용 방법은 표준 Kubernetes와 일치합니다.

## 작업 단계

### 환경 준비

1. EKS 클러스터 생성 구체적인 작업은 [클러스터 생성](https://intl.cloud.tencent.com/document/product/457/34048)을 참고하십시오.
2. 클러스터 액세스를 활성화하고 실제 상황에 따라 내부 네트워크 또는 외부 네트워크를 선택합니다. 구체적인 설명은 [클러스터 연결](https://intl.cloud.tencent.com/document/product/457/34049)을 참고하십시오.
3. `kubectl get ns` 명령을 실행하여 클러스터를 사용할 수 있는지 확인합니다.
<dx-codeblock>
::: shell shell
   -> goosefs kubectl get ns
   NAME              STATUS   AGE
   default           Active   7h31m
   kube-node-lease   Active   7h31m
   kube-public       Active   7h31m
   kube-system       Active   7h31m
:::
</dx-codeblock>
4. 'helm'을 가져오는 방법은 [Helm 공식 문서](https://helm.sh/docs/intro/install/#from-the-binary-releases)를 참고하십시오.

### GooseFS 설치 

1. `helm install` 명령을 입력하여 chart 패키지를 설치하고, fluid를 설치합니다.
<dx-codeblock>
::: shell shell
   -> goosefs helm install fluid ./charts/fluid-on-tke
   NAME: fluid
   LAST DEPLOYED: Tue Jul  6 17:41:20 2021
   NAMESPACE: default
   STATUS: deployed
   REVISION: 1
   TEST SUITE: None
:::
</dx-codeblock>
2. `fluid`와 관련된 pod의 상태를 확인합니다.
<dx-codeblock>
::: shell shell
   -> goosefs kubectl -n fluid-system get pod
   NAME                                         READY   STATUS    RESTARTS   AGE
   alluxioruntime-controller-78877d9d47-p2pv6   1/1     Running   0          59s
   dataset-controller-5f565988cc-wnp7l          1/1     Running   0          59s
   goosefsruntime-controller-6c55b57cd6-hr78j   1/1     Running   0          59s
:::
</dx-codeblock>
3. `dataset`을 생성하고 실제 필요에 따라 관련 변수를 수정한 다음 `kubectl apply -f dataset.yaml` 명령을 실행하여 `dataset`을 적용합니다.
<dx-codeblock>
::: yaml yaml
   apiVersion: data.fluid.io/v1alpha1
   kind: Dataset
   metadata:
     name: ${dataset-name}
   spec:
     mounts:
     - mountPoint: cosn://${bucket-name}
       name: ${dataset-name}
       options:
         fs.cosn.userinfo.secretKey: XXXXXXX
         fs.cosn.userinfo.secretId: XXXXXXX
         fs.cosn.bucket.region: ap-${region}
         fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
         fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
         fs.cos.app.id: ${user-app-id}
:::
</dx-codeblock>
4. `GooseFS` 클러스터를 생성하고 다음 yaml을 사용하여 `kubectl apply -f runtime.yaml`을 실행합니다.
<dx-codeblock>
::: yaml yaml
    apiVersion: data.fluid.io/v1alpha1
    kind: GooseFSRuntime
    metadata:
      name: slice1
      annotations:
        master.goosefs.eks.tencent.com/model: c6
        worker.goosefs.eks.tencent.com/model: c6
    spec:
      replicas: 6 # worker 수량. 컨트롤러가 확장을 지원하지만 goosefs는 현재 데이터의 자동 re-balance를 지원하지 않습니다.
      data:
        replicas: 1  # goosefs 데이터 복제본 수
      goosefsVersion:
        imagePullPolicy: Always
        image: ccr.ccs.tencentyun.com/cosdev/goosefs   # goosefs 클러스터에서 사용하는 미러 이미지 및 버전
        imageTag: v1.0.1
      tieredstore:
        levels:
          - mediumtype: MEM # 메모리, 고효율 클라우드 디스크, SSD 클라우드 디스크에 각각 해당하는 MEM, HDD, SSD 지원
            path: /data
            quota: 5G   # 메모리와 클라우드 디스크가 모두 적용되며, 클라우드 디스크는 최소 10G입니다.
            high: "0.95"
            low: "0.7"
      properties:
        goosefs.user.streaming.data.timeout: 5s
        goosefs.job.worker.threadpool.size: "22"
        goosefs.master.journal.type: UFS        # UFS 또는 EMBEDDED. 단일 master는 UFS 사용
    #    goosefs.worker.network.reader.buffer.size: 128MB
        goosefs.user.block.size.bytes.default: 128MB
    #    goosefs.user.streaming.reader.chunk.size.bytes: 32MB
    #    goosefs.user.local.reader.chunk.size.bytes: 32MB
        goosefs.user.metrics.collection.enabled: "false"
        goosefs.user.metadata.cache.enabled: "true"
        goosefs.user.metadata.cache.expiration.time: "2day"
      master:
        # POD에 해당하는 가상 머신의 사양을 설정합니다. 매개변수는 필수 사항이며, 미입력 시 기본값은 1c1g입니다.
        resources:
          requests:
            cpu: 8
            memory: "16Gi"
          limits:
            cpu: 8
            memory: "16Gi"
        replicas: 1
    #    journal:
    #      volumeType: pvc
    #      storageClass: goosefs-hdd
        jvmOptions:
          - "-Xmx12G"
          - "-XX:+UnlockExperimentalVMOptions"
          - "-XX:ActiveProcessorCount=8"
          - "-Xms10G"
      worker:
        jvmOptions:
          - "-Xmx28G"
          - "-Xms28G"
          - "-XX:+UnlockExperimentalVMOptions"
          - "-XX:MaxDirectMemorySize=28g"
          - "-XX:ActiveProcessorCount=8"
        resources:
          requests:
            cpu: 16
            memory: "32Gi"
          limits:
            cpu: 16
            memory: "32Gi"
      fuse:
        jvmOptions:
          - "-Xmx4G"
          - "-Xms4G"
          - "-XX:+UseG1GC"
          - "-XX:MaxDirectMemorySize=4g"
          - "-XX:+UnlockExperimentalVMOptions"
          - "-XX:ActiveProcessorCount=24"
:::
</dx-codeblock>
5. 클러스터 상태 및 PVC 상태를 확인합니다.
<dx-codeblock>
::: shell shell
   -> goosefs kubectl get pod
   NAME              READY   STATUS    RESTARTS   AGE
   slice1-master-0   2/2     Running   0          8m8s
   slice1-worker-0   2/2     Running   0          8m8s
   slice1-worker-1   2/2     Running   0          8m8s
   slice1-worker-2   2/2     Running   0          8m8s
   slice1-worker-3   2/2     Running   0          8m8s
   slice1-worker-4   2/2     Running   0          8m8s
   slice1-worker-5   2/2     Running   0          8m8s
   -> goosefs kubectl get pvc
   slice1 Bound default-slice1 100Gi ROX fluid 7m37s       # PVC 이름은 dataset 이름과 같고, 100Gi는 플레이스홀더로 사용하는 가상 값입니다.
:::
</dx-codeblock>


### 데이터 로딩
데이터를 미리 로딩하려면 다음 yaml을 사용하여 resource를 생성하기만 하면 됩니다. yaml의 예시는 `kubectl apply -f dataload.yaml`입니다. 실행 후 응답 예시는 다음과 같습니다.
```
   apiVersion: data.fluid.io/v1alpha1
   kind: DataLoad
   metadata:
     name: slice1-dataload
   spec:
     # 데이터 로딩을 실행해야 하는 dataset 정보 설정
     dataset:
       name: slice1
       namespace: default
```

생성 후 `kubectl get dataload slice1-dataload`를 통해 상태를 관찰할 수 있습니다.

### 비즈니스 Pod 마운트 PVC

사용자 서비스 컨테이너는 k8s 표준 사용법에 따라 사용하며, 자세한 내용은 [Kubernetes 공식 문서](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)를 참고하십시오.

### GooseFS 클러스터 폐기

GooseFS 클러스터는 `delete` 명령을 통해 폐기할 수 있으며, master 노드와 worker 노드를 삭제하도록 지정할 수 있습니다. **이 작업은 고위험 작업입니다. 비즈니스 pod에 Goosefs에 대한 IO 작업이 없는지 확인한 후 진행하십시오.**
```
   -> goosefs kubectl get sts
   NAME            READY   AGE
   slice1-master   1/1     14m
   slice1-worker   6/6     14m
   -> goosefs kubectl delete sts slice1-master slice1-worker
   statefulset.apps "slice1-master" deleted
   statefulset.apps "slice1-worker" deleted
```
