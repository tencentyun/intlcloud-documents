## 기능 설명

COSDistCp는 MapReduce를 기반으로 하는 분산형 파일 복사 툴로, 주로 HDFS와 COS 간의 데이터 복사에 사용합니다. 주요 기능은 다음과 같습니다.
- 길이, CRC 검사합을 기반으로 파일의 증분 마이그레이션 및 데이터 검사 수행
- 원본 디렉터리 파일에 정규식 필터링 진행
- 원본 디렉터리 파일을 압축 해제하여 설정된 압축 포맷으로 전환
- 정규식을 기반으로 텍스트 파일 취합
- 원본 파일 및 원본 디렉터리의 사용자, 그룹, 확장 속성 및 시간 보관
- 알람 및 Prometheus 모니터링 설정
- 파일 크기 분포 통계
- 읽기 대역폭에 속도 제한 설정

## 사용 환경

#### 시스템 환경

Linux 시스템 지원.

#### 소프트웨어 종속

Hadoop-2.6.0 버전 이상, Hadoop-COS 플러그 인 5.9.3 버전 이상.

## 다운로드 및 설치

#### COSDistCp jar 패키지 획득

- Hadoop 2.x 사용자는 [cos-distcp-1.12-2.8.5.jar 패키지](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-2.8.5.jar)를 다운로드하여 jar 패키지의 [MD5 검사 값](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-2.8.5-md5.txt)에 따라 다운로드한 jar 패키지가 완벽한지 확인합니다.
- Hadoop 3.x 사용자는 [cos-distcp-1.12-3.1.0.jar 패키지](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-3.1.0.jar)를 다운로드하여 jar 패키지의 [MD5 검사 값](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-3.1.0-md5.txt)에 따라 다운로드한 jar 패키지가 완벽한지 확인합니다.

#### 설치 설명

Hadoop 환경에서 [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884)를 설치하면 COSDistCp 툴을 실행할 수 있습니다.

