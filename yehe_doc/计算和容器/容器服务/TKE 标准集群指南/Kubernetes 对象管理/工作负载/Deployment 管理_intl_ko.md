## 소개

Deployment는 Pod 템플릿과 Pod 실행 정책을 선언합니다. 상태 비저장 응용 프로그램을 배포하는 데 사용됩니다. 필요에 따라 Deployment에서 실행 중인 Pod에 대한 복제본 수, 예약 정책 및 업데이트 정책을 지정할 수 있습니다.

## 콘솔을 통한 Deployment 사용

<span id="creatDeployment"></span>
### Deployment 생성
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. Deployment를 생성할 클러스터의 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.

3. [Create]를 클릭하여 ‘Create a workload’ 페이지로 이동합니다.
필요에 따라 Deployment 매개변수를 설정합니다. 주요 매개변수는 다음과 같습니다.
 - **Workload name**: 워크로드의 이름입니다.
 - **Namespace**: 네임스페이스를 선택합니다.
 - **Type**: [Deployment(deploy Pods in an extensible manner)]를 선택합니다.
 - **In-Pod containers**: Deployment의 Pod에 대해 하나 이상의 컨테이너를 설정합니다.
    - **Name**: 이름을 입력합니다.
    - **Image**: 이미지를 선택합니다.
    - **Image Tag**: 이미지의 태그입니다.
    - **Image pull policy**: 다음 중 하나를 선택합니다.
       이미지 가져오기 정책을 설정하지 않고  Image tag가 `latest`이거나 비어 있으면 Always가 사용됩니다. 그렇지 않으면 IfNotPresent가 사용됩니다.
         - **Always**: 이미지를 항상 원격 위치에서 가져옵니다.
         - **IfNotPresent**: 기본적으로 로컬 이미지를 사용합니다. 이미지를 로컬에서 사용할 수 없으면 원격 위치에서 가져옵니다.
         - **Never**: 로컬 이미지만 사용합니다. 이미지를 로컬에서 사용할 수 없는 경우 예외가 발생합니다.
    - **CPU/memory limits**: [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)에 따라 CPU 및 메모리 제한을 설정하여 비즈니스의 견고성을 향상시킵니다.
    - **Advanced settings**: ‘**working directory**’, ‘** run commands**’, ‘**run parameters**’, ‘**container health check**’ 및 ‘**privilege level**’과 같은 매개변수를 설정할 수 있습니다.
 - **Pod quantity**: 조정 방법을 선택하고 포드 수량을 설정합니다.
