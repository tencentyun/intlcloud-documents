## 배경

COS Ranger Service는 Tencent Cloud 스토리지-컴퓨팅 분리를 기반으로 한 빅 데이터 권한 제어 솔루션입니다. 미세한 세분성, Hadoop Ranger와의 호환성 및 플러그형 아키텍처를 특징으로하며 빅 데이터 컴포넌트와 클라우드의 스토리지 권한을 중앙에서 관리할 수 있도록 도와줍니다. 서비스 및 아키텍처 스키마에 대한 자세한 내용은 [COS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/436/39144)을 참고하십시오.

Cos Ranger Service는 출시 이후 널리 사용되었습니다. 다양한 비즈니스와 복잡한 배경을 가지고 있는 고객들의 질문에 답변하기 위해, 본문은 서비스와 버전 세부 사항 및 주의사항에 대해 설명합니다.

## 버전 설명

### 컴포넌트

컴포넌트에는 Ranger-Plugin, COS Ranger Server, COS Ranger Client (즉, Hadoop-Ranger-Client) 및 COSN Ranger Interface가 포함됩니다.

#### Ranger-Plugin

Ranger 프로토콜(자세한 내용은 [Apache 공식 문서](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=53741207)를 참고하십시오)을 기반으로 Ranger 서버에서 서비스 지정 플러그인을 제공하고 Ranger측의 COS 서비스 설명을 제공합니다. 이 플러그인이 배포 된 후에는 Ranger 제어 페이지에 Path, Bucket, user 및 group 액세스 정책과 같은 COS 권한 정책을 입력 할 수 있습니다.  

#### COS Ranger Server

Ranger의 클라이언트를 통합하고, 주기적으로 Ranger 서버에서 권한 정책을 동기화하며, 인증 요청을 수신 한 후 로컬에서 권한을 확인합니다. 또한, Hadoop에서 DelegationToken 생성 및 갱신 API를 제공합니다.

EMR 환경에서는 기본적으로 /usr/local/service/cosranger/lib에 설치됩니다. 예를 들어, 패키지 이름 cos-ranger-service-5.1.2-jar-with-dependencies.jar, 5.1.2는 cos ragner server의 버전 번호입니다.

#### COS Ranger Client

Hadoop sdk 플러그인은 core-site.xml 파일의 구성에 따라 COS Ranger 클라이언트를 동적으로 로딩하고 COS Ranger Server로 권한 확인 요청을 포워딩합니다.  

EMR 환경에서는 기본적으로 /usr/local/service/hadoop/share/hadoop/common/lib에 설치됩니다. 예를 들어, 패키지 이름 hadoop-ranger-client-for-hadoop-2.8.5-5.0.jar에서 2.8.5는 hadoop 버전 번호이고 5.0은 패키지 버전 번호입니다.

#### COSN Ranger Interface

이 플러그인은 COS Ranger Client 및 COS Ranger Client의 공통 데이터 및 API에 의해 정의됩니다.

EMR 환경에서는 /usr/local/service/hadoop/share/hadoop/common/lib에 설치됩니다. 예를 들어, 패키지 이름 cosn-ranger-interface-1.0.4.jar에서 1.0.4는 COSN Ranger Interface의 버전 번호입니다.

