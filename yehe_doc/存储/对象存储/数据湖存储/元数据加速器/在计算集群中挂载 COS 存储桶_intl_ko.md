## 소개

COS(Cloud Object Storage)에서는 메타데이터 가속을 활성화하여 HDFS 프로토콜 액세스 기능을 얻을 수 있습니다. 메타데이터 가속이 활성화되면 COS는 버킷에 대한 마운트 포인트를 생성합니다. 그런 다음 [HDFS 클라이언트](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)를 다운로드하고 클라이언트의 마운트 포인트를 사용하여 COS를 마운트할 수 있습니다. 본 문서에서는 컴퓨팅 클러스터에 메타데이터 가속이 활성화된 버킷을 마운트하는 방법을 소개합니다.

>! 
>- Hadoop-cos는 버전 8.1.5부터 `cosn://bucketname-appid/` 메소드에서 메타데이터 가속 버킷에 대한 액세스를 지원합니다.
>- 메타데이터 가속 기능은, 메모리 버킷 생성 시에만 활성화할 수 있으며 활성화 후에는 비활성화할 수 없습니다. 비즈니스 상황에 따라 활성화 여부를 **신중하게 고려**하십시오. 또한, 이전 버전의 Hadoop-cos 패키지는 일반적으로 메타데이터 가속이 활성화된 버킷에는 액세스할 수 없습니다.

## 전제 조건

