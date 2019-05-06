## 기능 설명
Hadoop cosn 플러그인은 Tencent Cloud COS를 기본 저장소로 사용하는 파일 시스템에서 상위 계층 컴퓨팅 작업을 실행할 수 있는 기능을 제공합니다. Hadoop 빅데이터 처리 엔진, 예를 들어 MapReduce，Hive、Spark、Tez 등을 사용하여 Tencent Cloud COS에 저장된 데이터를 처리할 수 있습니다.

## 사용 환경
### 운영 체제
Linux, Windows 및 MacOS 시스템을 지원합니다.

### 소프트웨어 의존
Hadoop-2.6.0 및 이상 버전.

## 다운로드 및 설치

### hadoop-cos 플러그인 확득
다운로드 링크: [hadoop-cos 플러그인](https://github.com/tencentyun/hadoop-cos).


### hadoop-cos 플러그인 설치

1. dep 디렉터리 아래의 cos_hadoop_api-5.2.6.jar과 hadoop-cos-2.X.X.jar을 `$HADOOP_HOME/share/hadoop/tools/lib` 아래에 복사합니다.
>?Hadoop의 버전에 따라 jar 패키지를 선택하십시오. dep 디렉터리에 일치하는 버전의 jar 패키지가 없으면 pom 파일에서 Hadoop의 버전 번호를 수정하여 다시 컴파일하고 생성할 수 있습니다.

2. hadoop_env.sh를 수정합니다.
`$HADOOP_HOME/etc/hadoop`디렉터리 아래 hadoop_env.sh에 들어가서 다음 내용을 추가하고 cosn 관련 jar 패키지를 Hadoop 환경 변수에 추가하십시오.
```shell
for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
  if [ "$HADOOP_CLASSPATH" ]; then
    export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
  else
    export HADOOP_CLASSPATH=$f
  fi
done
```

## 사용 방법

### 구성 항목 설명

| 속성키                             | 설명                |기본값|필수 항목|
|:-----------------------------------:|:----------------------|:-----:|:-----:|
|fs.cosn.userinfo.secretId/secretKey| 계정의 API 키 정보를 입력하십시오. [콘솔](https://console.cloud.tencent.com/capi)에 로그인하여 클라우드 API 키를 확인하십시오 | 없음  | 예|
|fs.cosn.credentials.provider|secret id와 secret key의 획득 방식을 구성합니다. 두 가지 획득 방식이 지원됩니다. 1.org.apache.hadoop.fs.auth.SimpleCredentialProvider: core-site.xml 구성 파일에서 fs.cosn.userinfo.secretId와 fs.cosn.userinfo.secretKey 읽기로 secret id와 secret key를 획득합니다. 2.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: 운영 체제 변수 COS_SECRET_ID와 COS_SECRET_KEY에서 획득합니다.|구성 항목 수정을 지정하지 않으면 다음과 같은 순서로 읽을 것입니다.1.org.apache.hadoop.fs.auth.SimpleCredentialProvider;2.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider.|아니요|
|fs.cosn.impl                      | cosn는 FileSystem에 대한 구현 클래스는 org.apache.hadoop.fs.CosFileSystem으로 고정됩니다| 없음 |예|
|fs.AbstractFileSystem.cosn.impl   | cosn는 AbstractFileSystem에 대한 구현 클래스는 org.apache.hadoop.fs.CosN으로 고정됩니다| 없음 |예|
|fs.cosn.userinfo.region           | 지역 정보를 입력하십시오. 열거형 값은 [가용 지역](https://cloud.tencent.com/document/product/436/6224)의 지역 약칭입니다. 예를 들어	ap-beijing、ap-guangzhou 등 | 없음 | 예|
|fs.cosn.userinfo.endpoint_suffix | 연결할 COS endpoint를 지정하십시오. 이 항목은 필수 항목입니다. 공용 클라우드 COS 사용자는 위의 지역 구성을 정확하게 입력하면 됩니다|없음|아니요|
|fs.cosn.tmp.dir                | 실제로 존재하는 로컬 디렉터리를 설정하십시오. 실행 중 생성된 임시 파일이 여기에 저장됩니다| /tmp/hadoop_cos | 아니요|
|fs.cosn.buffer.size        | COS에 스트림의 방식으로 파일을 업로드할 때 로컬에서 사용하는 메모리 버퍼의 크기입니다. 하나의 block 크기보다 큰거나 같습니다 | 33554432(32MB)|아니요|
|fs.cosn.block.size                | CosN 파일 시스템의 각 block 크기, 멀티파트 업로드의 각 파트의 크기이기도 합니다. COS의 멀티파트 업로드는 최대 10000개의 block만 지원할 수 있으므로 가능한 최대 파일 크기를 예측해야 합니다. 예를 들어 block 크기가 8MB일 경우 최대 78GB의 단일 파일 업로드를 지원할 수 있습니다. block 크기는 최대 2GB, 즉 단일 파일은 최대 19TB까지 지원합니다| 8388608（8MB） | 아니요 |
|fs.cosn.upload_thread_pool        | COS에 스트림의 방식으로 파일을 업로드할 때 동시 발생한 업로드의 스레드 | CPU코어*5 | 아니요 |
|fs.cosn.copy_thread_pool          |디렉터리 복사를 조작할 때 동시 발생한 업로드의 스레드 | CPU코어*3 | 아니요 |
|fs.cosn.read.ahead.block.size     | 미리 읽기 블록의 크기                                 | 524288(512KB) |  아니요 |
|fs.cosn.read.ahead.queue.size     | 미리 읽기 대기열의 길이                               | 10              | 아니요  |
|fs.cosn.maxRetries				   | COS에 접근하여 오류가 발생할 때 최대 재시도 횟수 | 3 | 아니요 |
|fs.cosn.retry.interval.seconds    | 재시도 시간 간격 | 3 | 아니요 |


### Hadoop 구성

 $HADOOP_HOME/etc/hadoop/core-site.xml을 수정하여 COS 관련 사용자 및 구현 클래스 정보를 추가하십시오. 예를 들면 다음과 같습니다.

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>cosn://<bucket-appid></value>
    </property>

    <property>
        <name>hadoop.tmp.dir</name>
        <value>${HADOOP_PATH}/tmp</value>
    </property>

    <property>
        <name>dfs.name.dir</name>
        <value>${HADOOP_PATH}/name</value>
    </property>

    <property>
        <name>fs.cosn.credentials.provider</name>
        <value>org.apache.hadoop.fs.auth.SimpleCredentialProvider</value>
        <description>

            This option allows the user to specify how to get the credentials.
            Comma-separated class names of credential provider classes which implement
            com.qcloud.cos.auth.COSCredentialsProvider:

            1.org.apache.hadoop.fs.auth.SimpleCredentialProvider: Obtain the secret id and secret key
            from fs.cosn.userinfo.secretId and fs.cosn.userinfo.secretKey in core-site.xml
            2.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider: Obtain the secret id and secret key
            from system environment variables named COS_SECRET_ID and COS_SECRET_KEY

            If unspecified, the default order of credential providers is:
            1. org.apache.hadoop.fs.auth.SimpleCredentialProvider
            2. org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider

        </description>
    </property>

    <property>
        <name>fs.cosn.userinfo.secretId</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Id </description>
    </property>

    <property>
        <name>fs.cosn.userinfo.secretKey</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxxx</value>
        <description>Tencent Cloud Secret Key</description>
    </property>

    <property>
        <name>fs.cosn.userinfo.region</name>
        <value>ap-xxx</value>
        <description>The region where the bucket is located</description>
    </property>

    <property>
        <name>fs.cosn.userinfo.endpoint_suffix</name>
        <value>cos.ap-xxx.myqcloud.com</value>
        <description>
          COS endpoint to connect to.
          For public cloud users, it is recommended not to set this option, and only the correct area field is required.
        </description>
    </property>

    <property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosFileSystem</value>
        <description>The implementation class of the CosN Filesystem</description>
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
    	<name>fs.cosn.buffer.size</name>
        <value>33554432</value>
        <description>The total size of the buffer pool</description>
    </property>

    <property>
    	<name>fs.cosn.block.size</name>
        <value>8388608</value>
        <description>Block size to use cosn filesysten, which is the part size for MultipartUpload.
        Considering the COS supports up to 10000 blocks, user should estimate the maximum size of a single file.
        for example, 8MB part size can allow  writing a 78GB single file.</description>
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

</configuration>
```

### 사용 예시

명령 형식: `hadoop fs -ls -R cosn://bucketname-appid/<경로>` 또는 `hadoop fs -ls -R /<경로>`(fs.defaultFS 옵션은 cosn://bucket-appid로 설정 필요) 다음 예시에는 이름이 examplebucket-1250000000인 버킷을 예로 들어 그 뒤에 구체적인 경로를 추가할 수 있습니다.

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

MapReduce에서 제공하는 wordcount를 실행하고 다음과 같은 명령을 실행합니다.
>!다음 명령에서 hadoop-mapreduce-examples-2.7.2.jar는 2.7.2 버전을 예로 들 수 있습니다. 버전이 다르면 대응하는 버전 번호로 수정하십시오.

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```

성공적으로 실행되면 다음과 같은 통계 정보를 반환합니다.
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
