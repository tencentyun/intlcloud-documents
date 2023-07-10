## 機能説明

Hadoop-COSは、Tencent Cloud Object Storage(COS)をベースとして標準的なHadoopファイルシステムを実装しています。これにより、Hadoop、Spark、TezなどのビッグデータコンピューティングフレームワークがCOSと統合し、HDFSファイルシステムにアクセスする場合と同じように、COSに保存されたデータの読み書きを可能にするサポートを提供しています。

Hadoop-COSはURIのschemeとしてcosnを使用するため、CosNファイルシステム用のHadoop-COSとも呼ばれます。


## 使用環境

#### システム環境

Linux、Windows、macOSシステムがサポートされています。

#### ソフトウェア依存

Hadoop-2.6.0およびそれ以降のバージョン。

>?
>1. 現在、Hadoop-COSは、Apache Hadoop-3.3.0に正式に統合されました[公式統合](https://hadoop.apache.org/docs/r3.3.0/hadoop-cos/cloud-storage/index.html)。
>2. Apache Hadoop-3.3.0以前のバージョンまたはCDHがHadoop-cos jarパッケージを統合した後、NodeManagerを再起動してjarパッケージをロードする必要があります。
>3. 特定のHadoopバージョンのjarパッケージをコンパイルする必要がある場合は、pomファイルのhadoop.versionを変更してコンパイルできます。
>



### ダウンロードとインストール

#### Hadoop-COSディストリビューションパッケージとその依存関係の取得

ダウンロードアドレス：[Hadoop-COS release](https://github.com/tencentyun/hadoop-cos/releases)。

#### Hadoop-COSプラグインのインストール

1. `hadoop-cos-{hadoop.version}-{version}.jar`と`cos_api-bundle-{version}.jar`を`$HADOOP_HOME/share/hadoop/tools/lib`にコピーします。
>? Hadoopの特定バージョンに応じて対応するjarパッケージを選択します。releaseの中に対応するバージョンのjarパッケージが提供されていない場合は、pomファイルのHadoopバージョン番号を変更することで再コンパイルと発行ができます。
> 
2. hadoop-env.shファイルを変更します。`$HADOOP_HOME/etc/hadoop`ディレクトリに移動し、hadoop-env.shファイルを編集して、以下の内容を追加し、cosn関連のjarパッケージをHadoop環境変数に追加します。
```shell
for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
  if [ "$HADOOP_CLASSPATH" ]; then
    export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
  else
    export HADOOP_CLASSPATH=$f
  fi
done
```

## 設定方法

### 設定項目の説明

|                  プロパティキー                  | 説明                                                         |                            デフォルト値                            | 入力必須項目 |
| :--------------------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------: | :----: |
|   fs.cosn.userinfo.<br>secretId/secretKey    | お客様のアカウントのAPIキー情報を入力します。[CAMコンソール](https://console.cloud.tencent.com/capi)にログインすれば、Tencent Cloud APIキーを確認することができます。 |                              なし                              |   はい   |
|       fs.cosn.<br>credentials.provider       | SecretIdとSecretKeyの取得方法を設定します。現在、5つの取得方法がサポートされています。<ol  style="margin: 0;"><li>org.apache.hadoop.fs.auth.SessionCredential<br>Provider：リクエストURIからsecret idとsecret keyを取得します。その形式は、次のとおりです。`cosn://{secretId}:{secretKey}@examplebucket-1250000000/`。</li><li>org.apache.hadoop.fs.auth.SimpleCredentialProvider：core-site.xml設定ファイルからfs.cosn.userinfo.secretIdとfs.cosn.userinfo.secretKeyを読み込み、SecretIdとSecretKeyを取得します。</li><li>org.apache.hadoop.fs.auth.EnvironmentVariableCredential<br>Provider：システム環境変数のCOS_SECRET_IDとCOS_SECRET_KEYから取得します。</li><li>org.apache.hadoop.fs.auth.SessionTokenCredentialProvider：[一時キー形式](https://intl.cloud.tencent.com/document/product/436/14048)を使用してアクセスします。</li><li>org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider：Tencent CloudのCloud Virtual Machine(CVM)にバインドされたロールを使用して、COSにアクセスするための一時キーを取得します</li><li>org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider：Tencent CloudのCloud Physical Machine(CPM)にバインドされたロールを使用して、COSにアクセスするための一時キーを取得します。</ li> <li> org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider：Tencent Cloud EMRインスタンスにバインドされたロールを使用して、COSにアクセスするための一時キーを取得します。</ li> <li> org.apache.hadoop.fs.auth.RangerCredentialsProviderは、rangerを使用してキーを取得します。</li></ol>| この設定項目が指定されていない場合、デフォルトで<br>以下の順序で読み込みます。<ol  style="margin: 0;"><li>org.apache.hadoop.fs.auth.SessionCredentialProvider</li><li>org.apache.hadoop.fs.auth.SimpleCredentialProvider</li><li>org.apache.hadoop.fs.auth.EnvironmentVariableCredentialProvider</li><li>org.apache.hadoop.fs.auth.SessionTokenCredentialProvider</li><li>org.apache.hadoop.fs.auth.CVMInstanceCredentialsProvider</li><li>org.apache.hadoop.fs.auth.CPMInstanceCredentialsProvider</li><li>org.apache.hadoop.fs.auth.EMRInstanceCredentialsProvider</li></ol> |   いいえ   |
| fs.cosn.useHttps | COSバックエンドでのトランスポートプロトコルとしてHTTPSを使用するかどうかを設定します。 | true | いいえ |
|               fs.cosn.impl               | FileSystem用のcosn実装クラス、org.apache.hadoop.fs.CosFileSystemに固定されます。 |                              なし                              |   はい   |
|     fs.AbstractFileSystem.<br>cosn.impl      | AbstractFileSystem用のcosn実装クラス、org.apache.hadoop.fs.CosNに固定されます。 |                              なし                              |   はい   |
|          fs.cosn.bucket.region           | アクセスするバケットのリージョン情報を入力してください。列挙値については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)のリージョンの略称をご参照ください。<br>例えば、ap-beijing、ap-guangzhouなどです。元の設定：fs.cosn.userinfo.regionと互換性があります。 |                              なし                              |   はい   |
|      fs.cosn.bucket.<br>endpoint_suffix      | 接続するCOS endpointを指定します。この項目は入力必須項目ではありません。パブリッククラウドCOSユーザーの場合、<br>上記のregionの設定を正しく入力するだけです。元の設定：fs.cosn.userinfo.endpoint_suffixと互換性があります。この項目を有効にするために、設定時にfs.cosn.bucket.regionの設定項目のendpointを削除してください。 | なし | いいえ |
|             fs.cosn.tmp.dir              | 実際に存在するローカルディレクトリを設定してください。プロセス実行中に生成された一時ファイルは、一時的にここに置かれます。 | /tmp/hadoop_cos | いいえ |
|          fs.cosn.upload.<br>part.size           | CosNファイルシステムの各blockのサイズです。マルチパートアップロードされた各part sizeのサイズでもあります。COSはマルチパートアップロードで最大10,000ブロックまでしかサポートできないため、使用できる最大1ファイルサイズを推定する必要があります。<br>例えば、part sizeが8MBの場合、最大で78GBの単一ファイルのアップロードに対応します。part sizeは最大2GBまで対応可能で、1ファイルあたり最大19TBまで対応できます。 | 8388608（8MB） |   いいえ   |
| fs.cosn.<br>upload.buffer | CosNファイルシステムがアップロード時に依存するバッファのタイプです。現在、非ダイレクトメモリバッファ(non_direct_memory)<br>ダイレクトメモリバッファ(direct_memory)、ディスクマップバッファ(mapped_disk)という3種類のバッファがサポートされています。非ダイレクトメモリバッファ<br>エリアではJVMヒープメモリが使用されますが、ダイレクトメモリバッファエリアではオフヒープメモリが使用されます。ディスクマップバッファはメモリファイルマッピングをベースとするバッファエリアです。| mapped_disk | いいえ |
| fs.cosn.<br>upload.buffer.size | CosNファイルシステムがアップロードに依存するバッファのサイズです。-1に指定されている場合、バッファに制限がないことを意味します。<br>バッファサイズが制限されていない場合、バッファタイプはmapped_diskである必要があります。指定されたサイズが0より大きい場合、この値は少なくとも1つのblockのサイズ以上である必要があります。 元の設定：fs.cosn.buffer.sizeと互換性があります。 | -1 | いいえ |
|  fs.cosn.block.size | CosNファイルシステムのblock sizeです。 | 134217728(128MB)| いいえ | 
|        fs.cosn.<br>upload_thread_pool        | ファイルがCOSにストリーミングされるときの同時アップロードスレッドの数です。                  |                        10                        |   いいえ   |
|         fs.cosn.<br>copy_thread_pool         | ディレクトリのコピー操作中にファイルを同時にコピーおよび削除するために使えるスレッドの数です。               |                   3                       |   いいえ   |
|      fs.cosn.<br>read.ahead.block.size       | 先読みブロックのサイズです。                                               |                        1048576(1MB)                        |   いいえ   |
|      fs.cosn.<br>read.ahead.queue.size       | 先読みキューの長さです。                                             |                              8                               |   いいえ   |
|            fs.cosn.maxRetries            | COSへのアクセス中にエラーが発生した場合の最大再試行回数です。                        |                             200                              |   いいえ   |
|      fs.cosn.retry.<br>interval.seconds      | 各再試行間の時間間隔です。                                         |                              3                               |   いいえ   |
| fs.cosn.<br>server-side-encryption.algorithm | COSサーバー側の暗号化アルゴリズムを設定します。SSE-CとSSE-COSをサポートしており、デフォルトでは空で、暗号化なしです。 |                             なし                              |   いいえ   |
|    fs.cosn.<br>server-side-encryption.key    | COSのSSE-Cサーバー暗号化アルゴリズムを有効にする場合は、SSE-Cのキーを設定する必要があります。<br>キーの形式は、base64でエンコードされたAES-256キーです。デフォルトでは空で、暗号化なしです。 |                              なし                              |  いいえ   |
| fs.cosn.<br>crc64.checksum.enabled | CRC64チェックを有効にするかどうかです。デフォルトでは有効になっていません。現時点では、hadoop fs -checksumコマンドを使用してファイルのCRC64チェックサムを取得することはできません。 | false | いいえ |
|fs.cosn.<br>crc32c.checksum.enabled    | CRC32Cチェックを有効にするかどうかです。デフォルトでは有効になっていません。現時点では、hadoop fs -checksumコマンドを使用してファイルのCRC32Cチェックサムを取得することはできません。有効にできるチェック方法は、crc32cかcrc64のうち1つだけです。| false | いいえ |
| fs.cosn.traffic.limit | アップロード帯域幅の制御オプション。819200 - 838860800 bits/s、デフォルト値は-1です。これは、デフォルトでは制限がないことを意味します。 | なし | いいえ | 


### Hadoopの設定

`$HADOOP_HOME/etc/hadoop/core-site.xml`を変更して、COS関連のユーザーおよび実装クラスの情報を追加します。次に例を示します。

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

このうちfs.defaultFSは、本番環境で設定することはお勧めしません。一部のテストシナリオ（例えば hive-testbenchなど）で使用する必要がある場合は、次の設定情報を追加できます。

```
<property>
          <name>fs.defaultFS</name>
          <value>cosn://examplebucket-1250000000</value>
        <description>
             This option is not advice to config, this only used for some special test cases.
        </description>
</property>
```

### サーバー側の暗号化

Hadoop-COSはサーバー側の暗号化をサポートしており、現在、COSホストキー方式(SSE-COS)とユーザー定義キー方式(SSE-C)という種類の暗号化方式があります。Hadoop-COSの暗号化機能はデフォルトでは無効状態になっており、ユーザーは以下の方法で設定して有効にすることができます。

#### SSE-COSの暗号化

SSE-COSの暗号化とは、COSホストキーによるサーバー側の暗号化です。Tencent Cloud COSはマスターキーをホストし、データを管理します。ユーザーはHadoop-COSを使用する場合、`$HADOOP_HOME/etc/hadoop/core-site.xml`ファイルに以下の設定を追加すると、SSE-COSの暗号化を実装することができます。

```shell
<property>
    	<name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-COS</value>
        <description>The server side encryption algorithm.</description>
</property>
```

#### SSE-Cの暗号化

SSE-Cの暗号化とは、ユーザー定義キーによるサーバー側の暗号化です。暗号化鍵はユーザーが提供し、COSはユーザーがオブジェクトをアップロードする際に、ユーザーが提供した暗号化鍵を使用して、ユーザーのデータをAES-256で暗号化します。Hadoop-COSを使用する場合、ユーザーは`$HADOOP_HOME/etc/hadoop/core-site.xml`ファイルに以下の設定を追加して、SSE-Cの暗号化を実装することができます。

```shell
<property>
        <name>fs.cosn.server-side-encryption.algorithm</name>
        <value>SSE-C</value>
        <description>The server side encryption algorithm.</description>
 </property>		
 <property>
  	<name>fs.cosn.server-side-encryption.key</name>
        <value>MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=</value> #ユーザーはSSE-Cのキーを自分で設定する必要があり、キーの形式はbase64でエンコードされたAES-256キーです。
        <description>The SSE-C server side encryption key.</description>
 </property> 
```

>!
> - Hadoop-COSのSSE-Cサーバー側の暗号化は、COSのSSE-Cサーバー側の暗号化に依存しています。したがってHadoop-COSは、ユーザーが提供する暗号化鍵を保存しません。また、COSのSSE-Cサーバー側の暗号化方式では、ユーザーが提供した暗号化鍵は保存されず、暗号化鍵にランダムデータが追加されたHMAC値が保存され、この値がオブジェクトにアクセスするためのユーザーのリクエストの認証に使われる点に注意する必要があります。COSは、ランダムデータのHMAC値を使用して暗号化鍵の値を推測したり、暗号化されたオブジェクトの内容を復号したりすることはできません。そのため、ユーザーが暗号化鍵を紛失した場合、このオブジェクトを再取得できなくなります。
> - Hadoop-COSがSSE-Cサーバー側暗号化アルゴリズムで設定されている場合、SSE-Cキーはfs.cosn.server-side-encryption.key設定項目で設定しなければなりません。キー形式は、base64でエンコードされたAES-256キーです。
> 

## 使用方法


### ユースケース

コマンド形式は、`hadoop fs -ls -R cosn://<BucketName-APPID>/<パス>`、または`hadoop fs -ls -R /<パス>`（`fs.defaultFS`オプションは`cosn://BucketName-APPID`に設定する必要あり）です。次の例では、examplebucket-1250000000という名のbucketを例として取り上げ、その後に具体的なパスを追加することができます。

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

MapReduceに付属しているwordcountを実行し、以下のコマンドを実行します。

>! 以下のコマンドのhadoop-mapreduce-examples-2.7.2.jarは、バージョン2.7.2を例としています。バージョンが異なる場合は、対応するバージョン番号に変更してください。
>

```shell
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount cosn://example/mr/input cosn://example/mr/output3
```

実行に成功すると、以下のような統計情報が返されます。

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

### JavaコードによるCOSNへのアクセス

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
        // COSNの設定項目については、https://cloud.tencent.com/document/product/436/6884#hadoop-.E9.85.8D.E7.BD.AEをご参照ください
        // 以下の設定は、入力必須項目です
        conf.set("fs.cosn.impl", "org.apache.hadoop.fs.CosFileSystem");
        conf.set("fs.AbstractFileSystem.cosn.impl", "org.apache.hadoop.fs.CosN");
        conf.set("fs.cosn.tmp.dir", "/tmp/hadoop_cos");
        conf.set("fs.cosn.bucket.region", "ap-guangzhou");
        conf.set("fs.cosn.userinfo.secretId", "AKXXXXXXXXXXXXXXXXX");
        conf.set("fs.cosn.userinfo.secretKey", "XXXXXXXXXXXXXXXXXX");
        conf.set("fs.ofs.user.appid", "XXXXXXXXXXX");
        // その他の設定については、公式サイトのドキュメントhttps://cloud.tencent.com/document/product/436/6884#hadoop-.E9.85.8D.E7.BD.AEをご参照ください
        // CRC64チェックを有効にするかどうかです。デフォルトでは有効になっていません。この時点では、hadoop fs -checksumコマンドを使用してファイルのCRC64チェックサムを取得することはできません
        conf.set("fs.cosn.crc64.checksum.enabled", "true");
        String cosnUrl = "cosn://f4mxxxxxxxx-125xxxxxxx";
        return FileSystem.get(URI.create(cosnUrl), conf);
    }

    private static void mkdir(FileSystem fs, Path filePath) throws IOException {
        fs.mkdirs(filePath);
    }

    private static void createFile(FileSystem fs, Path filePath) throws IOException {
        // ファイルを作成します（存在する場合は上書きします）
        // if the parent dir does not exist, fs will create it!
        FSDataOutputStream out = fs.create(filePath, true);
        try {
            // ファイルに書き込みます
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

    // 再帰的削除フラグは、ディレクトリを削除するために用いられます
    // 再帰がfalseで、dirが空でない場合、操作は失敗します
    private static void deleteFileOrDir(FileSystem fs, Path path, boolean recursive) throws IOException {
        fs.delete(path, recursive);
    }

    private static void closeFileSystem(FileSystem fs) throws IOException {
        fs.close();
    }

    public static void main(String[] args) throws IOException {
        // ファイルの初期化
        FileSystem fs = initFS();

        // ファイルの作成
        Path cosnFilePath = new Path("/folder/exampleobject.txt");
        createFile(fs, cosnFilePath);

        // ファイルの読み取り
        readFile(fs, cosnFilePath);

        // ファイルまたはディレクトリの照会
        queryFileOrDirStatus(fs, cosnFilePath);

        // ファイルのチェックサムの取得
        getFileCheckSum(fs, cosnFilePath);

        // ローカルからファイルをコピーする
        Path localFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
        copyFileFromLocal(fs, cosnFilePath, localFilePath);

        // ファイルをローカルで取得する
        Path localDownFilePath = new Path("file:///home/hadoop/ofs_demo/data/exampleobject.txt");
        copyFileToLocal(fs, cosnFilePath, localDownFilePath);

        listDirPath(fs, cosnFilePath);
        // リネーム
        mkdir(fs, new Path("/doc"));
        Path newPath = new Path("/doc/example.txt");
        renamePath(fs, cosnFilePath, newPath);

        // ファイルの削除
        deleteFileOrDir(fs, newPath, false);

        // ディレクトリの作成
        Path dirPath = new Path("/folder");
        mkdir(fs, dirPath);

        // ディレクトリにファイルを作成する
        Path subFilePath = new Path("/folder/exampleobject.txt");
        createFile(fs, subFilePath);

        // ディレクトリのリストアップ
        listDirPath(fs, dirPath);

        // ディレクトリの削除
        deleteFileOrDir(fs, dirPath, true);
        deleteFileOrDir(fs, new Path("/doc"), true);

        // ファイルシステムを閉じる
        closeFileSystem(fs);
    }
}
```

## よくあるご質問
Hadoopツールの使用に関するご質問は、[Hadoopツールに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/436/35706)をご参照ください。
