## 소개

Job은 1-N개 Pod를 생성하고 지정된 수의 Pod가 성공적으로 종료될 때까지 지정된 규칙에 따라 실행되도록 합니다. Job은 배치 컴퓨팅 및 데이터 분석과 같은 다양한 시나리오에서 사용할 수 있습니다. 반복 실행 횟수, 병렬 처리 수준 및 필요에 따라 다시 시작 정책을 지정할 수 있습니다.
Job은 기존 Pod를 유지하고 완료된 후 새 Pod를 생성하지 않습니다. ‘Log’에서 완료된 Pod의 로그를 볼 수 있습니다. Job을 삭제하면 생성된 Pod와 해당 Pod의 로그가 정리됩니다.

## 콘솔에서 Job 관리

### Job 생성

1. [TKE Console](https://console.cloud.tencent.com/tke2)에 로그인합니다.
2. 왼쪽 사이드바에서 [Cluster]를 클릭하여 클러스터 관리 페이지로 이동합니다.
3. Job을 생성할 클러스터의 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.
4. ‘Workload’ > ‘Job’을 선택하여 아래와 같이 Job 정보 페이지로 이동합니다.
![Job](https://main.qcloudimg.com/raw/b33fcb5fe7f6491ef71b53f21ed82051.png)
5. [Create]를 클릭하여 아래와 같이 ‘Create Workload’ 페이지로 이동합니다.
![Create a workload](https://main.qcloudimg.com/raw/e3e76bf1eeae83380d0f4b3f4e940934.png)
6. 실제 필요에 따라 Job 매개변수를 설정합니다. 주요 매개변수는 다음과 같습니다.
 - 워크로드 이름: 워크로드 이름을 사용자 정의합니다.
 - 네임스페이스: 실제 필요에 따라 네임스페이스를 선택합니다.
 - 유형: ‘Job (One-time Task)’을 선택합니다.
 - Job 설정: 필요에 따라 Job의 Pod에 대해 하나 이상의 컨테이너를 설정합니다.
    - 반복 시간: 이 Job에서 Pod의 반복 실행 시간을 설정합니다.
    - 동시 포드: 이 Job의 병렬 Pod 수를 설정합니다.
    - 재시작 정책: Pod 아래의 컨테이너가 비정상적으로 종료될 때 적용되는 재시작 정책을 설정합니다.
       - Never: Pod 아래의 모든 컨테이너가 종료될 때까지 컨테이너를 재시작하지 않습니다.
       - OnFailure: 컨테이너가 다시 시작되는 동안 Pod가 계속 실행됩니다.
 - Pod의 컨테이너: 필요에 따라 Job의 Pod에 대해 하나 이상의 컨테이너를 설정합니다.
    - 이름: Pod에 있는 컨테이너의 이름을 사용자 정의합니다.
    - 이미지: 실제 필요에 따라 이미지를 선택합니다.
    - 이미지 태그: 실제 필요에 따라 태그를 입력합니다.
    - CPU/메모리 제한: [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)에 따라 CPU 및 메모리 제한을 설정하여 비즈니스의 견고성을 향상시킵니다.
    - 고급 설정: ‘**Working Directory**’, ‘**Running Command**’, ‘**Running Parameter**’, ‘**Container Health Check**’ 및 ‘**Privileged Container**’와 같은 매개 변수를 설정할 수 있습니다.
7. [Create Workload]를 클릭하여 생성을 완료합니다.

### Job 상태 보기

1. [TKE Console](https://console.cloud.tencent.com/tke2)에 로그인합니다.
2. 왼쪽 사이드바에서 [Cluster]를 클릭하여 클러스터 관리 페이지로 이동합니다.
3. Job 상태를 확인할 클러스터의 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.
4. ‘Workload’ > ‘Job’을 선택하여 아래와 같이 Job 정보 페이지로 이동합니다.
![Job](https://main.qcloudimg.com/raw/522504f451b3234997b7c413724bdb04.png)
5. Job의 세부 정보를 보려면 해당 이름을 클릭합니다.

### Job 삭제

Job은 기존 Pod를 유지하고 완료된 후 새 Pod를 생성하지 않습니다. ‘Log’에서 완료된 Pod의 로그를 볼 수 있습니다. Job을 삭제하면 생성된 Pod와 해당 Pod의 로그가 정리됩니다.

## Kubectl을 통한 Job 관리

[](id:YAMLSample)
### YAML 예시

```Yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  completions: 2
  parallelism: 2
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
```
- kind: Job 리소스 유형을 식별합니다.
- metadata: Job 이름 및 Label과 같은 기본 정보입니다.
- metadata.annotations: Job에 대한 추가 설명입니다. 이 매개변수를 통해 TKE에 대한 추가 개선 사항을 설정할 수 있습니다.
- spec.completions: 이 Job에서 Pod가 반복적으로 실행된 시간입니다.
- spec.parallelism: 이 Job의 병렬 Pod 수입니다.
- spec.template: Job의 Pod에 대한 자세한 템플릿 구성입니다.

### Job 생성

1. [YAML sample](#YAMLSample)을 참고하여 Job YAML 파일을 준비합니다.
2. kubectl을 설치하고 클러스터에 연결합니다. 자세한 작업은 [클러스터 연결](https://intl.cloud.tencent.com/document/product/457/30639)을 참고하십시오.
3. Job YAML 파일을 생성합니다.
```
kubectl create -f Job YAML 파일 이름
```
예를 들어, pi.yaml이라는 Job YAML 파일을 생성하려면 다음 명령을 실행합니다.
```shell
kubectl create -f pi.yaml
```
4. 다음 명령어를 실행하여 Job이 성공적으로 생성되었는지 확인합니다.
```shell
kubectl get job
```
다음과 유사한 메시지가 반환되면 생성이 성공한 것입니다.
```
NAME      DESIRED   SUCCESSFUL   AGE
job       1         0            1m
```

### Job 삭제
다음 명령을 실행하여 Job을 삭제합니다.
```
kubectl delete job [NAME]
```