Hadoop 버전에 따라 위에 나열된 다운로드 주소에서 COSDistCp jar, Hadoop-COS jar 및 cos_api-bundle jar 패키지의 해당 버전을 다운로드할 수 있습니다. 그 다음 Hadoop-COS 관련 매개변수를 지정하여 복사 작업을 수행합니다. 여기서 jar 패키지 주소는 로컬 주소여야 합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar \
-libjars cos_api-bundle-${version}.jar,hadoop-cos-${version}.jar \
-Dfs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider \
-Dfs.cosn.userinfo.secretId=COS_SECRETID \
-Dfs.cosn.userinfo.secretKey=COS_SECRETKEY \
-Dfs.cosn.bucket.region=ap-guangzhou \
-Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
-Dfs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
--src /data/warehouse \
--dest cosn://examplebucket-1250000000/warehouse
```


## 원리 설명

COSDistCp는 MapReduce 프레임워크를 기반으로 구현되며, 멀티 프로세스+멀티 스레드 아키텍처입니다. 파일 복사, 데이터 검사, 압축, 파일 속성 유지, 복사 재시도 등의 작업을 진행할 수 있습니다. COSDistCp는 기본적으로 대상에 동일한 이름의 파일이 이미 존재하는 경우 덮어쓰기 합니다. 파일 마이그레이션 혹은 검사 실패 시 해당 파일은 복사 실패되며, 임시 디렉터리에 마이그레이션 실패 파일 정보를 기록합니다. 원본 디렉터리에 파일이 추가되었거나 파일 내용이 변경된 경우, skipMode 또는 diffMode로 파일 길이를 비교하거나 CRC 검사 값을 통해 데이터 검사 및 파일 증분 마이그레이션을 진행할 수 있습니다.


## 매개변수 설명

hadoop 사용자에서 `hadoop jar cos-distcp-${version}.jar --help` 명령어를 사용해 COSDistCp가 지원하는 매개변수 옵션을 조회할 수 있으며, 여기서 `${version}`은 버전 넘버입니다. 다음은 현재 버전 COSDistCp의 매개변수 설명입니다.


|                속성 키                | 설명                                                                                                                                                                                                                  |              기본값              | 필수 여부 |
|:---------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------:|:----:|
|              --help               | COSDistCp가 지원하는 매개변수를 출력합니다<br> 예: --help                                                                                                                                                                                  |               None               |  No   |
|          --src=LOCATION           | 복사할 데이터의 위치입니다. 이는 HDFS 또는 COS 위치일 수 있습니다.<br> 예: --src=hdfs://user/logs/                                                                                                                                                          |               None               |  Yes   |
|          --dest=LOCATION          | 데이터의 대상입니다. 이는 HDFS 또는 COS 위치일 수 있습니다.<br> 예: --dest=cosn://examplebucket-1250000000/user/logs                                                                                                                                |               None               |  Yes   |
|       --srcPattern=PATTERN        | 소스 위치에서 파일을 필터링하는 정규식입니다.<br>예: `--srcPattern='.*\.log$'`<br>**참고: 별표(`*`)가 shell에서 구문 분석되는 경우 매개 변수를 작은따옴표로 묶습니다**                                                                                                                      |               None               |  No   |
|        --taskNumber=VALUE         | 복사 스레드 수. 예: --taskNumber=10                                                                                                                                                                                          |              10               |  No   |
|       --workerNumber=VALUE        | 복사 스레드 수입니다. COSDistCp는 이 값 세트를 기반으로 각 복사 프로세스에 대해 복사 스레드 풀을 생성합니다.<br>예: --workerNumber=4                                                                                                                                                      |               4               |  No   |
|      --filesPerMapper=VALUE       | 각 Mapper에 입력되는 파일 수입니다.<br>예: --filesPerMapper=10000                                                                                                                                                                    |            500000             |  No   |
|         --groupBy=PATTERN         | 정규식과 일치하는 텍스트 파일을 연결하는 정규식입니다</br>예: --groupBy='.\*group-input/(\d+)-(\d+).\*'                                                                                                                                                   |               None               |  No   |
|        --targetSize=VALUE         | 생성할 파일의 크기(MB)입니다. 이 매개변수는 --groupBy와 함께 사용됩니다.</br>예: --targetSize=10                                                                                                                                                             |               None               |  No   |
|       --outputCodec=VALUE        | 출력 파일의 압축 방법. 유효한 값: gzip, lzo, snappy, none, keep. 여기: </br> 1. keep: 원본 파일의 압축 방식을 유지함을 나타냅니다<br>2. none: 파일 확장자를 기준으로 파일의 압축을 푼다는 것을 나타냅니다</br>예: --outputCodec=gzip </br>**참고: /dir/test.gzip 및 /dir/test.gz 파일이 있는 경우, 출력 형식을 lzo로 지정하면 /dir/test.lzo만 유지됩니다** |             keep              |  No   |
|         --deleteOnSuccess         | 소스 파일이 대상 디렉터리에 성공적으로 복사된 직후 소스 파일을 삭제합니다.</br>예: --deleteOnSuccess，</br>**참고: v1.7 이상에서는 더 이상 이 매개변수를 제공하지 않습니다. 데이터를 성공적으로 마이그레이션하고 확인을 위해 --diffMode를 사용한 후 소스 파일 시스템에서 데이터를 삭제하는 것이 좋습니다.**                                                                                                |             false             |  No   |
| --multipartUploadChunkSize=VALUE  | Hadoop-COS 플러그인을 사용하여 COS로 전송된 멀티파트 업로드 부분의 크기(MB)입니다. COS는 최대 10000개의 파트를 지원합니다. 파일 크기에 따라 값을 설정할 수 있습니다.</br>예: --multipartUploadChunkSize=20                                                                                              |              8MB              |  No   |
|     --cosServerSideEncryption     | COS 서버 측 암호화에 SSE-COS를 사용할지 여부를 지정합니다</br>예: --cosServerSideEncryption                                                                                                                                                   |             false             |  No   |
|      --outputManifest=VALUE       | 대상 위치에 복사된 모든 파일 목록이 포함된 파일(Gzip 압축)을 생성합니다</br>예: --outputManifest=manifest.gz                                                                                                                                        |               None               |  No   |
|     --requirePreviousManifest     | 이 매개변수가 true로 설정되면 증분 복사에 --previousManifest=VALUE를 지정해야 합니다</br>예: --requirePreviousManifest                                                                                                                                           |             false             |  No   |
|    --previousManifest=LOCATION    | 이전 복사 작업 중에 생성된 매니페스트 파일입니다<br>예: --previousManifest=cosn://examplebucket-1250000000/big-data/manifest.gz                                                                                                                        |               None               |  No   |
|        --copyFromManifest         | --previousManifest에 지정된 파일을 대상 파일 시스템에 복사합니다. 이것은 previousManifest=LOCATION과 함께 사용됩니다<br>예: --copyFromManifest                                                                                                                    |             false             |  No   |
|       --storageClass=VALUE       | 사용할 스토리지 유형입니다. 유효한 값은 STANDARD, STANDARD_IA, ARCHIVE, DEEP_ARCHIVE, INTELLIGENT_TIERING입니다. 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. |   None   |    No    |
|    --srcPrefixesFile=LOCATION     | 한 줄에 하나의 디렉터리씩 소스 디렉터리 목록을 포함하는 로컬 파일입니다.</br>예: --srcPrefixesFile=file:///data/migrate-folders.txt                                                                                                                                 |               None               |  No   |
|         --skipMode=MODE          | 파일 복사 전 원본 파일과 대상 파일이 동일한지 확인합니다. 동일하면 파일을 건너뜁니다. 유효한 값은 none(확인 안 함), length (길이), checksum(CRC 값), length-mtime(길이+mtime 값) 및 length-checksum(길이 + CRC 값)입니다.</br>예: --skipMode=length                                                                    |        length-checksum        |  No   |
|         --checkMode=MODE         | 복사가 완료되면 원본 파일과 대상 파일이 동일한지 확인합니다. 유효한 값은 none(확인 안 함), length (길이), checksum(CRC 값), length-mtime(길이+mtime 값) 및 length-checksum(길이 + CRC 값)입니다.<br/>예: --checkMode=length-checksum                                                          |        length-checksum        |  No   |
|          --diffMode=MODE          | 소스 및 대상 디렉터리에서 다른 파일 목록을 얻기 위한 규칙을 지정합니다. 유효한 값은 length (길이), checksum(CRC 값), length-mtime(길이+mtime 값) 및 length-checksum(길이 + CRC 값)입니다.</br>예: --diffMode=length-checksum                                                                             |               None               |  No   |
|       --diffOutput=LOCATION       | diffMode에서 HDFS 출력 디렉터리를 지정합니다. 이 디렉터리는 비어 있어야 합니다.<br/>예: --diffOutput=/diff-output                                                                                                                                                  |               None               |  No   |
|      --cosChecksumType=TYPE       | Hadoop-COS 플러그인에서 사용하는 CRC 알고리즘을 지정합니다. 유효한 값은 CRC32C 및 CRC64입니다.<br/>예: --cosChecksumType=CRC32C                                                                                                                                      |            CRC32C             |  No   |
|      --preserveStatus=VALUE      | 원본 파일의 user, group, permission, xattr, timestamps 메타데이터를 대상 파일에 복사할지 여부를 지정합니다. 유효한 값은 문자 ugpxt(각각 user, group, permission, xattr, timestamps의 영어 이니셜)의 조합입니다.<br/>예: --preserveStatus=ugpt                                                           |               None               |  No   |
|          --ignoreSrcMiss          | 매니페스트 파일에 존재하지만 복사 중에 찾을 수 없는 파일을 무시합니다.                                                                                                                                                                                               |             false             |  No   |
|    --promGatewayAddress=VALUE     | MapReduce 작업의 Counter 데이터를 푸시하기 위한 Prometheus PushGateway 주소 및 포트를 지정합니다.                                                                                                                                                     |               None               |  No   |
| --promGatewayDeleteOnFinish=VALUE | 지정된 작업이 완료되면 Prometheus PushGateway에서 JobName 메트릭을 삭제할지 여부입니다</br>예: --promGatewayDeleteOnFinish=true                                                                                                                           |             true              |  No   |
|    --promGatewayJobName=VALUE     | Prometheus PushGateway에 보고할 JobName 입니다</br>예: v --promGatewayJobName=cos-distcp-hive-backup                                                                                                                          |               None               |  No   |
|    --promCollectInterval=VALUE    | MapReduce 작업 Counter 정보를 수집하는 간격(ms)입니다 </br>예: --promCollectInterval=5000                                                                                                                                            |             5000              |  No   |
|         --promPort=VALUE          | Prometheus 메트릭을 노출하는 Server 포트입니다 <br>예: --promPort=9028                                                                                                                                                            |               None               |  No   |
|      --enableDynamicStrategy      | 동적 작업 할당 정책을 활성화하여 더 빠른 마이그레이션으로 더 많은 파일을 마이그레이션하는 작업을 수행합니다. </br>**참고: 이 모드에는 특정 제한이 있습니다. 예를 들어 프로세스가 예외적인 경우 작업 카운터가 부정확할 수 있습니다. 따라서 --diffMode를 사용하여 마이그레이션 후 데이터를 확인하십시오.** </br>예: --enableDynamicStrategy                                                                                |             false             |  No   |
|        --splitRatio=VALUE         | Dynamic Strategy의 분할 비율입니다. splitRatio가 높을수록 작업 세분성이 작음을 나타냅니다.</br>예: --splitRatio=8                                                                                                                                              |               8               |  No   |
|         --localTemp=VALUE         | Dynamic Strategy에 의해 생성된 작업 파일을 저장할 로컬 폴더입니다</br>예: --localTemp=/tmp                                                                                                                                                       |             /tmp              |  No   |
|  --taskFilesCopyThreadNum=VALUE   | Dynamic Strategy에 의해 생성된 작업 파일을 HDFS에 복사하기 위한 동시성 수 입니다</br>예: --taskFilesCopyThreadNum=32                                                                                                                                        |              32               |  No   |
|        --statsRange=VALUE         | 통계 범위입니다</br>예: ---statsRange=0,1mb,10mb,100mb,1gb,10gb,inf                                                                                                                                                        | 0,1mb,10mb,100mb,1gb,10gb,inf |  No   |
|         --printStatsOnly          | 데이터를 복사하지 않고 파일 크기 분포에 대한 통계만 수집합니다</br>예: --printStatsOnly                                                                                                                                                                       |               None               |  No   |
|            --bandWidth            | 마이그레이션된 각 파일을 읽기 위한 최대 대역폭(MB/s)입니다. 기본값: -1, 읽기 대역폭에 제한이 없음을 나타냅니다.</br>예: --bandWidth=10                                                                                                                                                          |               None               |  No   |
|             --jobName             | 마이그레이션 작업 이름입니다</br>예: --jobName=cosdistcp-to-warehouse                                                                                                                                                                  |               None               |  No   |
|   --compareWithCompatibleSuffix   | --skipMode 및 --diffMode 매개변수를 사용할 때 소스 파일 확장자 gzip을 gz로, lzop을 lzo로 변경할지 여부입니다.</br>예: --compareWithCompatibleSuffix                                                                                                    |               None               |  No   |
|             --delete              | 원본 디렉터리에는 있지만 대상 디렉터리에는 없는 파일을 별도의 trash 디렉터리로 옮기고 원본 디렉터리와 대상 디렉터리 간의 파일 일관성을 보장하기 위해 파일 목록을 생성합니다.</br>참고: 이 매개변수는 --diffMode와 함께 사용할 수 없습니다                                                                                                                           |    None   |  No   |
|          --deleteOutput           | delete에 대한 HDFS 출력 디렉터리를 지정합니다. 이 디렉터리는 비어 있어야 합니다.<br/>예: --deleteOutput=/dele-output                                                                                                                                                   |  None   |  No   |

## 사용 예시

### help 옵션 보기

매개변수 `--help`로 명령어를 실행해 COSDistCp에서 지원하는 매개변수를 조회합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --help
```
상기 명령어 중 `${version}`은 COSDistCp의 버전 넘버입니다. 예를 들어 1.0 버전의 COSDistCp jar 패키지 이름은 cos-distcp-1.0.jar입니다.

