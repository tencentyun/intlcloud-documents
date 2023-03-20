## 소개
COS(Cloud Object Storage)는 메타데이터 가속화 기능을 제공하여 고성능 파일 시스템 기능을 제공합니다. 메타데이터 가속화는 기본 계층에서 Cloud HDFS(CHDFS)의 강력한 메타데이터 관리 기능을 활용하여 COS 액세스에 파일 시스템 시맨틱을 사용할 수 있도록 합니다. 설계된 시스템 메트릭은 최대 100GB/s의 대역폭, 10만개 이상의 QPS(초당 쿼리) 및 ms의 대기 시간에 도달할 수 있습니다. 메타데이터 가속이 활성화된 버킷은 빅 데이터, 고성능 컴퓨팅, 기계 학습 및 AI와 같은 시나리오에서 널리 사용될 수 있습니다. 메타데이터 가속에 대한 자세한 내용은 [메타데이터 가속 개요](https://intl.cloud.tencent.com/document/product/436/43305)를 참고하십시오.

COS는 메타데이터 가속 서비스를 통해 Hadoop 시맨틱을 제공합니다. 따라서 [Hadoop Distcp 툴](https://intl.cloud.tencent.com/document/product/436/38863)을 사용하여 COS와 다른 Hadoop 파일 시스템 간의 양방향 데이터 마이그레이션을 쉽게 구현할 수 있습니다. 이 문서에서는 Hadoop Distcp를 사용하여 로컬 HDFS의 파일을 COS의 메타데이터 가속 버킷으로 마이그레이션하는 방법을 설명합니다.

## 마이그레이션 환경 준비

### 마이그레이션 툴


1. 아래 나열된 툴의 jar 패키지를 다운로드하고 /data01/jars와 같이 클러스터에서 마이그레이션 작업을 실행하는 노드의 로컬 디렉터리에 배치합니다.

<b>EMR 환경</b>
 
**설치 설명**

<table>
<thead>
<tr><th>jar 파일 이름</th><th>설명</th><th>다운로드 주소</th></tr>
</thead>
<tbody>
<tr>
<td>cos-distcp-1.12-3.1.0.jar</td>
<td>COSN에 데이터를 복사할 COSDistCp 패키지</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/38863">COSDistCp 툴</a>을 참고하십시오</td>
</tr>
<tr>
<td>chdfs_hadoop_plugin_network-2.8.jar</td>
<td>OFS 플러그인</td>
<td><a href="https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar">다운로드</a></td>
</tr>
</tbody>
</table>


<b>자체 구축 Hadoop/CDH 등 환경</b>

**소프트웨어 종속성**

Hadoop 2.6.0 이상 및 Hadoop-COS 8.1.5 이상이 필요합니다. cos_api-bundle 플러그인 버전은 <a href="https://github.com/tencentyun/hadoop-cos/releases">COSN github releases</a>에 설명된 대로 Hadoop-COS 버전과 일치해야 합니다.

**설치 설명**

Hadoop 환경에 다음 플러그인을 설치합니다.
<table>
<thead>
<tr><th>jar 파일 이름</th><th>설명</th><th>다운로드 주소</th></tr>
</thead>
<tbody>
<tr>
<td>cos-distcp-1.12-3.1.0.jar</td>
<td>COSN에 데이터를 복사할 COSDistCp 패키지</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/38863">COSDistCp 툴</a>을 참고하십시오</td>
</tr>
<tr>
<td>chdfs_hadoop_plugin_network-2.8.jar</td>
<td>OFS 플러그인</td>
<td><a href="https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar">다운로드</a></td>
</tr>
<tr>
<td>Hadoop-COS</td>
<td>Version >= 8.1.5</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6884">Hadoop-COS 툴</a>을 참고하십시오</td>
</tr>
<tr>
<td>cos_api-bundle</td>
<td>버전은 Hadoop-COS 버전과 일치해야 합니다</td>
<td><a href="https://github.com/tencentyun/hadoop-cos/releases">다운로드</a></td>
</tr>
</tbody>
</table>

>!
>- Hadoop-cos는 버전 8.1.5부터 `cosn://bucketname-appid/` 형식의 메타데이터 가속 버킷에 대한 액세스 지원;
>- 메타데이터 가속화 기능은 버킷 생성 중에만 활성화할 수 있으며 일단 활성화되면 비활성화할 수 없습니다. 따라서 비즈니스 조건에 따라 활성화할지 여부를 신중하게 고려하십시오. 또한 레거시 Hadoop-COS 패키지는 메타데이터 가속 버킷에 액세스할 수 없습니다.

2. [HDFS 프로토콜을 사용하여 메타데이터 가속이 활성화된 버킷에 액세스](https://intl.cloud.tencent.com/document/product/436/46198)의 ‘버킷 생성 및 HDFS 프로토콜 구성’의 지침에 따라 메타데이터 가속 버킷을 생성하고 이에 대한 HDFS 프로토콜을 구성합니다.
3. 마이그레이션 클러스터의 `core-site.xml`을 수정하고 구성을 모든 노드에 배포합니다. 데이터만 마이그레이션해야 하는 경우 빅 데이터 컴포넌트를 다시 시작할 필요가 없습니다.
<table>
<thead>
<tr><th>key</th><th>value</th><th>구성 파일</th><th>설명</th></tr>
</thead>
<tbody>
<tr>
<td>fs.cosn.trsf.fs.ofs.impl</td>
<td>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</td>
<td>core-site.xml</td>
<td>COSN 구현 클래스, 필수 입력</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl</td>
<td>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</td>
<td>core-site.xml</td>
<td>COSN 구현 클래스, 필수 입력</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.tmp.cache.dir</td>
<td>/data/emr/hdfs/tmp/ 형식</td>
<td>core-site.xml</td>
<td>임시 디렉터리로 필수 입력 항목입니다. 모든 MRS 노드에 생성됩니다. 충분한 공간과 권한이 있는지 확인해야 합니다.</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.user.appid</td>
<td>COS bucket의 appid</td>
<td>core-site.xml</td>
<td>필수</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.ranger.enable.flag</td>
<td>false</td>
<td>core-site.xml</td>
<td>필수 입력 항목입니다. 값이 false인지 확인해야 합니다.</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.bucket.region</td>
<td>bucket region</td>
<td>core-site.xml</td>
<td>필수 입력 항목입니다. 유효한 값: eu-frankfurt(프랑크푸르트), ap-chengdu(청두) 및 ap-singapore(싱가포르)</td>
</tr>
</tbody>
</table>
4. [HDFS 프로토콜을 사용하여 메타데이터 가속이 활성화된 버킷에 액세스](https://intl.cloud.tencent.com/document/product/436/46198)의 ‘COS에 액세스하도록 컴퓨팅 클러스터 구성’에 설명된 대로 사설망을 통해 메타데이터 가속 버킷에 액세스하여 마이그레이션을 확인할 수 있습니다. 마이그레이션 클러스터 제출자를 사용하여 COS에 성공적으로 액세스할 수 있는지 확인하십시오.



## 기존 데이터 마이그레이션

### 1. 마이그레이션할 디렉터리 결정

일반적으로 HDFS 스토리지 데이터가 먼저 마이그레이션됩니다. 원본 HDFS 클러스터에서 마이그레이션할 디렉터리가 선택되며 대상 경로는 원본 경로와 동일해야 합니다.

HDFS 디렉터리 `hdfs:///data/user/target`을 `cosn://{bucketname-appid}/data/user/target`으로 마이그레이션해야 한다고 가정합니다.

원본 디렉터리의 파일이 마이그레이션 중에 변경되지 않도록 하기 위해 HDFS의 스냅샷 기능을 사용하여 원본 디렉터리의 스냅샷(현재 날짜로 명명됨)을 생성합니다.

```shell
hdfs dfsadmin -disallowSnapshot hdfs:///data/user/
hdfs dfsadmin -allowSnapshot hdfs:///data/user/target
hdfs dfs -deleteSnapshot hdfs:///data/user/target {현재 날짜}
hdfs dfs -createSnapshot hdfs:///data/user/target {현재 날짜}
```

성공 예시 참고:
![](https://qcloudimg.tencent-cloud.cn/raw/b96ef1500668c059909eb1ced5744a3f.png)

스냅샷을 생성하지 않으려면 원본 디렉터리에서 target 파일을 직접 마이그레이션할 수 있습니다.

### 2. 마이그레이션에 COSDistCp 사용

COSDistCp 작업을 시작하여 원본 HDFS에서 대상 COS 버킷으로 파일을 복사합니다.

COSDistCp 작업은 본질적으로 MapReduce 작업입니다. 인쇄된 MapReduce 작업 로그에는 MR 작업이 성공적으로 실행되었는지 여부가 표시됩니다. 작업이 실패하면 YARN 페이지를 보고 문제 해결을 위해 로그 또는 예외 정보를 COS 팀에 제출할 수 있습니다. COSDistCp를 사용하여 다음 단계에서 마이그레이션 작업을 실행할 수 있습니다.
(1) 임시 디렉터리 생성
(2) COSDistCp 작업 실행
(3) 실패한 파일을 다시 마이그레이션

#### (1) 임시 디렉터리 생성

```shell
hadoop fs -libjars /data01/jars/chdfs_hadoop_plugin_network-2.8.jar -mkdir cosn://bucket-appid/distcp-tmp
```

#### (2) COSDistCp 작업 실행

```shell
nohup hadoop jar /data01/jars/cos-distcp-1.10-2.8.5.jar -libjars  /data01/jars/chdfs_hadoop_plugin_network-2.8.jar --src=hdfs:///data/user/target/.snapshot/{현재 날짜}  --dest=cosn://{bucket-appid}/data/user/target   --temp=cosn://bucket-appid/distcp-tmp/ --preserveStatus=ugpt  --skipMode=length-checksum --checkMode=length-checksum --cosChecksumType=CRC32C --taskNumber 6 --workerNumber 32 --bandWidth 200 >> ./distcp.log &
```

매개변수는 아래에 자세히 설명되어 있습니다. 필요에 따라 해당 값을 조정할 수 있습니다.
- --taskNumber=VALUE: 복사 스레드 수. 예: --taskNumber=10.
-  --workerNumber=VALUE: 복사 스레드 수. COSDistCp는 이 값 세트를 기반으로 각 복사 프로세스에 대해 복사 스레드 풀을 생성합니다. 예: --workerNumber=4.
-  --bandWidth: 마이그레이션된 각 파일 읽기 최대 대역폭(MB/s). 기본값: -1, 읽기 대역폭에 제한이 없음을 나타냅니다. 예:--bandWidth=10.
- --cosChecksumType=CRC32C: 기본적으로 CRC32C가 사용되지만 HDFS 클러스터는 COMPOSITE_CRC32를 확인할 수 있어야 합니다. Hadoop 버전은 3.1.1+이어야 합니다. 그렇지 않으면 이 매개변수를 --cosChecksumType=CRC64로 변경해야 합니다.

>!COSDistCp 마이그레이션의 총 대역폭 제한을 계산하는 공식은 taskNumber x workerNumber x bandWidth입니다. workerNumber를 1로 설정하고 taskNumber 매개변수를 사용하여 동시 마이그레이션 수를 제어하고 bandWidth 매개변수를 사용하여 단일 동시 마이그레이션의 대역폭을 제어할 수 있습니다.

복사 작업이 끝나면 작업 로그는 복사본에 대한 통계를 출력합니다. 카운터는 다음과 같습니다.
여기서 FILES_FAILED는 실패한 파일의 수를 나타냅니다. FILES_FAILED 카운터가 없으면 모든 파일이 성공적으로 마이그레이션된 것입니다.
```
CosDistCp Counters
        BYTES_EXPECTED=10198247
        BYTES_SKIPPED=10196880
        FILES_COPIED=1
        FILES_EXPECTED=7
        FILES_FAILED=1
        FILES_SKIPPED=5

```

출력 결과의 구체적인 통계 항목은 아래와 같습니다.

| 통계 항목          | 설명                                               |
| --------------- | -------------------------------------------------- |
|  BYTES_EXPECTED  | 원본 디렉터리 통계에 따라 복사할 파일의 총 크기, 단위: 바이트   |
|  FILES_EXPECTED  | 원본 디렉터리 통계에 따라 복사할 파일 수. 디렉터리 파일 포함   |
|  BYTES_SKIPPED  | 스킵할 수 있는 파일의 총 크기(바이트)(동일한 길이 또는 체크섬 값)  |
|  FILES_SKIPPED  | 스킵할 수 있는 원본 파일 수(동일한 길이 또는 체크섬 값)               |
| FILES_COPIED    | 복사 성공한 원본 파일 수                                 |
| FILES_FAILED    | 복사 실패한 원본 파일 수                                 |
|  FOLDERS_COPIED  | 복사 완료한 디렉터리 수   |
| FOLDERS_SKIPPED | 스킵한 디렉터리 수                                       |


#### (3) 실패한 파일을 다시 마이그레이션

COSDistCp는 비효율적인 파일 마이그레이션의 대부분의 문제를 해결할 뿐만 아니라 `--delete` 매개변수를 사용하여 HDFS와 COS 데이터 간의 완전한 일관성을 보장할 수 있습니다.

`--delete` 매개변수를 사용할 때 `--deleteOutput=/xxx(사용자 지정)` 매개변수를 추가해야 하지만 `--diffMode` 매개변수는 추가하지 않아야 합니다.

```shell
nohup hadoop jar /data01/jars/cos-distcp-1.10-2.8.5.jar -libjars /data01/jars/chdfs_hadoop_plugin_network-2.8.jar --src=--src=hdfs:///data/user/target/.snapshot/{현재 날짜} --dest=cosn://{bucket-appid}/data/user/target --temp=cosn://bucket-appid/distcp-tmp/ --preserveStatus=ugpt --skipMode=length-checksum --checkMode=length-checksum --cosChecksumType=CRC32C --taskNumber 6 --workerNumber 32 --bandWidth 200 --delete --deleteOutput=/dele-xx >> ./distcp.log &
```

실행 후 HDFS와 COS 사이의 다른 데이터는 `trash` 디렉터리로 이동되고 이동된 파일 목록은 `/xxx/failed` 디렉터리에 생성됩니다. `hadoop fs -rm URL` 또는 `hadoop fs -rmr URL`을 실행하여 `trash` 디렉터리의 데이터를 삭제할 수 있습니다.

## 증분 마이그레이션

나중에 증분 데이터를 마이그레이션해야 하는 경우 모든 데이터가 마이그레이션될 때까지 전체 마이그레이션 단계를 반복하기만 하면 됩니다.

