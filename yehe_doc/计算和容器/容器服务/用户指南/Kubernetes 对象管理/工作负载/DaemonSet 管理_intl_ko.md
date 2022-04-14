## 소개

DaemonSet은 로그 데몬과 같은 클러스터에 상주하는 백그라운드 프로그램 배포에 사용됩니다. DaemonSet은 지정된 Pod가 모든 또는 특정 노드에서 실행되고 있는지 확인합니다. 클러스터에 새 노드를 추가하면 Pod가 자동으로 배포됩니다. 클러스터에서 노드가 제거되면 Pod가 자동으로 재소유됩니다.

## 스케쥴링

Pod에 nodeSelector 또는 affinity가 설정된 경우 DaemonSet에서 관리하는 Pod는 기존 정책에 따라 예약됩니다. 그렇지 않은 경우 Pod가 모든 노드에 배포됩니다.

## 콘솔을 통해 DaemonSet 사용

### DaemonSet 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. DaemonSet을 생성해야 하는 클러스터의 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.
3. [Workload]>[DaemonSet]을 선택하여 아래와 같이 DaemonSet 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/ec694431e23d70a8f327fb7ef497480b.png)
4. [Create]을 클릭하여 ‘Create Workload’ 페이지로 이동합니다.
필요에 따라 DaemonSet 매개변수를 설정합니다. 주요 매개변수는 다음과 같습니다.
 - **Workload name**: 워크로드의 이름입니다.
 - **Namespace**: 필요에 따라 선택합니다.
 - **Type**: [DaemonSet(run the Pod on each server)]을 선택합니다.
 - **In-Pod containers**: DaemonSet Pod의 컨테이너를 설정합니다.
    - **Name**: 이름을 입력합니다.
    - **Image**: 원하는 이미지를 선택합니다.
    - **Image tag**: 이미지에 대한 태그를 입력합니다.
    - **Image pull policy**: 다음 세 가지 정책을 사용할 수 있습니다. 필요에 따라 선택합니다.
      이미지 가져오기 정책을 설정하지 않고 Image Tag가 `latest`이거나 비어 있는 경우 Always를 사용합니다. 그렇지 않으면 IfNotPresent를 사용합니다.
       - **Always**: 이미지는 항상 원격 위치에서 가져옵니다.
       - **IfNotPresent**: 기본적으로 로컬 이미지를 사용합니다. 이미지를 사용할 수 없는 경우 원격 위치에서 가져옵니다.
       - **Never**: 로컬 이미지만 사용합니다. 이미지를 사용할 수 없으면 예외가 발생합니다.
    - **CPU/memory limits**: [Kubernetes resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)에 따라 CPU 및 메모리 제한을 설정하여 서비스 견고성을 향상시킵니다.
    - 고급 설정: ‘**working directory**’, ‘**run commands**’, ‘**run parameters**’, ‘**container health check**’ 및 ‘**privilege level**’과 같은 매개변수를 설정할 수 있습니다.
5. [Create a workload]를 클릭하여 생성을 완료합니다.

### DaemonSet 업데이트

#### YAML 파일 업데이트
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. YAML을 업데이트하려는 클러스터 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.
3.[Workload]>[DaemonSet]을 선택하여 DaemonSet 페이지로 이동합니다.
5. YAML을 업데이트할 DaemonSet의 행에서 [More]>[Edit YAML]을 클릭하여 DaemonSet 업데이트 페이지로 이동합니다.
6. ‘Update a DaemonSet’ 페이지에서 YAML을 편집하고 [Finish]를 클릭하여 YAML을 업데이트합니다.

#### Pod 설정 업데이트
> DaemonSet의 롤링 업데이트는 Kubernetes v1.6 이상에서만 지원됩니다.
>
1. 클러스터 관리 페이지에서 Pod 설정을 업데이트할 클러스터의 ID를 클릭하고 클러스터의 관리 페이지로 이동합니다.
2. Pod 설정을 업데이트할 DaemonSet에 해당하는 [Update Pod Configurations]를 클릭합니다.
3. ‘Updating Pod Configurations’ 페이지에서 필요에 따라 업데이트 방법을 수정하고 매개변수를 설정합니다.
4. [Finish]를 클릭하여 Pod 설정을 업데이트합니다.

## kubectl을 통해 DaemonSet 사용