### 마이그레이션할 파일의 크기 분포 정보 통계

매개변수 `--printStatsOnly` 및 `--statsRange=VALUE`로 명령어를 실행하여 마이그레이션할 파일의 크기 분포 정보를 출력합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /wookie/data --dest cosn://examplebucket-1250000000/wookie/data --printStatsOnly  --statsRange=0,1mb,10mb,100mb,1gb,10gb,inf

Copy File Distribution Statistics:
Total File Count: 4
Total File Size: 1190133760
| SizeRange         | TotalCount          | TotalSize           |
| 0MB ~ 1MB         | 0(0.00%)            | 0(0.00%)            |
| 1MB ~ 10MB        | 1(25.00%)           | 1048576(0.09%)      |
| 10MB ~ 100MB      | 1(25.00%)           | 10485760(0.88%)     |
| 100MB ~ 1024MB    | 1(25.00%)           | 104857600(8.81%)    |
| 1024MB ~ 10240MB  | 1(25.00%)           | 1073741824(90.22%)  |
| 10240MB ~ LONG_MAX| 0(0.00%)            | 0(0.00%)            |
```

### 마이그레이션할 파일의 원본 디렉터리와 대상 디렉터리 지정

매개변수 `--src`와 `--dest`로 명령어를 실행하며, 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse
```


