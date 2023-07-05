## 소개

워크로드의 고급 설정에서 스케줄링 정책을 설정하여 클러스터의 워크로드에서 Pod의 스케줄링을 지정할 수 있습니다. 다음은 일반적인 사용 사례입니다.
- 특정 노드에서 Pod를 실행합니다.
- 특정 범위(가용존, 모델 등이 될 수 있음)의 노드에서 Pod를 실행합니다.
- Pod가 별도의 노드에서 실행되도록 합니다(각 노드에 하나씩, 부적격 Pod 스케쥴링이 중지됨).

## 사용 방법

### 전제 조건

- 워크로드의 고급 설정에서 스케줄링 정책을 설정합니다. Kubernetes 1.7 이상 버전이어야 합니다.
- Pod가 성공적으로 스케쥴링될 수 있도록 하려면 스케쥴링 정책이 설정된 후 노드에 컨테이너 스케쥴링에 사용할 수 있는 리소스가 있어야 합니다.
- 사용자 정의 스케쥴링 기능을 사용하는 경우 노드 Label이 필요합니다. 자세한 내용은 [Setting Node Label](https://intl.cloud.tencent.com/document/product/457/30657)을 참고하십시오.

### 스케쥴링 정책 설정

Kubernetes 1.7 이상을 사용하여 클러스터를 생성한 경우 워크로드 생성 시 스케쥴링 정책을 설정할 수 있습니다.
다음 스케쥴링 유형 중 하나를 선택합니다.

- **Schedule to a specific node**: 일치하는 노드 레이블이 있는 특정 노드에 Pod를 스케쥴링합니다.
![](https://main.qcloudimg.com/raw/d999b561e17200605ed662f9fb427b33.png)
- **Custom scheduling**: Pod 레이블을 매칭하여 Pod가 스케쥴링되는 방식을 사용자 정의합니다.
![](https://main.qcloudimg.com/raw/8dc1bb38e4b982de9124eb0f9188359d.png)

사용자 정의 스케쥴링 정책에는 다음과 같은 모드가 있습니다.
- 충족해야 하는 조건: 노드가 친화성 조건을 충족하면 해당 node에 Pod가 스케쥴링됩니다. 그렇지 않으면 스케줄링이 실패합니다.
- 가능하면 충족해야 하는 조건: 노드가 친화성 조건을 충족하면 해당 node에 Pod가 스케쥴링됩니다. 그렇지 않은 경우 포드는 임의의 노드로 스케쥴링됩니다.

여러 사용자 정의 스케쥴링 정책을 추가할 수 있습니다. 다음은 오퍼레이터 목록입니다.
- In: Label의 value가 목록에 있습니다.
- NotIn: Label의 value가 목록에 없습니다.
- Exists: Label의 key가 존재합니다.
- DoesNotExits: Label의 key가 존재하지 않습니다.
- Gt: Label 값이 나열된 값보다 큽니다(문자열 일치).
- Lt: Label 값이 나열된 값보다 작습니다(문자열 일치).

## 작동 원리

Kubernetes는 Yaml 파일을 사용하여 스케쥴링 정책을 배포하고 Affinity and anti-affinity 메커니즘은 Pod가 규칙에 따라 스케쥴링되도록 합니다. 이 메커니즘에 대한 자세한 내용은 Kubernetes의 Affinity and anti-affinity [Kubernetes official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) 문서를 참고하십시오.


