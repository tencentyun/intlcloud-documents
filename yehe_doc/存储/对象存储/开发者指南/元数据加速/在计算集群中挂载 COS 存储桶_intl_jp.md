## 概要

Cloud Object Storage（COS）はメタデータアクセラレーション機能を有効にすることで、HDFSプロトコルによるアクセスが可能になります。メタデータアクセラレーション機能を有効にすると、COSはバケットにマウントポイントを作成し、お客様は[HDFSクライアント](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)をダウンロードすることで、クライアントにこのマウントポイントを入力してCOSをマウントできます。ここでは、コンピューティングクラスターに、メタデータアクセラレーションを有効にしたバケットをマウントする方法について詳しくご説明します。

>! 
>- Hadoop-cosは、バージョン8.1.5以降、`cosn://bucketname-appid/`メソッドによるメタデータアクセラレーションバケットへのアクセスをサポートしています。
>- メタデータアクセラレーション機能は、バケット作成時にのみオンにすることができ、一度オンにするとオフにすることはできません。お客様のビジネスシーンに応じて、オンにするかどうか**慎重にご検討ください**。また、旧バージョンのHadoop-cosパッケージは、メタデータアクセラレーション機能がオンになっているバケットには正常にアクセスできませんのでご注意ください。

## 前提条件

