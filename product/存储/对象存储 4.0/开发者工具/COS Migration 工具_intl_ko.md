## 기능 설명
COS 마이그레이션은 COS 데이터 마이그레이션 기능을 통합된 도구입니다. 사용자는 간단한 구성 작업으로 데이터를 COS로 빠르게 마이그레이션할 수 있습니다. 다음 특징을 지니고 있습니다.
- 다양한 데이터 소스:
   - 로컬 데이터: 로컬 데이터를 COS로 마이그레이션합니다.
   - 기타 클라우드 스토리지: 현재 AWS S3, Alibaba Cloud OSS, Qiniu Cloud Storage를 COS로 마이그레이션하는 것을 지원하고 있으며, 앞으로 확장될 예정입니다.
   - URL 리스트: 지정된 URL 다운로드 리스트에 따라 다운로드하여 COS로 마이그레이션합니다.
   - 버킷 상호 복사: COS의 버킷 데이터는 서로 복사되며 계정 및 지역 간 복사를 지원합니다.
- 중단점 업로드 재개: 도구는 업로드 중단점 재개를 지원합니다. 일부 대용량 파일은 중간에 로그아웃하거나 서비스 장애로 인해 업로드가 완료되지 않을 경우 도구를 다시 실행하여 업로드가 완료되지 않은 파일은 다시 업로드될 수 있습니다.
- 멀티파트 업로드: 객체를 멀티파트로 COS에 업로드합니다.
- 병렬 업로드: 여러 객체를 동시에 업로드할 수 있습니다.
- 마이그레이션 검증: 객체 마이그레이션 후의 확인.

## 사용 환경
### 운영 체제
Windows, Linux 및 macOS

