
## 간단한 예
본 예제는 명령행을 사용하여 간단한 작업을 제출하는 방법을 소개합니다. 예시는 Python을 이용해 실현한 피보나치 수열 합계로 Python 코드는 태스크의 Application 매개변수의 명령 필드에 의해 지정됩니다. 결과는 작업 구성 stdout 출력 주소에 바로 출력하였습니다.

## 시작 전 준비
시작하기 전에 문서 [시작 전 준비](
/doc/product/599/10807)의 검사 리스트에 따라 잘 준비하십시오. 본 예시는 CLI와 COS를 사용하기 때문에 사용자는 CLI를 설치 및 구성하고 COS Bucket을 생성해야 합니다.

### CLI 설치 및 구성
CLI 구성은 [CLI 구성](/doc/product/440/6184)을 참조하십시오. 설치 후 설치 성공 여부를 검사하십시오.
```
qcloudcli batch help

DescribeAvailableCvmInstanceTypes       	|DescribeTask
DescribeJob                             	|SubmitJob
DescribeJobs                            	|TerminateTaskInstance
```

### 결과 저장용 COS Bucket 생성

이 간단한 예시에서 결과는 시스템 표준 출력에 바로 출력됩니다. Batch는 시스템 표준 출력 stdout와 stderr를 수집할 수 있고 태스크 종료 후 정보를 지정한 COS Bucket에 업로드할 수 있습니다. 정보 저장용 Bucket과 서브 폴더를 미리 준비해야 합니다.

[CLI - 사전 준비](/doc/product/599/10548)에서 3장 **"COS 디렉터리 준비"**를 참조하여 대응하는 COS Bucket과 서브 폴더를 생성하십시오.

## 작업 구성 설명

홈페이지에서 제공하는 예제를 수정하여 계정에 실행할 수 있는 Batch 작업 구성을 구성할 수 있습니다. 그 전에 우선 작업의 각 구성 항목의 함의를 확인하십시오.

```
qcloudcli batch SubmitJob --Version 2017-03-12 --Job '{
    "JobName": "TestJob",       // 작업 이름
    "JobDescription": "for test ",    // 작업 설명
    "Priority": "1",            // 작업 우선 순위
    "Tasks": [                  // 작업 목록(본 예시에 1개 태스크만 포함)
        {
            "TaskName": "Task1",   // 태스크 1 이름
            "Application": {        // 태스크 실행 명령
                "DeliveryForm": "LOCAL",    // 로컬 명령 실행
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // 명령의 구체적인 내용(피보나치 수열 총합)
            },
            "ComputeEnv": {         // 컴퓨팅 환경 구성
                "EnvType": "MANAGED",   // 컴퓨팅 환경 유형, 관리 및 비관리
                "EnvData": {        // 구체적인 구성(현재 관리됨임. CVM 인스턴스 생성 설명 참조)
                    "InstanceType": "S1.SMALL1",    // CVM 인스턴스 유형
                    "ImageId": "img-m4q71qnf",      // CVM 이미지 ID(교체가 필요함)
                }
            },
            "RedirectInfo": {       // 표준 출력 리디렉션 구성           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",    // 표준 출력(교체 필요)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // 표준 오류(교체 필요)
            }
        }
    ]
}'
--Placement'{
    "Zone": "ap-guangzhou-2"    // 가용 영역(교체 필요할 수 있음)
}'
```

Batch의 SubmitJob 명령은 3개의 매개변수를 포함합니다.
* **Version**: 버전 번호로 현재 2017-03-12를 고정 입력합니다.
* **Job**: 작업 구성, JSON 형식, 상세 필드 의미는 예제를 참조하십시오.
* **Placement**: 작업 실행 가용 영역

``* 1. 작업은 Job의 교체가 필요한 필드는 사용자의 정보로 교체해야 실행할 수 있습니다(예를 들어, 사용자 지정 이미지 ID, VPC 관련 정보, COS Bucket 주소와 대응 SecretId, SecretKey) ``

``* 2. 위의 예는 주석이 추가되어 있기 때문에 CLI에서 직접 실행할 수 없습니다. 아래의 예를 복사한 뒤 "입력 예정" 필드를 입력한 뒤 다시 실행하십시오. 명령이 길면 백 엔드 복사 버튼을 사용하여 불완전 복제를 방지하십시오. ``