기본적으로 COSDistCp는 복사에 실패한 파일에 대해 5번 재시도합니다. 복사가 계속 실패하면 이 파일은 /tmp/${randomUUID}/output/failed/ 디렉터리에 기록됩니다. 여기서 ${randomUUID}는 임의의 문자열입니다. 실패한 파일 정보를 기록한 후 COSDistCp는 나머지 파일을 계속 마이그레이션하며 일부 파일의 마이그레이션 실패로 인해 마이그레이션 작업이 실패하지 않습니다. 마이그레이션 작업이 완료되면 COSDistcp는 카운터 정보를 출력하고(작업 제출 시스템이 MapReduce 작업의 제출에서 INFO 로그 출력으로 설정되어 있는지 확인하십시오), 파일 마이그레이션 실패 여부를 판단하며, 마이그레이션 실패한 경우 작업을 제출한 클라이언트에 이상 경고가 발생합니다.

다음 유형의 원본 파일 정보는 출력 파일에 포함되어 있습니다.
1. 원본 파일의 리스트가 존재하지만, 복사 시 원본 파일이 존재하지 않는 경우 SRC_MISS로 기록
2. 기타 원인으로 인해 복사 실패 시 모두 COPY_FAILED로 기록

복사 명령어를 다시 실행하여 증분 마이그레이션을 수행할 수 있습니다. 다음 명령어를 통해 MapReduce 작업의 로그를 획득하여 파일 복사 실패 원인을 확인할 수 있습니다. application_1610615435237_0021은 애플리케이션 ID입니다.
```plaintext
yarn logs -applicationId application_1610615435237_0021 > application_1610615435237_0021.log
```

### Counters 조회 

복사 작업 종료 시 파일 복사 통계 정보를 출력하며, 관련 카운터는 다음과 같습니다.

```plaintext
CosDistCp Counters
        BYTES_EXPECTED=10198247
        BYTES_SKIPPED=10196880
        FILES_COPIED=1
        FILES_EXPECTED=7
        FILES_FAILED=1
        FILES_SKIPPED=5
```

파일 복사의 통계 정보 관련 설명은 다음과 같습니다.

|  통계 항목   |  설명  |
| -----|-----|
|  BYTES_EXPECTED  | 원본 디렉터리 통계에 따라 복사할 파일의 총 크기, 단위: 바이트   |
|  FILES_EXPECTED  | 원본 디렉터리 통계에 따라 복사할 파일 수. 디렉터리 파일 포함   |
|  BYTES_SKIPPED  | 길이 또는 검사합이 동일하여 복사하지 않은 파일의 총 크기, 단위: 바이트  |
|  FILES_SKIPPED  | 길이 또는 검사합이 동일하여 복사하지 않은 원본 파일 수  |
|  FILES_COPIED  | 복사 완료한 원본 파일 수   |
|  FILES_FAILED  | 복사 실패한 원본 파일 수   |
|  FOLDERS_COPIED  | 복사 완료한 디렉터리 수   |
|  FOLDERS_SKIPPED  | 건너뛴 디렉터리 수   |


### 복사 프로세스의 수 및 각 복사 프로세스의 복사 스레드 수 지정