### 소프트웨어 의존
- JDK1.7 X64 또는 이상 버전, JDK 설치 및 구성에 대한 자세한 내용은 [Java 설치 및 구성](https://cloud.tencent.com/document/product/436/10865)을 참조하십시오.

## 사용 방법
### 1. 도구 획득
[COS Migration 도구](https://github.com/tencentyun/cos_migrate_tool_v5)로 이동하여 다운로드하십시오.

### 2. 도구 패키지 압축 해제
#### Windows
 압축을 해제하고 디렉터리에 저장합니다. 예를 들어
<pre>
C:\Users\Administrator\Downloads\cos_migrate
</pre>

#### Linux
압축을 해제하고 디렉터리에 저장합니다.
<pre>
unzip cos_migrate_tool_v5-master.zip && cd cos_migrate_tool_v5-master
</pre>

#### 마이그레이션 도구 구조
압축 해제 후의 COS Migration 도구 디렉터리 구조는 다음과 같습니다.
<pre>
COS_Migrate_tool
|——conf  #구성 파일이 위치한 디렉터리
|   |——config.ini  #마이그레이션 구성 파일
|——db    #마이그레이션 성공 기록 저장
|——dep   #프로그램 메인 로직에 의해 컴파일하여 생성된 JAR 패키지
|——log   #도구 사용 시 생성된 로그
|——opbin #컴파일에 사용되는 스크립트
|——src   #도구 소스 코드
|——tmp   #임시 파일 스토리지 디렉터리
|——pom.xml #프로젝트 구성 파일
|——README  #설명 문서
|——start_migrate.sh  #Linux에서 시동 스크립트 마이그레이션
|——start_migrate.bat #Windows에서 시동 스크립트 마이그레이션
</pre>

>?
 - db 디렉터리는 주로 도구 마이그레이션 성공의 파일 표시를 기록합니다. 마이그레이션할 때 먼저 db의 기록을 비교합니다. 해당 파일의 표시가 기록된 경우 해당 파일을 건너뛰고 그렇지 않으면 파일 마이그레이션을 진행합니다.
 - log 디렉터리는 도구 마이그레이션 시 모든 로그를 기록하고 있으며 마이그레이션 과정에서 오류가 발생하면 해당 디렉터리 아래의 error.log를 확인하십시오.

### 3. config.ini 구성 파일 수정
시동 스크립트를 마이그레이션하기 전에 config.ini 구성 파일 수정(경로: `./conf/config.ini`)을 진행해야 하며 config.ini 콘텐츠는 다음과 같이 여러 부분으로 나눌 수 있습니다.

#### 3.1 마이그레이션 유형 구성
type은 마이그레이션 유형을 표시하고 사용자는 마이그레이션 수요에 따라 대응하는 표식을 입력합니다. 예를 들어 로컬 데이터를 COS로 마이그레이션하려면 `[migrateType]`의 구성 콘텐츠는 `type=migrateLocal`입니다.
<pre>[migrateType]
type=migrateLocal
</pre>

지원되는 마이그레이션 유형은 다음과 같습니다.

| migrateType | 설명 |
| ------| ------ |
| migrateLocal| 로컬에서 COS로 마이그레이션 |
| migrateAws| AWS S3 로컬에서 COS로 마이그레이션 |
| migrateAli| Alibaba Cloud OSS에서 COS로 마이그레이션 |
| migrateQiniu| Qiniu Cloud에서 COS로 마이그레이션 |
| migrateUrl| 다운로드 URL에서 COS로 마이그레이션 |
| migrateBucketCopy| 소스 버킷에서 목표 버킷으로 복사|

#### 3.2 마이그레이션 태스크 구성
사용자는 실제 마이그레이션 수요에 따라 해당 구성을 진행하는데, 주로 목표 COS 정보 구성 및 마이그레이션 태스크 관련 구성을 포함합니다.
<pre>
# 마이그레이션 도구의 공공 구성 섹션은 목표 COS로 마이그레이션할 계정 정보를 포함합니다.
[common]
secretId="COS_SECRETID"
secretKey="COS_SECRETKEY"
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
damonMode=off
damonModeInterVal=60
executeTimeWindow=00:00,24:00
</pre>

| 이름 | 설명 | 기본값|
| ------| ------ |----- |
| secretId| 사용자 키 SecretId. [클라우드 API  키 콘솔](https://console.cloud.tencent.com/cam/capi)에서 확인 가능 |-|
| secretKey| 사용자 키 SecretKey. [클라우드 API  키 콘솔]( https://console.cloud.tencent.com/cam/capi)에서 확인 가능|-|
| bucketName| 대상 버킷의 이름, 이름 형식은 `<BucketName-APPID>`입니다. 즉, 버킷 이름에 APPID가 포함되어야 합니다. 예를 들어 examplebucket-1250000000 |-|
| region| 대상 버킷의 지역 정보. COS 지역 약칭에 대한 자세한 내용은 [가용 지역](https://cloud.tencent.com/document/product/436/6224)을 참조하십시오 |-|
| storageClass|스토리지 클래스: Standard - 표준 스토리지, Standard_IA - 저빈도 스토리지 |Standard|
| cosPath|마이그레이션할 COS 경로. `/`는 버킷 루트 경로로 마이그레이션하는 것을 의미합니다. `/aaa/bbb/`는 버킷의 ` /aaa/bbb/`로 마이그레이션하는 것을 의미합니다. `/aaa/bbb/`가 존재하지 않으면 경로는 자동으로 생성됩니다 |/|
| https| HTTPS를 사용하여 전송 여부: on은 전송, off는 전송하지 않음을 표시합니다. 전송 사용 후 속도가 느려서 전송 보안 요구가 높은 시나리오에 적용됩니다|off|
| tmpFolder|다른 클라우드 저장소에서 COS로 마이그레이션 할 때 임시 파일을 저장하는 데 사용되는 디렉터리. 마이그레이션이 완료된 후 삭제됩니다. 요구 양식은 절대 경로입니다. <br>Linux에서 분리 기호는 ` /a/b/c`와 같은 단일 슬래시입니다. <br>Windows에서 구분 기호는 `E:\\a\\b\\c`와 같은 두 개의 슬래시입니다. <br>기본적으로 도구 경로 아래의 tmp 디렉터리입니다| /.tmp|
| smallFileThreshold|  소용량 파일의 바이트 임계값입니다. 이 임계값보다 크거나 같은 경우에 멀티파트 업로드를 사용합니다. 그렇지 않으면 간편 업로드를 사용하며 기본적으로 5MB입니다. |5242880|
| smallFileExecutorNum|소용량 파일(파일은 smallFileThreshold보다 작음)의 동시 발생 수이며 간편 업로드를 사용합니다. COS를 공중망으로 연결하고 대역폭이 작은 경우 해당 동시 발생 수를 줄여주십시오|64|
| bigFileExecutorNum| 대용량 파일(파일은 smallFileThreshold보다 크거나 같음)의 동시 발성 수이며 멀티파트 업로드를 사용합니다. COS를 공중망으로 연결하고 대역폭이 작은 경우 해당 동시 발성 수를 줄여주십시오|8|
| entireFileMd5Attached|마이그레이션 도구가 전체 텍스트의 MD5를 계산하여 파일의 사용자 지정 헤더 x-cos-meta-md5에 저장함을 표시하며 후속 검증에 사용됩니다. COS 멀티파트 업로드된 대용량 파일의 etag는 전체 텍스트의 MD5가 아니기 때문입니다|on|
| damonMode|damon 모드 시동 여부: on은 켜짐, off는 꺼짐을 표시합니다. damon은 프로그램이 동기화를 순환적으로 실행할 수 있음을 표시하며, 각 동기화 간격은 damonModeInterVal 매개변수에 의해 설정됩니다|off|
| damonModeInterVal|각 동기화가 완료된 후 다음 동기화가 언제 실행되는지 나타내며 단위가 초입니다 |60|
| executeTimeWindow|실행 시간 창. 시간 세분화가 분이며 이 매개변수는 마이그레이션 도구가 매일 수행하는 시간대를 정의합니다. 예를 들어 <br>매개변수 03:30, 21:00는 새벽 03:30에서 저녁 21:00 사이에 태스크를 실행하는 것을 표시합니다. 그 외의 시간은 휴면 상태에 들어갑니다. 휴면 상태에 마이그레이션이 일시적으로 중지되면 마이그레이션 진도가 유지되며 다음 시간까지 창이 자동으로 실행됩니다.|00:00,24:00|

#### 3.3 데이터 소스 정보 구성
`[migrateType]`의 마이그레이션 유형에 따라 해당 섹션을 구성합니다. 예를 들어 `[migrateType]`의 구성 내용이 `type=migrateLocal`일 경우, 사용자는 `[migrateLocal]` 섹션만 구성하면 됩니다.

**3.3.1 로컬 데이터 소스 구성 migrateLocal**

로컬에서 COS로 마이그레이션 하려면 해당 부분 구성을 진행해야 합니다. 구체적인 구성 항목 및 설명은 다음과 같습니다.
<pre>
# 로컬에서 COS로 마이그레이션 하기 위한 섹션 구성
[migrateLocal]
localPath=E:\\code\\java\\workspace\\cos_migrate_tool\\test_data
exeludes=
ignoreModifiedTimeLessThanSeconds=
</pre>

| 구성 항목 | 설명 |
| ------| ------ |
|localPath|로컬 경로는 요구 양식은 절대 경로입니다. <br>Linux에서 분리 기호는 `/a/b/c`와 같은 단일 슬래시입니다. <br>Windows에서 구분 기호는 `E:\\a\\b\\c`와 같은 두 개의 슬래시입니다.|
|excludes| 제외할 디렉터리 또는 파일의 절대 경로는 localPath 아래 일부 디렉터리 또는 파일을 마이그레이션 하지 않음을 표시합니다. 여러 개 절대 경로 전에 구분 번호로 분할하고 입력하지 않음은 localPath 아래 모든 파일을 마이그레이션하는 것을 표시합니다|
|ignoreModifiedTimeLessThanSeconds| 업데이트 시점은 현재 시간과 차이가 일정 시간대 미만인 파일을 제외하고 단위는 초이며, 기본적으로 설정 안 함으로 lastmodified 시간에 따라 선별되지 않음을 표시하며 고객은 파일을 업데이트하는 동시에 마이그레이션 도구를 실행하는 데 적용되며 업데이트 중인 파일을 COS로 마이그레이션 및 업로드하지 않도록 요청합니다. 예를 들어 300으로 설정하면 업데이트된 5분 이상의 파일만 업로드되었음을 표시합니다|

**3.3.2 Alibaba Cloud OSS 데이터 소스 구성 migrateAli**

Alibaba Cloud OSS에서 COS로 마이그레이션할 경우 해당 부분 구성을 진행하며 구체적인 구성 항목 및 설명은 다음과 같습니다.
<pre># Alibaba Cloud OSS에서 COS로 마이그레이션 하기 위한 구성 섹션
[migrateAli]
bucket=bucket-aliyun
accessKeyId="<yourAccessKeyId>"
accessKeySecret="<yourAccessKeySecret>"
endPoint= oss-cn-hangzhou.aliyuncs.com
prefix=
proxyHost=
proxyPort=
</pre>

| 구성 항목 | 설명 |
| ------| ------ |
|bucket|Alibaba Cloud OSS 버킷 이름|
|accessKeyId|사용자 키 accessKeyId |
|accessKeySecret| 사용자 키 accessKeySecret|
|endPoint|Alibaba Cloud endpoint 주소|
|prefix|마이그레이션 할 경로의 접두사입니다. 버킷 아래의 모든 데이터를 마이그레이션할 경우 접두사가 비어 있습니다|
|proxyHost|프록시로 접근하려면 프록시 IP 주소를 입력하십시오|
|proxyPort|프록시 포트|

**3.3.3 AWS 데이터 소스 구성 migrateAws **

AWS에서 COS로 마이그레이션할 경우 해당 부분 구성을 진행하며 구체적인 구성 항목 및 설명은 다음과 같습니다.
<pre># AWS에서 COS로 마이그레이션 및 구성 섹션
[migrateAws]
bucket=bucket-aws
accessKeyId="AccessKeyId"
accessKeySecret="SecretAccessKey"
endPoint=s3.us-east-1.amazonaws.com
prefix=
proxyHost=
proxyPort=
</pre>

| 구성 항목 | 설명 |
| ------| ------ |
|bucket| AWS COS 버킷 이름|
|accessKeyId|사용자 키 accessKeyId |
|accessKeySecret| 사용자 키 accessKeySecret|
|endPoint|AWS endpoint 주소는 도메인 이름을 사용해야 하며 지역을 사용할 수 없습니다|
|prefix|마이그레이션 할 경로의 접두사입니다. 버킷 아래의 모든 데이터를 마이그레이션 할 경우 prefix가 비어 있습니다|
|proxyHost|프록시로 접근하려면 프록시 IP 주소를 입력하십시오|
|proxyPort|프록시 포트|


**3.3.4 Qiniu 데이터 소스 구성 migrateQiniu**

Qiniu에서 COS로 마이그레이션 할 경우 해당 부분 구성을 진행하며 구체적인 구성 항목 및 설명은 다음과 같습니다.
<pre># Qiniu에서 COS로 마이그레이션하기 위한 구성 섹션
[migrateQiniu]
bucket=bucket-qiniu
accessKeyId=”AccessKey”
accessKeySecret=”SecretKey”
endPoint=www.bkt.clouddn.com
prefix=
proxyHost=
proxyPort=
</pre>

| 구성 항목 | 설명 |
| ------| ------ |
|bucket|Qiniu COS 버킷 이름|
|accessKeyId|사용자 키 accessKeyId |
|accessKeySecret| 사용자 키 accessKeySecret|
|endPoint|Qiniu 다운로드 주소는 downloadDomain에 대응합니다|
|prefix|마이그레이션 할 경로의 접두사입니다. 버킷 아래의 모든 데이터를 마이그레이션 할 경우 prefix가 비어 있습니다|
|proxyHost|프록시로 접근하려면 프록시 IP 주소를 입력하십시오|
|proxyPort|프록시 포트|


**3.3.5 URL 리스트 데이터 소스 구성 migrateUrl**

지정된 URL 리스트에서 COS로 마이그레이션 할 경우 해당 부분 구성을 진행하며 구체적인 구성 항목 및 설명은 다음과 같습니다.
<pre>
# URL 리스트에서 COS로 마이그레이션 하기 위한 구성 섹션
[migrateUrl]
urllistPath=D:\\folder\\urllist.txt
</pre>

| 구성 항목 | 설명 |
| ------| ------ |
|urllistPath|URL 리스트 주소입니다. 내용은 URL 텍스트이며, 행 한 줄씩 URL 원본 주소(예를 들어 `http://aaa.bbb.com/yyy/zzz.txt`, 이중 따옴표 또는 다른 기호를 추가할 필요 없음)입니다. URL 리스트의 주소는 절대 경로여야 합니다. <br>Linux에서 분리 기호는 `/a/b/c.txt`와 같은 단일 슬래시입니다. <br>Windows에서 구분 기호는 `E:\\a\\b\\c.txt`와 같은 두 개의 슬래시입니다.<br>리스트를 입력했다면, 해당 리스트 아래의 모든 파일을 urllist 파일로 스캔을 하여 마이그레이션 할 것입니다|


**3.3.6 버킷 상호 복사 구성 migrateBucketCopy**

COS의 지정된 버킷에서 다른 버킷으로 마이그레이션 할 경우 해당 부분 구성을 진행하며 구체적인 구성 항목 및 설명은 다음과 같습니다.
<pre>
# 소스 버킷에서 목표 버킷으로 마이그레이션 구성 섹션
[migrateBucketCopy]
srcRegion=ap-shanghai
srcBucketName=examplebucket-1250000000
srcSecretId="COS_SECRETID"
srcSecretKey="COS_SECRETKEY"
srcCosPath=/
</pre>

| 구성 항목 | 설명 |
| ------| ------ |
|srcRegion|소스 버킷의 지역 정보는 [가용 지역](https://cloud.tencent.com/document/product/436/6224)을 참조하십시오|
|srcBucketName|소스 버킷 이름입니다. 명명 형식은 `<BucketName-APPID>`이며, 즉, 버킷 이름에 APPID가 포함되어야 합니다. 예를 들어 examplebucket-1250000000|
|srcSecretId|소스 버킷 소속 사용자의 키 SecretId입니다. [클라우드 API  키](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다. 동일한 사용자의 데이터일 경우 srcSecretId 및 common에 있는 SecretId가 동일하고 그렇지 않으면 계정간의 버킷 복사입니다.|
|srcSecretKey|소스 버킷 소속 사용자의 키 secret_key입니다. [클라우드 API  키](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다. 동일한 사용자의 데이터일 경우 srcSecretId 및 common에 있는 SecretId가 동일하고 그렇지 않으면 계정간의 버킷 복사입니다.|
|srcCosPath|마이그레이션 할 COS 경로입니다. 해당 경로 아래의 파일을 목표 버킷으로 마이그레이션하는 것을 표시합니다|


### 4. 마이그레이션 도구 실행
#### Windows
**start_migrate.bat**를 두 번 클릭하여 실행할 수 있습니다.

#### Linux
1.config.ini 구성 파일에서 구성을 읽으며 실행 명령은 다음과 같습니다.
<pre>
sh start_migrate.sh
</pre>
2.일부 매개변수는 명령행에서 구성을 읽으며 실행 명령은 다음과 같습니다.
<pre>
sh start_migrate.sh -Dcommon.cosPath=/savepoint0403_10/
</pre>

>?
> - 도구는 구성 항목 읽기를 지원하는 방식에는 명령행 읽기와 구성 파일 읽기 두 가지가 있습니다.
> - 명령행 우선 순위가 구성 파일보다 높을 경우 같은 구성 항목이 명령행에 있는 매개변수를 우선 적용합니다.
> - 명령행에서 구성 항목을 읽는 방식은 사용자가 서로 다른 마이그레이션 태스크를 동시에 실행하는 데 편리하지만, 두 번 태스크에서 키 구성 항목이 완전히 동일하지 않음을 전제로 합니다. 예를 들어 버킷 이름, COS 경로, 마이그레이션할 소스 경로 등이 있습니다. 마이그레이션 태스크에 따라 서로 다른 db 리스트에 들어가기 때문에 동시 발생 마이그레이션을 보장할 수 있습니다. 이전 글에서 도구 구조에 있는 db 정보를 참조하십시오.
> - 구성 항목의 형식은 **-D{sectionName}.{sectionKey}={sectionValue}**입니다. sectionName은 구성 파일의 섹션 이름이며 sectionKey는 섹션 중 구성 항목 이름, sectionValue는 섹션 중 구성 항목 값을 표시합니다. 예를 들어 COS로 마이그레이션할 경로를 설정할 경우 **-Dcommon.cosPath=/bbb/ddd**로 표시합니다

## 마이그레이션 메커니즘 및 프로세스
### 마이그레이션 메커니즘 및 원리
COS 마이그레이션 도구는 상태가 있고 마이그레이션이 성공되면 db 리스트에 기록되며 KV 형식으로 leveldb 파일에 저장됩니다. 마이그레이션 하기 전에 마이그레이션 할 경로에 대해 db에 존재하는지 확인해야 합니다. 존재하며 속성은 db에 존재하는 것과 일치할 경우 마이그레이션을 건너뛰고 그렇지 않으면 마이그레이션이 실행됩니다. 속성은 마이그레이션 유형에 따라 다르며 로컬 마이그레이션에 대해 mtime을 판단합니다. 다른 클라우드 저장소의 마이그레이션과 버킷 복사에 대해 소스 파일의 etag 및 길이가 db와 일치하는지 판단합니다. 그러므로 COS에 확인하는 것이 아니라 db에 마이그레이션 성공 기록이 있는지 참조해야 합니다. 마이그레이션 도구를 우회하여 다른 방식(예: COSCMD 또는 콘솔)으로 파일을 삭제 및 수정을 했다면 이러한 변화를 감지하지 못하기 때문에 다시 마이그레이션하지 않을 것입니다.

### 마이그레이션 프로세스 절차
1. 구성 파일을 읽고 마이그레이션 유형에 따라 응답하는 구성 섹션을 읽으며 매개변수 검사를 실행합니다.
2. 지정한 마이그레이션 유형에 따라 대조 db에 마이그레이션할 파일 표시를 스캔하여 대비함으로 업로드를 허용할지 판단합니다.
3. 마이그레이션 실행 중에 실행 결과를 출력하는데, 그중에 inprogress는 마이그레이션 중, skip는 건너뛰기, fail은 실패, ok는 성공을 표시하고 condition_not_match는 마이그레이션 조건을 충족하지 않아 건너뛴 파일(예: lastmodifed 및 excludes)을 표시합니다. 실패에 대한 자세한 정보는 log의 error 로그에서 확인할 수 있습니다. 실행 과정의 설명도는 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/7561d07ea315c9bacbb228b36d6ad6d6.png)
4. 전체 마이그레이션이 완료되면 통계 정보가 출력되며, 누적된 마이그레이션 성공 수량, 실패 수량, 건너뛰기 수량, 소모 시간이 포함됩니다. 실패한 경우, error 로그를 확인하거나 다시 실행하십시오. 마이그레이션 도구는 성공한 마이그레이션을 건너뛰고 실패한 마이그레이션만 마이그레이션하기 때문입니다. 실행 완료 결과는 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/2534fd390218db29bb03f301ed2620c8.png)

## FAQ
COS 마이그레이션 도구 사용 중에 마이그레이션 실패, 실행 오류 등과 같은 문제가 발생하면 [COS 마이그레이션 도구 FAQ](https://cloud.tencent.com/document/product/436/30745)를 참조하여 문제를 해결하십시오.
