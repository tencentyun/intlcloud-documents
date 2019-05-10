CLI를 설치하기 전, 시스템에 Python 환경이 설치되어 있는지 확인하십시오. 즉, Python2.7과 python-pip을 설치해야 합니다.

## 1. Tencent Cloud CLI 설치
### I. **내부 테스트판 신청을 통과**했는지 확인하십시오.
그렇지 않을 경우, CLI의 Batch 관련 명령을 사용할 때 접근 권한이 없다는 알림이 나타납니다.

### II. CLI 설치:
* CLI 미설치: pip를 이용하면 Tencent Cloud CLI를 빠르게 설치할 수 있습니다.
```
$ sudo pip install qcloudcli
```

* CLI 설치 완료: pip를 이용하면 빠르게 업그레이드할 수 있습니다. 명령은 다음과 같습니다.
```
$ sudo pip install --upgrade qcloudcli
```

### III. CLI를 성공적으로 설치하고 Batch 관련 능력이 포함되는지 확인합니다.
```
$ qcloudcli batch help
You should use the qcloudcli as follow format:
qcloudcli <module> <action> [options and parameters]
The action name you input is error! The module [batch] support the valid action as follows:

DescribeAvailableCvmInstanceTypes       	|DescribeTask
DescribeJob                             	|SubmitJob
DescribeJobs                            	|TerminateTaskInstance
```

## 2. SecretID와 SecretKey 획득
### I. Tencent Cloud [API 키 콘솔](https://console.cloud.tencent.com/capi)에 로그인합니다.

### II. 키를 생성하거나 기존 클라우드 API 키를 사용합니다. 클라우드 API 키 ID를 클릭하여 세부 정보 페이지에 진입해 SecretID 및 SecretKey를 획득합니다.
![Alt text](https://main.qcloudimg.com/raw/a9b9eec169c95925417b8393d00a15ee.png)

## 3. COS 디렉터리 준비
### I. Bucket과 서브 폴더 생성
![2](https://main.qcloudimg.com/raw/bed6776e552501ddaf7327b6303e2fae.png)
Bucket 1개를 생성하고 이름을 임의로 지정합니다. 후속 사용을 위해 Bucket에 3개 폴더를 생성합니다. 폴더 이름은 위 그림과 같이 지정합니다.

### II. COS 접근 주소 저장
![3](https://main.qcloudimg.com/raw/5672b6494624a073ade3c706a2f65597.png)

우선 위 그림의 지시에 따라 COS Bucket의 접근 도메인 이름을 확인한 뒤 도메인 이름 + 폴더 이름으로 3개 폴더의 접근 도메인 이름을 만듭니다. 공식 계정에서 생성한 3개 폴더의 접근 주소는 다음과 같습니다.

* cos://batchdemo-1251783334.cosgz.myqcloud.com/logs/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/input/
* cos://batchdemo-1251783334.cosgz.myqcloud.com/output/

``` 자신의 Bucket의 도메인 이름에 따라 폴더 접근 주소를 만듭니다. ```

## 4. Batch Demo 파일 다운로드

[다운로드 주소](http://batchdemo-1251783334.cosgz.myqcloud.com/demo/BatchDemo.zip). 압축 해제 후 파일 디렉터리 구조는 다음과 같습니다. 그리고 다음 순서에 따라 Batch 사용과 기능을 체험하십시오.

* [1_SimpleStart](https://cloud.tencent.com/document/product/599/10551)
* [2_RemoteCodePkg](https://cloud.tencent.com/document/product/599/10552)
* [3_StoreMapping](https://cloud.tencent.com/document/product/599/10983)

``` Demo는 Python + Batch CLI의 형식으로 제공되며, Batch 기능과 구성 가능한 항목이 다양하고 Python 스크립트를 통해 더 손쉽게 작업할 수 있습니다. ```

## 5. Demo 사용자 지정 메시지 공용 부분 설명
"1_SimpleStart"의 사용자 지정 메시지 부분을 예로 듭니다.

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

* imageId: 내부 테스트 기간에는 Cloud-init 서비스를 포함한 이미지를 사용해야 합니다. Cloud Market에서 공식적으로 CentOS 7.2 버전의 직접 사용 가능한 이미지를 제공합니다. 이미지 ID는 **img-31tjrtph**입니다. 사용자 지정 이미지는 이 이미지를 기반으로 제작해야 합니다.
* StdoutRedirectPath、StderrRedirectPath: 3단계에서 준비한 COS 디렉터리의 logs 폴더의 완전한 접근 주소를 입력하십시오. 예제 중에는 cos://batchdemo-1251783334.cosgz.myqcloud.com/logs/입니다. 이를 자신의 접근 주소로 교체하십시오.
* Application: 명령행을 시작합니다. 수정할 필요가 없습니다.