4. 아래 이미지와 같이 [Create Workload]를 클릭하여 생성을 완료합니다.
실행 수량이 예상 수량과 같으면 Deployment 아래의 모든 Pod가 생성됩니다.
![](https://main.qcloudimg.com/raw/c458fdbc8d9770d8704327a9dbd16f55.png)

### Deployment 업데이트

#### YAML 파일 업데이트
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. Deployment를 업데이트할 클러스터의 ID를 클릭하면 아래와 같이 클러스터의 관리 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/7e7acba7f2d84a9a0626458efb357ff0.png)
3. YAML을 업데이트할 Deployment 행에서 [More]>[Edit YAML]을 클릭하여 Deployment 업데이트 페이지로 이동합니다.
5. ‘Update Deployment’ 페이지에서 YAML을 편집하고 [Finish]를 클릭하여 아래와 같이 YAML을 업데이트합니다.
![Updating the YAML file](https://main.qcloudimg.com/raw/93c576f09ad8817abb794385f68b38ad.png)

#### Pod 설정 업데이트

1. 클러스터 관리 페이지에서 Pod 설정을 업데이트할 클러스터의 ID를 클릭하여 클러스터의 관리 페이지로 이동합니다.
2. Pod 설정을 업데이트할 DaemonSet 행에서 [Update Pod Configurations]를 클릭합니다.
3. ‘ Update Pod Configurations’ 페이지에서 업데이트 방법을 수정하고 필요에 따라 매개변수를 설정합니다.
4. [Finish]를 클릭하여 Pod 설정을 업데이트합니다.

### Deployment 롤백
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. 클러스터의 관리 페이지로 이동하려면 Deployment 롤백이 필요한 클러스터의 ID를 클릭합니다.
4. 롤백할 Deployment 이름을 클릭하여 Deployment 정보 페이지로 이동합니다.
4. [Modification History] 탭을 선택하고 롤백할 버전 행에서 [Rollback]을 클릭합니다.
6. ‘Roll back a resource’ 페이지에서 [Submit]을 클릭하여 롤백을 완료합니다.

### Pod 수량 조정
1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Clusters](https://console.cloud.tencent.com/tke2/cluster)]를 선택합니다.
2. Pod 수량을 조정할 클러스터의 ID를 클릭하여 클러스터의 관리 페이지로 이동합니다.

3. Pod 수량을 조정할 Deployment 행에서 [Update Pod quantity]를 클릭하여 Pod 수량 업데이트 페이지로 이동합니다.
5. 실제 필요에 따라 Pod 수량을 조정하고 [Update Pod quantity]를 클릭하여 조정을 완료합니다.

## kubectl을 통한 Deployment 사용

### YAML 파일 예시<span id="YAMLSample"></span>
```Yaml
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
  labels:
    app: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```
- **kind**: Deployment 리소스 유형.
- **metadata**: Deployment 이름, Namespace 및 Label과 같은 정보입니다.
- **metadata.annotations**: Deployment에 대한 추가 설명입니다. 이 매개변수를 통해 TKE에 대한 추가 개선 사항을 설정할 수 있습니다.
- **spec.replicas**: Deployment에서 관리하는 Pod의 수.
- **spec.selector**: Deployment에 의해 관리되는 Seletor에 의해 선택된 Pod의 Label.
- **spec.template**: Deployment에서 관리하는 Pod의 세부 템플릿 구성입니다.

매개변수에 대한 자세한 내용은 [Kubernetes official documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)을 참고하십시오.

### Kubectl 사용하여 Deployment 생성

1. Deployment YAML 파일을 준비하려면 [sample YAML file](#YAMLSample)을 참고하십시오.
2. kubectl을 설치하고 클러스터에 연결합니다. 자세한 내용은 [클러스터 연결](https://intl.cloud.tencent.com/document/product/457/30639)을 참고하십시오.
3. 다음 명령을 실행하여 Deployment YAML 파일을 만듭니다.
```shell
kubectl create -f Deployment YAML 파일 이름
```
예를 들어 nginx.yaml이라는 Deployment YAML 파일을 생성하려면 다음 명령을 실행합니다.
```shell
kubectl create -f nginx.yaml
```
4. 다음 명령어를 실행하여 서비스 YAML 파일이 성공적으로 생성되었는지 확인합니다.
```shell
kubectl get deployments
```
아래와 유사한 메시지는 파일이 성공적으로 생성되었음을 나타냅니다.
```
NAME             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
first-workload   1         1         1            0           6h
ng               1         1         1            1           42m
```

### kubectl을 사용하여 Deployment 업데이트

kubectl을 사용하여 다음과 같은 방식으로 Deployment를 업데이트할 수 있습니다. [Method 1](#Method1) 및 [Method 2](#Method2)는 **Recreate** 및 **RollingUpdate** 업데이트 정책을 모두 지원합니다.
- Recreate 모든 Pod는 Deployment를 사용하여 종료되고 다시 생성됩니다.
- RollingUpdate 각 Pod는 하나씩 업데이트됩니다. RollingUpdate는 일시 중지 및 업데이트 간격도 지원합니다.

<span id="Method1"></span>
#### 방법1

다음 명령을 실행하여 Deployment를 업데이트합니다.
```
kubectl edit  deployment/[name]
```
디버깅 및 인증에 사용합니다. 프로덕션 환경에서는 사용하지 않는 것이 좋습니다. 이 방법으로 모든 Deployment 매개변수를 업데이트할 수 있습니다.

<span id="Method2"></span>
#### 방법2

다음 명령어를 실행하여 특정 컨테이너의 이미지를 업데이트합니다.
```
kubectl set image deployment/[name] [containerName]=[image:tag]
```
서비스를 업데이트할 때만 매개변수를 변경하지 않고 컨테이너 이미지를 업데이트하는 것이 좋습니다.

<span id="Method3"></span>
#### 방법3

다음 명령을 실행하여 지정된 리소스에 대한 롤링 업데이트를 수행합니다.
```
kubectl rolling-update [NAME] -f FILE
```


### kubectl 사용하여 Deployment 롤백

1. 다음 명령을 실행하여 Deployment의 업데이트 기록을 봅니다.
```
kubectl rollout history deployment/[name]
```
2. 특정 버전의 세부 정보를 보려면 다음 명령을 실행합니다.
```
kubectl rollout history deployment/[name] --revision=[REVISION]
```
3. 다음 명령을 실행하여 마지막 버전으로 롤백합니다.
```
kubectl rollout undo deployment/[name]
```
롤백할 버전을 지정하려면 다음 명령을 실행합니다.
```
kubectl rollout undo deployment/[name] --to-revision=[REVISION]
```

### kubectl을 사용하여 Pod 수량 업데이트

#### Pod 수량 수동 업데이트

다음 명령을 실행하여 Pod 수량을 수동으로 업데이트합니다.
```
kubectl scale deployment [NAME] --replicas=[NUMBER]
```

#### Pod 수량 자동 업데이트

**Prerequisites**

HPA가 활성화되었습니다. TKE 생성 클러스터에는 기본적으로 HPA가 활성화되어 있습니다.

**Directions**

다음 명령을 실행하여 Deployment에 대한 자동 크기 조정을 설정합니다.
```
kubectl autoscale deployment [NAME] --min=10 --max=15 --cpu-percent=80
```

### kubectl 사용하여 Deployment 삭제

다음 명령어를 실행하여 Deployment를 삭제합니다.
```
kubectl delete deployment [NAME]
```
