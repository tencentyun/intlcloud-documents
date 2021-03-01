## 기능 설명
COS Migration은 COS 데이터 마이그레이션 기능이 통합된 통합형 툴입니다. 사용자는 간단한 설정 작업을 통해 원본 주소 데이터를 COS에 신속하게 마이그레이션합니다. 특징은 다음과 같습니다.
- 풍부한 데이터 소스:
   - 로컬 데이터: 로컬에 저장된 데이터를 COS에 마이그레이션합니다.
   - 기타 클라우드 스토리지: 현재 AWS S3, Alibaba Cloud OSS, Qiniu 스토리지에 대한 COS 마이그레이션을 지원하며 향후 지속적으로 확장해 나갈 계획입니다.
   - URL 리스트: 특정 URL 다운로드 리스트에 따라 COS로 다운로드 및 마이그레이션합니다.
   - Bucket 상호 복사: COS의 Bucket 데이터를 상호 복사하고 계정 간, 리전 간 데이터 복사를 지원합니다.
- 중단된 시점부터 이어 올리기: 툴에서는 업로드 시 중단된 시점부터 이어 올리기를 지원합니다. 큰 용량의 파일의 경우 중도에 종료되었거나 서비스 장애가 발생하였다면 다시 툴을 실행하여 업로드가 완료되지 않은 파일을 계속해서 업로드할 수 있습니다.
- 멀티파트 업로드: 객체를 멀티파트 방식에 따라 COS에 업로드합니다.
- 동시 업로드: 여러 객체의 동시 업로드를 지원합니다.
- 마이그레이션 인증: 객체 마이그레이션 후 인증을 진행합니다.

>
>- COS Migration의 인코딩 형식은 UTF-8 형식만 지원합니다.
>- 해당 툴을 이용하여 동일한 이름의 파일을 업로드하면 더 오래된 동일한 이름의 파일을 덮어쓰며, 동일한 이름의 파일이 있는지 여부를 비교하는 기능은 지원하지 않습니다.

## 사용 환경
#### 시스템 환경
Windows, Linux, macOS 시스템

