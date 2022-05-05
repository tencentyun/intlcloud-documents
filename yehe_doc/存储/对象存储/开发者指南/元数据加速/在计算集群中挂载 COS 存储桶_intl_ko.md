## 소개

COS(Cloud Object Storage)에서는 메타데이터 가속을 활성화하여 HDFS 프로토콜 액세스 기능을 얻을 수 있습니다. 메타데이터 가속이 활성화되면 COS는 버킷에 대한 마운트 포인트를 생성합니다. 그런 다음 [HDFS 클라이언트](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)를 다운로드하고 클라이언트의 마운트 포인트를 사용하여 COS를 마운트할 수 있습니다. 본 문서에서는 컴퓨팅 클러스터에 메타데이터 가속이 활성화된 버킷을 마운트하는 방법을 소개합니다.

## 전제 조건

- [Java 1.8](https://www.oracle.com/java/technologies/downloads/)은 마운트할 컴퓨팅 클러스터의 머신 또는 컨테이너에 설치됩니다.
- 마운트할 컴퓨팅 클러스터의 머신 또는 컨테이너에 액세스 권한이 부여됩니다. HDFS 권한 구성에서 액세스할 수 있는 VPC 및 IP를 지정해야 합니다.

## 작업 단계

1. [Hadoop 클라이언트 설치 패키지](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)를 다운로드합니다.
2. 컴퓨팅 작업에 해당하는 디렉터리에 설치 패키지를 배치합니다. EMR 클러스터의 경우 모든 노드의 `/usr/local/service/hadoop/share/hadoop/common/lib/` 디렉터리에 동기화할 수 있습니다.
3.`core-site.xml` 파일을 편집하여 다음 기본 설정을 추가합니다. 
```
<!--chdfs 구현 유형-->
<property>
		 <name>fs.AbstractFileSystem.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>

<!--chdfs 구현 유형-->
<property>
		 <name>fs.ofs.impl</name>
		 <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>

<!--로컬 cache의 임시 디렉터리로, 데이터 읽기/쓰기의 경우 메모리 cache가 부족할 때는 로컬 디스크에 쓰기 하고 관련 경로가 없을 때는 자동 생성-->
<property>
		 <name>fs.ofs.tmp.cache.dir</name>
		 <value>/data/chdfs_tmp_cache</value>
</property>

<!-- Tencent Cloud 콘솔(https://console.cloud.tencent.com/developer)에서 얻을 수 있는 귀하의 appId-->      
<property>
		 <name>fs.ofs.user.appid</name>
		 <value>1250000000</value>
</property>

<!--flush 의미. 기본값은 false(비동기 플러시)입니다. 아래 이미지에서 데이터 가시성 및 지속성 세부 정보를 참고하십시오 -->      
<property>
		 <name>fs.ofs.upload.flush.flag</name>
		 <value>false</value>
</property>

```
4. `core-site.xml`을 모든 `hadoop` 노드에 동기화 합니다. 
>? EMR 클러스터의 경우, 상기 3, 4단계를 통해 EMR 콘솔 컴포넌트 관리에서 HDFS 설정을 수정할 수 있습니다. 
>
5. `hadoop fs` 명령줄 도구를 사용하여 `hadoop fs -ls ofs://${bucketname-appid}/` 명령을 실행합니다. 여기서 `bucketname-appid`는 마운트 주소, 즉 버킷 이름입니다. 파일 목록이 제대로 출력되면 COS 버킷이 성공적으로 마운트된 것입니다.
6. `hadoop` 또는 `mr` 작업의 다른 구성 항목을 사용하여 메타데이터 가속이 활성화된 버킷에서 데이터 작업을 실행할 수도 있습니다. `mr` 작업의 경우 `-Dfs.defaultFS=ofs://${bucketname-appid}/`를 통해 작업의 기본 입력 및 출력 파일 'FS'를 해당 버킷으로 변경할 수 있습니다.

## 시나리오 설명

### 데이터 가시성 및 지속성

메타데이터 가속을 활성화하면 `COS`를 클라우드 분산 파일 시스템으로 사용할 수 있습니다. `Hadoop` 클라이언트 도구를 사용하여 파일을 열면 클라이언트는 특정 크기(보통 4MB)에 도달하면 파일을 비동기식으로 플러시하고 퍼블릭 클라우드의 `COS` 버킷에 데이터를 씁니다. 상위 레이어 컴퓨팅 서비스가 데이터 출력 스트림의 `Flush` API를 사전에 호출하는 경우 **플러시 API에 대한 이 호출은 기본적으로 무시되고(이 동작은 일반 동기화 flush semantics와 다릅니다)** 클라이언트는 데이터가 데이터를 비동기적으로 `flush`하기 전에 특정 양에 도달하도록 작성됩니다. 클라이언트 강제는 `Close`가 마지막으로 호출될 때 동기화 플러시를 실행합니다. `Close`가 성공적으로 처리된 후 데이터가 성공적으로 유지되며 향후에도 제대로 읽을 수 있습니다.

클라우드 액세스 지연이 로컬 디스크 액세스 지연보다 높기 때문에 `Hadoop` 클라이언트 도구는 기본적으로 비동기 `Flush`를 사용합니다. 비동기 `Flush`는 클라우드와의 상호 작용을 줄이고 `Flush` 작업이 사용자 쓰기 작업을 차단하는 것을 방지하여 쓰기 성능을 크게 개선하고 작업 시간을 줄입니다. 위험 포인트는 `Close` API가 결국 사전에 호출되지 않으면 플러시되지 않은 데이터가 손실될 수 있다는 것입니다.

따라서 **`Hbase Wal Log` 및 `Journal` 로그와 같이 클라우드에 대한 즉각적인 가시성과 지속성을 보장하기 위해 실시간으로 작성해야 하는 데이터의 경우 구성 항목 `fs.ofs.upload.flush.flag`에 대한 설명을 참고하여 동기화 `Flush`를 활성화합니다.**

## 설정 항목 설명

|        설정 항목      |                             설명                             |  기본값   | 필수 입력 여부 |
| :------------------------------| :----------------------------------------------------| :-------| :------ |
|       fs.ofs.tmp.cache.dir        |   임시 데이터 저장    |    없음     |    Yes    |
|       fs.ofs.map.block.size       | 클라이언트는 데이터를 쓸 때 데이터를 `Block`으로 나누고 이 구성 항목은 데이터 block 크기를 바이트 단위로 지정합니다. 기본값은 128MB(이 항목은 map 분할에만 영향을 미치며 CHDFS의 기본 스토리지 블록 크기와 무관) | 134217728 |    No    |
| fs.ofs.data.transfer.thread.count |               클라이언트가 데이터를 전송할 때 병렬 스레드 수                |    32     |    No    |
| fs.ofs.block.max.memory.cache.mb  | 클라이언트 플러그인이 사용하는 메모리 `Buffer`의 크기, 단위는 MB.(읽기 및 쓰기 모두 가속화) |    16     |    No    |
|  fs.ofs.block.max.file.cache.mb   |  CHDFS 플러그인에서 사용하는 디스크 `Buffer`의 크기, 단위는 MB.(쓰기 가속화)  |    256    |    No    |
|   fs.ofs.prev.read.block.count    | 읽기 중 미리 읽은 데이터 `Block` 수(블록 크기는 일반적으로 4MB). (랜덤 읽기 시나리오의 경우 필요에 따라 값을 줄이고, 순차 읽기 시나리오의 경우 필요에 따라 값과 메모리 buffer 크기를 늘립니다)|     4     |    No    |
|  fs.ofs.prev.read.block.release.enable| 읽은 마지막 데이터 `Block`의 Buffer를 해제할지 여부를 지정합니다. 순차 읽기 시나리오의 경우 이 옵션을 활성화합니다. 임의 읽기 시나리오의 경우 특정 데이터를 자주 읽는 경우 이 옵션을 비활성화하는 것이 좋습니다. 유효한 값: `true(활성화됨)`, `false(비활성화됨)` | `true` | No |
|      fs.ofs.plugin.info.log       |          클라이언트 디버깅 로그를 인쇄할지 여부를 지정합니다. 로그는 info 수준에서 인쇄됩니다. 유효한 값: true(활성화됨), false(비활성화됨) |   false   |    No    |
|      fs.ofs.upload.flush.flag     | 데이터 쓰기 중에 출력 스트림 `Flush` API가 호출될 때 데이터를 동기적으로 플러시할지 여부를 지정합니다. 기본값은 `false`(비동기 플러시)입니다. 동기화 플러시가 필요한 경우 이 구성 항목을 `true`로 설정하십시오. | false | No |

