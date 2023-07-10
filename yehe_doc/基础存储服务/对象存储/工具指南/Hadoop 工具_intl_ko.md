## 기능 설명

Hadoop-COS는 Tencent Cloud Cloud Object Storage(COS)를 기반으로 표준의 Hadoop 파일 시스템을 구현하며 Hadoop, Spark, Tez 등 빅 데이터 연산 프레임워크의 통합을 지원하여 HDFS 파일 시스템 액세스 시와 동일하게 COS에 저장된 데이터를 읽고 쓸 수 있습니다.

Hadoop-COS는 cosn을 URI의 scheme으로 사용하여 CosN 파일 시스템이라고도 합니다.


## 사용 환경

#### 시스템 환경

Linux, Windows, macOS 시스템을 지원합니다.

#### 소프트웨어 종속

Hadoop-2.6.0 이상 버전

>?
>1. 현재 Hadoop-COS는 정식으로 Apache Hadoop-3.3.0에 의해 [공식 통합](https://hadoop.apache.org/docs/r3.3.0/hadoop-cos/cloud-storage/index.html)되었습니다.
>2. Apache Hadoop-3.3.0 이전 버전이거나 CDH에 Hadoop-cos jar 패키지를 통합한 후에는 NodeManager를 재시작해야 jar 패키지를 로딩할 수 있습니다.
>3. 구체적인 Hadoop 버전의 jar 패키지를 컴파일해야 하는 경우 pom 파일의 hadoop.version을 수정하여 컴파일할 수 있습니다.
>



## 다운로드 및 설치

#### Hadoop-COS 배포 패키지 및 해당 종속 획득

다운로드 주소: [Hadoop-COS release](https://github.com/tencentyun/hadoop-cos/releases)。

#### Hadoop-COS 플러그 인 설치

1. `hadoop-cos-{hadoop.version}-{version}.jar`와 `cos_api-bundle-{version}.jar`를`$HADOOP_HOME/share/hadoop/tools/lib`에 복사합니다.
>? Hadoop의 실제 버전에 따라 해당하는 jar 패키지를 선택합니다. release에 매칭되는 버전의 jar 패키지가 없는 경우 직접 pom 파일의 Hadoop 버전을 수정하여 다시 컴파일해 생성할 수 있습니다.
> 
2. hadoop-env.sh 파일을 수정합니다. `$HADOOP_HOME/etc/hadoop` 디렉터리에 들어가 hadoop-env.sh 파일을 편집하고, 다음 내용을 추가하여 cosn 관련 jar 패키지를 Hadoop 환경 변수에 추가합니다.
```shell
for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
  if [ "$HADOOP_CLASSPATH" ]; then
    export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
  else
    export HADOOP_CLASSPATH=$f
  fi
done
```

## 설정 방법

### 설정 항목 설명

|                  속성 키                  | 설명                                                         |                            기본값                            | 필수 여부 |
| :--------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----: |
|   fs.cosn.userinfo.<br>secretId/secretKey    | 사용자 계정의 API 키 정보를 입력합니다. [CAM 콘솔](https://console.cloud.tencent.com/capi)에 로그인하여 Tencent Cloud API 키를 확인할 수 있습니다. |                              없음                              |   예   |
|       fs.cosn.<br>credentials.provider       | SecretId와 SecretKey 획득 방법을 설정합니다. 현재는 다음과 같이 5가지 방법을 지원합니다: <ol  style="margin: 0;"><li>org.apache.hadoop.fs.auth.SessionCredentialProvider: 요청 URI에서 secret id 및 secret key를 획득합니다. 형식: `cosn://{secretId}:{secretKey}@examplebucket-1250000000/`. </li><li>org.apache.hadoop.fs.auth.SimpleCredentialProvider: core-site.xml 구성 파일에서 fs.cosn.userinfo.secretId와 fs.cosn.userinfo.secretKey를 읽어와 SecretId 및 SecretKey를 획득합니다. </li><li>org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: 시스템 환경 변수 COS_SECRET_ID 및 COS_SECRET_KEY에서 획득합니다. </li><li>org.apache.hadoop.fs.auth.SessionTokenCredentialProvider: [임시 키](https://intl.cloud.tencent.com/document/product/436/14048)를 사용하여 액세스합니다. </li><li>org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider: Tencent Cloud CVM 바인딩 역할을 사용하는 COS에 액세스할 수 있는 임시 키를 얻습니다. </li><li>org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider: Tencent Cloud CPM 바인딩 역할을 사용하는 COS에 액세스할 수 있는 임시 키를 얻습니다. </li><li>org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider: Tencent Cloud EMR 인스턴스 바인딩한 역할을 사용하는 COS에 액세스할 수 있는 임시 키를 얻습니다. </li><li>org.apache.hadoop.fs.auth.RangerCredentialsProvider는 ranger를 사용하여 키를 가져옵니다. </li></ol>| 이 매개변수를 지정하지 않으면 기본적으로<br>다음 순서에 따라 읽어옵니다: <ol  style="margin: 0;"><li>org.apache.hadoop.fs.auth.SessionCredentialProvider</li><li>org.apache.hadoop.fs.auth.SimpleCredentialProvider</li><li>org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider</li><li>org.apache.hadoop.fs.auth.SessionTokenCredentialProvider</li><li>org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider</li><li>org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider</li><li>org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider</li></ol> |   아니오   |
| fs.cosn.useHttps | HTTPS를 COS의 백그라운드 전송 프로토콜로 사용할지 여부를 설정합니다. | true | 아니오 |
|               fs.cosn.impl               | cosn은 FileSystem에 대한 구현 클래스로, org.apache.hadoop.fs.CosFileSystem으로 고정되어 있습니다. |                              없음                              |   예   |
|     fs.AbstractFileSystem.<br>cosn.impl      | cosn은 AbstractFileSystem의 구현 클래스로, org.apache.hadoop.fs.CosN으로 고정되어 있습니다. |                              없음                              |   예   |
|          fs.cosn.bucket.region           | 액세스할 버킷의 리전 정보를 입력합니다. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)의 도메인 약칭을 참고하십시오.<br>예: ap-beijing, ap-guangzhou 등, 기존 설정 호환: fs.cosn.userinfo.region |                              없음                              |   예   |
|      fs.cosn.bucket.<br>endpoint_suffix      | 연결할 COS endpoint를 지정하며, 해당 항목은 필수 입력 항목이 아닙니다. 퍼블릭 클라우드 COS 사용자의 경우<br>상기 region 설정만 정확하게 입력하면 됩니다. 기존 설정 호환: fs.cosn.userinfo.endpoint_suffix. 이 항목을 구성할 때 fs.cosn.bucket.region 구성 항목 endpoint를 삭제해야 적용됩니다. | 없음 | 아니오 |
|             fs.cosn.tmp.dir              | 실제 존재하는 로컬 디렉터리를 입력합니다. 실행 과정에서 생성되는 임시 파일이 잠시 해당 디렉터리에 저장됩니다. | /tmp/hadoop_cos | 아니오 |
|          fs.cosn.upload.<br>part.size           | CosN 파일 시스템의 각 block의 크기, 즉 멀티파트 업로드의 각 part size의 크기입니다. COS의 멀티파트 업로드는 최대 10000개까지 가능하므로 사용할 단일 파일의 최대 크기를 예측해야 합니다.<br>예를 들어 part size가 8MB인 경우 최대 78GB의 단일 파일 업로드를 지원합니다. part size는 최대 2GB까지 설정할 수 있으며, 이에 따라 단일 파일 크기는 최대 19TB까지 지원합니다. | 8388608(8MB) |   아니오   |
| fs.cosn.<br>upload.buffer | CosN 파일 시스템에서 업로드 시 종속되는 버퍼 유형입니다. 현재 간접 메모리 버퍼(non_direct_memory),<br>직접 메모리 버퍼(direct_memory), 디스크 매핑 버퍼(mapped_disk) 세 가지 버퍼 유형을 지원합니다.<br>간접 메모리 버퍼는 JVM on-heap 메모리를 사용하며, 직접 메모리 버퍼는 off-heap 메모리를 사용하고, 디스크 매핑 버퍼는 메모리 파일 매핑을 기반으로 버퍼를 획득합니다.| mapped_disk | 아니오 |
| fs.cosn.<br>upload.buffer.size | CosN 파일 시스템에서 업로드 시 종속되는 버퍼 크기입니다. -1로 설정할 경우 버퍼를 제한하지 않는다는 의미이며,<br>버퍼 크기를 제한하지 않을 경우 버퍼 유형은 반드시 mapped_disk로 지정해야 합니다. 0 이상으로 설정할 경우 해당 값은 최소 block 크기 이상이어야 합니다. 기존 설정 호환: fs.cosn.buffer.size。 | -1 | 아니오 |
|  fs.cosn.block.size | CosN 파일 시스템의 block size입니다. | 134217728(128MB)| 아니오 | 
|        fs.cosn.<br>upload_thread_pool        | 파일을 스트리밍 방식으로 COS에 업로드할 때 동시 업로드 스레드 수입니다.                  |                        10                        |   아니오   |
|         fs.cosn.<br>copy_thread_pool         | 디렉터리 복사 작업 시, 파일 동시 복사 및 삭제에 사용할 수 있는 스레드 수입니다.               |                   3                       |   아니오   |
|      fs.cosn.<br>read.ahead.block.size       | 미리 읽어 오는 블록 크기입니다.                                               |                        1048576(1MB)                        |   아니오   |
|      fs.cosn.<br>read.ahead.queue.size       | 미리 읽어 오는 큐 길이입니다.                                             |                              8                               |   아니오   |
|            fs.cosn.maxRetries            | COS 액세스 시 오류가 발생하는 경우, 최대 재시도 횟수입니다.                        |                             200                              |   아니오   |
|      fs.cosn.retry.<br>interval.seconds      | 재시도 시간 간격입니다.                                         |                              3                               |   아니오   |
| fs.cosn.<br>server-side-encryption.algorithm | COS 서버의 암호화 알고리즘을 설정합니다. SSE-C와 SSE-COS를 지원하며, 기본값은 비어 있으며 암호화하지 않습니다. |                              없음                              |   아니오   |
|    fs.cosn.<br>server-side-encryption.key    | COS의 SSE-C 서버 암호화 알고리즘을 활성화하면 반드시 SSE-C 키를 설정해야 합니다.<br>키 형식은 base64으로 인코딩된 AES-256 키로, 기본값은 비어 있으며 암호화하지 않습니다. |                              없음                              |   아니오   |
| fs.cosn.<br>crc64.checksum.enabled | CRC64 검증 활성화 여부입니다. 기본적으로 비활성화되어 있으며, 이 경우 hadoop fs -checksum 명령어를 사용해 파일의 CRC64 검증값을 획득할 수 없습니다. | false | 아니오 |
|fs.cosn.<br>crc32c.checksum.enabled    | CRC32C 검증 활성화 여부입니다.기본적으로 비활성화되어 있으며, 이 경우 hadoop fs -checksum 명령어를 사용해 파일의 CRC32C 검증값을 획득할 수 없습니다. crc32c 또는 crc64 중 하나만 활성화할 수 있습니다.| false | 아니오 |
| fs.cosn.traffic.limit | 업로드 대역폭 제한 옵션으로 819200 - 838860800 bits/s입니다. 기본값은 -1로, 제한하지 않는다는 의미입니다. | 없음 | 아니오 | 


### Hadoop 설정

`$HADOOP_HOME/etc/hadoop/core-site.xml`을 수정하여 COS 관련 사용자 및 구현 클래스 정보를 추가합니다. 예시:

```xml
<configuration>
    <property>
        <name>fs.cosn.credentials.provider</name>
        <value>org.apache.hadoop.fs.auth.SimpleCredentialProvider</value>
        <description>

            This option allows the user to specify how to get the credentials.
            Comma-separated class names of credential provider classes which implement
            com.qcloud.cos.auth.COSCredentialsProvider:

            1.org.apache.hadoop.fs.auth.SessionCredentialProvider: Obtain the secret id and secret key from the URI: cosn://secretId:secretKey@examplebucket-1250000000/;
            2.org.apache.hadoop.fs.auth.SimpleCredentialProvider: Obtain the secret id and secret key
            from fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey in core-site.xml;
            3.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: Obtain the secret id and secret key
            from system environment variables named COS_SECRET_ID and COS_SECRET_KEY.

            If unspecified, the default order of credential providers is:
            1. org.apache.hadoop.fs.auth.SessionCredentialProvider
            2. org.apache.hadoop.fs.auth.SimpleCredentialProvider
            3. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider
            4. org.apache.hadoop.fs.auth.SessionTokenCredentialProvider
            5. org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider
            6. org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider
            7. org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider
        </description>
    </property>
  
    <property>
        <name>fs.cosn.userinfo.secretId</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Id</description>
    </property>
      
    <property>
        <name>fs.cosn.userinfo.secretKey</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Key</description>
    </property>
      
    <property>
        <name>fs.cosn.bucket.region</name>
        <value>ap-xxx</value>
        <description>The region where the bucket is located.</description>
    </property>
      
    <property>
        <name>fs.cosn.bucket.endpoint_suffix</name>
        <value>cos.ap-xxx.myqcloud.com</value>
        <description>
          COS endpoint to connect to. 
          For public cloud users, it is recommended not to set this option, and only the correct area field is required.
        </description>
    </property>
      
    <property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosFileSystem</value>
        <description>The implementation class of the CosN Filesystem.</description>
    </property>
      
    <property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosN</value>
        <description>The implementation class of the CosN AbstractFileSystem.</description>
    </property>

    <property>
        <name>fs.cosn.tmp.dir</name>
        <value>/tmp/hadoop_cos</value>
        <description>Temporary files will be placed here.</description>
    </property>

    <property>
        <name>fs.cosn.upload.buffer</name>
        <value>mapped_disk</value>
        <description>The type of upload buffer. Available values: non_direct_memory, direct_memory, mapped_disk</description>
    </property>

    <property>
        <name>fs.cosn.upload.buffer.size</name>
        <value>134217728</value>
        <description>The total size of the upload buffer pool. -1 means unlimited.</description>
    </property>
	
    <property>
    	<name>fs.cosn.upload.part.size</name>
        <value>8388608</value>
        <description>Block size to use cosn filesysten, which is the part size for MultipartUpload.
        Considering the COS supports up to 10000 blocks, user should estimate the maximum size of a single file.
        For example, 8MB part size can allow  writing a 78GB single file.</description>
    </property>
      
    <property>
    	<name>fs.cosn.maxRetries</name>
      <value>3</value>
      <description>
        The maximum number of retries for reading or writing files to
        COS, before we signal failure to the application.
      </description>
    </property>
      
    <property>
    	<name>fs.cosn.retry.interval.seconds</name>
      <value>3</value>
      <description>The number of seconds to sleep between each COS retry.</description>
    </property>
   
    <property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value></value>
        <description>The server side encryption algorithm.</description>
    </property>	
	
     <property>
    	<name>fs.cosn.server-side-encryption.key</name>
        <value></value>
        <description>The SSE-C server side encryption key.</description>
    </property> 
      
</configuration>
```

여기에서 fs.defaultFS는 생성 환경에서 설정하는 것은 권장하지 않으며, 일부 테스트 시나리오(예: hive-testbench 등)에 사용할 경우 다음 설정 정보를 추가할 수 있습니다.

```
<property>
          <name>fs.defaultFS</name>
          <value>cosn://examplebucket-1250000000</value>
        <description>
             This option is not advice to config, this only used for some special test cases.
        </description>
</property>
```

### 서버 암호화

Hadoop-COS는 서버 암호화를 지원하며, 현재 COS 호스팅 키 방식(SSE-COS), 사용자 지정 키 방식(SSE-C)의 두 가지 암호화 방식을 제공합니다. Hadoop-COS의 암호화 기능은 기본적으로 비활성화 상태로 설정되어 있으며, 사용자는 이를 활성화할 수 있고 다음 방식을 통해 설정할 수 있습니다.

#### SSE-COS 암호화

SSE-COS 암호화는 COS 호스팅 키의 서버 암호화로, Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리합니다. Hadoop-COS 사용 시, 사용자는 `$HADOOP_HOME/etc/hadoop/core-site.xml` 파일에서 다음 설정을 추가하여 SSE-COS 암호화를 구현할 수 있습니다.

```shell
<property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-COS</value>
        <description>The server side encryption algorithm.</description>
</property>
```

#### SSE-C 암호화

SSE-C 암호화는 사용자 지정 키의 서버 암호화입니다. 암호화 키는 사용자가 제공하며, 사용자가 객체 업로드 시 COS가 사용자가 제공한 암호화 키를 사용하여 사용자 데이터에 대해 AES-256 암호화를 진행합니다. Hadoop-COS 시, 사용자는 `$HADOOP_HOME/etc/hadoop/core-site.xml` 파일에 다음 설정을 추가하여 SSE-C 암호화를 구현할 수 있습니다.

```shell
<property>
        <name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-C</value>
        <description>The server side encryption algorithm.</description>
 </property>		
 <property>
  	<name>fs.cosn.server-side-encryption.key</name>
        <value>MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=</value> #사용자가 직접 SSE-C 키를 설정해야 하며, 키 형식은 base64으로 인코딩된 AES-256 키입니다.
        <description>The SSE-C server side encryption key.</description>
 </property> 
```

>!
> - Hadoop-COS의 SSE-C 서버 암호화는 COS의 SSE-C 서버 암호화에 종속됩니다. 따라서 Hadoop-COS에는 사용자가 제공하는 암호화 키가 존재하지 않습니다. 또한 주의해야 할 점은 COS의 SSE-C 서버 암호화 방식은 사용자가 제공하는 암호화 키를 저장하지 않고 암호화 키에 랜덤 데이터인 HMAC 값을 추가하여 저장한다는 것으로, 해당 값을 사용자의 객체 액세스 요청을 검증하는 데 사용합니다. COS는 랜덤 데이터인 HMAC 값을 사용해 암호화 키 값을 유추하거나 암호화 객체 콘텐츠를 복호화할 수 없습니다. 따라서 사용자가 암호화 키를 분실하는 경우 다시는 해당 객체를 획득할 수 없습니다.
> - Hadoop-COS에 SSE-C 서버 암호화 알고리즘을 설정하면 반드시 fs.cosn.server-side-encryption.key 설정 항목에서 SSE-C 키를 설정해야 합니다. 암호화 형식은 base64으로 인코딩된 AES-256 키입니다.
> 

## 사용 방법


### 이용 사례

명령어 형식은 `hadoop fs -ls -R cosn://<BucketName-APPID>/<경로>` 또는 `hadoop fs -ls -R /<경로>`(`fs.defaultFS` 옵션을 `cosn://BucketName-APPID`로 설정해야 함)입니다. 다음은 이름이 examplebucket-1250000000인 bucket을 예시이며, 뒤에 구체적인 경로를 추가합니다.

```shell
hadoop fs -ls -R cosn://examplebucket-1250000000/
-rw-rw-rw-   1 root root       1087 2018-06-11 07:49 cosn://examplebucket-1250000000/LICENSE
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://examplebucket-1250000000/hdfs
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://examplebucket-1250000000/hdfs/2018
-rw-rw-rw-   1 root root       1087 2018-06-12 03:26 cosn://examplebucket-1250000000/hdfs/2018/LICENSE
-rw-rw-rw-   1 root root       2386 2018-06-12 03:26 cosn://examplebucket-1250000000/hdfs/2018/ReadMe
drwxrwxrwx   - root root          0 1970-01-01 00:00 cosn://examplebucket-1250000000/hdfs/test
-rw-rw-rw-   1 root root       1087 2018-06-11 07:32 cosn://examplebucket-1250000000/hdfs/test/LICENSE
-rw-rw-rw-   1 root root       2386 2018-06-11 07:29 cosn://examplebucket-1250000000/hdfs/test/ReadMe
```

MapReduce에 포함되어 있는 wordcount를 실행해 다음 명령어를 실행합니다.

>! 다음 명령어 중 hadoop-mapreduce-examples-2.7.2.jar은 2.7.2 버전의 예시입니다. 버전이 다른 경우 해당하는 버전으로 수정하십시오.
>

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```

실행 완료 후 통계 정보를 반환합니다. 예시는 다음과 같습니다.

```shell
File System Counters
COSN: Number of bytes read=72
COSN: Number of bytes written=40
COSN: Number of read operations=0
COSN: Number of large read operations=0
COSN: Number of write operations=0
FILE: Number of bytes read=547350
FILE: Number of bytes written=1155616
FILE: Number of read operations=0
FILE: Number of large read operations=0
FILE: Number of write operations=0
HDFS: Number of bytes read=0
HDFS: Number of bytes written=0
HDFS: Number of read operations=0
HDFS: Number of large read operations=0
HDFS: Number of write operations=0
Map-Reduce Framework
Map input records=5
Map output records=7
Map output bytes=59
Map output materialized bytes=70
Input split bytes=99
Combine input records=7
Combine output records=6
Reduce input groups=6
Reduce shuffle bytes=70
Reduce input records=6
Reduce output records=6
Spilled Records=12
Shuffled Maps =1
Failed Shuffles=0
Merged Map outputs=1
GC time elapsed (ms)=0
Total committed heap usage (bytes)=653262848
Shuffle Errors
BAD_ID=0
CONNECTION=0
IO_ERROR=0
WRONG_LENGTH=0
WRONG_MAP=0
WRONG_REDUCE=0
File Input Format Counters
Bytes Read=36
File Output Format Counters
Bytes Written=40
```

### Java 코드로 COSN 액세스

```
package com.qcloud.chdfs.demo;

import org.apache.commons.io.IOUtils;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FSDataInputStream;
import org.apache.hadoop.fs.FSDataOutputStream;
import org.apache.hadoop.fs.FileChecksum;
import org.apache.hadoop.fs.FileStatus;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

import java.io.IOException;
import java.net.URI;
import java.nio.ByteBuffer;

public class Demo {
    private static FileSystem initFS() throws IOException {
        Configuration conf = new Configuration();
        // COSN의 구성 항목은 https://cloud.tencent.com/document/product/436/6884#hadoop-.E9.85.8D.E7.BD.AE 에서 확인할 수 있습니다.
        // 다음 설정은 필수 항목입니다. 
        conf.set("fs.cosn.impl", "org.apache.hadoop.fs.CosFileSystem");
        conf.set("fs.AbstractFileSystem.cosn.impl", "org.apache.hadoop.fs.CosN");
        conf.set("fs.cosn.tmp.dir", "/tmp/hadoop_cos");
        conf.set("fs.cosn.bucket.region", "ap-guangzhou");
        conf.set("fs.cosn.userinfo.secretId", "AKXXXXXXXXXXXXXXXXX");
        conf.set("fs.cosn.userinfo.secretKey", "XXXXXXXXXXXXXXXXXX");
        conf.set("fs.ofs.user.appid", "XXXXXXXXXXX");
        // 기타 구성은 공식 웹사이트 문서를 참고하십시오. https://cloud.tencent.com/document/product/436/6884#hadoop-.E9.85.8D.E7.BD.AE
        // CRC64 체크 활성화 여부. 기본적으로 활성화되어 있지 않으며, 이 때 hadoop fs -checksum 명령을 사용하여 파일의 CRC64 체크섬 값을 가져올 수 없습니다.
        conf.set("fs.cosn.crc64.checksum.enabled", "true");
        String cosnUrl = "cosn://f4mxxxxxxxx-125xxxxxxx";
        return FileSystem.get(URI.create(cosnUrl), conf);
    }

    private static void mkdir(FileSystem fs, Path filePath) throws IOException {
        fs.mkdirs(filePath);
    }

    private static void createFile(FileSystem fs, Path filePath) throws IOException {
        // 파일 생성 (이미 있는 경우 덮어쓰기）
        // if the parent dir does not exist, fs will create it!
        FSDataOutputStream out = fs.create(filePath, true);
        try {
            // 파일 입력
            String content = "test write file";
            out.write(content.getBytes());
        } finally {
            IOUtils.closeQuietly(out);
        }
    }

    private static void readFile(FileSystem fs, Path filePath) throws IOException {
        FSDataInputStream in = fs.open(filePath);
        try {
            byte[] buf = new byte[4096];
            int readLen = -1;
            do {
                readLen = in.read(buf);
            } while (readLen >= 0);
        } finally {
            IOUtils.closeQuietly(in);
        }
    }

    private static void queryFileOrDirStatus(FileSystem fs, Path path) throws IOException {
        FileStatus fileStatus = fs.getFileStatus(path);
        if (fileStatus.isDirectory()) {
            System.out.printf("path %s is dir\n", path);
            return;
        }
        long fileLen = fileStatus.getLen();
        long accessTime = fileStatus.getAccessTime();
        long modifyTime = fileStatus.getModificationTime();
        String owner = fileStatus.getOwner();
        String group = fileStatus.getGroup();

        System.out.printf("path %s is file, fileLen: %d, accessTime: %d, modifyTime: %d, owner: %s, group: %s\n",
                path, fileLen, accessTime, modifyTime, owner, group);
    }
    
    private static void getFileCheckSum(FileSystem fs, Path path) throws IOException {
        FileChecksum checksum = fs.getFileChecksum(path);
        System.out.printf("path %s, checkSumType: %s, checkSumCrcVal: %d\n",
                path, checksum.getAlgorithmName(), ByteBuffer.wrap(checksum.getBytes()).getInt());
    }

    private static void copyFileFromLocal(FileSystem fs, Path cosnPath, Path localPath) throws IOException {
        fs.copyFromLocalFile(localPath, cosnPath);
    }

    private static void copyFileToLocal(FileSystem fs, Path cosnPath, Path localPath) throws IOException {
        fs.copyToLocalFile(cosnPath, localPath);
    }

    private static void renamePath(FileSystem fs, Path oldPath, Path newPath) throws IOException {
        fs.rename(oldPath, newPath);
    }

    private static void listDirPath(FileSystem fs, Path dirPath) throws IOException {
        FileStatus[] dirMemberArray = fs.listStatus(dirPath);

        for (FileStatus dirMember : dirMemberArray) {
            System.out.printf("dirMember path %s, fileLen: %d\n", dirMember.getPath(), dirMember.getLen());
        }
    }

    // 재귀 삭제 마크는 디렉터리 삭제에 사용됩니다. 
    // 재귀가 false 이고 dir가 비어있지 않으면 작업이 수행되지 않습니다. 
    private static void deleteFileOrDir(FileSystem fs, Path path, boolean recursive) throws IOException {
        fs.delete(path, recursive);
    }

    private static void closeFileSystem(FileSystem fs) throws IOException {
        fs.close();
    }

    public static void main(String[] args) throws IOException {
        // 파일 초기화
        FileSystem fs = initFS();

        // 파일 생성 
        Path cosnFilePath = new Path("/folder/exampleobject.txt");
        createFile(fs, cosnFilePath);

        // 파일 불러오기
        readFile(fs, cosnFilePath);

        // 파일 또는 디렉터리 조회
        queryFileOrDirStatus(fs, cosnFilePath);

        // 파일 검사합 가져오기
        getFileCheckSum(fs, cosnFilePath);

        // 로컬에서 파일 복사 
        Path localFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
        copyFileFromLocal(fs, cosnFilePath, localFilePath);

        // 파일을 로컬로 가져오기
        Path localDownFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
        copyFileToLocal(fs, cosnFilePath, localDownFilePath);

        listDirPath(fs, cosnFilePath);
        // 이름 변경
        mkdir(fs, new Path("/doc"));
        Path newPath = new Path("/doc/example.txt");
        renamePath(fs, cosnFilePath, newPath);

        // 파일 삭제
        deleteFileOrDir(fs, newPath, false);

        // 디렉터리 생성
        Path dirPath = new Path("/folder");
        mkdir(fs, dirPath);

        // 디렉터리에 파일 생성
        Path subFilePath = new Path("/folder/exampleobject.txt");
        createFile(fs, subFilePath);

        // 디렉터리 나열
        listDirPath(fs, dirPath);

        // 디렉터리 삭제
        deleteFileOrDir(fs, dirPath, true);
        deleteFileOrDir(fs, new Path("/doc"), true);

        // 파일 시스템 비활성화 
        closeFileSystem(fs);
    }
}
```

## FAQ
Hadoop 툴 사용 중 문의 사항이 있는 경우 [Hadoop 툴 관련 FAQ](https://intl.cloud.tencent.com/document/product/436/35706)를 참고하십시오.