[Github](https://github.com/tencentyun/cos-ranger-service)에서 상기 jar 패키지를 가져올 수 있습니다. impala 및 presto의 COS Ranger Client 패키지와 같은 다른 컴포넌트의 경우 EMR 팀에 문의하십시오.  

상기 컴포넌트는 EMR 콘솔에서 Ranger 및 cosranger 컴포넌트를 구매할 때 자동으로 설치됩니다. [CHDFS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/1106/41973)의 지침에 따라 직접 설치할 수도 있습니다.

### 버전 설명 

버전은 핵심 아키텍처에 따라 두 가지 유형으로 나눌 수 있습니다: **zookeeper에 의존하는 서비스 등록 및 검색**과 **zookeeper에 의존하지 않는 서비스 등록 및 검색**입니다. COS Ranger Server는 COS Ranger Client가 호출 할 수 있는 서비스를 제공합니다.  
- COS Ranger Client가 zookeeper를 통해 COS Ranger Server의 서비스 주소를 검색하면 **zookeeper에 의존하는 버전**에만 특정한 기능인 zookeeper 주소를 구성해야 합니다.
- COS Ranger Client가 zookeeper에 의존하지 않고 COS Ranger Server 서비스를 검색하는 경우 **zookeeper 에 의존하지 않는 버전**에만 특정한 기능인 COS Ranger Server의 서비스 주소를 직접 지정하는 qcloud.object.storage.ranger.service.address를 구성해야 합니다.

### 버전 매핑

| 컴포넌트 | zookeeper에 의존하는 서비스 등록 및 검색 | zookeeper에 의존하지 않는 서비스 등록 및 검색 |
| ---- | --- | ---- |
|COS Ranger Server| v5.0.9 이하 | v5.1.1 이상 |
|COS Ranger Client | v3.9 이하 | v4.1 이상 |
|COSN Ranger Interface | v1.0.3 | v1.0.4 이상 |

>! **서비스 등록 및 검색을 위해 zookeeper에 의존하지 않는** 버전을 사용하는 경우 COS Ranger Server는 v5.1.1 이상(**v5.1.2** 권장)이어야 하며 COS Ranger Client는 v4.1 이상(**v5.0** 권장)이어야 하며 COSN Ranger Interface는 v1.0.4 이상이어야 합니다.
>

### 버전 호환성

버전은 상기 두 가지 유형을 기반으로 매핑할 수 있습니다. 그러나 복잡한 배경을 가진 고객의 다양성으로 인해 버전이 두 가지 유형으로 구분되지 않을 수 있으므로 컴포넌트 간의 호환성 관계는 다음과 같습니다. 같은 행에 있는 컴포넌트는 서로 호환됩니다.

| COS Ranger Client 버전   | COS Ranger Server 버전  | COSN Ranger Interface 버전| 서비스 등록 및 검색을 위한 zookeeper 의존성  |
|  -----------------------|  ----------------------  | ------------------------ | ------|
|   version ≤ v3.9       |    version ≤ v5.0.9     |       v1.0.3             |  Yes |
|   version ≤ v3.9       |    version ≥ v5.1.1     |       v1.0.4             |  Yes |
|   version ≥ v4.1       |    version ≥ v5.1.1     |       v1.0.4             |  No |
|   version ≥ v5.0       |    version ≤ v5.0.9     |       v1.0.4             |  Yes |
|   version ≥ v5.0       |    version ≥ v5.1.1     |       v1.0.4             |  No |


>!
> - COS Ranger Client v5.0은 모든 버전의 COS Ranger Server와 호환됩니다.
> - COS Ranger Client v4.1은 COS Ranger Server v5.1.1 이상과만 호환됩니다.
> - COS Ranger Client v3.x는 모든 버전의 COS Ranger Server와 호환되지만 COS Ranger Server 서비스를 검색하기 위해 zookeeper에 의존할 수밖에 없습니다 (zookeeper에 의존하는 버전의 단점은 아래에서 자세히 설명됩니다).
> - COS Ranger Client 및 COSN Ranger Interface 패키지는 hadoop sdk 플러그인이 동적으로 로딩되도록 동일한 디렉터리에 배치되어야 합니다.
> 

### 사용 설명

- 콘솔에서 메타데이터 가속 버킷 또는 CHDFS 파일 시스템에 대해 Ranger 검증을 활성화해야 합니다.
- **서비스 등록 및 검색을 위해 zookeeper에 의존**하는 버전을 사용하는 경우 core-site.xml에서 qcloud.object.storage.zk.address, value를 zookeeper 주소로 설정해야 합니다(여러 개의 주소는 쉼표로 구분).
- COS Ranger Server v5.1.1 또는 v5.1.2를 사용하지만 COS Ranger Client v3.x를 사용하는 경우 서비스 등록 및 검색을 위해 여전히 zookeeer에 의존해야 하므로 core-site.xml에서 qcloud.object.storage.zk.address, value를 zookeeer 주소로 설정해야 합니다(여러 개의 주소는 10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181과 같이 쉼표로 구분).
- **서비스 등록 및 검색을 위해 ZooKeeper에 의존하지 않는** 버전을 사용하는 경우 qcloud.object.storage.ranger.service.address, value를 core-site.xml에서 COS Ranger Server의 서비스 주소로 설정해야 합니다(여러 개의 주소는 `127.0.0.1:9999,128.0.0.1:9999`와 같이 쉼표로 구분).
- ofs 프로토콜을 사용하여 액세스하려면 core-site.xml에서 fs.ofs.ranger.enable.flag를 true로 설정해야 합니다.
- cosn 프로토콜을 사용하여 액세스하려면 core-site.xml에서 fs.cosn.credentials.provider를 org.apache.hadoop.fs.auth.RangerCredentialsProvider로 설정해야 합니다.

### 구성 항목 설명

| 구성 항목 | 설명 | 예 |
| --- | --- | --- |
| qcloud.object.storage.zk.address | COS Ranger Server 등록을 위한 zk 주소 | 10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181  |
| qcloud.object.storage.ranger.service.address | COS Ranger Server RPC 서비스 주소 | 127.0.0.1:9999,128.0.0.1:9999 |
| fs.ofs.ranger.enable.flag | ofs 프로토콜 사용 시 Ranger 토글 | true |
| fs.cosn.credentials.provider | cosn 프로토콜 사용 시 Ranger 인증 클래스 경로 | org.apache.hadoop.fs.auth.RangerCredentialsProvider |
| fs.cosn.posix.bucket.use_ofs_ranger.enabled | chdfs ranger 인증 사용 여부| 기본값은 false이며 COSN Ranger 인증을 나타냅니다. <br>true로 설정하면 chdfs ranger 인증을 사용합니다. <br>참고: 이 구성 항목은 hadoop-cos v8.1.7 이상에 추가되었습니다.  |


### 구성 항목

| 컴포넌트 버전 | 구성 항목 |
| --- | --- |
| cos ranger verser ≤ v5.0.9<br> cos ranger client ≤ v3.9 OR = v5.0<br> ofs 프로토콜을 통한 액세스| qcloud.object.storage.zk.address<br> fs.ofs.ranger.enable.flag |
| cos ranger verser ≤ v5.0.9<br> cos ranger client ≤ v3.9 OR = v5.0<br> cosn 프로토콜을 통한 액세스| qcloud.object.storage.zk.address<br> fs.cosn.credentials.provider |
| cos ranger verser = v5.1.1 OR = v5.1.2<br> cos ranger client ≥ v4.1<br> ofs 프로토콜을 통한 액세스|qcloud.object.storage.ranger.service.address<br> fs.ofs.ranger.enable.flag|
| cos ranger verser = v5.1.1 OR = v5.1.2<br> cos ranger client ≥ v4.1<br> cosn 프로토콜을 통한 액세스|qcloud.object.storage.ranger.service.address<br> fs.cosn.credentials.provider|

>!
> - cosn 프로토콜을 통해 메타데이터 가속 버킷에 액세스하고 chdfs ranger 인증을 수행하려면 fs.cosn.posix.bucket.use_ofs_ranger.enabled를 true로 설정해야 합니다. 또한 hadoop-cos 버전은 v8.1.7 이상이어야 합니다.
> - 상기 구성 항목을 추가하거나 수정하는 경우 YARN의 ResourceManager/NodeManager, Hive의 HiveMetaStore/HiveServer2, Impala 및 Presto의 애플리케이션과 같은 빅 데이터 컴포넌트를 다시 시작해야 합니다.
> 

### 권장 버전

| 컴포넌트 | 버전 번호 |
| ---| ---|
| cos-ranger-server| >= v5.1.2 |
| cos-ranger-client| >= v5.0   |
| cosn-ranger-interface| >= v1.0.4|


### 권장 사항 설명

상기 버전은 다음과 같은 이유로 권장됩니다.

- zookeeper는 마스터 선택에만 사용되며 서비스 등록 및 검색에는 사용되지 않으므로 빅 데이터 작업 중에 zookeeper에 대한 부담을 크게 완화합니다. 각각의 빅 데이터 작업 중에 많은 수의 작업이 zookeeper에 액세스하여 COS Ranger Server 서비스를 검색하므로 zookeeper에 큰 부담이 되고 다른 빅 데이터 컴포넌트의 안정성에 영향을 미칩니다.
- v5.0의 hadoop-ranger-client 패키지는 COS Ranger Server 패키지의 초기 버전과 호환되므로 이전 사용자가 COS Ranger Server를 쉽게 업그레이드할 수 있습니다.
- COS Ranger Server 5.1.2 이전 버전에서는 획득한 leader IP가 leader latch의 IP와 다를 수 있습니다. 또한 COS Ranger Server가 zk에 등록하는 정보는 후속 확장 또는 업그레이드를 용이하게 하기 위해 단순화됩니다.
- 여러 bug가 수정되었습니다.


## 인증 FAQ

### IOException: init fs.ofs.ranger.client.impl failed 오류가 보고되면 어떻게 해야 하나요?

- Caused by: java.io.IOException: invalid zk address null이 출력되는 경우 qcloud.object.storage.zk.address, value를 core-site.xml에서 zookeeper 주소로 설정해야 합니다(여러 개의 주소는 10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181과 같이 쉼표로 구분).
- Caused by: java.io.IOException: ranger client is null, maybe ranger server for qcloud object storage is not deployed!가 표시되면 다음 질문을 참고하십시오.

### ranger client is null, maybe ranger server for qcloud object storage is not deployed! 오류가 보고되면 어떻게 해야 합니까?

오류 원인은 다음과 같습니다.
- hadoop-ranger-client 패키지가 v3.8 이하인 경우 zookeeper watch가 손실될 수 있습니다. 이 경우 패키지를 v5.0으로 업그레이드하는 것이 좋습니다.
- 구성 항목 qcloud.object.storage.zk.address 또는 qcloud.object.storage.ranger.service.address를 확인합니다.
- COS Ranger Server 서비스 및 프로세스가 정상인지 확인하십시오.

### Expect ranger service addresses: [127.0.0.1:6080,128.0.0.1:6080], but actual ranger service address 오류가 보고되면 어떻게 해야 하나요?

![오류 보고 이미지](https://qcloudimg.tencent-cloud.cn/raw/5cc5ce4451bbe5bfe91835befd1a49db.png)

- 이 오류는 메타데이터 가속 버킷 또는 CHDFS에 대해 Ranger 인증이 콘솔에서 활성화되었지만 클라이언트에서는 활성화되지 않았기 때문에 발생합니다.
- ofs 프로토콜을 사용하여 액세스하려면 core-site.xml에서 fs.ofs.ranger.enable.flag를 true로 설정해야 합니다.
- cosn 프로토콜을 사용하여 액세스하려면 core-site.xml에서 fs.cosn.credentials.provider를 org.apache.hadoop.fs.auth.RangerCredentialsProvider로 설정해야 합니다.

### RangerQcloudObjectStorageClient 클래스가 없으면 어떻게 해야 하나요?

![오류 보고 이미지](https://qcloudimg.tencent-cloud.cn/raw/6558d81d1269320c53379c44c7f254ca.png)

- cosn-ranger-interface 패키지가 누락되었습니다. [Github](https://github.com/tencentyun/cos-ranger-service)의 cosn-ranger-interface 디렉터리에서 가져올 수 있습니다.
- 다른 관련 클래스를 찾을 수 없습니다. cosn-ranger-interface 및 hadoop-ranger-client 패키지가 존재하는지, 버전이 일치하는지, 올바른 경로에 배치되었는지 확인합니다.
- 다른 해당 클래스가 없는 경우 패키지 shade 경로 때문일 수 있습니다. 이 경우 당사에 도움을 요청하십시오.

### NoSuchMethodError 오류가 보고되면 어떻게 해야 하나요?

![오류 보고 이미지](https://qcloudimg.tencent-cloud.cn/raw/4b3fdbf027180095ca32292d54a05279.jpg)

이 오류는 메소드가 원래 존재하지만 로딩된 클래스에 없기 때문에 발생하며 다음과 같은 원인일 수 있습니다.

- 버전 반복 후 이 메소드가 패키지에 추가되었지만 이전 버전에는 존재하지 않습니다.
- 다른 패키지에 있는 같은 이름의 클래스가 로딩되었습니다.

/usr/local/service에서 다음 명령을 실행합니다.
```
find . -name "*.jar" -exec grep -Hls "org/apache/hadoop/fs/cosn/ranger/client/RangerQcloudObjectStorageClientImpl" {} \;
```
관련 패키지를 찾아 삭제합니다. 다른 클래스의 경우 상기 명령에서 클래스 경로를 수정하기만 하면 됩니다.

### java.lang.ClassCastException org.apache.hadoop.fs.cosn.ranger.protocol.ClientQCloudObjectStorageProtocolProtos$GetSTSRequest cannot be cast to com.google.protobuf.Message 오류가 보고되면 어떻게 해야 하나요?

이와 유사한 오류는 일반적으로 패키지 오염 문제입니다. 이전 버전의 패키지가 서버에 존재하고 protobuf 프로토콜이 일치하지 않아 발생하며, 일반적으로 아래의 alluxio 패키지 오염과 동일합니다.  

/usr/local/service에서 다음 명령을 실행합니다.
```
find . -name "*.jar" -exec grep -Hls "org/apache/hadoop/fs/cosn/ranger/protocol/ClientQCloudObjectStorageProtocolProtos" {} \;
```
관련 패키지를 찾아 삭제합니다. 다른 클래스의 경우 상기 명령에서 클래스 경로를 수정하기만 하면 됩니다.

### 수정된 Ranger policy이 적용되지 않으면 어떻게 해야 하나요?

- chdfs 정책의 경우 COS Ranger Server 구성 파일 ranger-chdfs-security.xml에서 밀리초 단위로 ranger.plugin.chdfs.policy.pollIntervalMs 값을 줄입니다.
- cosn 정책의 경우 COS Ranger Server 구성 파일 ranger-cos-security.xml에서 밀리초 단위로 ranger.plugin.cos.policy.pollIntervalMs 값을 줄입니다.

### Ranger policy에 대해 구성된 group이 적용되지 않으면 어떻게 해야 합니까?

구성된 user가 적용되면 EMR 팀에 연락하여 group 동기화를 확인해야 합니다. 기타 상황은 당사에 연락하여 도움을 받으십시오.

### Ranger policy 에서 스토리지 경로 정책 규칙을 구성하려면 어떻게 해야 합니까?

Ranger에는 주로 문자열 일치를 기반으로 하는 간단한 Path 인증 규칙이 있습니다. policy의 path 규칙이 파일 /a/b/c에 대해 **/a/** 로 설정된 경우 sdk가 끝에서 **/** 를 제거하고 경로는 Ranger에서 **/a** 가 되며 **/a/** 와 일치할 수 없기 때문에 **/a** 또는 **/a/** 를 통해 파일에 액세스할 수 없습니다. **/a/b** 또는 **/a/b/c** 에 액세스하는 경우 두 path의 접두사가 policy의 path 규칙 **/a/** 과 일치할 수 있습니다.

### 테이블 생성을 위해 Hive에서 COSN 또는 OFS 경로를 지정할 때 HiveAccessControlException 오류가 보고되면 어떻게 해야 합니까?

![오류 보고 이미지](https://qcloudimg.tencent-cloud.cn/raw/928c7f08b597170da831dcca0e7edc42.png)

ranger 콘솔에서 hive의 URL을 허용하는 권한을 구성하여 hive에서 url 인증을 비활성화해야 합니다.

![Ranger Admin](https://qcloudimg.tencent-cloud.cn/raw/8db0474e6ec152f92b61c98f6ac5d83c.png)

>! Ranger 서비스에서 보고될 가능성이 높은 오류 로그 형식에 유의해야 하며, 대부분의 경우 ranger admin이 구성한 권한이 올바르지 않아 오류가 발생합니다.

### 인증에 kerberos를 사용하는 환경에서 spark 작업을 제출할 때 HiveAccessControlException 오류가 보고되면 어떻게 해야 하나요?

응용 프로그램이 다른 보안 Hadoop 파일 시스템과 상호 작용해야 하는 경우 시작 중에 해당 URI를 Spark에 명시적으로 제공해야 합니다. [Spark 보안](https://spark.apache.org/docs/latest/security.html)에 설명된 대로 spark.kerberos.access.hadoopFileSystems=cosn://bucket-appid,ofs://f4mxxxxxxxx-Xxxx.chdfs.ap-guangzhou.myqcloud.com 매개변수를 구성할 수 있습니다.

### 테이블이 SPARK에 삭제된 후 휴지통으로 이동되지 않으면 어떻게 해야 하나요?

Spark에서 create table을 실행할 때 Location을 지정하면 외부 테이블이 생성되고 데이터가 삭제된 후에도 삭제되지 않습니다. 자세한 내용은 [Spark SQL 1.6에서 2.0으로 업그레이드](https://spark.apache.org/docs/latest/sql-migration-guide.html#upgrading-from-spark-sql-16-to-20)를 참고하십시오.

>? hive on mr에서 drop table을 실행하면 데이터가 삭제될 수 있습니다.
>

### Hive가 INSERT 문을 실행할 때 AccessControlException 오류가 보고되면 어떻게 해야 하나요?

Hive의 기본 엔진은 MapReduce입니다. yarn-site.xml 파일에 다음 구성 항목을 추가합니다.
```
<property>
    <name>mapreduce.job.hdfs-servers</name>
    <value>
        ofs://f4mxxxxxxx-XXXX,cosn://bucketname-appid,${fs.defaultFS}
    </value>
</property>
```
hive 엔진이 tez인 경우 tez-site.xml 파일에 tez.job.fs-servers 구성 항목을 추가하고 위의 value로 설정합니다.

beeline을 사용하여 hive에 연결하는 경우 hiveserver2를 다시 시작하고 새 yarn-site 구성을 로딩합니다.

### OFS 액세스 시 오류가 발생하면 어떻게 해야 하나요?

![](https://qcloudimg.tencent-cloud.cn/raw/006df64050758fb2e4551d68335b94dd.png)

오류는 ofs 백엔드에서 반환됩니다. ranger가 활성화된 후 다음 위치에서 posix를 비활성화해야 합니다.

- CHDFS 콘솔

- COS bucket 구성


### YARN 명령을 통해 작업을 제출할 때 renew token failed 오류가 보고되면 어떻게 해야 하나요?

yarn 명령을 실행하려면 -Dmapreduce.job.send-token-conf 매개변수가 필요합니다.

### cosranger는 어떻게 구축하나요?

자세한 내용은 [COS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/436/39144) 및 [CHDFS Ranger 권한 시스템 솔루션](https://intl.cloud.tencent.com/document/product/1106/41973)을 참고하십시오.

### EMR에서 Ranger를 어떻게 활성화합니까?

emr 콘솔에서 Ranger 및 cosranger 컴포넌트를 구매하면 직접 배포할 필요가 없습니다.  
- chdfs의 경우 core-site.xml에 새 구성 항목 fs.ofs.ranger.enable.flag를 추가하고 true로 설정합니다.
- cosn의 경우 core-site.xml에 새 구성 항목 fs.cosn.credentials.provider를 추가하고 다음과 같이 설정합니다.
org.apache.hadoop.fs.auth.RangerCredentialsProvider。

### NodeCache null 포인터 예외가 발생하면 어떻게 해야 하나요?

hadoop-ranger-client 버전을 확인하십시오. v3.8인 경우 v5.0으로 업그레이드하는 것이 좋습니다. 기타 상황은 당사에 연락하여 도움을 받으십시오.
이 오류는 빅 데이터 작업의 동시성이 높고 zookeeper에 대한 압력이 높으며 zookeeper watch가 손실되었기 때문에 발생합니다.

### cosranger가 활성화된 후 hadoop fs 명령을 실행할 때 java.lang.IllegalArgumentException: Failed to specify server's Kerberos principal name 오류가 보고되면 어떻게 해야 합니까?

- core-site.xml에 다음 구성 항목을 추가합니다: qcloud.object.storage.kerberos.principal.
- hdfs 클러스터에서 오류가 보고되면 core-site.xml에 다음 구성 항목을 추가합니다: dfs.namenode.kerberos.principal.