매개변수 `--taskNumber` 및 `--workersNumber`로 명령어를 실행합니다. COSDistCp는 멀티 프로세스+멀티 스레드의 복사 구조를 사용하며, 다음 작업이 가능합니다.
- `--taskNumber`를 통해 복사 프로세스 수 지정
- `--workerNumber`를 통해 각 복사 프로세스 내의 복사 스레드 수 지정

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse --taskNumber=10 --workerNumber=5
```

### 검사 값이 동일한 파일은 건너뛰고 증분 마이그레이션 수행

'--skipMode' 매개변수를 사용하여 명령어를 실행합니다. 길이와 검사합이 동일한 원본 및 대상 파일의 복사본은 건너뜁니다. 기본값은 length-checksum입니다.
```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse  --skipMode=length-checksum
```

`--skipMode` 옵션은 파일 복사 전에 원본 파일과 대상 파일의 일치 여부를 검사하는 데 사용하며, 일치할 경우 건너뜁니다. none(검사 안 함), length(길이), checksum(CRC 값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.

원본과 대상 파일 시스템의 검사 및 알고리즘이 일치하지 않는 경우 원본 파일의 새로운 검사합을 계산합니다. 원본이 HDFS일 경우 다음 방식으로 HDFS 원본의 COMPOSITE-CRC32C 검사 알고리즘 지원 여부를 확인할 수 있습니다.

```plaintext
hadoop fs  -Ddfs.checksum.combine.mode=COMPOSITE_CRC -checksum /data/test.txt
/data/test.txt  COMPOSITE-CRC32C        6a732798
```

### 마이그레이션 후 데이터 검사 및 증분 마이그레이션

매개변수 `--diffMode` 및 `--diffOutput`으로 명령어를 실행합니다.
- `--diffMode`의 옵션 값은 length와 length-checksum이 있습니다.
 - `--diffMode=length`는 파일 크기 동일 여부에 따라 변경 파일 리스트를 획득합니다.
 - `--diffMode=length-checksum`은 파일 크기 및 CRC 검사 동일 여부에 따라 변경 파일 리스트를 획득합니다.
- `--diffOutput`은 diff 작업의 출력 디렉터리를 지정합니다.
대상 파일 시스템이 COS이고 원본 파일 시스템의 CRC 알고리즘이 다른 경우, COSDistCp는 원본 파일을 가져와 대상 파일 시스템의 CRC를 계산하여 동일한 CRC 알고리즘 값을 비교합니다. 다음 예시에서는 마이그레이션이 완료된 후 --diffMode 매개변수를 사용하여 파일 크기 및 CRC 값에 따라 원본 파일과 대상 파일이 동일한지 검사합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

상기 명령어가 성공적으로 실행되면 원본 파일 시스템 파일 리스트를 기반으로 한 카운터 정보가 출력됩니다(작업 제출 시스템이 MapReduce 작업의 제출에서 INFO 로그 출력으로 구성되어 있는지 확인하십시오). 카운터 정보에 따라 원본과 대상이 동일한지 분석할 수 있습니다. 카운터 정보 관련 설명은 다음과 같습니다.

1. 원본 및 대상 파일이 동일한 경우, SUCCESS로 기록
2. 대상 파일이 존재하지 않을 경우 DEST_MISS로 기록
3. 원본 디렉터리의 리스트가 존재하지만, 검사 시 원본 파일이 존재하지 않는 경우 SRC_MISS로 기록
4. 원본 파일과 대상 파일 크기가 다른 경우 LENGTH_DIFF로 기록
5. 원본 파일과 대상 파일의 CRC 알고리즘 값이 다른 경우 CHECKSUM_DIFF로 기록
6. 읽기 권한 부족 등의 사유로 diff 작업에 실패하는 경우 DIFF_FAILED로 기록
7. 원본은 디렉터리, 대상은 파일인 경우, TYPE_DIFF로 기록

또한 COSDistcp는 HDFS의 `/tmp/diff-output/failed` 디렉터리에(1.0.5 및 이전 버전은 /tmp/diff-output임) 변경 파일 리스트를 생성합니다. 다음 명령어를 사용하여 SRC_MISS 이외의 변경 파일 리스트를 가져올 수 있습니다.

```plaintext
hadoop fs -getmerge /tmp/diff-output/failed diff-manifest
grep -v '"comment":"SRC_MISS"' diff-manifest |gzip > diff-manifest.gz
```

다음 명령어를 실행해 변경 파일 리스트에 따라 증분 마이그레이션을 진행할 수 있습니다.

```plaintext
hadoop  jar cos-distcp-${version}.jar --taskNumber=20 --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --previousManifest=file:///usr/local/service/hadoop/diff-manifest.gz --copyFromManifest
```
증분 마이그레이션이 완료된 후 --diffMode 매개변수와 함께 명령어를 다시 실행하여 파일이 완전히 일치하는지 검사합니다.

### 원본 파일과 대상 파일이 동일한 CRC 보유 여부 검사

`--checkMode` 매개변수로 명령어를 실행하고 파일 복사가 완료되면 원본 파일과 대상 파일의 길이와 검사합이 동일한지 검사합니다. 기본값은 length-checksum입니다.

비 COS 파일 시스템에서 COS로 동기화할 때, 원본의 CRC 알고리즘과 Hadoop-COS의 CRC 알고리즘이 일치하지 않을 경우 복사 시 CRC를 계산합니다. 복사 완료 후 대상 COS 파일의 CRC를 획득하고, 계산으로 획득한 원본 파일의 CRC를 대조해 검사합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar   --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --checkMode=length-checksum
```
>! --groupBy가 지정되지 않고 --outputCodec가 기본값인 경우에 적용됩니다.


### 단일 파일의 읽기 대역폭 제한

