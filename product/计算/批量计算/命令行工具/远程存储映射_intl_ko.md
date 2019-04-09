원격 매핑은 Batch가 저장에 사용하는 관련 보조 기능으로 COS, CFS 등 원격 저장을 로컬 폴더에 매핑할 수 있습니다.

## 1. 사전 준비
[사전 준비]() 설명에 따라 준비하고 사용자 지정 메시지의 공용 부분 구성 방법을 파악하십시오.

## 2. 입력 데이터 파일 업로드
number.txt 내용은 다음과 같습니다.
```
1
2
3
4
5
6
7
8
9
```

파일을 사전 준비에 생성한 input 폴더에 업로드합니다.

![](https://main.qcloudimg.com/raw/66a259fd93c8454d1888604c5af8e456.png)

## 3. Demo 보기 및 수정
편집기를 사용하여 3_StoreMapping.py 파일을 엽니다.
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/countnum.py",
    "PackagePath": "http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
InputMapping = {
    "SourcePath": "your input remote path",
    "DestinationPath": "/data/input/"
}
OutputMapping = {
    "SourcePath": "/data/output/",
    "DestinationPath": "your output remote path"
}
```
2_RemoteCodePkg.py와 비교하면 사용자 지정 부분 중 수정한 부분은 다음과 같습니다.
* Application의 Command를 countnum.py 실행으로 변경 
* InputMapping: 입력 매핑. SourcePath 원격 저장 주소(사전 준비 input 폴더의 주소로 수정), DestinationPath 로컬 디렉터리(수정하지 않음)
* OutputMapping 출력 매핑. SourcePath 로컬 디렉터리(수정하지 않음), DestinationPath 원격 저장 주소(사전 준비 output 폴더의 주소로 수정)

countnum.py 내용은 다음과 같습니다.
```
import os

inputfile = "/data/input/number.txt"
outputfile = "/data/output/result.txt"

def readFile(filename):
    total = 0
    fopen = open(filename, 'r')
    for eachLine in fopen:
        total += int(eachLine)
    fopen.close()
    print "total = ",total
    fwrite = open(outputfile, 'w')
    fwrite.write(str(total))
    fwrite.close()

print("Local input file is ",inputfile)
readFile(inputfile)
```
파일 input/number.txt를 열고 각 행의 숫자를 더한 뒤 결과를 output/Result.txt에 입력합니다.

## 4. 작업 제출
Demo에는 이미 Python 스크립트 + Batch 내부 테스트판 CLI 형식으로 작업 제출 프로세스를 캡슐화하였기 때문에 아래의 예제에 따라 Python 스크립트를 실행하면 됩니다.
```
$ python 3_StoreMapping.py
{
    "Response": {
        "RequestId": "d069ce2f-abfc-451f-81fd-9327dbf5cf39",
        "JobId": "job-clump52n"
    }
}
```

JobId 필드가 반환되면 제출에 성공하며, JobId 필드가 반환되지 않았을 경우 반환값 오류를 검사하거나 [사용자 피드백]()을 통해 관리자에게 문의할 수 있습니다.

## 5. 상태 보기
[빠른 시작]() 중 같은 이름의 장을 참조하십시오.

## 6. 결과 보기
Batch는 출력 데이터를 로컬 디렉터리에서 원격 저장 디렉터리로 복사합니다. 3_StoreMapping.py 실행 결과는 result.txt에 저장되고 이 파일은 COS에 자동 동기화됩니다.
![pic](https://main.qcloudimg.com/raw/4cb37736a9da3ca6c66295f8bcf48ae3.png)
```
45
```