``* 3. Job 구성에 대한 상세한 설명은 `` [작업 구성 설명](https://cloud.tencent.com/document/product/599/11040)``을 참조하십시오. ``

```
qcloudcli batch SubmitJob --Version 2017-03-12  --Job '{"JobName": "TestJob",  "JobDescription": "for test", "Priority": "1", "Tasks": [{"TaskName": "Task1",  "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command":  "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "},  "ComputeEnv": {"EnvType":  "MANAGED", "EnvData": {"InstanceType": "S1.SMALL1",  "ImageId": "교체 예정" }  }, "RedirectInfo": {"StdoutRedirectPath": "교체 예정", "StderrRedirectPath":   "교체 예정"}, "MaxRetryCount":  1 } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

### 구성 수정

#### 1. ImageId 입력
```"ImageId": "교체 예정"```

내부 테스트는 Cloud-init 서비스에 기반하여 구성한 이미지를 사용하여야 합니다. 공식적으로 제공한 CentOS 6.5는 이미지를 직접 사용할 수 있으며, 이미지 ID는 img-m4q71qnf입니다. Windows Server 2012의 공식 이미지 ID는 img-er9shcln입니다.

#### 2. StdoutRedirectPath와 StderrRedirectPath 구성
```"StdoutRedirectPath": "교체 예정", "StderrRedirectPath":   "교체 예정"```

사전 준비에 생성한 COS Bucket 접근 주소를 StdoutRedirectPath와 StderrRedirectPath에 입력합니다.

#### 3. (옵션)가용 영역 수정
```
--Placement '{"Zone": "ap-guangzhou-2"}'
```

본 예제는 광저우 2지역에 대해 리소스 신청을 지정합니다. CLI에서 구성한 기본 지역에 따라 상응하는 가용 영역을 선택하여 리소스를 신청할 수 있습니다. 지역과 가용 영역의 상세 정보는 [지역과 가용 영역>>](/doc/product/213/6091)을 참조하십시오.

#### 4. Windows CLI에서 JSON 형식 데이터 입력(옵션)
Windows CLI에서 입력한 JSON 형식 데이터는 Linux와 구별됩니다. 예를 들어, " 는 \"로 교체해야 합니다. 더 자세한 설명은 [Tencent Cloud CLI 시작 가이드](/doc/product/440/6185)의 "JSON 형식 데이터를 입력 매개변수로" 장을 참조하십시오.

## 결과 보기

```
{
    "Response": {
        "RequestId": "5d928636-bba2-4ab3-bef3-cf17d7c73c51",
        "JobId": "job-1rqdgnqn"
    }
}
```
JobId가 반환되면 실행 성공을 의미합니다.

```
$ qcloudcli batch DescribeJob  --Version 2017-03-12 --JobId job-1z4yl2bp
{
    "Response": {
        "JobState": "STARTING",
        "Zone": "ap-guangzhou-2",
        "JobName": "test job",
        "Priority": 1,
        "RequestId": "b116f9b5-410c-4a69-bbe8-b695a2d6a869",
        "TaskSet": [
            {
                "TaskName": "hello2",
                "TaskState": "STARTING"
            }
        ],
        "JobId": "job-1z4yl2bp",
        "DependenceSet": []
    }
}
```
DescribeJob을 통해 방금 제출한 태스크 정보를 확인할 수 있습니다.

```
$ qcloudcli batch DescribeJobs  --Version 2017-03-12
```
DescribeJobs을 통해 현재 지역 작업 목록도 확인할 수 있습니다.

## 다음 단계에서는 무엇을 할 수 있을까요?

이것은 가장 간단한 예이며, 단일 태스크의 작업입니다. 원격 저장 매핑 능력을 사용하지 않고 사용자에게 가장 기본적인 기능을 보여주기 위해서입니다. API 설명 문서에 따라 계속해서 Batch의 한 차원 높은 기능을 테스트할 수 있습니다.

* **더 간단한 작업 방법**: Batch는 기능이 뛰어나고 구성 항목이 많은 편이기 때문에 스크립트를 통해 호출하면 더 간단하고 빠르게 작업할 수 있습니다. [사전 준비](/doc/product/599/10548)와 [1_빠른 시작](/doc/product/599/10551)에서 이러한 방식을 체험해 보십시오.

* **원격 코드 패키지 실행**: Batch는 **사용자 지정 이미지 + 원격 코드 패키지 + 명령행**의 방식을 제공하여 기술 측면에서 사용자의 수요를 전방위적으로 커버할 수 있습니다. 상세 정보는 [2_원격 코드 패키지 실행](/doc/product/599/10552)을 조회하십시오.

* **원격 저장 매핑**: Batch는 저장소 접근을 최적화하여 원격 저장 서비스 접근을 로컬 파일 시스템 작업으로 간소화합니다. 상세 정보는 [3_원격 저장 매핑](/doc/product/599/10983)을 조회하십시오.

