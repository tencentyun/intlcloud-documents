## 소개

CronJob 객체는 crontab(cron table) 파일의 라인과 유사합니다. 지정된 일정에 따라 주기적으로 Job을 실행합니다. 형식에 대한 자세한 내용은 Cron 설명서를 참고하십시오.
Cron 형식은 다음과 같습니다.
```
# 파일 형식 설명
#  --분(0 - 59)
# |  --시간(0 - 23)
# | |  --일(1 - 31)
# | | |  --월(1 - 12)
# | | | |  --주(0 - 6)
# | | | | |
# * * * * *
```

## CronJob Console 작업 가이드

### CronJob 생성

1. [TKE Console](https://console.cloud.tencent.com/tke2)에 로그인합니다.
2. 왼쪽 사이드바에서 [Clusters]를 클릭하여 클러스터 관리 페이지로 이동합니다.
3. CronJob을 생성해야 하는 클러스터의 ID를 클릭하여 클러스터 관리 페이지로 들어갑니다.
4. ‘Workload’ > ‘CronJob’을 선택하여 CronJob 정보 페이지로 이동합니다. 아래 이미지를 참고하십시오.
![CronJob](https://main.qcloudimg.com/raw/881d1fd3e52cfc6fa421f22820c09419.png)
5. [Create]을 클릭하여 ‘Create a workload’ 페이지로 이동합니다. 아래 이미지를 참고하십시오.
![Create a workload](https://main.qcloudimg.com/raw/cc40dbd25618e72c92e47b0397443e7d.png)
6. 실제 필요에 따라 CronJob 매개변수를 설정합니다. 주요 매개변수는 다음과 같습니다.
 - 워크로드 이름: 사용자 정의.
 - 네임스페이스: 실제 필요에 따라 선택합니다.
 - 유형: ‘CronJob(Cron 일정에 따라 실행)’을 선택합니다.
 - 실행 정책: Cron 형식을 기반으로 작업의 주기적 실행 정책을 설정합니다.
 - Job 설정
    - 반복 횟수: Job 관리형 Pod를 반복해야 하는 횟수입니다.
    - 병렬 처리: Job이 병렬로 실행되는 Pod의 수입니다.
    - 재시작 정책: Pod의 컨테이너가 예외적으로 종료된 후의 재시작 정책입니다.
        - Never: Pod의 모든 컨테이너가 종료될 때까지 컨테이너를 재시작하지 마십시오.
        - OnFailure: Pod가 계속 실행되고 컨테이너가 다시 시작됩니다.
 - In-Pod 컨테이너: 실제 필요에 따라 CronJob의 Pod에 대해 하나 이상의 다른 컨테이너를 설정합니다.
    - 이름: 사용자 정의.
    - 이미지: 실제 필요에 따라 선택하십시오.
    - 이미지 버전: 실제 필요에 따라 입력합니다.
    - CPU/메모리 제한: [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)에 따라 CPU 및 메모리 제한을 설정하여 비즈니스의 견고성을 향상시킵니다.
    - 고급 설정: ‘**working directory**’, ‘**run commands**’, ‘**run parameters**’, ‘**container health check**’ 및 ‘**privilege level**’과 같은 매개변수를 설정할 수 있습니다.
7. [Create a workload]을 클릭하면 생성이 완료됩니다.

### CronJob 상태 보기

1. [TKE console](https://console.cloud.tencent.com/tke2)에 로그인합니다.
2. 왼쪽 사이드바에서 [Clusters]를 클릭하여 클러스터 관리 페이지로 이동합니다.
3. CronJob 상태를 확인할 클러스터의 ID를 클릭하여 클러스터 관리 페이지로 이동합니다.
4. ‘Workload’ > ‘CronJob’을 선택하여 CronJob 정보 페이지로 이동합니다. 아래 이미지를 참고하십시오.
![CronJob](https://main.qcloudimg.com/raw/adee4e9199660c39f61fc091273d3999.png)
5. 세부 정보를 보려면 상태를 볼 CronJob의 이름을 클릭합니다.

## kubectl을 사용하여 CronJob 조작

<span id="YAMLSample"></span>
### YAML 예시

```Yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox
            args:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```
- kind: CronJob 리소스 유형을 식별합니다.
- metadata: CronJob 이름 및 Label과 같은 기본 정보입니다.
- metadata.annotations: CronJob에 대한 추가 설명입니다. 이 매개변수를 통해 TKE에 대한 추가 개선 사항을 설정할 수 있습니다.
- spec.schedule: CronJob이 실행하는 Cron 정책.
- spec.jobTemplate: Cron이 실행하는 Job 템플릿입니다.

### CronJob 생성

#### 방법1

1. CronJob YAML 파일을 준비하려면 [YAML sample](#YAMLSample)를 참고하십시오.
2. kubectl을 설치하고 클러스터에 연결합니다. 자세한 내용은 [Install kubectl and connect to a cluster](https://cloud.tencent.com/document/product/457/8438)를 참고하십시오.
3. 다음 명령어를 실행하여 CronJob YAML 파일을 생성합니다.
```shell
kubectl create -f CronJob YAML 파일 이름
```
예를 들어 cronjob.yaml이라는 CronJob YAML 파일을 생성하려면 다음 명령을 실행합니다.
```shell
kubectl create -f cronjob.yaml
```

#### 방법2

1. `kubectl run` 명령을 실행하여 CronJob을 빠르게 생성합니다.
예를 들어 전체 설정 정보를 작성할 필요가 없는 CronJob을 빠르게 생성하려면 다음 명령을 실행합니다.
```shell
kubectl run hello --schedule="*/1 * * * *" --restart=OnFailure --image=busybox -- /bin/sh -c "date; echo Hello"
```
2. 다음 명령을 실행하여 CronJob을 성공적으로 생성했는지 확인합니다.
```shell+-
kubectl get cronjob [NAME]
```
아래와 유사한 메시지는 항목을 성공적으로 생성했음을 나타냅니다.
```
NAME      SCHEDULE    SUSPEND   ACTIVE    LAST SCHEDULE   AGE
cronjob   * * * * *   False     0         <none>          15s
```

### CronJob 삭제
>!
> - 이 삭제 명령을 실행하기 전에 생성 중인 Job이 있는지 확인하십시오. 그렇다면 이 명령을 실행하면 해당 Job이 종료됩니다.
> - 이 삭제 명령을 실행하면 생성된 Job과 완료된 Job은 종료되거나 삭제되지 않습니다.
> -  CronJob에 의해 생성된 Job을 삭제하려면 수동으로 삭제하십시오.

다음 명령어를 실행하여 CronJob을 삭제합니다.
```
kubectl delete cronjob [NAME]
```


