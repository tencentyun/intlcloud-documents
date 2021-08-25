## 기능 설명

COSDistCp는 MapReduce를 기반으로 하는 분산형 파일 복사 툴로, 주로 HDFS와 COS 간의 데이터 복사에 사용합니다. 주요 기능은 다음과 같습니다.
- 길이, CRC 검사합에 따라 파일의 증분 마이그레이션, 실시간 검증 진행 및 변경 파일 리스트 획득
- 원본 디렉터리 파일에 정규식 필터링 진행
- 원본 디렉터리 파일을 압축 해제하여 설정된 압축 포맷으로 전환
- 정규식을 기반으로 텍스트 파일 취합
- 원본 파일 및 원본 디렉터리의 사용자, 그룹, 확장 속성 및 시간 보관
- 알람 및 Prometheus 모니터링 설정
- 마이그레이션 파일의 크기 분포 통계
- 읽기 대역폭에 속도 제한 설정

## 사용 환경

#### 시스템 환경

Linux 시스템 지원

#### 소프트웨어 종속

Hadoop-2.6.0 버전 이상, Hadoop-COS 플러그 인 5.9.3 버전 이상

## 다운로드와 설치

#### COSDistCp jar 패키지 획득

- Hadoop 2.x 사용자는 [cos-distcp-1.6-2.8.5.jar 패키지](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.6-2.8.5.jar)를 다운로드하여 jar 패키지의 [MD5 검증 값](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.6-2.8.5-md5.tx)t에 따라 다운로드한 jar 패키지가 완벽한지 확인합니다.
- Hadoop 3.x 사용자는 [cos-distcp-1.6-3.1.0.jar 패키지](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.6-3.1.0.jar)를 다운로드하여 jar 패키지의 [MD5 검증 값](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.6-3.1.0-md5.txt)에 따라 다운로드한 jar 패키지가 완벽한지 확인합니다.

#### 설치 설명

Hadoop 환경에서 [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884)를 설치하면 COSDistCp 툴을 실행할 수 있습니다.


## 원리 설명

COSDistCp는 MapReduce를 기반으로 프레임워크를 실현하며, Mapper에서 파일을 분할하고 Reducer 프로세스에서 멀티 스레드를 사용해 파일 복사, 압축, 데이터 검증, 파일 속성 유지, 재시도 등의 작업을 진행합니다. 기본적으로 타깃에 동일한 이름의 파일이 이미 존재하는 경우 덮어씁니다. 파일 마이그레이션 혹은 검증 실패 시 해당 파일은 복사에 실패하며 임시 디렉터리에 마이그레이션에 실패한 파일 정보를 기록합니다. 원본 디렉터리에 파일이 추가되었거나 파일 내용이 변경된 경우 skipMode 또는 diffMode로 파일 길이를 비교하거나 CRC 검증 값을 통해 파일을 증분 마이그레이션할 수 있습니다.


## 매개변수 설명

`hadoop jar cos-distcp-${version}.jar --help` 명령어를 사용해 COSDistCp가 지원하는 매개변수 옵션을 조회할 수 있으며, 여기서 `${version}`은 버전 넘버입니다. 다음은 COSDistCp 매개변수 설명입니다.