매개변수 `--bandWidth`으로 명령을 실행합니다. 값 단위는 MB이며, 각 마이그레이션 파일의 읽기 대역폭 10MB/s로 제한합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --bandWidth=10
```

### 다중 디렉터리 동기화

로컬 파일(예: srcPrefixes.txt)을 생성하고, 해당 파일에 마이그레이션할 여러 디렉터리의 절대 경로를 파일에 추가합니다. 이러한 디렉터리 간에 부모-자식 관계가 없어야 합니다. 추가 후 cat 명령어를 통해 이를 확인할 수 있으며, 예시는 다음과 같습니다.

```plaintext
cat srcPrefixes.txt 
/data/warehouse/20181121/
/data/warehouse/20181122/
```

`--srcPrefixesFile` 매개변수를 사용하여 해당 파일을 지정하고 마이그레이션 명령어를 실행합니다.

```plaintext
hadoop jar  cos-distcp-${version}.jar --src /data/warehouse  --srcPrefixesFile file:///usr/local/service/hadoop/srcPrefixes.txt --dest  cosn://examplebucket-1250000000/data/warehouse/ --taskNumber=20
```

### 입력 파일을 정규식으로 필터링

매개변수 `--srcPattern`으로 명령어를 실행합니다. `/data/warehouse/` 디렉터리의 확장자가 .log인 로그 파일만 동기화합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse --srcPattern='.*\.log$'
```
.temp 또는 .tmp로 끝나는 파일은 마이그레이션되지 않습니다.
```
 hadoop jar cos-distcp-${version}.jar --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse/ --srcPattern='.*(?<!\.temp|\.tmp)$'
```

### Hadoop-COS의 파일 검사와 유형 지정

매개변수 `--cosChecksumType`으로 명령어를 실행합니다. 기본 값은 CRC32C이며, CRC32C와 CRC64를 선택할 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --cosChecksumType=CRC32C
```

### COS 파일의 스토리지 유형 지정

매개변수 `--storageClass`로 명령어를 실행합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest-2020-01-10.gz --storageClass=STANDARD_IA
```


### 대상 파일의 압축 유형 지정

매개변수 `--outputCodec`으로 명령어를 실행합니다. 해당 매개변수를 통해 HDFS의 데이터를 실시간으로 압축해 COS에 백업할 수 있어 스토리지 비용을 절약할 수 있습니다. 매개변수 옵션 값은 keep, none, gzip, lzop, snappy가 있으며, none은 대상 파일을 압축하지 않은 상태로 저장하고, keep은 원본 파일의 압축 상태를 유지합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/logs --dest cosn://examplebucket-1250000000/data/warehouse/logs-gzip --outputCodec=gzip
```

>! 여기에서 keep을 제외한 모든 값은 먼저 파일을 압축 해제한 후 대상 압축 유형으로 변환합니다. 따라서 keep을 제외하고는 압축 매개변수 등이 일치하지 않아 대상 파일과 원본 파일이 동일하지 않을 수 있으나 압축 해제한 파일은 동일합니다. --groupBy 미지정 및 --outputCodec가 기본값인 경우, 증분 마이그레이션에 --skipMode를 사용할 수 있으며, --checkMode를 통해 데이터 검증을 수행할 수 있습니다.
>

### 원본 파일 삭제

매개변수 `--deleteOnSuccess`로 명령을 실행합니다. `/data/warehouse` 디렉터리의 파일을 HDFS에서 COS로 동기화한 후 즉시 원본 디렉터리에서 해당 파일을 삭제합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --deleteOnSuccess
```

>! 해당 옵션을 지정하면 파일 하나의 마이그레이션이 완료될 때마다 즉시 해당하는 원본 파일을 삭제합니다. 전체 마이그레이션이 완료된 후 원본 파일을 삭제하는 것이 아니므로 신중하게 사용하십시오. 1.7 이상 버전에서는 더 이상 이 매개변수를 제공하지 않습니다.
>

### 대상 매니페스트 파일 생성 및 이전 매니페스트 출력 파일 지정

매개변수 `--outputManifest` 및 `--previousManifest`로 명령어를 실행합니다.

- `--outputManifest` 해당 옵션은 먼저 로컬에 gzip으로 압축된 manifest.gz를 생성하고 마이그레이션 완료 시 `--dest`에서 지정한 디렉터리로 이동됩니다.
- `--previousManifest`로 바로 이전의 `--outputManifest` 출력 파일을 지정하여 COSDistCp가 동일한 길이 및 크기의 파일을 건너뜁니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest  cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest.gz --previousManifest= cosn://examplebucket-1250000000/data/warehouse/manifest-2020-01-10.gz
```

>! 상기 명령어의 증분 마이그레이션은 파일 크기가 변경된 파일만 동기화할 수 있으며 파일 내용이 변경된 파일은 동기화할 수 없습니다. 파일 내용이 변경된 경우 --diffMode 사용 예시를 참고하여 파일 CRC에 따라 변경된 파일 리스트를 확인하십시오.
>


### 마이그레이션 작업 할당 정책을 동적 할당으로 지정

파일 크기 분포가 매우 고르지 못한 경우, 예시: 매우 적은 대용량 파일, 많은 소용량 파일 또는 마이그레이션 기기 부하가 상이할 경우, `--enableDynamicStrategy`를 사용하여 작업 동적 할당 정책을 활성화하여 작업 속도가 빠른 작업에 더 많은 파일을 마이그레이션하여 작업 시간을 줄일 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse    --dest  cosn://examplebucket-1250000000/data/warehouse --enableDynamicStrategy
```
마이그레이션이 완료된 후 마이그레이션된 데이터를 검사합니다.
```
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

>! 이 모드에는 제한이 있습니다. 예를 들어 프로세스가 비정상적일 때 작업 카운터가 정확하지 않을 수 있습니다. 마이그레이션이 완료된 후 데이터를 검사하려면 --diffMode를 사용하십시오.
>

### 복사 파일의 메타 정보

매개변수 `--preserveStatus`로 명령을 실행합니다. 원본 파일 또는 원본 디렉터리의 user, group, permission, timestamps(modification time, access time)를 대상 파일 또는 대상 디렉터리에 복사합니다. 이 매개변수는 HDFS에서 CHDFS로 파일을 복사할 때 적용됩니다.
예시는 다음과 같습니다.
```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --preserveStatus=ugpt
```


### Prometheus 모니터링 설정

Yarn 관리 페이지에서 마이그레이션 완료 파일 수, 바이트 수 및 기타 정보를 포함한 COSDistcp 마이그레이션 작업 카운터를 볼 수 있습니다. 마이그레이션 작업 카운터의 곡선 변화를 보다 편리하게 보려면 간단한 설정을 통해 Prometheus + Grafana 모니터링 시스템에 COSDistcp 마이그레이션 작업 카운터를 표시하고, prometheus.yml 설정 및 캡처 작업을 추가합니다.

```plaintext
- job_name: 'cos-distcp-hive-backup'
    static_configs:
      - targets: ['172.16.16.139:9028']