- [Java 1.8](https://www.oracle.com/java/technologies/downloads/)은 마운트할 컴퓨팅 클러스터의 머신 또는 컨테이너에 설치됩니다.
- 마운트할 컴퓨팅 클러스터의 머신 또는 컨테이너에 액세스 권한이 부여됩니다. HDFS 권한 구성에서 액세스할 수 있는 VPC 및 IP를 지정해야 합니다.
- 종속 JAR 패키지 설명:
1. [chdfs_hadoop_plugin_network-2.8.jar](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) verison>=2.7;
2. [cos_api-bundle.jar](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar) version>=5.6.69;
3. [Hadoop-cos](https://github.com/tencentyun/hadoop-cos/releases) version>=8.1.5
4. ofs-java-sdk.jar(version >=1.0.4)는 설치 없이 자동으로 풀링하며, hadoop fs ls를 성공적으로 실행한 후 해당 버전이 fs.cosn.trsf.fs.ofs.tmp.cache.dir에 의해 구성된 디렉터리에서 예상과 부합하는지 확인합니다.

## 작업 단계
1. [Hadoop 클라이언트 설치 패키지](https://github.com/tencentyun/hadoop-cos/releases)를 다운로드합니다.
2. [POSIX Hadoop 클라이언트 설치 패키지](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)를 다운로드합니다.
3. [cos java sdk 설치 패키지](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar)를 다운로드합니다.
4. 설치 패키지를 각 노드의 classpath 아래에 두어 작업 시작이 정상적으로 로딩될 수 있도록 합니다(예: `$HADOOP_HOME/share/hadoop/common/lib/' 아래).
>! EMR 환경은 종속 jar 패키지와 함께 제공되므로 설치할 필요가 없습니다. POSIX semantics를 통해 메타데이터 가속 버킷에 직접 액세스할 수 있습니다. s3 프로토콜을 사용하여 액세스해야 하는 경우, fs.cosn.posix_bucket.fs.impl 구성 항목을 변경하고 자세한 내용은 아래를 참고하십시오.
>
5.`core-site.xml` 파일을 편집하여 다음 기본 설정을 추가합니다. 
```
<!--계정에 대한 API Keys 정보입니다. [액세스 관리 콘솔](https://console.cloud.tencent.com/capi)에 로그인하면 Tencent Cloud API 키를 조회할 수 있습니다. -->
<property>
		 <name>fs.cosn.userinfo.secretId/secretKey</name>
		 <value>AKIDxxxxxxxxxxxxxxxxxxxxx</value>
</property>

<!--cosn의 구현 클래스-->
<property>
		 <name>fs.AbstractFileSystem.cosn.impl</name>
		 <value>org.apache.hadoop.fs.CosN</value>
</property>

<!--cosn의 구현 클래스-->
<property>
		 <name>fs.cosn.impl</name>
		 <value>org.apache.hadoop.fs.CosFileSystem</value>
</property>

<!--ap-guangzhou 형식의 사용자 버킷 리전 정보-->      
<property>
		 <name>fs.cosn.bucket.region</name>
		 <value>ap-guangzhou</value>
</property>

<!--실행 중 생성된 임시 파일을 저장하는 데 사용되는 로컬 임시 디렉터리->      
<property>
		 <name>fs.cosn.tmp.dir</name>
		 <value>/tmp/hadoop_cos</value>
</property>
```
4. `core-site.xml`을 모든 `hadoop` 노드에 동기화 합니다. 
>? EMR 클러스터의 경우, 상기 3, 4단계를 통해 EMR 콘솔 컴포넌트 관리에서 HDFS 설정을 수정할 수 있습니다.
>
5. `hadoop fs` 명령줄 도구를 사용하여 `hadoop fs -ls cosn://${bucketname-appid}/` 명령을 실행합니다. 여기서 `bucketname-appid`는 마운트 주소, 즉 버킷 이름입니다. 파일 목록이 제대로 출력되면 COS 버킷이 성공적으로 마운트된 것입니다.
6. `hadoop` 또는 `mr` 작업의 다른 구성 항목을 사용하여 메타데이터 가속이 활성화된 버킷에서 데이터 작업을 실행할 수도 있습니다. `mr` 작업의 경우 `-Dfs.defaultFS=ofs://${bucketname-appid}/`를 통해 작업의 기본 입력 및 출력 파일 'FS'를 해당 버킷으로 변경할 수 있습니다.

## 설정 항목 설명

### 1. 일반 필수 구성 항목

| 구성 항목                              | 구성 항목 콘텐츠                         | 설명                                                         |
| ----------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| fs.cosn.userinfo.secretId/secretKey | 형식은 AKIDxxxxxxxxxxxxxxxxxxxx와 같습니다 | 사용자 계정의 API 키 정보를 입력합니다. [CAM 콘솔](https://console.cloud.tencent.com/capi)에 로그인하여 Tencent Cloud API 키를 확인할 수 있습니다. |
| fs.cosn.impl                        | org.apache.hadoop.fs.CosFileSystem | cosn은 FileSystem에 대한 구현 클래스로 고정되어 있습니다.                           |
| fs.AbstractFileSystem.cosn.impl     | org.apache.hadoop.fs.CosN          | cosn은 AbstractFileSystem의 구현 클래스로 고정되어 있습니다.                |
| fs.cosn.bucket.region           | 형식은 ap-beijing과 같습니다.               | 액세스할 버킷의 리전 정보를 입력합니다. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)의 도메인 약칭을 참고하십시오. 예: ap-beijing, ap-guangzhou 등. 기존 설정 호환: fs.cosn.userinfo.region |
| fs.cosn.tmp.dir                     | 기본값/tmp/hadoop_cos                | 실제 존재하는 로컬 디렉터리를 입력합니다. 실행 과정에서 생성되는 임시 파일이 잠시 해당 디렉터리에 저장됩니다. 동시에 각 노드의 디렉터리에 대해 충분한 공간과 권한을 구성하는 것이 좋습니다. |



### 2. POSIX 액세스 모드 필수 구성 항목(권장 방식)

| 구성 항목                 | 구성 항목 콘텐츠     | 설명 |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.posix_bucket.fs.impl         | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter                |      POSIX 모드 액세스 구성은 com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter입니다. S3 프로토콜 모드 액세스 구성은 기본 POSIX 모드 액세스인 org.apache.hadoop.fs.CosNFileSystem입니다.               |
| fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl | com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter                      |      메타데이터 버킷 액세스 구현 클래스                                           |
| fs.cosn.trsf.fs.ofs.impl                    | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter                |     메타데이터 버킷 액세스 구현 클래스                                                          |
| fs.cosn.trsf.fs.ofs.tmp.cache.dir           | 형식은 /data/emr/hdfs/tmp/posix-cosn/과 같습니다.  |실제 로컬 디렉터리를 설정하면 작업 중 생성된 임시 파일이 여기에 임시 저장됩니다. 동시에 "/data/emr/hdfs/tmp/posix-cosn/"과 같이 각 노드에서 이 디렉터리에 대한 충분한 공간과 권한을 구성하는 것이 좋습니다.                                                                      |
| fs.cosn.trsf.fs.ofs.user.appid              | 형식은 12500000000과 같습니다.  | 필수. 사용자 appid |
| fs.cosn.trsf.fs.ofs.bucket.region           | 형식은 ap-beijing과 같습니다.  | 필수. 사용자 bucket의 region |


### 3. S3 프로토콜 액세스 모드 필수 구성 항목

| 구성 항목                 | 구성 항목 콘텐츠     | 설명 |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.posix_bucket.fs.impl         | org.apache.hadoop.fs.CosNFileSystem |      POSIX 모드 액세스 구성은 com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter입니다. S3 프로토콜 모드 액세스 구성은 기본 POSIX 모드 액세스인 org.apache.hadoop.fs.CosNFileSystem입니다.                                        |

### 4. 기타 구성 항목

- [기타 Hadoop-cos 설정 항목](https://intl.cloud.tencent.com/document/product/436/6884)
- [기타 POSIX 모드 설정 항목](https://intl.cloud.tencent.com/document/product/1106/41965), 다른 POSIX 모드 구성 항목은 "fs.cosn.trsf." 접두사를 추가하여 메타데이터 가속 버킷에 액세스하는 데 사용할 수 있습니다.

### 5. 주의사항

1. 이전 hadoop cos jar 패키지를 사용하여 메타데이터 가속이 활성화된 bucket에 액세스할 수 없습니다.
2. Hadoop cos <= 8.1.5 버전 posix를 사용하여 메타데이터 가속 bucket에 액세스하려면 콘솔에서 ranger 인증을 비활성화해야 합니다.