|              속성 키              | 설명                                                         | 기본값 | 필수 입력 여부 |
| :------------------------------: | :----------------------------------------------------------- | :----: | :------: |
|              --help              | COSDistCp 출력에 지원하는 매개변수 옵션<br> 예시: --help               |   없음   |    아니요    |
|          --src=LOCATION          | 복사하는 원본 디렉터리 지정, HDFS 또는 COS 경로 가능<br> 예시: --src=hdfs://user/logs/ |   없음   |    예    |
|         --dest=LOCATION          | 복사하는 타깃 디렉터리 지정, HDFS 또는 COS 경로 가능<br> 예시: --dest=cosn://examplebucket-1250000000/user/logs |   없음   |    예 |
|       --srcPattern=PATTERN | 정규식으로 원본 디렉터리에 있는 파일 필터링<br>예시: `--srcPattern='.*.log'`<br>**주의: `*`가 shell에 의해 해석되지 않도록 매개변수는 작은따옴표로 묶어야 합니다.** | 없음 | 아니요 |
| --taskNumber=VALUE | 복사 프로세스 수 지정. 예: --taskNumber=10 | 10 | 아니오 |
| --workerNumber=VALUE | 복사 스레드 수 지정. COSDistCp는 각 복사 프로세스에서 해당 매개변수 크기의 복사 스레드 풀을 생성합니다.<br>예: --workerNumber=4 | 4 | 아니요 |
|      --filesPerMapper=VALUE      | 각 Mapper의 입력 파일의 행 개수 지정<br>예시: --filesPerMapper=10000 | 500000 |    아니요    |
|        --groupBy=PATTERN         | 정규식을 지정해 파일 취합</br>예시: --groupBy='.\*group-input/(\d+)-(\d+).\*' |   없음   |    아니요    |
|        --targetSize=VALUE        | 타깃 파일의 크기 지정. 단위: MB, --groupBy와 함께 사용합니다.</br>예시: --targetSize=10 |   없음   |    아니요    |
|       --outputCodec=VALUE        | 출력 파일의 압축 방식 지정. gzip, lzo, snappy, none, keep을 선택할 수 있습니다. </br> 1. keep: 기존 파일의 압축 방식 유지<br>2. none: 파일 확장자에 따라 파일 압축 해제</br>예시: --outputCodec=gzip |  keep  |    아니요    |
|        --deleteOnSuccess         | 원본 파일을 타깃 디렉터리로 복사 완료한 경우 즉시 원본 파일을 제거하도록 지정</br>예시: --deleteOnSuccess | false  |    아니요    |
| --multipartUploadChunkSize=VALUE | Hadoop-COS 플러그 인에서 COS로 파일 전송 시 멀티파트 크기 지정. COS는 최대 10000개의 파트 수를 지원하며 파일 크기에 따라 파트 크기를 조정할 수 있습니다. 단위: MB, 기본 값: 8MB</br>예시: --multipartUploadChunkSize=20 |  8MB   |    아니요    |
|    --cosServerSideEncryption     | 파일을 COS로 업로드 시 SSE-COS를 암호화/복호화 알고리즘으로 사용 지정</br>예시: --cosServerSideEncryption | false  |    아니요    |
|      --outputManifest=VALUE      | 복사 완료 시 타깃 디렉터리에 이번 복사의 타깃 파일 정보 리스트(GZIP 압축) 생성 지정</br>예시:--outputManifest=manifest.gz |   없음   |    아니요    |
|    --requirePreviousManifest     | --previousManifest=VALUE 매개변수 지정을 요청해 증분 복사 진행</br>예시: --requirePreviousManifest | false  |    아니요    |
|   --previousManifest=LOCATION    | 이전에 복사하여 생성된 타깃 파일 정보<br>예시: --previousManifest=cosn://examplebucket-1250000000/big-data/manifest.gz |   없음   |    아니요    |
|        --copyFromManifest        | --previousManifest=LOCATION과 함께 사용 시, --previousManifest의 파일을 타깃 파일 시스템으로 복사 가능<br>예시: --copyFromManifest | false  |    아니요    |
|       --storageClass=VALUE       | 객체 스토리지 유형 지정. STANDARD, STANDARD_IA, ARCHIVE, DEEP_ARCHIVE, INTELLIGENT_TIERING 중 선택할 수 있으며, 지원되는 스토리지 유형 및 소개에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. |   없음   |    아니요    |
|    --srcPrefixesFile=LOCATION    | 각 행마다 복사할 원본 디렉터리가 포함된 로컬 파일 지정</br>예시: --srcPrefixesFile=file:///data/migrate-folders.txt |   없음   |    아니요    |
|         --skipMode=MODE          | 파일 복사 전 원본 파일과 타깃 파일의 일치 여부를 검증하며, 일치할 경우 건너뜁니다. none(검증 안 함), length (길이), checksum(CRC 값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.</br>예시: --skipMode=length |  length-checksum  |    아니요    |
|         --checkMode=MODE         | 파일 복사 완료 시 원본 파일과 타깃 파일의 일치 여부를 검증하며, 일치하지 않을 경우 복사를 중지합니다. none(검증 안 함), length (길이), checksum(CRC 값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.<br/>예시: --checkMode=length-checksum |  length-checksum  |    아니요    |
|         --diffMode=MODE          | 변경 파일 리스트를 획득하는 기준 지정. length(길이), checksum(CRC 값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.</br>예시: --diffMode=length-checksum |   없음   |    아니요    |
|      --diffOutput=LOCATION       | 변경 파일 리스트의 출력 디렉터리 지정. 해당 출력 디렉터리는 반드시 비어 있어야 합니다.<br/>예시: --diffOutput=/diff-output |   없음   |    아니요    |
|      --cosChecksumType=TYPE      | Hadoop-COS 플러그 인이 사용하는 CRC 알고리즘 지정. CRC32C와 CRC64 중 선택할 수 있습니다.<br/>예시: --cosChecksumType=CRC32C | CRC32C |    아니요    |
|      --preserveStatus=VALUE      | 원본 파일의 user, group, permission, xattr, timestamps 메타 정보를 타깃 파일에 복사할지 여부 설정. ugpxt(user, group, permission, xattr, timestamps의 영어 이니셜)로 설정할 수 있습니다.<br/>예시: --preserveStatus=ugpt |   없음   |    아니요    |
|      --ignoreSrcMiss      | 파일 리스트에 존재하나 작업 시 존재하지 않는 파일 생략 |   false   | 아니요       |
| --promGatewayAddress=VALUE | MapReduce 작업에 의해 실행된 Counter 데이터가 푸시되는 Prometheus PushGateway 주소 및 포트 지정 | 없음 | 아니오 |
| --promGatewayDeleteOnFinish=VALUE | 지정된 작업이 완료되면 Prometheus PushGateway 중의 JobName의 메트릭 집합 삭제</br> 예: --promGatewayDeleteOnFinish=true | true | 아니오 |
| --promGatewayJobName=VALUE | Prometheus PushGateway에 리포트되는 JobName 지정 </br>예: --promGatewayJobName=cos-distcp-hive-backup | 없음 | 아니오 |
| --promCollectInterval=VALUE | MapReduce 작업 Counter 정보 수집 간격 지정, 단위: ms </br>예: --promCollectInterval=5000 | 5000 | 아니요 |
| --promPort=VALUE | Prometheus 메트릭을 외부 서버 포트에 노출하도록 지정 <br>예: --promPort=9028 | 없음 | 아니요 |
| --enableDynamicStrategy | 작업 동적 할당 정책을 사용하도록 지정하여 마이그레이션 속도가 빠른 작업이 더 많은 파일을 마이그레이션할 수 있도록 함</br>예: --enableDynamicStrategy | false | 아니요 |
| --splitRatio=VALUE | Dynamic Strategy 의 분할 비율 지정. splitRatio 값이 클수록 작업 세분성이 작아짐</br>예: --splitRatio=8 | 8 | 아니요 |
| --localTemp=VALUE | Dynamic Strategy이 생성한 작업 정보 파일이 위치하는 로컬 폴더 지정</br>예: --localTemp=/tmp | /tmp | 아니요 |
| --taskFilesCopyThreadNum=VALUE | Dynamic Strategy 작업 정보 파일을 HDFS로 복사할 때의 동시성 정도 지정 </br>예: --taskFilesCopyThreadNum=32 | 32 | 아니요 |
| --statsRange=VALUE | 통계 구간 범위 지정</br> 예: ---statsRange=0,1mb,10mb,100mb,1gb,10gb,inf | 0,1mb,10mb,100mb,1gb,10gb,inf | 아니요 |
| --printStatsOnly | 마이그레이션할 파일 크기의 배포 정보만 통계하고 데이터를 마이그레이션하지 않음</br>예: --printStatsOnly | 없음 | 아니요 |


## 사용 예시

### help 옵션 조회

매개변수 `--help`로 명령을 실행해 COSDistCp에서 지원하는 매개변수를 조회합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --help
```
위 명령어 중 `${version}`은 COSDistCp의 버전 넘버입니다. 예를 들어 1.0 버전의 COSDistCp jar 패키지 이름은 cos-distcp-1.0.jar입니다.

### 마이그레이션할 파일의 원본 디렉터리와 타깃 디렉터리 지정

매개변수 `--src`와 `--dest`로 명령을 실행하며, 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse
```

COSDistCp는 기본적으로 파일 복사 실패 시 5번 재시도하며 계속 실패할 경우, 실패 파일 정보를 /tmp/${randomUUID}/output/failed/ 디렉터리에 입력합니다. 여기서 ${randomUUID}는 랜덤 문자열입니다.

다음 유형의 원본 파일 정보는 출력 파일에 포함되어 있습니다.
1. 원본 파일의 리스트가 존재하지만, 복사 시 원본 파일이 존재하지 않는 경우 SRC_MISS로 기록
2. 기타 원인으로 인해 복사 실패 시 모두 COPY_FAILED로 기록

다음 명령어를 통해 SRC_MISS를 제외한 변경 파일 리스트를 획득할 수 있습니다.
```plaintext
hadoop fs -getmerge /tmp/${randomUUID}/output/failed/ failed-manifest
grep -v '"comment":"SRC_MISS"' failed-manifest |gzip > failed-manifest.gz
```

다음 명령어를 실행하여 실패 파일 리스트에 따라 마이그레이션을 재시도합니다.
```plaintext
hadoop  jar cos-distcp-${version}.jar --taskNumber=20 --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --previousManifest=file:///usr/local/service/hadoop/failed-manifest.gz --copyFromManifest
```

다음 명령어를 통해 MapReduce 작업의 로그를 획득하여 파일 복사 실패 원인을 확인할 수 있습니다. 여기서 application_1610615435237_0021은 애플리케이션 ID입니다.
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
|  BYTES_EXPECTED|  원본 디렉터리 통계에 따라 복사할 파일의 총 크기, 단위: 바이트|  
|  FILES_EXPECTED|  원본 디렉터리 통계에 따라 복사할 파일 수|  
|  BYTES_SKIPPED|  길이 또는 검사합이 동일하여 복사하지 않은 파일의 총 크기, 단위: 바이트|  
|   FILES_SKIPPED|  길이 또는 검사합이 동일하여 복사하지 않은 원본 파일 수|  
|  FILES_COPIED  |  복사 완료한 원본 파일 수|
|  FILES_FAILED  |  복사 실패한 원본 파일 수|



### 마이그레이션할 파일의 크기 분포 정보 통계

매개변수 `--printStatsOnly` 및 `--statsRange=VALUE`로 명령을 실행하여 마이그레이션할 파일의 크기 분포 정보를 출력합니다.

```plaintext
hadoop jar cos-distcp-1.6-3.1.0.jar --src /wookie/data --dest cosn://examplebucket-1250000000/wookie/data --printStatsOnly  --statsRange=0,1mb,10mb,100mb,1gb,10gb,inf

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

### 입력 파일을 정규식으로 필터링

매개변수 `--srcPattern`으로 명령을 실행합니다. `/data/warehouse/logs` 디렉터리의 확장자가 .log인 로그 파일만 동기화합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse/logs --dest cosn://examplebucket-1250000000/data/warehouse --srcPattern='.*/logs/.*\.log'
```

### 복사 프로세스의 수와 각 복사 프로세스의 복사 스레드 수를 지정합니다.

매개변수 --taskNumber`와 `--workersNumber`로 명령을 실행합니다. COSDistCp는 멀티 프로세스+멀티 스레드의 복사 구조를 사용하며, 다음 작업이 가능합니다.
- `--taskNumber`를 통해 복사 프로세스 수 지정
- `--workerNumber`를 통해 각 복사 프로세스 내의 복사 스레드 수를 지정할 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse --taskNumber=10 --workerNumber=5
```

### 원본 파일 삭제

매개변수 `--deleteOnSuccess`로 명령을 실행합니다. `/data/warehouse` 디렉터리의 파일을 HDFS에서 COS로 동기화한 후 즉시 원본 디렉터리에서 해당 파일을 삭제합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --deleteOnSuccess
```

>! 해당 옵션을 지정하면 파일 하나의 마이그레이션이 완료될 때마다 즉시 해당하는 원본 파일을 삭제합니다. 전체 마이그레이션이 완료된 후 원본 파일을 삭제하는 것이 아니므로 신중하게 사용하십시오.
>

### 단일 파일의 읽기 대역폭 제한

매개변수 `--bandWidth`로 명령을 실행합니다. 값의 단위는 MB이며, 각 마이그레이션 파일의 읽기 대역폭을 10MB/s로 제한합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --bandWidth=10
```

### Hadoop-COS의 파일 검증과 유형 지정

매개변수 `--cosChecksumType`으로 명령을 실행합니다. 기본 값은 CRC32C이며, CRC32C와 CRC64를 선택할 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --cosChecksumType=CRC32C
```

### 같은 길이의 파일 건너뛰기

매개변수 `--skipMode`로 명령을 실행합니다. 원본과 타깃의 길이가 같은 파일은 복사를 건너뜁니다.
```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse  --skipMode=length
```

`--skipMode` 옵션은 파일 복사 전에 원본 파일과 타깃 파일의 일치 여부를 검증하는 데 사용하며, 일치할 경우 건너뜁니다. none(검증 안 함), length(길이), checksum(CRC 값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.

원본과 타깃 파일 시스템의 검증 및 알고리즘이 일치하지 않는 경우 원본 파일의 새로운 검사합을 계산합니다. 원본이 HDFS일 경우 다음 방식으로 HDFS 원본의 COMPOSITE-CRC32C 검증 알고리즘 지원 여부를 확인할 수 있습니다.

```plaintext
hadoop fs  -Ddfs.checksum.combine.mode=COMPOSITE_CRC -checksum /data/test.txt
/data/test.txt  COMPOSITE-CRC32C        6a732798
```

### 원본 파일과 타깃 파일이 동일한 CRC 보유 여부 검증

매개변수 `--checkMode`로 명령을 실행합니다. 파일 복사 완료 시 원본 파일과 타깃 파일의 검사합 일치 여부를 검증합니다.

비 COS 파일 시스템에서 COS로 동기화할 때, 원본의 CRC 알고리즘과 Hadoop-COS의 CRC 알고리즘이 일치하지 않을 경우 복사 시 CRC를 계산합니다. 복사 완료 후 타깃 COS 파일의 CRC를 획득하고, 계산으로 획득한 원본 파일의 CRC를 대조해 검증합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar   --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --checkMode=checksum
```

### 타깃 파일의 압축 유형 지정

매개변수 `--outputCodec`으로 명령을 실행합니다. 해당 매개변수를 통해 HDFS의 데이터를 실시간으로 압축해 COS에 백업할 수 있어 스토리지 비용을 절약할 수 있습니다. 매개변수 옵션 값은 keep, none, gzip, lzop, snappy가 있으며, none은 타깃 파일을 압축하지 않은 상태로 저장하고, keep은 원본 파일의 압축 상태를 유지합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/logs --dest cosn://examplebucket-1250000000/data/warehouse/logs-gzip --outputCodec=gzip
```

>! 여기에서 keep을 제외한 모든 값은 먼저 파일을 압축 해제한 후 타깃 압축 유형으로 변환합니다. 따라서 keep을 제외하고는 압축 매개변수 등이 일치하지 않아 타깃 파일과 원본 파일이 동일하지 않을 수 있으나 압축 해제한 파일은 동일합니다.
>

### 다중 디렉터리 동기화

로컬 파일(예: srcPrefixes.txt)을 생성하고 해당 파일에 마이그레이션할 여러 디렉터리를 추가합니다. 추가한 후 cat 명령어를 통해 이를 확인할 수 있으며, 예시는 다음과 같습니다.

```plaintext
cat srcPrefixes.txt 
/data/warehouse/20181121/
/data/warehouse/20181122/
```

`--srcPrefixesFile` 매개변수를 사용하여 해당 파일을 지정하고 마이그레이션 명령어를 실행합니다.

```plaintext
hadoop jar  cos-distcp-${version}.jar --src /data/warehouse  --srcPrefixesFile file:///usr/local/service/hadoop/srcPrefixes.txt --dest  cosn://examplebucket-1250000000/data/warehouse/ --taskNumber=20
```

### 타깃 매니페스트 파일 생성 및 이전 매니페스트 출력 파일 지정

매개변수 `--outputManifest`와 `--previousManifest`로 명령을 실행합니다.

- `--outputManifest` 해당 옵션은 먼저 로컬에 gzip으로 압축된 manifest.gz를 생성하고 마이그레이션 완료 시 `--dest`에서 지정한 디렉터리로 이동됩니다.
- `--previousManifest`로 바로 이전의 `--outputManifest` 출력 파일을 지정하여 COSDistCp가 동일한 길이 및 크기의 파일을 건너뜁니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest  cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest.gz --previousManifest= cosn://examplebucket-1250000000/data/warehouse/manifest-2020-01-10.gz
```

>! 위 명령어의 증분 마이그레이션은 파일 크기가 변경된 파일만 동기화할 수 있으며 파일 내용이 변경된 파일은 동기화할 수 없습니다. 파일 내용이 변경된 경우 --diffMode 사용 예시를 참고하여 파일 CRC에 따라 변경된 파일 리스트를 확인하십시오.
>

### CRC에 따른 변경 파일 리스트 획득 및 증분 마이그레이션

매개변수 `--diffMode`와 `--diffOutput`으로 명령을 실행합니다.
- `--diffMode`의 옵션 값은 length와 length-checksum이 있습니다.
 - `--diffMode=length`는 파일 크기 동일 여부에 따라 변경 파일 리스트를 획득합니다.
 - `--diffMode=length-checksum`은 파일 크기 및 CRC 검증 동일 여부에 따라 변경 파일 리스트를 획득합니다.
- `--diffOutput`은 diff 작업의 출력 디렉터리를 지정합니다.

다음 예시는 파일 크기 및 CRC 값에 따라 원본 파일과 타깃 파일의 동일 여부를 검증합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

>! 타깃 파일 시스템이 COS이고 원본 파일 시스템의 CRC 알고리즘과 다른 경우 COSDistCp는 원본 파일을 풀링해 새로운 CRC를 계산하여 동일한 CRC 알고리즘 값으로 비교합니다.
>

위 명령어 실행이 완료되면 HDFS의 `/tmp/diff-output` 디렉터리에 변경 파일 리스트가 생성되며, 아래 유형의 원본 파일 정보가 포함되어 출력됩니다.

1. 타깃 파일이 존재하지 않을 경우 DEST_MISS로 기록
2. 원본 디렉터리의 리스트가 존재하지만, 검증 시 원본 파일이 존재하지 않는 경우 SRC_MISS로 기록
3. 원본 파일과 타깃 파일 크기가 다른 경우 LENGTH_DIFF로 기록
4. 원본 파일과 타깃 파일의 CRC 알고리즘 값이 다른 경우 CHECKSUM_DIFF로 기록
5. 읽기 권한 부족 등의 사유로 diff 작업에 실패하는 경우 DIFF_FAILED로 기록

다음 명령어를 통해 SRC_MISS를 제외한 변경 파일 리스트를 획득할 수 있습니다.

```plaintext
hadoop fs -getmerge /tmp/diff-output diff-manifest
grep -v '"comment":"SRC_MISS"' diff-manifest |gzip > diff-manifest.gz
```

다음 명령어를 실행해 변경 파일 리스트에 따라 증분 마이그레이션을 진행할 수 있습니다.

```plaintext
hadoop  jar cos-distcp-${version}.jar --taskNumber=20 --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --previousManifest=file:///usr/local/service/hadoop/diff-manifest.gz --copyFromManifest
```

### COS 파일의 스토리지 유형 지정

매개변수 `--storageClass`로 명령을 실행합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest-2020-01-10.gz --storageClass=STANDARD_IA
```

### 작업 할당 정책을 동적 할당으로 지정

파일 크기 분포가 매우 고르지 못한 경우, 예: 매우 적은 대용량 파일, 많은 소용량 파일 또는 마이그레이션 기기 부하가 상이할 경우, `--enableDynamicStrategy`를 사용하여 작업 동적 할당 정책을 활성화하여 작업 속도가 빠른 작업에 더 많은 파일을 마이그레이션하여 작업 시간을 줄일 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse    --dest  cosn://examplebucket-1250000000/data/warehouse --enableDynamicStrategy
```

### 복사 파일의 메타 정보

매개변수 `--preserveStatus`로 명령을 실행합니다. 원본 파일 또는 원본 디렉터리의 user, group, permission, timestamps(modification time, access time)를 타깃 파일 또는 타깃 디렉터리에 복사합니다. 예시는 다음과 같습니다.
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

`--promPort=VALUE` 매개변수로 명령을 실행하여 현재 MapReduce 작업의 카운터를 외부에 노출합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --promPort=9028
```

예제 [Grafana Dashboard](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/COSDistcp-Grafana-Dashboard.json)를 다운로드하여 가져오십시오. Grafana는 다음과 같이 표시됩니다.
![COSDistcp-Grafana](https://main.qcloudimg.com/raw/8bc614ef9364b03f8dd27075fcb8380e.png)


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

위 명령어에서 alarmPolicyId는 클라우드 모니터링 알람 정책이며, 클라우드 모니터링 콘솔에서 생성 및 설정(알람 관리>알람 설정>사용자 정의 메시지)할 수 있습니다.



## FAQ

### 환경에서 Hadoop-COS를 설정하지 않은 경우, COSDistCp는 어떻게 실행하나요?

환경에서 Hadoop-COS 플러그 인을 설정하지 않은 사용자는 Hadoop 버전에 따라 해당 버전의 COSDistCp jar 패키지를 다운로드한 후 Hadoop-COS 관련 매개변수를 지정하여 복사 작업을 실행할 수 있습니다.

```plaintext
hadoop jar cos-distcp-1.3-2.8.5.jar \
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
2. 작업을 요청한 사용자에게 원본 파일 읽기 또는 타깃 파일 쓰기 권한이 없거나 기타 원인이 있을 경우 COPY_FAILED로 기록

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
COSDistCp는 네트워크 이상, 원본 파일 결함, 권한 부족 등의 상황에서 타깃에 원본과 동일한 크기의 파일을 생성할 수 없습니다.
- COSDistCp 1.5 버전 이하인 경우, COSDistCp는 타깃에 생성한 파일에 대해 삭제를 시도합니다. 삭제에 실패하는 경우, 복사 작업을 다시 실행하여 해당 파일을 덮어쓰거나 수동으로 해당 불완전 파일을 삭제해야 합니다.
- COSDistCp 1.5 버전 이상이고 Hadoop COS 플러그 인 버전이 5.9.3 이상인 실행 환경에서 COS 복사 작업에 실패한 경우, COSDistCp는 abort 인터페이스를 호출하여 현재 업로드 중인 요청을 중지합니다. 따라서 이상 상황이 발생해도 불완전 파일이 생성되지 않습니다.
- COSDistCp 1.5 버전 이상이고 Hadoop COS 플러그 인 버전이 5.9.3 미만인 실행 환경에서는 5.9.3 이상의 버전으로 업그레이드하는 것을 권장합니다.
- COS의 타깃이 아닌 경우 COSDistCp는 타깃 파일에 대한 삭제를 시도합니다.