#### 소프트웨어 종속
- JDK 1.8 X64 이상이어야 하며, JDK 설치 및 설정에 대한 자세한 내용은 [Java 설치 및 설정](https://intl.cloud.tencent.com/document/product/436/10865)을 참조하십시오.

## 사용 방법
### 1. 툴 획득
[COS Migration 툴](https://github.com/tencentyun/cos_migrate_tool_v5)에서 다운로드합니다.

### 2. 툴 패키지 압축 해제
#### Windows
 특정 디렉터리에 압축 해제 및 저장합니다. 예시:
<pre>
C:\Users\Administrator\Downloads\cos_migrate
</pre>

#### Linux
특정 디렉터리에 압축 해제 및 저장합니다.
<pre>
unzip cos_migrate_tool_v5-master.zip && cd cos_migrate_tool_v5-master
</pre>

#### 마이그레이션 툴 구조
정확하게 압축 해제한 COS Migration 툴 디렉터리 구조는 다음과 같습니다.
<pre>
COS_Migrate_tool
|——conf  #구성 파일이 존재하는 디렉터리
|   |——config.ini  #구성 파일 마이그레이션
|——db    #마이그레이션 성공 기록 저장
|——dep   #프로그램 메인 로직 컴파일로 생성한 JAR 패키지
|——log   #툴 실행 중 생성된 로그
|——opbin #컴파일에 사용되는 스크립트
|——src   #툴 소스 코드
|——tmp   #임시 파일 저장 디렉터리
|——pom.xml #프로젝트 구성 파일
|——README  #설명 문서
|——start_migrate.sh  #Linux에서 마이그레이션 시 스크립트 실행
|——start_migrate.bat #Windows에서 마이그레이션 시 스크립트 실행
</pre>

>
 - db 디렉터리는 주로 툴 마이그레이션에 성공한 파일을 기록하여 표시합니다. 매번 마이그레이션 작업 시 먼저 db 상의 기록을 비교하고 이미 현재 파일에 기록되어 있는 경우 해당 파일은 건너뛰며, 기록되어 있지 않은 경우 마이그레이션합니다.
 - log 디렉터리는 툴 마이그레이션 시 모든 로그를 기록합니다. 마이그레이션 과정에서 오류가 발생할 경우 먼저 해당 디렉터리에 있는 error.log를 확인하십시오.

### 3. config.ini 구성 파일 수정
마이그레이션 시 스크립트 실행 전 먼저 반드시 config.ini 구성 파일을 수정(경로: `./conf/config.ini`)해야 하며, config.ini 내용은 다음과 같은 몇 가지 부분으로 나눌 수 있습니다.

#### 3.1 마이그레이션 유형 설정
type은 마이그레이션 유형을 뜻하며, 사용자는 마이그레이션 수요에 따라 해당하는 표시를 입력합니다. 예를 들어, 로컬 데이터를 COS로 마이그레이션할 경우 `[migrateType]`의 설정 내용을 `type=migrateLocal`로 설정합니다.
<pre>[migrateType]
type=migrateLocal
</pre>

현재 지원하는 마이그레이션 유형은 다음과 같습니다.

| migrateType | 설명 |
| ------| ------ |
| migrateLocal| 로컬에서 COS로 마이그레이션 |
| migrateAws| AWS S3에서 COS로 마이그레이션 |
| migrateAli| Alibaba OSS에서 COS로 마이그레이션 |
| migrateQiniu| Qiniu에서 COS로 마이그레이션 |
| migrateUrl| 다운로드 URL을 COS로 마이그레이션 |
| migrateBucketCopy| 원본 Bucket에서 타깃 Bucket으로 복사|
|migrateUpyun  | Upyun에서 COS로 마이그레이션 |

#### 3.2 마이그레이션 작업 설정
사용자는 실제 마이그레이션 수요에 따라 마이그레이션하는 타깃 COS 정보 설정 및 마이그레이션 작업 설정을 포함한 관련 설정을 진행합니다.
<pre>
# 마이그레이션 툴의 일반 설정 단계에는 마이그레이션할 타깃 COS의 계정 정보가 포함됩니다.
[common]
secretId=COS_SECRETID
secretKey=COS_SECRETKEY
bucketName=examplebucket-1250000000
region=ap-guangzhou
storageClass=Standard
cosPath=/
https=off
tmpFolder=./tmp
smallFileThreshold=5242880
smallFileExecutorNum=64
bigFileExecutorNum=8
entireFileMd5Attached=on
daemonMode=off
daemonModeInterVal=60
executeTimeWindow=00:00,24:00
encryptionType=sse-cos
</pre>

| 이름| 설명 |기본값|
| ------| ------ |----- |
| secretId| 사용자 보안키 SecretId입니다. `COS_SECRETID`를 실제 키 정보로 대체하여 사용하십시오. [액세스 관리 콘솔](https://console.cloud.tencent.com/cam/capi)의 Tencent Cloud API 키 페이지에서 획득할 수 있습니다. |-|
| secretKey| 사용자 보안키 SecretKey입니다. `COS_SECRETKEY`를 실제 키 정보로 대체하여 사용하십시오. [액세스 관리 콘솔](https://console.cloud.tencent.com/cam/capi)의 Tencent Cloud API 키 페이지에서 획득할 수 있습니다.|-|
| bucketName| 타깃 Bucket의 이름이며, `<BucketName-APPID>`와 같은 형식으로 이름이 생성됩니다. 즉, examplebucket-1250000000와 같이 Bucket 이름에는 반드시 APPID가 포함됩니다. |-|
| region| 타깃 Bucket의 Region 정보입니다. COS의 리전 약어로, [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오. |-|
| storageClass|스토리지 유형: Standard(표준 스토리지), Standard_IA(표준IA 스토리지), Archive(CAS) |Standard|
| cosPath|마이그레이션할 COS 경로입니다. `/`는 Bucket의 루트 경로에 마이그레이션한다는 의미이며, `/folder/doc/`는 Bucket의 `/folder/doc/`에 마이그레이션한다는 의미입니다. `/folder/doc/`가 존재하지 않는 경우 자동으로 해당 경로를 생성합니다.|/|
| https| HTTPS를 사용한 전송 여부이며, on은 활성화, off는 비활성화의 의미입니다. 활성화할 경우 속도가 비교적 느려지므로 전송에 대한 보안 요구가 높은 시나리오에 적합합니다.|off|
| tmpFolder|기타 클라우드 스토리지에서 COS로 마이그레이션하는 과정에서 임시로 파일을 저장하는 디렉터리이며 마이그레이션 완료 후 삭제됩니다. 다음과 같은 절대 경로가 요구됩니다.<br>Linux에서는 단일 슬래시가 세퍼레이터입니다. 예: `/a/b/c`<br>Windows에서는 2개의 역슬래시가 세퍼레이터입니다. 예: `E:\\a\\b\\c`<br>기본값은 툴이 존재하는 경로의 하위 tmp 디렉터리입니다.|./tmp|
| smallFileThreshold| 저용량 파일의 임계값 바이트 설정입니다. 해당 임계값 이상인 경우 멀티파트 업로드를 진행하며, 미만인 경우 단순 업로드합니다. 기본값은 5MB입니다. |5242880|
| smallFileExecutorNum|저용량 파일(smallFileThreshold 값 미만의 파일)의 동시 접속 수로, 단순 업로드를 사용합니다. 외부 네트워크를 통해 COS에 접속하고 대역폭이 비교적 작은 경우 해당 동시 접속 수를 작게 설정하십시오.|64|
| bigFileExecutorNum| 대용량 파일(smallFileThreshold 값 이상의 파일)의 동시 접속 수로, 멀티파트 업로드를 사용합니다. 외부 네트워크를 통해 COS에 접속하고 대역폭이 비교적 작은 경우 해당 동시 접속 수를 작게 설정하십시오.|8|
| entireFileMd5Attached|마이그레이션 툴이 문서 전체에 대해 MD5 컴퓨팅 후 파일의 사용자 지정 헤더 x-cos-meta-md5에 삽입하여 이후 인증에 사용합니다. 이는 COS에서 멀티파트로 업로드하는 파일의 etag가 문서 전체에 대한 MD5가 아니기 때문입니다.|on|
| daemonMode|daemon 모드 사용 여부이며 on은 활성화, off는 비활성화의 의미합니다. daemon은 프로그램이 멈추지 않고 순환하면서 동기화를 진행한다는 의미로, 매번 동기화별 간격은 daemonModeInterVal 매개변수로 설정합니다.|off|
| daemonModeInterVal|매번 동기화 종료 후, 얼마가 지난 후 다음 동기화를 진행할지를 설정하며 단위는 초입니다. |60|
| executeTimeWindow|실행 시간 창입니다. 시간 단위는 분이며, 해당 매개변수로 마이그레이션 툴이 매일 실행되는 시간대를 정의합니다. 예시:<br>매개변수를 03:30,21:00로 설정하는 경우, 오전 03:30부터 오후21:00 사이에 작업을 진행하고 다른 시간에는 휴면 상태가 된다는 의미입니다. 휴면 상태에서는 마이그레이션을 일시 중지하고 다음 번 시간 창이 자동으로 이어서 실행할 때까지 마이그레이션 진도를 보관합니다.|00:00,24:00|
| encryptionType  |  sse-cos 서버를 사용하여 암호화한다는 의미입니다.    |     기본적으로 입력되어 있지 않으며, 서버에서 암호화가 필요한 경우 작성합니다.       |

#### 3.3 데이터 소스 정보 설정
`[migrateType]` 마이그레이션 유형에 따라 상응하는 부분을 참고하여 설정합니다. 예를 들어, `[migrateType]`을 `type=migrateLocal`로 설정한 경우 `[migrateLocal]` 부분만 설정하면 됩니다.

**3.3.1 로컬 데이터 소스 migrateLocal 설정**

로컬에서 COS로 마이그레이션하는 경우 이 부분과 같이 설정합니다. 자세한 설정 및 설명은 다음과 같습니다.
<pre>
# 로컬에서 COS로 마이그레이션 시 설정
[migrateLocal]
localPath=E:\\code\\java\\workspace\\cos_migrate_tool\\test_data
excludes=
ignoreModifiedTimeLessThanSeconds=
</pre>

| 설정 페이지 | 설명 |
| ------| ------ |
|localPath|로컬 디렉터리로, 다음과 같은 절대 경로가 요구됩니다.<br><li>Linux에서는 단일 슬래시가 세퍼레이터입니다. 예: `/a/b/c`<br><li>Windows에서는 2개의 역슬래시가 세퍼레이터입니다. 예: `E:\\a\\b\\c`|
|excludes| 제외할 디렉터리 또는 파일의 절대 경로로, localPath 하위에 있는 특정 디렉터리 또는 파일은 마이그레이션을 진행하지 않습니다. 여러 개의 절대 경로 사이에는 ;로 나누고, 입력하지 않는 경우 localPath 하위를 모두 마이그레이션합니다.|
|ignoreModifiedTimeLessThanSeconds| 업데이트 시간과 현재 시간의 시간 사이의 일정 시간이 지나지 않은 파일을 제외하며, 단위는 초입니다. 기본적으로 설정되어 있지 않으며 lastmodified 시간에 따라 필터링하지 않음을 의미합니다. 클라이언트에서 파일을 업데이트하는 중 마이그레이션 툴이 동시에 실행될 때 현재 업데이트 중인 파일을 COS에 업데이트하지 않습니다. 예를 들어, 300으로 설정하는 경우 5분 이내에 업데이트된 파일은 업로드하지 않는다는 의미입니다.|

**3.3.2 Ali OSS 데이터 소스 migrateAli 설정**

Alibaba Cloud OSS에서 COS로 마이그레이션하는 경우 이 부분과 같이 설정합니다. 자세한 설정 및 설명은 다음과 같습니다.
<pre># Ali 클라우드 OSS에서 COS로 마이그레이션 시 설정
[migrateAli]
bucket=bucket-aliyun
accessKeyId=yourAccessKeyId
accessKeySecret=yourAccessKeySecret
endPoint= oss-cn-hangzhou.aliyuncs.com
prefix=
proxyHost=
proxyPort=
</pre>

| 설정 페이지 | 설명 |
| ------| ------ |
|bucket|Alibaba Cloud OSS  Bucket 이름|
|accessKeyId|yourAccessKeyId를 사용자의 키로 대체 |
|accessKeySecret| yourAccessKeySecret를 사용자의 키로 대체|
|endPoint|Alibaba Cloud endpoint 주소|
|prefix|마이그레이션할 경로의 접두사입니다. Bucket의 하위 모든 데이터를 마이그레이션하는 경우 prefix 값은 비워둡니다.|
|proxyHost|프록시를 사용해 액세스하는 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

**3.3.3 AWS 데이터 소스 migrateAws 설정**

AWS에서 COS로 마이그레이션하는 경우 이 부분과 같이 설정합니다. 자세한 설정 및 설명은 다음과 같습니다.
<pre># AWS에서 COS로 마이그레이션 시 설정
[migrateAws]
bucket=bucket-aws
accessKeyId=AccessKeyId
accessKeySecret=SecretAccessKey
endPoint=s3.us-east-1.amazonaws.com
prefix=
proxyHost=
proxyPort=
</pre>

| 설정 페이지 | 설명 |
| ------| ------ |
|bucket| AWS 객체 스토리지 Bucket 이름|
|accessKeyId|AccessKeyId를 사용자의 키로 대체|
|accessKeySecret| SecretAccessKey를 사용자의 키로 대체|
|endPoint|AWS의 endpoint 주소입니다. 반드시 도메인을 사용해야 하며 region을 사용할 수 없습니다.|
|prefix|마이그레이션할 경로의 접두사입니다. Bucket의 하위 모든 데이터를 마이그레이션하는 경우 prefix 값은 비워둡니다.|
|proxyHost|프록시를 사용해 액세스하는 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

 
**3.3.4 Qiniu 데이터 소스 migrateQiniu 설정**

Qiniu에서 COS로 마이그레이션하는 경우 이 부분과 같이 설정합니다. 자세한 설정 및 설명은 다음과 같습니다.
<pre># Qiniu에서 COS로 마이그레이션 시 설정
[migrateQiniu]
bucket=bucket-qiniu
accessKeyId=AccessKey
accessKeySecret=SecretKey
endPoint=www.bkt.clouddn.com
prefix=
proxyHost=
proxyPort=
</pre>

| 설정 페이지 | 설명 |
| ------| ------ |
|bucket|Qiniu 객체 스토리지 Bucket 이름|
|accessKeyId|AccessKey를 사용자의 키로 대체|
|accessKeySecret| SecretKey를 사용자의 키로 대체|
|endPoint|Qiniu 다운로드 주소, downloadDomain에 해당|
|prefix|마이그레이션할 경로의 접두사입니다. Bucket의 하위 모든 데이터를 마이그레이션하는 경우 prefix 값은 비워둡니다.|
|proxyHost|프록시를 사용해 액세스하는 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

 
**3.3.5 URL 리스트 데이터 소스 migrateUrl 설정**

URL 리스트에서 COS로 마이그레이션하는 경우 이 부분과 같이 설정합니다. 자세한 설정 및 설명은 다음과 같습니다.
<pre>
# URL 리스트에서 COS로 다운로드 및 마이그레이션 시 설정
[migrateUrl]
urllistPath=D:\\folder\\urllist.txt
</pre>
     
| 설정 페이지 | 설명 |
| ------| ------ |
|urllistPath|URL 리스트 주소입니다. URL로 이루어져 있으며, 한 행이 URL 원시 주소(예: `http://aaa.bbb.com/yyy/zzz.txt`, 큰따옴표 또는 기타 부호 추가 필요 없음)입니다. URL 리스트 주소는 절대 경로여야 합니다.<br><li>Linux에서는 단일 슬래시가 세퍼레이터입니다. 예: `/a/b/c.txt`<br><li>Windows에서는 2개의 역슬래시가 세퍼레이터입니다. 예: `E:\\a\\b\\c.txt`<br>디렉터리를 입력하는 경우 해당 디렉터리에 있는 모든 파일을 urllist 파일로 간주하며 모두 스캔하여 마이그레이션합니다.|

 
**3.3.6 Bucket 간 상호 복사 migrateBucketCopy 설정**

COS의 특정 Bucket에서 다른 Bucket으로 마이그레이션하는 경우 이 부분과 같이 설정합니다. 자세한 설정 및 설명은 다음과 같습니다.
>마이그레이션을 요청한 계정은 원본 읽기 권한 및 타깃 쓰기 권한을 가지고 있어야 합니다.

<pre>
# 원본 Bucket에서 타깃 Bucket으로 마이그레이션 시 설정
[migrateBucketCopy]
srcRegion=ap-shanghai
srcBucketName=examplebucket-1250000000
srcSecretId=COS_SECRETID
srcSecretKey=COS_SECRETKEY
srcCosPath=/
</pre>

| 설정 페이지 | 설명 |
| ------| ------ |
|srcRegion|원본 Bucket의 Region 정보이며, 자세한 내용은 [가용 리전](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오.|
|srcBucketName|원본 Bucket의 이름이며, `<BucketName-APPID>`와 같은 형식으로 이름이 생성됩니다. 즉, examplebucket-1250000000와 같이 Bucket 이름에는 반드시 APPID가 포함됩니다.|
|srcSecretId|원본 Bucket이 종속되어 있는 사용자 키 SecretId이며, [Tencent Cloud API 키](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다. 동일한 사용자의 데이터인 경우 srcSecretId와 common의 SecretId가 동일하며, 그렇지 않을 경우 계정 간 Bucket 복사입니다.|
|srcSecretKey|원본 Bucket이 종속되어 있는 사용자 키 secret_key이며, [Tencent Cloud API 키](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다. 동일한 사용자의 데이터인 경우 srcSecretKey와 common의 secretKey가 동일하며, 그렇지 않을 경우 계정 간 Bucket 복사입니다.|
|srcCosPath|마이그레이션할 COS의 경로로, 해당 경로의 하위 파일을 타깃 Bucket으로 마이그레이션합니다.|

**3.3.7 Upyun 데이터 소스 migrateUpyun 설정**
Upyun에서 COS로 마이그레이션하는 경우 이 부분과 같이 설정합니다. 자세한 설정 및 설명은 다음과 같습니다.

```
[migrateUpyun]
# Upyun에서 마이그레이션
bucket=xxx
#Upyun 작업자 ID
accessKeyId=xxx
#Upyun 작업자 비밀번호     
accessKeySecret=xxx       
prefix=

#Upyun sdk 제한으로, 해당 proxy는 전역 proxy로 설정됩니다.
proxyHost=
proxyPort=
```

| 설정 페이지 | 설명 |
| ------| ------ |
|bucket|Upyun USS Bucket 이름|
|accessKeyId|Upyun 작업자 ID로 대체|
|accessKeySecret| Upyun 작업자 비밀번호로 대체|
|prefix|마이그레이션할 경로의 접두사입니다. Bucket의 하위 모든 데이터를 마이그레이션하는 경우 prefix 값은 비워둡니다.|
|proxyHost|프록시를 사용해 액세스하는 경우 프록시 IP 주소를 입력합니다.|
|proxyPort|프록시 포트|

### 4. 마이그레이션 툴 실행
#### Windows
**start_migrate.bat**을 더블 클릭하면 실행됩니다.

#### Linux
1.config.ini 구성 파일에서 설정을 읽어옵니다. 명령어는 다음과 같습니다.
<pre>
sh start_migrate.sh
</pre>
2.일부 매개변수는 명령 라인에서 설정을 읽어옵니다. 실행 명령어는 다음과 같습니다.
<pre>
sh start_migrate.sh -Dcommon.cosPath=/savepoint0403_10/
</pre>

>
> - 툴에서 설정 항목을 읽어오는 방법은 명령 라인에서 읽어오는 방법과 구성 파일에서 읽어오는 방법 두 가지가 있습니다.
> - 명령 라인의 우선순위가 구성 파일의 우선순위보다 높습니다. 즉, 동일한 설정 항목인 경우 명령 라인의 매개변수를 우선 채용합니다.
> - 명령 라인에서 설정 항목을 읽어오는 방법은 사용자가 동시에 서로 다른 마이그레이션 작업을 실행할 때 편리합니다. 그러나 두 작업의 주요 설정 항목인 Bucket 이름, COS 경로, 마이그레이션할 원본 경로 등이 완전이 달라야 합니다. 이는 각 마이그레이션 작업별로 서로 다른 db 디렉터리에 쓰기를 진행하여 마이그레이션을 동시에 진행할 수 있도록 보장하기 때문입니다. 상기 툴 구조의 db 정보 내용을 참조하십시오.
> - 설정 항목 형식: **-D{sectionName}.{sectionKey}={sectionValue}**. 여기에서 sectionName은 구성 파일의 섹션 이름이며, sectionKey는 섹션의 설정 항목 이름이고, sectionValue는 섹션의 설정값입니다. 마이그레이션할 타깃 COS 경로를 설정할 경우 **-Dcommon.cosPath=/bbb/ddd**로 표시합니다.

## 마이그레이션 메커니즘 및 프로세스
### 마이그레이션 메커니즘 원리

COS 마이그레이션 툴은 스테이트풀 툴이며, 마이그레이션 완료를 db 디렉터리에 기록하고 KV 형식으로 leveldb 파일에 저장합니다. 매번 마이그레이션 전 마이그레이션할 경로에 대해 먼저 db 존재 여부를 확인하고, 존재하면서 속성과 db가 일치하는 경우 마이그레이션을 건너뛰며, 존재하지 않을 경우 마이그레이션을 진행합니다. 여기에서 속성은 마이그레이션 유형에 따라 달라지며, 로컬 마이그레이션의 경우 mtime을 판단하고 기타 클라우드 스토리지 마이그레이션과 Bucket 복사는 원본 파일의 etag와 길이가 db와 일치하는지 판단합니다. 이와 같이 Tencent Cloud에서는 COS를 조회하는 방법이 아닌 db에 마이그레이션을 완료한 기록이 있는지를 참조하므로 마이그레이션 툴을 우회하여 다른 방식(예: COSCMD 또는 콘솔)을 이용해 파일을 삭제하거나 수정한 경우, 마이그레이션 툴 실행 시 해당 변경 사항을 감지하지 못해 다시 마이그레이션하지 않습니다.

### 마이그레이션 프로세스 순서

1. 구성 파일을 읽어옵니다. 마이그레이션 type에 따라 해당 설정 섹션을 읽어오며 매개변수를 확인합니다.
2. 지정한 마이그레이션 유형에 따라 db 하위에 있는 모든 마이그레이션 파일의 표시를 스캔하고 비교하여 업로드를 허용할지 여부를 판단합니다.
3. 마이그레이션 과정에서 실행 결과를 출력합니다. 여기에서 inprogress는 마이그레이션 중임을 의미하며, skip은 건너뜀, fail은 실패, ok는 성공, condition_not_match는 마이그레이션 조건을 충족하지 않아 건너뛴 파일(예: lastmodifed 및 excludes)을 의미합니다. 실패에 대한 상세 정보는 log의 error 로그에서 확인할 수 있으며, 실행 과정은 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/7561d07ea315c9bacbb228b36d6ad6d6.png)
4. 전체 마이그레이션 완료 후 누적 마이그레이션 성공량, 실패량, 건너뛰기량, 소모시간을 포함한 통계 정보를 출력합니다. 실패 현황에 대해서는 error 로그를 확인하거나 재실행합니다. 마이그레이션 툴은 마이그레이션에 성공한 경우 건너뛰므로 성공하지 못한 부분을 다시 마이그레이션합니다. 실행 완료 결과는 다음과 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/2534fd390218db29bb03f301ed2620c8.png)

## FAQ
COS Migration 툴 사용 과정에서 마이그레이션 실패, 실행 오류 등 오류가 발생하는 경우 [COS Migration 툴 FAQ](https://intl.cloud.tencent.com/document/product/436/30585)를 참조하여 해결하십시오.