- コンピューティングクラスター内のマウントしたいマシンまたはコンテナ内に、[Java 1.8](https://www.oracle.com/java/technologies/downloads/)がインストールされていることをご確認ください。
- コンピューティングクラスター内のマウントしたいマシンまたはコンテナがアクセス権限を有していることをご確認ください。HDFS権限設定で、アクセス可能なVPCネットワークおよびIPアドレスを指定する必要があります。
- 依存するJARパッケージの説明
1. [chdfs_hadoop_plugin_network-2.8.jar](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) verison>=2.7;
2. [cos_api-bundle.jar](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar) version>=5.6.69;
3. [Hadoop-cos](https://github.com/tencentyun/hadoop-cos/releases) version>=8.1.5
4. ofs-java-sdk.jar (version >=1.0.4)はインストールを必要とせず、自動的にプルされます。hadoop fs lsを実行し成功すると、fs.cosn.trsf.fs.ofs.tmp.cache.dirで設定したディレクトリにおいて、対応するバージョンが想定どおりになっているかどうかを確認できます。

## 操作手順
1. [Hadoopクライアントツールインストールパッケージ](https://github.com/tencentyun/hadoop-cos/releases)をダウンロードします。
2. [POSIX Hadoopクライアントツールインストールパッケージ](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)をダウンロードします。
3. [cos java sdkインストールパッケージ](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar)をダウンロードします。
4. タスクの起動時に正しくロードされるように、各ノードのclasspathにインストールパッケージを設定します。例えば、`$HADOOP_HOME/share/hadoop/common/lib/`下などです。
>! EMR環境には独自の依存関係のあるjarパッケージがあるため、インストールする必要はなく、POSIXセマンティクスを介してメタデータアクセラレーションバケットに直接アクセスすることができます。s3プロトコルを使用してアクセスする必要がある場合は、fs.cosn.posix_bucket.fs.impl設定項目を変更します。詳細については、下記をご参照ください。
>
5. `core-site.xml`ファイルを編集し、次の基本設定を追加します。
```
<!--アカウントのAPIキー情報です。[CAMコンソール](https://console.cloud.tencent.com/capi)にログインすると、Tencent Cloud APIキーを確認することができます。-->
<property>
		 <name>fs.cosn.userinfo.secretId/secretKey</name>
		 <value>AKIDxxxxxxxxxxxxxxxxxxxxx</value>
</property>

<!--cosnの実装クラス-->
<property>
		 <name>fs.AbstractFileSystem.cosn.impl</name>
		 <value>org.apache.hadoop.fs.CosN</value>
</property>

<!--cosnの実装クラス-->
<property>
		 <name>fs.cosn.impl</name>
		 <value>org.apache.hadoop.fs.CosFileSystem</value>
</property>

<!--ユーザーバケットのリージョン情報です。フォーマットはap-guangzhou-->などです      
<property>
		 <name>fs.cosn.bucket.region</name>
		 <value>ap-guangzhou</value>
</property>

<!--プロセス実行中に生成される一時ファイル保存用のローカル一時ディレクトリ->      
<property>
		 <name>fs.cosn.tmp.dir</name>
		 <value>/tmp/hadoop_cos</value>
</property>
```
4. `core-site.xml`をすべての`hadoop`ノードに同期します。
>?EMRクラスターの場合、EMRコンソールのコンポーネント管理で上記のステップ3と4において、HDFSの設定を変更することができます。
>
5. `hadoop fs`コマンドラインツールを使用して、`hadoop fs -ls cosn://${bucketname-appid}/`コマンドを実行します。この`bucketname-appid`はマウントアドレス、すなわちバケット名です。ファイルリストが正常にリストアップされている場合は、COSバケットが正常にマウントされたことを意味します。
6. ユーザーは`hadoop`の他の設定項目または`mr`タスクを使用して、メタデータアクセラレーション機能を有効にしたCOSバケット上でデータタスクを実行することもできます。`mr`タスクの場合、`-Dfs.defaultFS=ofs://${bucketname-appid}/`によって、このタスクのデフォルトの入力・出力`FS`を対応するバケットに変更することができます。

## 設定項目の説明

### 1. 一般的な入力必須設定項目

| 設定項目                              | 設定項目内容                         | 説明                                                         |
| ----------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| fs.cosn.userinfo.secretId/secretKey | フォーマット例：AKIDxxxxxxxxxxxxxxxxxxxx | お客様のアカウントのAPIキー情報を入力します。[CAMコンソール](https://console.cloud.tencent.com/capi)にログインすれば、Tencent Cloud APIキーを確認することができます。 |
| fs.cosn.impl                        | org.apache.hadoop.fs.CosFileSystem | FileSystem用のcosn実装クラスは、固定されます。                          |
| fs.AbstractFileSystem.cosn.impl     | org.apache.hadoop.fs.CosN          | FileSystem用のcosn実装クラスは、以下に固定されます。                |
| fs.cosn.bucket.region               | フォーマット例：ap-beijing               | アクセスするバケットのリージョン情報を入力してください。列挙値については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)のリージョンの略称をご参照ください。例えば、ap-beijing、ap-guangzhouなどです。元の設定：fs.cosn.userinfo.regionと互換性があります。 |
| fs.cosn.tmp.dir                     | デフォルト/tmp/hadoop_cos                | 実際に存在するローカルディレクトリを設定してください。プロセス実行中に生成された一時ファイルは、一時的にここに保存されます。また、各ノードでこのディレクトリに十分なスペースと権限を割り当てることをお勧めします |



### 2. POSIXアクセスメソッド入力必須設定項目（推奨方式）

| 設定項目                | 設定項目内容     | 説明 |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.posix_bucket.fs.impl         | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter                |      POSIXメソッドのアクセス設定は、com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter S3プロトコルメソッドのアクセス設定は、org.apache.hadoop.fs.CosNFileSystemで、デフォルトはPOSIXメソッドでのアクセスです。               |
| fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl | com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter                      |      メタデータバケットアクセス実装クラス                                             |
| fs.cosn.trsf.fs.ofs.impl                    | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter                |     メタデータバケットアクセス実装クラス                                                          |
| fs.cosn.trsf.fs.ofs.tmp.cache.dir           | フォーマット例：/data/emr/hdfs/tmp/posix-cosn/  |実際に存在するローカルディレクトリを設定してください。プロセス実行中に生成された一時ファイルは、一時的にここに保存されます。また、各ノードでこのディレクトリに十分なスペースと権限を割り当てることをお勧めします。例："/data/emr/hdfs/tmp/posix-cosn/"                                                                      |
| fs.cosn.trsf.fs.ofs.user.appid              | フォーマット例：12500000000  | 入力必須。ユーザーappid |
| fs.cosn.trsf.fs.ofs.bucket.region           | フォーマット例：ap-beijing  | 入力必須。ユーザーbucketがregionに対応します |


### 3. S3プロトコルアクセスメソッド入力必須設定項目

| 設定項目                | 設定項目内容     | 説明 |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.posix_bucket.fs.impl         | org.apache.hadoop.fs.CosNFileSystem |      POSIXメソッドのアクセス設定は、com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter S3プロトコルメソッドのアクセス設定は、org.apache.hadoop.fs.CosNFileSystem、デフォルトはPOSIXメソッドでのアクセスです。                                        |

### 4. その他の設定項目

- [その他のHadoop-cos設定項目](https://intl.cloud.tencent.com/document/product/436/6884)
- [その他のPOSIXメソッド設定項目](https://intl.cloud.tencent.com/document/product/1106/41965)、その他のPOSIXXメソッド設定項目は、「fs.cosn.trsf.」というプレフィックスを追加することでメタデータアクセラレーションバケットにアクセスすることができます。

### 5. 注意事項

1. 古いhadoop cos jarパッケージを使用してメタデータアクセラレーションbucketにアクセスすることはできません。
2. Hadoop cos <= バージョン8.1.5のposixメソッドを使用してメタデータアクセラレーションバケットにアクセスする場合は、コンソールのrangerチェックを無効にしておく必要があります。


