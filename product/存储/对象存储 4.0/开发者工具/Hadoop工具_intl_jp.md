## 機能説明
Hadoop cosnプラグインは、COSは下位ストレージファイルシステムとして上位計算タスクを実行する機能を実現し、Hadoopビッグデータ処理エンジン（例えば、MapReduce、Hive、Spark、Tezなど）を使用します。COSに保存されるデータを処理できます。

## 使用環境
### システム環境
Linux、Windows、macOSシステムをサポートします。

### ソフトウェア依存
Hadoop-2.6.0以降のバージョン。

## ダウンロードおよびインストール

### hadoop-cosプラグインを取得する
ダウンロードアドレス：[hadoop-cosプラグイン](https://github.com/tencentyun/hadoop-cos)。


### hadoop-cosプラグインをインストールする

1. depディレクトリのcos_hadoop_api-5.2.6.jarとhadoop-cos-2.X.X.jarを`$HADOOP_HOME/share/hadoop/tools/lib`にコピーします。
>?Hadoopの具体的なバージョンに応じてjarパッケージを選択します。depディレクトリには対応バージョンのjarパッケージが提供されていない場合、自らpomファイルのHadoopバージョン番号を変更し、コンパイルして生成することができます。 

2. hadoop_env.shの変更
`$HADOOP_HOME/etc/hadoop`ディレクトリでhadoop_env.shを開き、以下の内容を追加し、cosn関連のjarパッケージをHadoop環境変数に追加します。
```shell
for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
  if [ "$HADOOP_CLASSPATH" ]; then
    export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
  else
    export HADOOP_CLASSPATH=$f
  fi
done
```

## 使用方法

### 構成項目説明

| 属性キー                             | 説明                |デフォルト値|必須項目|
|:-----------------------------------:|:----------------------|:-----:|:-----:|
|fs.cosn.userinfo.secretId/secretKey| アカウントのAPI暗号鍵情報を入力します。[コンソール](https://console.cloud.tencent.com/capi)にログインしてクラウドAPI暗号鍵を確認できます | なし  | はい|
|fs.cosn.credentials.provider|secret idとsecret keyの取得方法を構成します。現時点で次の2つの取得方式をサポートします。1.org.apache.hadoop.fs.auth.SimpleCredentialProvider：core-site.xml構成ファイルからfs.cosn.userinfo.secretIdとfs.cosn.userinfo.secretKeyを読取りsecret idとsecret keyを取得します。 2.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider：システム環境変数COS_SECRET_IDとCOS_SECRET_KEYから取得します|構成項目を指定しない場合、デフォルトで以下の順序で読取ります。1.org.apache.hadoop.fs.auth.SimpleCredentialProvider。2.org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider。|いいえ|
|fs.cosn.impl                      | FileSystemに対するcosnの実装クラス（org.apache.hadoop.fs.CosFileSystem）| なし |はい|
|fs.AbstractFileSystem.cosn.impl   | AbstractFileSystemに対するcosnの実装クラス（org.apache.hadoop.fs.CosN） | なし |はい|
|fs.cosn.userinfo.region           | 地域情報を入力してください。列挙値は[可能な地域](https://cloud.tencent.com/document/product/436/6224)の地域略語です。例えば、	ap-beijing、ap-guangzhouなど | なし | はい|
|fs.cosn.userinfo.endpoint_suffix | 接続するCOS endpointを指定します。この項目は非必須項目です。パブリッククラウドCOSユーザにとって、上記のregion構成を正しく入力だけでよい|なし|いいえ|
|fs.cosn.tmp.dir                | 1つの実際的に存在するローカルのディレクトリを設定してください。実行するときに生成する一時ファイルがそこに格納されます| /tmp/hadoop_cos | いいえ|
|fs.cosn.buffer.size        | COSにファイルをストリーミングアップロードするときに、ローカルで使用されるメモリバッファの大きさ。すくなくとも1つのblockの大きさ以上と要求されます | 33554432（32MB）|いいえ|
|fs.cosn.block.size                | CosNファイルシステムの各blockの大きさであり、分割アップロードする各part sizeの大きさです。COSは最大10000パートを分割アップロードできますので、使用可能な単一ファイルの最大サイズを予測する必要があります。例えば、block sizeは8MBの場合、最大78GBの単一ファイルのアップロードをサポートします。block sizeは、最大2GBまでサポートできます。すなわち、単一ファイルは最大19TBまでサポートできます| 8388608（8MB） | いいえ |
|fs.cosn.upload_thread_pool        | ファイルをCOSにストリーミングアップロードするときの並行アップロードするスレッド数 | CPUコア数*5 | いいえ |
|fs.cosn.copy_thread_pool          |ディレクトリコピー操作を実行するときの並行コピーファイルに使用されるスレッド数 | CPUコア数*3 | いいえ |
|fs.cosn.read.ahead.block.size     | 先読みパートの大きさ                                 | 524288（512KB） |  いいえ |
|fs.cosn.read.ahead.queue.size     | 先読みキューの長さ                               | 10              | いいえ  |
|fs.cosn.maxRetries				   | COSにアクセスするときにエラーが発生した場合の最大再試行回数 | 3 | いいえ |
|fs.cosn.retry.interval.seconds    | 毎回再試行の時間間隔 | 3 | いいえ |


### Hadoop構成

$HADOOP_HOME/etc/hadoop/core-site.xmlを変更し、COSの関連ユーザと実装クラスの情報を追加します。例えば：

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

### 使用例

コマンド形式：`hadoop fs -ls -R cosn://bucketname-appid/<パス>`または`hadoop fs -ls -R /<パス>`（fs.defaultFSオプションにcosn://bucket-appidを設定する必要がある）。下例で、名前examplebucket-1250000000のBucketの後に具体的なパスを追加できます。

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

MapReduceに付属されるwordcountを実行し、以下のコマンドを実行します。
>!以下のコマンドは、バージョン2.7.2のhadoop-mapreduce-examples-2.7.2.jarを例として使用します。バージョンが違う場合、対応するバージョン番号に変更してください。

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```

実行が成功すると、統計情報を以下のように返します。
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

