## 기능 설명

COSDistCp는 MapReduce를 기초로 한 분산형 파일 복사 툴로 주로 HDFS와 COS간의 데이터 복사에 사용합니다. COSDistCp는 파일 필터, 압축, 파일 취합, 대역폭 제한 읽기, 파일 속성 유지 등 실용적인 복사 기능을 제공합니다. 이와 동시에 COS를 기초로 한 지원의 특성으로 COSDistCp 툴은 길이, CRC 검사합을 기초로 증분 복사와 실시간 인증 기능을 제공합니다. 

## 사용 환경

#### 시스템 환경

Linux 시스템 지원

#### 소프트웨어 종속

Hadoop-2.6.0 이상 버전, Hadoop-COS 플러그 인 5.8.7 이상 버전

## 다운로드와 설치

#### COSDistCp jar 패키지 획득

[cos-distcp-1.2.jar 패키지](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.2.jar) 다운로드
>?사용자는 jar 패키지의 [MD5 인증 값](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.2-md5.txt)에 따라 다운로드한 jar 패키지가 완벽한지 확인합니다.

## 설치 설명

Hadoop 환경에서 [Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884?!preview=&!editLang=zh&from_cn_redirect=1&lang=en&pg=#download-and-installation)를 설치하면 COSDistCp 툴을 실행할 수 있습니다.


## 원리 설명

COSDistCp는 MapReduce를 기초로 프레임워크를 실현하여 Mapper에서 파일 배분을 진행하고, Reducer 프로세스 중에서 멀티 스레드를 사용해 파일 복사, 압축, 데이터 인증과 파일 속성 유지 등 작업을 진행합니다. 파일 마이그레이션 혹은 인증을 실패한 경우에는 작업 실행에 실패할 수 있습니다. 소스 파일 시스템에 파일이 증가하거나 파일 콘텐츠에 변경이 발생했을 경우 skipMode와 diffMode 모드로 파일의 길이 혹은 CRC 검사합을 대조하여 파일의 증분 마이그레이션을 실현할 수 있습니다.


## 매개변수 설명

`hadoop jar cos-distcp-${version}.jar --help` 명령어를 사용해 COSDistCp가 지원하는 매개변수 옵션을 조회할 수 있으며, 그중 `${version}`는 버전 번호입니다. 다음은 COSDistCp 매개변수 설명입니다.


|              속성 키              | 설명                                                         | 기본 값 | 필수 여부 |
| :------------------------------: | :----------------------------------------------------------- | :----: | :----: |
|              --help              | COSDistCp 출력에 지원하는 매개변수 옵션<br> 예시: --help               |   없음   |   아니요   |
|          --src=LOCATION          | 복사의 소스 디렉터리 지정, HDFS 혹은 COS 경로일 수 있습니다.<br> 예시: --src=hdfs://user/logs/ |   없음   |   예   |
|         --dest=LOCATION          | 복사본의 타깃 디렉터리 지정. HDFS 혹은 COS 경로일 수 있습니다.<br> 예시: --dest=cosn://examplebucket-1250000000/user/logs |   없음   |   예   |
|       --srcPattern=PATTERN       | 정규식의 소스 디렉터리의 파일에 필터링 진행 지정<br>예시: `--srcPattern='.*.log'`<br>**주의: 매개변수를 따옴표로 쌀 경우 `*` 부호가 shell로 해석되지 않도록 주의하십시오**. |   없음   |   아니요   |
|      --reducerNumber=VALUE       | reducer 프로세스 개수 지정<br>예시: --reducerNumber=10            |   10   |   아니요   |
|       --workerNumber=VALUE       | 각 reducer의 복사 스레드 수 지정, COSDistCp가 각 reducer에 해당 매개변수 크기의 복사 스레드 풀을 생성합니다.<br>예시: --workerNumber=4 |   4   |   아니요   |
|      --filesPerMapper=VALUE      | 각 Mapper의 입력 파일의 행 수 지정<br>예시: --filesPerMapper=10000 | 500000 |   아니요   |
|        --groupBy=PATTERN         | 정규식을 지정해 파일 취합 진행<br>예시: --groupBy='.\*group-input/(\d+)-(\d+).*' |   없음   |   아니요   |
|        --targetSize=VALUE        | 타깃 파일의 크기 지정, 단위: MB, --groupBy와 함께 사용합니다.<br>예시: --targetSize=10 |   없음   |   아니요   |
|       --outputCodec=VALUE        | 출력 파일의 압축 방식 지정. gzip, lzo, snappy, none, keep을 선택할 수 있습니다.<br> 1. keep은 원래 파일의 압축 방식 유지<br>2. none은 파일 확장자에 따라 파일 압축 해제<br>예시: --outputCodec=gzip |  keep  |   아니요   |
|        --deleteOnSuccess         | 소스 파일을 타깃 디렉터리로 복사를 성공한 경우 즉시 소스 파일을 제거하도록 지정합니다.<br>예시: --deleteOnSuccess | false  |   아니요   |
| --multipartUploadChunkSize=VALUE | Hadoop-COS 플러그 인 파일이 COS로 전송될 경우 파트의 크기 지정. COS가 지원하는 최대 파트 수는 10000, 파일 크기에 따라 파트 크기 조정할 수 있으며 단위는 MB, 기본값 8MB입니다.<br>예시: --multipartUploadChunkSize=20 |  8MB   |   아니요   |
|    --cosServerSideEncryption     | 지정 파일을 COS로 업로드할 경우 SSE-COS를 암호화/복호화 알고리즘으로 사용합니다.<br />예시: --cosServerSideEncryption | false  |   아니요   |
|      --outputManifest=VALUE      | 복사 완료 시 타깃 디렉터리에 이번 복사의 타깃 파일 정보 리스트(GZIP 압축) 생성 지정<br>예시:--outputManifest=manifest.gz |   없음   |   아니요   |
|    --requirePreviousManifest     |  --previousManifest=VALUE 매개변수 지정을 요청해 증분 복사를 진행합니다.<br>예시: --requirePreviousManifest | false  |   아니요   |
|   --previousManifest=LOCATION    | 이전 복사 시 생성된 타깃 파일 정보<br>예시: --previousManifest=cosn://examplebucket-1250000000/big-data/manifest.gz |   없음   |   아니요   |
|        --copyFromManifest        | --previousManifest=LOCATION과 함께 사용하면 --previousManifest의 파일을 타깃 파일 시스템에 복사할 수 있습니다.<br>예시: --copyFromManifest | false  |   아니요   |
|       --storageClass=VALUE       | 객체 스토리지 유형 지정, 값을 STANDARD, STANDARD_IA, ARCHIVE, DEEP_ARCHIVE, INTELLIGENT_TIERING으로 선택할 수 있습니다. 더 많은 지원하는 스토리지 유형과 소개는 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오. |   없음   |   아니요   |
|    --srcPrefixesFile=LOCATION    | 로컬 파일 지정, 해당 파일의 매 행에는 복사가 필요한 소스 디렉터리가 포함되어 있습니다.<br/>예시: --srcPrefixesFile=file:///data/migrate-folders.txt |   없음   |   아니요   |
|         --skipMode=MODE          | 파일 복사 전에 소스 파일과 타깃 파일의 일치 여부를 인증합니다. 일치할 경우에는 건너뛰고 none(인증 안함), length (길이), checksum(CRC값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.<br/>예시: --skipMode=length |  none  |   아니요   |
|         --checkMode=MODE         | 파일 복사를 완료하면 소스 파일과 타깃 파일의 일치 여부를 인증합니다. 다를 시에는 복사를 정지하고 none(인증 안함), length (길이), checksum(CRC값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.<br/>예시: --checkMode=length-checksum |  none  |   아니요   |
|         --diffMode=MODE          | 다른 문서 리스트를 획득하는 기준 지정, length(길이), checksum(CRC 값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.<br/>예시: --diffMode=length-checksum |   없음   |   아니요   |
|      --diffOutput=LOCATION       | 다른 문서 리스트의 출력 디렉터리 지정, 해당 출력 디렉터리는 반드시 비어 있어야 합니다.<br/>예시: --diffOutput=/diff-output |   없음   |   아니요   |
|      --cosChecksumType=TYPE      | Hadoop-COS 플러그 인이 사용하는 CRC 알고리즘 지정, 값을 CRC32C와 CRC64으로 선택할 수 있습니다.<br/>예시: --cosChecksumType=CRC32C | CRC32C |   아니요   |
|      --preserveStatus=VALUE      | 소스 파일의 user, group, permission, xattr와 timestamps 메타 정보를 타깃 파일에 복사합니다. 선택 가능한 값은 ugpxt(즉 user, group, permission, xattr와 timestamps의 영문 이니셜)입니다.<br/>예시: --preserveStatus=ugpt | 없음 |   아니요   |


## 사용 예시

### help 옵션 조회

매개변수 `--help`로 명령을 실행해 COSDistCp를 지원하는 매개변수를 조회합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --help
```
위 명령어 중 `${version}`는 COSDistCp 버전 넘버입니다. 예를 들어 1.0 버전의 COSDistCp jar 패키지 이름은 cos-distcp-1.0.jar입니다.

### 마이그레이션 대기 파일의 소스 디렉터리와 타깃 디렉터리 지정

`--src`와 `--dest` 매개변수로 명령 실행, 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse
```

### 입력 파일에 정규식 필터링 진행

매개변수 `--srcPattern`로 명령을 실행합니다. `/data/warehouse/logs` 디렉터리의 .log로 끝나는 로그 파일만 동기화 합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse/logs --dest cosn://examplebucket-1250000000/data/warehouse --srcPattern='.*/logs/.*\.log'
```

### reducer 개수 및 reducer당 프로세스 내의 복사 스레드 수 지정

매개변수 `--reducerNumber`와 `--workersNumber`로 명령을 실행합니다. COSDistCp는 멀티 프로세스+멀티 스레드로 구성을 사용합니다.
- `--reducerNumber`로 reducer 프로세스 개수를 지정할 수 있습니다.
- `--workerNumber`로 각 reducer 내의 복사 스레드 수를 지정할 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse --reducerNumber=10 --workerNumber=5
```

### 소스 파일 삭제

매개변수 `--deleteOnSuccess`로 명령을 실행합니다. `/data/warehouse` 디렉터리의 파일을 HDFS에서 COS로 동기화한 후 즉시 소스 디렉터리의 대응되는 파일을 제거합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --deleteOnSuccess
```

>!해당 옵션 지정 후 파일 1개 마이그레이션 완료 즉시 대응되는 소스 파일을 삭제하며, 전체 마이그레이션이 끝나고 소스 파일을 삭제하는 것이 아니니 신중하게 사용하십시오.

### 단일 파일 대역폭 읽기 제한

매개변수 `--bandWidth`으로 명령을 실행합니다. 값 단위는 MB이며, 각 마이그레이션 파일의 읽기 대역폭 10MB/s로 제한합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --bandWidth=10
```

### Hadoop-COS의 파일 검증과 유형 지정

매개변수 `--cosChecksumType`으로 명령을 실행합니다. 기본값 CRC32C이며, CRC32C와 CRC64를 선택할 수 있습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --cosChecksumType=CRC32C
```

### 같은 길이의 파일 건너뛰기

매개변수 `--skipMode`로 명령을 실행합니다. 소스와 타깃의 길이가 같은 파일 복사는 건너뜁니다.
```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse  --skipMode=length
```

`--skipMode` 옵션은 파일 복사 전에 소스 파일과 타깃 파일의 일치 여부 인증에 사용합니다. 일치할 경우에는 건너뛰고 none(인증 안함), length(길이), checksum(CRC 값), length-checksum(길이 + CRC 값)을 선택할 수 있습니다.

소스와 타깃 파일 시스템 인증과 알고리즘이 일치하지 않는 경우에는 소스 파일의 새로운 검사합을 계산합니다. 소스가 HDFS일 경우 다음 방식으로 HDFS 소스의 COMPOSITE-CRC32C 인증 알고리즘 지원 여부를 확인할 수 있습니다.

```plaintext
hadoop fs  -Ddfs.checksum.combine.mode=COMPOSITE_CRC -checksum /data/test.txt
/data/test.txt  COMPOSITE-CRC32C        6a732798
```

### 소스 파일과 타깃 파일의 같은 CRC 보유 여부 인증

매개변수 `--checkMode`로 명령을 실행합니다. 파일 복사 완료 시 소스 파일과 타깃 파일의 검사합 일치 여부를 인증합니다.

비 COS 파일 시스템에서 COS로 동기화 할 시 소스 CRC 알고리즘과 Hadoop-COS의 CRC 알고리즘이 일치하지 않을 경우 복사 시 CRC를 계산합니다. 복사 완료 후 타깃 COS 파일의 CRC를 획득하고 계산으로 획득한 소스 파일 CRC를 대조해 인증합니다.

```plaintext
hadoop jar cos-distcp-${version}.jar   --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --checkMode=checksum
```

### 타깃 파일의 압축 유형 지정

매개변수 `--outputCodec`로 명령을 실행합니다. 해당 매개변수로 HDFS의 데이터를 실시간으로 COS로 압축해 스토리지 비용을 절약할 수 있습니다. 선택 가능한 매개변수 값은 keep, none, gzip, lzop, snappy입니다. none 옵션은 저장한 타깃 파일을 압축하지 않으며, keep은 원래 문서의 압축 상태를 유지합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/logs --dest cosn://examplebucket-1250000000/data/warehouse/logs-gzip --outputCodec=gzip
```

>!그중 keep 옵션을 제외하고 모든 파일의 압축을 해제한 후 타깃 압축 유형을 전화합니다. 이 때문에 keep 옵션 이외는 모두 압축 매개변수가 일치하지 않아 타깃 파일과 소스 파일이 일치하지 않을 수 있습니다. 하지만 압축을 해제한 파일은 일치합니다.

### 다중 디렉터리 동기화

로컬 파일 1개를 생성하고(예시: srcPrefixes.txt) 해당 파일에 마이그레이션이 필요한 여러 디렉터리를 추가합니다. 추가 후 cat 명령어로 조회할 수 있습니다. 예시는 다음과 같습니다.

```plaintext
cat srcPrefixes.txt 
/data/warehouse/20181121/
/data/warehouse/20181122/
```

`--srcPrefixesFile` 매개변수를 사용해 해당 파일 지정, 마이그레이션 실행 명령어:

```plaintext
hadoop jar  cos-distcp-${version}.jar --src /data/warehouse  --srcPrefixesFile file:///usr/local/service/hadoop/srcPrefixes.txt --dest  cosn://examplebucket-1250000000/data/warehouse/ --reducerNumber=20
```

### 타깃 매니페스트 파일 생성과 이전 리스트의 출력 파일 지정

매개변수 `--outputManifest`와 `--previousManifest`로 명령을 실행합니다.

- `--outputManifest` 해당 옵션은 우선 로컬에 gzip으로 압축한 manifest.gz를 생성하고 마이그레이션 성공 시 `--dest`에서 지정한 디렉터리로 이동합니다.
- `--previousManifest` 이전 `--outputManifest` 출력 파일 지정, COSDistCp에서 길이가 같은 파일 건너뛰기

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest  cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest.gz --previousManifest= cosn://examplebucket-1250000000/data/warehouse/manifest-2020-01-10.gz
```

>!상술한 명령어의 증분 마이그레이션은 파일 크기가 변경된 파일만 가능하며, 콘텐츠가 변경된 파일은 동기화할 수 없습니다. 파일 콘텐츠에 변경이 발생할 가능성이 있는 경우에는 --diffMode 사용 예시를 참조해 파일의 CRC에 따라 파일에 변경 사항과 파일 리스트를 확인하십시오.

### CRC에 따라 다른 파일 리스트를 획득하고 증분 마이그레이션

매개변수 `--diffMode`와 `--diffOutput`을 실행 명령어로:
- `--diffMode`는 length와 length-checksum 값 선택 가능
 - `--diffMode=length`는 파일 크기의 일치 여부를 표시, 다른 파일 리스트 획득
 - `--diffMode=length-checksum`, 파일 크기와 CRC 검증, 일치 여부에 따라 다른 파일 리스트 획득
- `--diffOutput` diff 작업의 출력 디렉터리 지정

다음 예시에서 파일 크기와 CRC 값에 따라 소스와 타깃 파일의 일치 여부를 인증합니다. 지정 mapred.max.split.size는 100KB입니다.

```plaintext
hadoop jar cos-distcp-${version}.jar -Dmapred.max.split.size=102400  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

>!타깃 파일 시스템이 COS고 소스 파일 시스템의 CRC 알고리즘과 다를 경우 COSDistCp가 소스 파일로 새로운 CRC를 계산해 같은 CRC 알고리즘 값 비교를 진행합니다.

위 명령 실행 성공 후 HDFS의 `/tmp/diff-output` 디렉터리에 다른 파일 리스트를 생성합니다. 다음 유형의 소스 파일 정보가 포함되어 출력됩니다.

1. 소스 파일 시스템 존재, 타깃 파일 시스템 존재하지 않음
2. 소스 파일 시스템과 타깃 파일 시스템의 크기 다름
3. 소스 파일 시스템과 타깃 파일 시스템의 CRC 알고리즘 혹은 값 다름

다음 명령어로 다른 파일 리스트를 합병할 수 있습니다.

```plaintext
hadoop fs -getmerge /tmp/diff-output diff-manifest
gzip diff-manifest
```

다음 명령을 실행해 다른 파일 리스트를 증분 마이그레이션합니다.

```plaintext
hadoop  jar cos-distcp-${version}.jar --reducerNumber=20 --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --previousManifest=file:///usr/local/service/hadoop/diff-manifest.gz –copyFromManifest
```

### COS 파일의 스토리지 유형 지정

매개변수 `--storageClass`로 명령을 실행합니다. 예시는 다음과 같습니다.

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest-2020-01-10.gz --storageClass=STANDARD_IA
```

### 복사 파일의 메타 정보

매개변수 `--preserveStatus`로 명령을 실행합니다. 소스 파일 혹은 소스 디렉터리의 user, group, permission과 timestamps(modification time과 access time)을 타깃 파일 혹은 타깃 디렉터리에 복사합니다. 예시는 다음과 같습니다.
```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --preserveStatus=ugpt
```
