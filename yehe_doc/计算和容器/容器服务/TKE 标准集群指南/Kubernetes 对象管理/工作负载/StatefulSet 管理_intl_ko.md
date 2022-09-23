## 소개

StatefulSet는 상태 저장 애플리케이션을 관리하는 데 사용됩니다. 각 Pod에 대한 표준 영구 식별자를 생성합니다. 식별자는 Pod가 마이그레이션, 종료 또는 다시 시작된 후에도 유지됩니다. 영구 저장소를 사용할 때 저장소 볼륨을 식별자에 매핑할 수 있습니다. 애플리케이션에 영구 식별자가 필요하지 않은 경우 Deployment를 사용하여 애플리케이션을 배포하는 것이 좋습니다.

## 콘솔을 통해 StatefulSet 사용

<span id="createStatefulSet"></span>

### StatefulSet 생성

1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. StatefulSet을 생성할 클러스터의 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.
3. [Workload]>[StatefulSet]을 선택하여 아래와 같이 StatefulSet의 관리 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/88ece12d8464711824eadfb35db0c050.png)
4. [Create]를 클릭하여 ‘Create Workload’ 페이지로 이동합니다.
필요에 따라 StatefulSet 매개변수를 설정합니다. 주요 매개변수는 다음과 같습니다.
 - **Workload**: 워크로드의 이름입니다.
 - **Namespace**: 네임스페이스를 선택합니다.
 - **Type**: [StatefulSet(run the Pod in a stateful manner)]을 선택합니다.
 - **In-Pod containers**: 필요에 따라 StatefulSet의 Pod에 대해 하나 이상의 컨테이너를 설정합니다.
    - **Name**: 이름을 입력합니다.
    - **Image**: 이미지를 선택합니다.
    - **Image Tag**: 이미지 태그를 입력합니다.
    - **Image pull policy**: 다음 중 하나를 선택합니다.
       이미지 가져오기 정책을 설정하지 않고 이미지 태그가 `latest`이거나 비어 있으면 Always가 사용됩니다. 그렇지 않으면 IfNotPresent가 사용됩니다.
        - **Always**: 이미지를 항상 원격 위치에서 가져오기합니다.
        - **IfNotPresent**: 기본적으로 로컬 이미지를 사용합니다. 이미지를 사용할 수 없는 경우 원격 위치에서 이미지를 가져옵니다.
        - **Never**: 로컬 이미지만 사용합니다. 이미지를 사용할 수 없으면 예외가 발생합니다.
    - **CPU/memory limits**: [Kubernetes resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)에 따라 CPU 및 메모리 제한을 설정하여 서비스 견고성을 향상시킵니다.
    - **Advanced settings**: ‘**working directory**’, ‘**run commands**’, ‘**run parameters**’, ‘**container health check**’ 및 ‘**privilege level**’과 같은 매개변수를 설정합니다.
 - **Pod quantity**: 조정 방법을 선택하고 포드 수량을 설정합니다.
5. [Create a workload]을 클릭하여 생성을 완료합니다.

### StatefulSet 업데이트

#### YAML 업데이트
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. YAML을 업데이트할 클러스터 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.
3. [Workload]>[StatefulSet]을 선택하여 StatefulSet의 관리 페이지로 이동합니다.
4. YAML을 업데이트할 StatefulSet의 행에서 [More]>[Edit YAML]을 클릭하여 StatefulSet 업데이트 페이지로 이동합니다.
5. ‘Update StatefulSet’ 페이지에서 YAML을 편집하고 [Finish]를 클릭하여 YAML을 업데이트합니다.

#### Pod 설정 업데이트
1. 클러스터 관리 페이지에서 Pod 설정을 업데이트할 StatefulSet 클러스터의 ID를 클릭하여 StatefulSet 클러스터 관리 페이지로 이동합니다.
2. Pod 설정을 업데이트할 StatefulSet 행에서 [Update Pod Configurations]를 클릭합니다.
3. ‘Update Pod Configurations’ 페이지에서 업데이트 방법을 수정하고 필요에 따라 매개변수를 설정합니다.
4. [Finish]를 클릭하여 Pod 설정을 업데이트합니다.

## kubectl을 통한 StatefulSet 사용

<span id="YAMLSample"></span>

### YAML 파일 예시

