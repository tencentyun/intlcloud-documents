### Cluster Autoscaler와 모니터링 메트릭을 기반으로 하는 노드 오토 스케일링의 차이점은 무엇입니까?

Cluster Autoscaler는 클러스터의 모든 Pod가 실제 부하와 상관없이 스케쥴링될 수 있도록 하는 반면 모니터링 메트릭을 기반으로 하는 노드 오토 스케일링은 오토 스케일링 동안 Pod를 고려하지 않습니다. 따라서 Pod가 없는 노드가 추가되거나 kube-dns와 같은 시스템에 중요한 Pod가 있는 노드가 오토 스케일링 중에 삭제될 수 있습니다. Kubernetes는 후자의 오토 스케일링 메커니즘을 권장하지 않습니다. 결론적으로 이 두 모드는 충돌하므로 동시에 활성화하면 안 됩니다.

### CA는 오토 스케일링 그룹과 어떻게 작동합니까?

CA 지원 클러스터는 선택한 노드의 구성에 따라 시작 구성을 생성하고 여기에 오토 스케일링 그룹을 바인딩합니다. 그러면 클러스터는 이 바인딩된 오토 스케일링 그룹에서 scale-in/out을 수행합니다. 확장된 CVM 인스턴스는 클러스터에 자동으로 추가됩니다. 자동으로 확장/축소되는 노드는 사용한 만큼만 요금이 청구됩니다. 오토 스케일링 그룹에 대한 자세한 내용은 [Auto Scaling](https://intl.cloud.tencent.com/document/product/377)을 참고하십시오.

### TKE 콘솔에 수동으로 추가된 노드를 CA에서 축소할 수 있습니까?

아니요. CA는 오토 스케일링 그룹 내의 노드만 확장합니다. [TKE 콘솔](https://console.cloud.tencent.com/tke2)에 추가된 노드는 오토 스케일링 그룹에 추가되지 않습니다.

### 오토 스케일링 콘솔에서 CVM 인스턴스를 추가하거나 제거할 수 있습니까?

아니요. [오토 스케일링 콘솔](https://console.cloud.tencent.com/autoscaling)을 수정하지 않는 것이 좋습니다.

### 확장하는 동안 선택한 노드의 어떤 구성이 상속됩니까?

오토 스케일링 그룹을 생성할 때 클러스터의 노드를 참고로 선택하여 [시작 구성](https://intl.cloud.tencent.com/document/product/377/8543)을 생성해야 합니다. 참고용 노드 구성에는 다음이 포함됩니다.
 - vCPU
 - 메모리
 - 시스템 디스크 크기
 - 데이터 디스크 크기
 - 디스크 유형
 - 대역폭
 - 대역폭 과금 방식
 - 공용 IP 할당 여부
 - 보안 그룹
 - Virtual Private Cloud
 - 서브넷

### 여러 오토 스케일링 그룹을 사용하려면 어떻게 해야 합니까?

서비스의 레벨과 종류에 따라 여러 개의 오토 스케일링 그룹을 생성한 후 각각 다른 label을 설정하고, 오토 스케일링 그룹에서 스케일 아웃된 노드의 label을 지정하여 서비스를 분류할 수 있습니다.

### 스케일링 최대 할당량은 얼마입니까?

각 Tencent Cloud 사용자에게는 각 가용존에서 종량제 CVM 인스턴스 30개의 할당량이 제공됩니다. 오토 스케일링 그룹에 더 많은 인스턴스를 신청하기 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category)할 수 있습니다.
할당량에 대한 자세한 내용은 현재 가용존에 대한 [CVM 인스턴스 수량 및 할당량](https://console.cloud.tencent.com/cvm/overview)을 참고하십시오. 또한 오토 스케일링의 인스턴스는 최대 200개로 제한됩니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 더 높은 할당량을 신청할 수 있습니다.

### 스케일 다운이 클러스터에 안전한가요?

노드가 축소되면 Pod가 다시 예약되므로 서비스가 일정 변경 및 단기 중단을 허용할 수 있는 경우에만 축소를 수행할 수 있습니다. [PDB](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) 사용을 권장합니다. PDB는 항상 사용 가능한 상태로 유지되는 Pod 세트에 대한 복제본의 최소 수/백분율을 지정할 수 있습니다. PodDisruptionBudget을 사용하면 애플리케이션 배포자가 Pod를 적극적으로 제거하는 클러스터 작업이 한 번에 너무 많은 Pod를 종료하지 않도록 하여 데이터 손실, 서비스 중단 또는 허용할 수 없는 서비스 저하를 방지할 수 있습니다.

### 노드의 어떤 유형의 Pod가 축소되지 않습니까?

 - Pod에 대해 엄격한 PodDisruptionBudget을 설정한 경우 PDB가 충족되지 않으면 축소되지 않습니다.
 - Kube-system의 Pod.
 - deployment, replica set, job 또는 stateful set과 같은 컨트롤러에서 생성되지 않은 노드의 Pod.
 - 로컬 스토리지가 있는 Pod.
 - 다른 노드에 예약할 수 없는 Pod입니다.

### 조건이 충족된 후 축소를 트리거하는 데 얼마나 걸립니까?

10분.

### 노드가 Not Ready로 표시될 때 축소를 트리거하는 데 얼마나 걸립니까?

20분.

### 스케일링을 위해 노드를 얼마나 자주 스캔합니까?

10초.

#### CVM 인스턴스를 확장하는 데 얼마나 걸립니까?

일반적으로 10분 미만이 소요됩니다. 자세한 내용은 [오토 스케일링](https://intl.cloud.tencent.com/document/product/377)을 참고하십시오.

### Unschedulable Pod가 있는 노드가 확장되지 않는 이유는 무엇입니까?

다음을 확인하십시오.
- Pod의 요청된 리소스가 너무 크지 않은지.
- node selector 설정 여부.
- 오토 스케일링 그룹의 최대 노드 수 도달 여부.
- 계정 잔액 충분 여부(계정 잔액이 부족한 경우 수평 확장을 트리거할 수 없음), 할당량 부족 여부. 자세한 내용은 [Troubleshooting](https://intl.cloud.tencent.com/document/product/377/8626)을 참고하십시오.


### Cluster Autoscaler가 특정 노드에서 확장되지 않도록 하려면 어떻게 해야 합니까?

``` sh
# 노드의 annotations에서 다음 정보를 설정할 수 있습니다.
kubectl annotate node <nodename> cluster-autoscaler.kubernetes.io/scale-down-disabled=true
```


### 스케일링 이벤트에 대한 세부 정보는 어디에서 찾을 수 있나요?

오토 스케일링 그룹의 스케일링 이벤트를 조회하고 오토 스케일링 콘솔에서 K8s 이벤트를 볼 수 있습니다. 이벤트는 다음 세 가지 리소스에서 찾을 수 있습니다.
- kube-system/cluster-autoscaler-status config map
    - **ScaledUpGroup** - CA가 스케일 업을 트리거합니다.
    - **ScaleDownEmpty** - CA는 실행 중인 Pod가 없는 노드를 삭제합니다.
    - **ScaleDown** - CA가 스케일 다운을 트리거합니다.
- node
    - **ScaleDown** - CA가 스케일 다운을 트리거합니다.
    - **ScaleDownFailed** - CA가 스케일 다운을 트리거하지 못했습니다.
- pod
    - **TriggeredScaleUp** - CA는 이 Pod로 인해 스케일 업을 트리거합니다.
    - **NotTriggerScaleUp** - CA가 이 Pod를 스케쥴링하기 위해 사용 가능한 오토 스케일링 그룹을 찾을 수 없습니다.
    - **ScaleDown** - CA는 노드를 스케일 업하기 위해 이 Pod를 드레이닝하려고 합니다.


