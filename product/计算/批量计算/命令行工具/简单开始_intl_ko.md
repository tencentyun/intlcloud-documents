## 1. 사전 준비
[사전 준비]() 설명에 따라 준비하고 사용자 지정 메시지의 공용 부분 구성 방법을 파악하십시오.

## 2. Demo 보기 및 수정
편집기를 사용하여 1_SimpleStart.py 파일을 엽니다.
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
사용자 지정 부분(custom)은 Application을 제외한 나머지 부분 모두 사전 준비에서 이미 설명하였으며 다음은 Application 함의를 설명합니다.
* DeliveryForm: 애플리케이션 딜리버리 방식으로 소프트웨어 패키징, 용기 이미지, CVM 내부 직접 실행 이 세 가지를 포함하며 여기에서 LOCAL은 CVM 내부 직접 실행을 의미합니다.
* Command: 태스크 시작 명령으로 여기에서 실행한 것은 Python 스크립트입니다. 1부터 시작하며 피보나치 수열의 앞부분 20개 숫자를 합하여 StdOutput에 결과를 출력합니다.

1_SimpleStart.py는 비교적 간단합니다. 사전 준비에 따라 공용 부분만 수정하면 직접 실행할 수 있고 별도 수정이 필요하지 않습니다.

## 3. 작업 제출
Demo에는 이미 Python 스크립트 + Batch CLI의 형식으로 작업 제출 프로세스를 캡슐화하였기 때문에 아래의 예제에 따라 Python 스크립트를 실행하면 됩니다.
```
$ python 1_SimpleStart.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

JobId 필드가 반환되면 제출에 성공하며, JobId 필드가 반환되지 않았을 경우 반환값 오류를 검사하거나 [사용자 피드백]()을 통해 관리자에게 문의할 수 있습니다.

## 4. 상태 보기

```
$ qcloudcli batch DescribeJob  --Version 2017-03-12 --JobId job-xxx
```
DescribeJob을 통해 실행 상태를 확인합니다. --JobId를 실제 JobId로 교체하십시오. 일반 상태는 다음과 같습니다.
* STARTING  시작 중
* RUNNING   실행 중
* SUCCEED   실행 성공
* FAILED    실행 실패

완전 반환 정보는 다음과 같습니다.

```
{
    "Response": {
        "JobState": "STARTING",
        "Zone": "ap-guangzhou-2",
        "JobName": "SimpleStart",
        "Priority": 1,
        "RequestId": "8e5ef77c-fa41-4b9f-8c80-107f2546e8ed",
        "TaskSet": [
            {
                "TaskName": "Task1",
                "TaskState": "STARTING"
            }
        ],
        "JobId": "job-n4ohivif",
        "DependenceSet": []
    }
}
```

## 5. 결과 보기

결과는 사전 준비에 구성한 StdoutRedirectPath와 StderrRedirectPath 디렉터리에 저장됩니다. 결과는 다음과 같습니다.

![](https://main.qcloudimg.com/raw/0a7b87d0286c93a6025beeb566718e05.png)

성공 시 표준 출력 stdout.job-xxx.xxxx.0.log를 조회하십시오. 내용은 다음과 같습니다.
```
6765
```

실패 시 표준 오류 stderr.job-xxx.xxxx.0.log를 조회하십시오. 가능한 내용은 다음과 같습니다.
```
/bin/sh: -c: line 0: syntax error near unexpected token `('
/bin/sh: -c: line 0: ` python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" '
```