```Yaml
apiVersion: v1
kind: Service  ## 네트워크 도메인을 제어하기 위한 Headless Service 생성
metadata:
  name: nginx
  namespace: default
  labels:
    app: nginx
spec:
  ports:
  - port: 80
    name: web
  clusterIP: None
  selector:
    app: nginx
---
apiVersion: apps/v1
kind: StatefulSet ### Nginx StatefulSet 생성
metadata:
  name: web
  namespace: default
spec:
  selector:
    matchLabels:
      app: nginx
  serviceName: "nginx"
  replicas: 3 # by default is 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "cbs"
      resources:
        requests:
          storage: 10Gi
```
- **kind**: StatefulSet 리소스 유형.
- **metadata**: StatefulSet 이름 및 Label과 같은 정보입니다.
- **metadata.annotations**: StatefulSet에 대한 추가 설명입니다. 이 매개변수를 통해 TKE에 대한 추가 개선 사항을 설정할 수 있습니다.
- **spec.template**: StatefulSet에서 관리하는 Pod의 세부 템플릿 구성입니다.
- **spec.volumeClaimTemplates**: PVC&PV 생성을 위한 템플릿입니다.

자세한 내용은 [Kubernetes official documentation](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)을 참고하십시오.

### StatefulSet 생성

1. [sample YAML file](#YAMLSample)을 사용하여 StatefulSet YAML 파일을 준비합니다.
2. kubectl을 설치하고 클러스터에 연결합니다. 자세한 작업은 [클러스터 연결](https://intl.cloud.tencent.com/document/product/457/30639)을 참고하십시오.
3. 다음 명령을 실행하여 StatefulSet YAML 파일을 생성합니다.
```shell
kubectl create -f StatefulSet YAML 파일 이름
```
예를 들어 web.yaml이라는 StatefulSet YAML 파일을 생성하려면 다음 명령을 실행합니다.
```shell
kubectl create -f web.yaml
```
4. 다음 명령을 실행하여 파일이 성공적으로 생성되었는지 확인합니다.
```shell
kubectl get StatefulSet
```
아래와 유사한 메시지는 파일이 생성되었음을 나타냅니다.
```
NAME      DESIRED   CURRENT   AGE
test      1         1         10s
```

### StatefulSet 업데이트

StatefulSet의 업데이트 정책 유형을 보려면 다음 명령을 실행합니다.
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
StatefulSet에는 다음과 같은 업데이트 정책 유형이 있습니다.
– OnDelete: 기본 업그레이드 정책입니다. StatefulSet가 업데이트된 후 새 Pod를 생성하려면 이전 StatefulSet Pod를 수동으로 삭제해야 합니다.
- RollingUpdate: Kubernetes 1.7 이상만 지원됩니다. 이전 StatefulSet Pod는 종료되고 StatefulSet이 업데이트된 후 롤링 업데이트를 통해 새로운 StatefulSet Pod(Kubernetes 1.7 이상)가 생성됩니다.

#### 방법1

다음 명령을 실행하여 StatefulSet을 업데이트합니다.
```
kubectl edit StatefulSet/[name]
```
디버깅 및 확인에 사용합니다. 프로덕션 환경에서는 이것을 사용하지 않는 것이 좋습니다. 이 방법으로 모든 StatefulSet 매개변수를 업데이트할 수 있습니다.

#### 방법2

다음 명령어를 실행하여 특정 컨테이너의 이미지를 업데이트합니다.
```
kubectl patch statefulset <NAME> --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/image", "value":"<newImage>"}]'
```
서비스가 업데이트될 때 컨테이너 이미지만 업데이트하고 다른 매개변수는 변경하지 않는 것이 좋습니다.

StatefulSet이 롤링 업데이트를 사용하여 업데이트된 경우 다음 명령을 실행하여 업데이트 상태를 확인할 수 있습니다.
```
kubectl rollout status sts/<StatefulSet-name>
```

### StatefulSet 삭제

다음 명령을 실행하여 StatefulSet을 삭제합니다.
```
kubectl delete  StatefulSet [NAME] --cascade=false
```
--cascade=false는 Pod가 아닌 StatefulSet만 삭제됨을 나타냅니다. Pod도 삭제해야 하는 경우 다음 명령을 실행합니다.
```
kubectl delete  StatefulSet [NAME]
```
StatefulSet에 대한 자세한 내용은 [Kubernetes official documentation](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/#scaling-a-statefulset)을 참고하십시오.