### YAML 예시 파일<span id="YAMLSample"></span>
```Yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-elasticsearch
  namespace: kube-system
  labels:
    k8s-app: fluentd-logging
spec:
  selector:
    matchLabels:
      name: fluentd-elasticsearch
  template:
    metadata:
      labels:
        name: fluentd-elasticsearch
    spec:
      tolerations:
      - key: node-role.kubernetes.io/master
        effect: NoSchedule
      containers:
      - name: fluentd-elasticsearch
        image: k8s.gcr.io/fluentd-elasticsearch:1.20
        resources:
          limits:
            memory: 200Mi
          requests:
            cpu: 100m
            memory: 200Mi
        volumeMounts:
        - name: varlog
          mountPath: /var/log
        - name: varlibdockercontainers
          mountPath: /var/lib/docker/containers
          readOnly: true
      terminationGracePeriodSeconds: 30
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
      - name: varlibdockercontainers
        hostPath:
          path: /var/lib/docker/containers
```
>상기 YAML 예시 파일은 `https://kubernetes.io/docs/concepts/workloads/controllers/daemonset`에서 가져옵니다. 생성하는 동안 컨테이너 이미지를 사용하지 못할 수 있습니다. 예시는 DaemonSet 생성을 설명하기 위해서만 사용됩니다.

- **kind**: DaemonSet 리소스 유형입니다.
- **metadata**: DaemonSet 이름 및 Label과 같은 정보입니다.
- **metadata.annotations**: DaemonSet에 대한 추가 설명입니다. 이 매개변수를 통해 TKE에 대한 추가 개선 사항을 설정할 수 있습니다.
- **spec.template**: DaemonSet에서 관리하는 Pod의 세부 템플릿 설정입니다.

자세한 내용은 [Kubernetes official documentation](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)을 참고하십시오.

### kubectl 사용하여 DaemonSet 생성

1. [sample YAML file](#YAMLSample)을 참고하여 StatefulSet YAML 파일을 준비합니다.
2. kubectl을 설치하고 클러스터에 연결합니다. 자세한 내용은 [Connecting to Clusters](https://intl.cloud.tencent.com/document/product/457/30639)를 참고하십시오.
3. 다음 명령을 실행하여 DaemonSet YAML 파일을 생성합니다.
```shell
kubectl create -f DaemonSet YAML 파일 이름
```
예를 들어 fluentd-elasticsearch.yaml이라는 StatefulSet YAML 파일을 생성하려면 다음 명령을 실행합니다.
```shell
kubectl create -f fluentd-elasticsearch.yaml
```
4. 다음 명령을 실행하여 파일이 성공적으로 생성되었는지 확인합니다.
```shell
kubectl get DaemonSet
```
아래와 유사한 메시지는 YAML 파일이 성공적으로 생성되었음을 나타냅니다.
```
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR       AGE
frontend   0         0         0         0            0           app=frontend-node   16d
```

### kubectl 사용하여 DaemonSet 업데이트

DaemonSet의 업데이트 정책 유형을 보려면 다음 명령을 실행합니다.
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
DaemonSet에는 다음과 같은 업데이트 정책 유형이 있습니다.
- OnDelete: 기본 업데이트 정책입니다. DaemonSet이 업데이트된 후 새 DaemonSet Pod를 생성하려면 이전 DaemonSet Pod를 수동으로 삭제해야 합니다.
- RollingUpdate: Kubernetes 1.6 이상만 지원됩니다. DaemonSet가 업데이트되면 이전 DaemonSet Pod가 종료되고 롤링 업데이트를 통해 새 Pod가 생성됩니다.

#### 방법1

DaemonSet를 업데이트하려면 다음 명령을 실행합니다.
```
kubectl edit DaemonSet/[name]
```
디버깅 또는 확인에 사용합니다. 프로덕션 환경에서는 사용하지 않는 것이 좋습니다. 이 방법으로 모든 DaemonSet 매개변수를 업데이트할 수 있습니다.

#### 방법2

다음 명령어를 실행하여 특정 컨테이너의 이미지를 업데이트합니다.
```
kubectl set image ds/[daemonset-name][container-name]=[container-new-image]
```
다른 DaemonSet 매개변수를 변경하지 않고 유지하고 서비스를 업데이트할 때 컨테이너 이미지만 업데이트하는 것이 좋습니다.

### kubectl 사용하여 DaemonSet 롤백

1. DaemonSet의 업데이트 기록을 보려면 다음 명령을 실행합니다.
```
kubectl rollout history daemonset /[name]
```
2. 특정 버전의 세부 정보를 보려면 다음 명령을 실행합니다.
```
kubectl rollout history daemonset /[name] --revision=[REVISION]
```
3. 다음 명령을 실행하여 마지막 버전으로 롤백합니다.
```
kubectl rollout undo daemonset /[name]
```
롤백 버전을 지정하려면 다음 명령을 실행합니다.
```
kubectl rollout undo daemonset /[name] --to-revision=[REVISION]
```

### kubectl 사용하여 DaemonSet 삭제
DaemonSet을 삭제하려면 다음 명령을 실행합니다.
```
kubectl delete  DaemonSet [NAME]
```
