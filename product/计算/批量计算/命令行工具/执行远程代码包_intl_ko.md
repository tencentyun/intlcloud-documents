Batch는 HTTP의 방식으로 .tgz 형식의 파일에서 코드 패킷을 획득하는 것을 지원합니다. 사용자는 코드를 압축한 뒤 COS에 업로드할 수 있으며, LOCAL 모드보다 더욱 손쉽게 코드를 관리할 수 있습니다.

## 1. 사전 준비
[사전 준비](https://cloud.tencent.com/document/product/599/10548)의 설명에 따라 준비를 완료하고 사용자 지정 메시지의 공용 부분 구성 방법을 파악하십시오.

## 2. Demo 보기 및 수정
편집기를 사용하여 2_RemoteCodePkg.py 파일을 엽니다.
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/fib.py",
    "PackagePath": "http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
사용자 지정 부분(custom)은 Application을 제외한 나머지 부분 모두 사전 준비에서 이미 설명하였으며 다음은 Application 함의를 설명합니다.
* DeliveryForm: 애플리케이션 딜리버리 방식으로 소프트웨어 패키징, 용기 이미지, CVM 내부 직접 실행을 이 세 가지를 포함하며 여기에서 PACKAGE는 소프트웨어 패키징 방식을 의미합니다.
* PackagePath: 소프트웨어 패킷의 주소로 HTTP 방식으로 제공되며 반드시 .tgz 형식이어야 합니다. Batch는 이 소프트웨어 패킷을 스케줄링된 CVM의 어느 디렉터리에 다운로드한 뒤 해당 디렉터리에서 Command를 실행합니다.
* Command: 태스크 시작 명령입니다. 여기에서 소프트웨어 패킷의 Python 스크립트 파일을 직접 호출합니다. 소프트웨어 패킷을 다운로드하고 안의 파일 구조와 내용을 확인할 수 있습니다.

fib.py의 내용은 다음과 같습니다.
```
fib = lambda n:1 if n<=2 else fib(n-1)+fib(n-2)
print("Remote Code Package : %d"%(fib(20)))
```

2_RemoteCodePkg.py는 비교적 간단합니다. 사전 준비에 따라 공용 부분만 수정하면 직접 실행할 수 있고 별도 수정이 필요하지 않습니다.

## 3. 작업 제출
Demo에는 이미 Python 스크립트 + Batch 내부 테스트판 CLI 형식으로 작업 제출 프로세스를 캡슐화하였기 때문에 아래의 예제에 따라 Python 스크립트를 실행하면 됩니다.
```
$ python 2_RemoteCodePkg.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

JobId 필드가 반환되면 제출에 성공하며, JobId 필드가 반환되지 않았을 경우 반환값 오류를 검사하거나 [사용자 피드백](https://cloud.tencent.com/document/product/599/10806)의 채팅 그룹에 가입하여 관리자에게 문의할 수 있습니다.

## 4. 상태 보기
[빠른 시작](https://cloud.tencent.com/document/product/599/10551)과 같은 이름의 장을 참조하십시오.

## 5. 결과 보기
[빠른 시작](https://cloud.tencent.com/document/product/599/10551)과 같은 이름의 장을 참조하십시오.

2_RemoteCodePkg.py의 실행 결과는 다음과 같습니다.
```
Remote Code Package : 6765
```