```

`--promPort=VALUE` 매개변수로 명령어를 실행하여 현재 MapReduce 작업의 카운터를 외부에 노출합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --promPort=9028
```

[Grafana Dashboard](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/COSDistcp-Grafana-Dashboard.json) 예시를 다운로드하여 가져옵니다. Grafana는 다음과 같이 표시됩니다.
![COSDistcp-Grafana](https://staticintl.cloudcachetci.com/yehe/backend-news/2Rc8914_2.png)


### 파일 복사 실패 시 알람
매개변수 `--completionCallbackClass`로 콜백 클래스 경로를 지정해 명령어를 실행하면, COSDistCp가 복사 작업 완료 시 수집한 작업 정보를 매개변수로 하여 콜백 함수를 실행합니다. 사용자 정의한 콜백 함수는 다음과 같은 인터페이스를 구현해야 하며, [콜백 예시 코드 다운로드](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-alarm-1.0.jar)로 이동합니다.

```plaintext
package com.qcloud.cos.distcp;
import java.util.Map;
public interface TaskCompletionCallback {
/**
 * @description: When the task is completed, the callback function is executed
 * @param jobType Copy or Diff
 * @param jobStartTime  the job start time
 * @param errorMsg  the exception error msg
 * @param applicationId the MapReduce application id
 * @param: cosDistCpCounters the job 
*/

void doTaskCompletionCallback(String jobType, long jobStartTime, String errorMsg, String applicationId, Map<String, Long> cosDistCpCounters);

/**
 *  @description: init callback config before execute
 */
void init() throws Exception;
}
```

COSDistCp 내부에 클라우드 모니터링 알람이 통합되어 있으며, 작업에 이상 경고가 발생하거나 파일 복사에 실패하는 경우 알람이 실행됩니다.

```plaintext
export alarmSecretId=SECRET-ID
export alarmSecretKey=SECRET-KEY
export alarmRegion=ap-guangzhou
export alarmModule=module
export alarmPolicyId=cm-xxx
hadoop jar cos-distcp-1.4-2.8.5.jar \
-Dfs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider \
-Dfs.cosn.userinfo.secretId=SECRET-ID \
-Dfs.cosn.userinfo.secretKey=SECRET-KEY \
-Dfs.cosn.bucket.region=ap-guangzhou \
-Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
-Dfs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
--src /data/warehouse \
--dest cosn://examplebucket-1250000000/data/warehouse/ \
--checkMode=checksum \
--completionCallbackClass=com.qcloud.cos.distcp.DefaultTaskCompletionCallback
```

상기 명령어에서 alarmPolicyId는 클라우드 모니터링 알람 정책이며, 클라우드 모니터링 콘솔에서 생성 및 설정(알람 관리>알람 설정>사용자 정의 메시지)할 수 있습니다.



## FAQ
### COSDistcp를 사용하여 HDFS 데이터 패킷을 마이그레이션하는 방법은 무엇이며, 마이그레이션 성능을 조정하고 데이터의 정확성을 보장하는 방법은 무엇입니까?
COSDistcp가 파일 마이그레이션을 완료할 때마다 checkMode에 따라 마이그레이션된 파일을 인증합니다.
```
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --taskNumber=20
```
또한 마이그레이션이 완료되면 다음 명령어를 실행하여 원본과 대상 간의 변경 파일 리스트를 조회할 수도 있습니다.
```
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

### 환경에서 Hadoop-COS를 설정하지 않은 경우, COSDistCp는 어떻게 실행하나요?

환경에서 Hadoop-COS 플러그 인을 설정하지 않은 사용자는 Hadoop 버전에 따라 해당 버전의 COSDistCp jar 패키지를 다운로드한 후 Hadoop-COS 관련 매개변수를 지정하여 복사 작업을 실행할 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar \
-Dfs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider \
-Dfs.cosn.userinfo.secretId=COS_SECRETID \
-Dfs.cosn.userinfo.secretKey=COS_SECRETKEY \
-Dfs.cosn.bucket.region=ap-guangzhou \
-Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
-Dfs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
--src /data/warehouse \
--dest cosn://examplebucket-1250000000/warehouse
```

### 일부 파일 복사에 실패했다고 복사 결과에 표시됩니다. 어떻게 처리해야 하나요?

COSDistCp는 복사 과정에서 IOException이 발생할 경우 5번 재시도하며, 5번의 재시도에도 복사에 실패하는 경우 실패한 파일 정보를 `/tmp/${randomUUID}/output/failed/` 디렉터리에 입력합니다. 여기서 ${randomUUID}는 랜덤 문자열이며, 복사에 실패하는 주요 원인은 다음과 같습니다.
1. 원본 파일이 복사 리스트에는 존재하지만, 복사 시 원본 파일이 존재하지 않는 경우 SRC_MISS로 기록
2. 작업을 요청한 사용자에게 원본 파일 읽기 또는 대상 파일 쓰기 권한이 없거나 기타 원인이 있을 경우 COPY_FAILED로 기록

로그 정보 기록에 원본 파일이 존재하지 않고 원본 파일이 확실하게 생략 가능한 경우, 다음 명령어를 통해 SRC_MISS를 제외한 변경 파일 리스트를 획득할 수 있습니다.
```plaintext
hadoop fs -getmerge /tmp/${randomUUID}/output/failed/ failed-manifest
grep -v '"comment":"SRC_MISS"' failed-manifest |gzip > failed-manifest.gz
```
SRC_MISS를 제외한 실패 파일이 존재하는 경우 `/tmp/${randomUUID}/output/logs/` 디렉터리의 오류 로그 정보 및 풀링 애플리케이션 로그를 종합하여 원인을 진단할 수 있습니다. 예를 들어, yarn 애플리케이션의 로그를 풀링하는 경우 다음 명령어를 사용할 수 있습니다.
```plaintext
yarn logs -applicationId application_1610615435237_0021 > application_1610615435237_0021.log
```
여기에서 application_1610615435237_0021은 애플리케이션 ID입니다.

### COSDistCp는 네트워크 등에 이상이 발생하는 경우 불완전 복사 파일을 생성하나요?

COSDistCp는 네트워크 이상, 원본 파일 결함, 권한 부족 등의 상황에서 대상에 원본과 동일한 크기의 파일을 생성할 수 없습니다.
- COSDistCp 1.5 버전 이하인 경우, COSDistCp는 대상에 생성한 파일에 대해 삭제를 시도합니다. 삭제에 실패하는 경우, 복사 작업을 다시 실행하여 해당 파일을 덮어쓰거나 수동으로 해당 불완전 파일을 삭제해야 합니다.
- COSDistCp 1.5 버전 이상이고 Hadoop COS 플러그 인 버전이 5.9.3 이상인 실행 환경에서 COS 복사 작업에 실패한 경우, COSDistCp는 abort 인터페이스를 호출하여 현재 업로드 중인 요청을 중지합니다. 따라서 이상 상황이 발생해도 불완전 파일이 생성되지 않습니다.
- COSDistCp 1.5 버전 이상이고 Hadoop COS 플러그 인 버전이 5.9.3 미만인 실행 환경에서는 5.9.3 이상의 버전으로 업그레이드하는 것을 권장합니다.
- COS의 대상이 아닌 경우 COSDistCp는 대상 파일에 대한 삭제를 시도합니다.

### COS 버킷에 저장 공간을 차지하며 보이지 않는 업로드 미완료 파일이 있습니다. 어떻게 해야 하나요?
시스템 이상 및 프로세스 kill 등의 요인으로 인해 COS 버킷의 일부 조각난 파일이 저장 공간을 차지할 수 있습니다. 공식 웹사이트의 [라이프사이클 문서](https://intl.cloud.tencent.com/document/product/436/14605)를 참고하여 조각 삭제 규칙을 설정하십시오.

### 마이그레이션 과정에서 메모리 오버플로우와 작업 시간 초과가 발생하는데 매개변수 최적화는 어떻게 합니까?
마이그레이션 과정에서 COSDistcp 및 COS와 CHDFS에 액세스하기 위한 툴은 자체 로직에 따라 일부 메모리를 점유합니다. 메모리 오버플로우 및 작업 시간 초과를 방지하기 위해 다음과 같은 MapReduce 작업의 일부 매개변수 조정을 수행할 수 있습니다. 예시:
```
hadoop jar cos-distcp-${version}.jar -Dmapreduce.task.timeout=18000 -Dmapreduce.reduce.memory.mb=8192 --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse  
```
이 중, 작업 시간 초과 시간 mapreduce.task.timeout을 18000초로 조정하여 초대형 파일을 복사할 때 작업 시간 초과를 방지합니다. 메모리 오버플로우를 방지하기 위해 Reduce 프로세스의 메모리 공간 mapreduce.reduce.memory.mb를 8GB로 조정합니다.

### 전용 회선 마이그레이션을 통해 마이그레이션 작업의 마이그레이션 대역폭을 제어하는 ​​방법은 무엇입니까?
COSDistcp 마이그레이션의 총 대역폭 제한 계산 공식은 taskNumber * workerNumber * bandWidth이며, workerNumber를 1로 설정하고 동시 마이그레이션의 수는 매개변수 taskNumber에 의해 제어되고 단일 동시성의 대역폭은 매개변수 bandWidth에 의해 제어됩니다.



