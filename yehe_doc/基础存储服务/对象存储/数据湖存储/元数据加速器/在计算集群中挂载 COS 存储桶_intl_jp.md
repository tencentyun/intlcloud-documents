## 概要

Cloud Object Storage（COS）はメタデータアクセラレーション機能を有効にすることで、HDFSプロトコルによるアクセスが可能になります。メタデータアクセラレーション機能を有効にすると、COSはバケットにマウントポイントを作成し、お客様は[HDFSクライアント](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)をダウンロードすることで、クライアントにこのマウントポイントを入力してCOSをマウントできます。ここでは、コンピューティングクラスターに、メタデータアクセラレーションを有効にしたバケットをマウントする方法について詳しくご説明します。

>! 
> - Hadoop-cosは、バージョン8.1.5以降、`cosn://bucketname-appid/`メソッドによるメタデータアクセラレーションバケットへのアクセスをサポートしています。
> - メタデータアクセラレーション機能は、バケット作成時にのみオンにすることができ、一度オンにするとオフにすることはできません。お客様のビジネスシーンに応じて、オンにするかどうか**慎重にご検討ください**。また、旧バージョンのHadoop-cosパッケージは、メタデータアクセラレーション機能がオンになっているバケットには正常にアクセスできませんのでご注意ください。
> 

##  前提条件

- コンピューティングクラスター内のマウントしたいマシンまたはコンテナ内に、[Java 1.8](https://www.oracle.com/java/technologies/downloads/)がインストールされていることをご確認ください。
- コンピューティングクラスター内のマウントしたいマシンまたはコンテナがアクセス権限を有していることをご確認ください。HDFS権限設定で、アクセス可能なVPCネットワークおよびIPアドレスを指定する必要があります。
- 依存するJARパッケージの説明
 1. [chdfs_hadoop_plugin_network-2.8.jar](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar) verison ≥ 2.7。
 2. [cos_api-bundle.jar](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar) version ≥ 5.6.69。
 3. [Hadoop-cos](https://github.com/tencentyun/hadoop-cos/releases) version ≥ 8.1.5。
 4. ofs-java-sdk.jar (version ≥ 1.0.4) はインストールを必要とせず、自動的にプルされます。 hadoop fs lsを実行し成功すると、fs.cosn.trsf.fs.ofs.tmp.cache.dirで設定したディレクトリにおいて、対応するバージョンが想定どおりになっているかどうかを確認できます。

## 操作手順
1. [Hadoopクライアントツールインストールパッケージ](https://github.com/tencentyun/hadoop-cos/releases)をダウンロードします。
2. [POSIX Hadoopクライアントツールインストールパッケージ](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)をダウンロードします。
3. [cos java sdkインストールパッケージ](https://search.maven.org/artifact/com.qcloud/cos_api-bundle/5.6.69/jar)をダウンロードします。
4. タスクの起動時に正しくロードされるように、各ノードのclasspathにインストールパッケージを設定します。例えば、`$HADOOP_HOME/share/hadoop/common/lib/`下などです。
>! EMR環境には独自の依存関係のあるjarパッケージがあるため、インストールする必要はなく、POSIXセマンティクスを介してメタデータアクセラレーションバケットに直接アクセスすることができます。s3プロトコルを使用してアクセスする必要がある場合は、fs.cosn.posix_bucket.fs.impl設定項目を変更します。詳細については、下記をご参照ください。
>
5. `core-site.xml`ファイルを編集し、次の基本設定を追加します。
>!
>- 設定の際にパーマネントキーはできるだけ使用しないことをお勧めします。サブアカウントキーまたは一時キー方式を用いると業務の安全性が向上します。サブアカウントへの権限承認の際は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従い、データが意図せず漏洩しないようにしてください。
>- どうしてもパーマネントキーを使用したい場合は、パーマネントキーの権限範囲を限定することをお勧めします。[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)を参照し、パーマネントキーで実行できるアクション、リソースの範囲および条件（アクセスIPなど）を限定することで、使用上の安全性を向上させることができます。

```
<!--アカウントのAPIキー情報です。[CAMコンソール](https://console.cloud.tencent.com/capi)にログインすると、Tencent Cloud APIキーを確認することができます。-->
<!--設定の安全性向上のため、サブアカウントキーまたは一時キー方式を使用して設定を行うことをお勧めします。サブアカウントへの権限承認の際は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従ってください。-->
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

<!--ユーザーバケットのリージョン情報です。形式はap-guangzhou-->のようになります      
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
6. `core-site.xml`をすべての`hadoop`ノードに同期します。
>?EMRクラスターの場合、EMRコンソールのコンポーネント管理で上記の手順3と4において、HDFSの設定を変更することができます。
>
7. `hadoop fs` コマンドラインツールを使用して、`hadoop fs -ls cosn://${bucketname-appid}/`コマンドを実行します。この`bucketname-appid`はマウントアドレス、すなわちバケット名です。ファイルリストが正常にリストアップされている場合は、COSバケットが正常にマウントされたことを意味します。
8. ユーザーは`hadoop`の他の設定項目または`mr`タスクを使用して、メタデータアクセラレーション機能を有効にしたCOSバケット上でデータタスクを実行することもできます。`mr` タスクの場合，`-Dfs.defaultFS=ofs://${bucketname-appid}/`によって、このタスクのデフォルトの入力・出力`FS`を対応するバケットに変更することができます。

## 設定項目の説明

>? ここではPOSIXセマンティックによるアクセス、S3プロトコルによるアクセスの2つの方式によってメタデータアクセラレーションバケットにアクセスすることができます。ここではより良い性能を得るために、POSIXセマンティックによるアクセス方式を使用することをお勧めします。
>

### 1. 一般的な入力必須設定項目

>! どの方式でメタデータアクセラレーションバケットにアクセスするかに関わらず、以下の共通設定項目を設定する必要があります。
>

| 設定項目                              | 設定項目内容                         | 説明                                                         |
| ----------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| fs.cosn.userinfo.secretId/secretKey | フォーマット例：AKIDxxxxxxxxxxxxxxxxxxxx | お客様のアカウントのAPIキー情報を入力します。[CAMコンソール](https://console.cloud.tencent.com/capi)にログインすれば、Tencent Cloud APIキーを確認することができます。 |
| fs.cosn.impl                        | org.apache.hadoop.fs.CosFileSystem | FileSystem用のcosn実装クラスです。org.apache.hadoop.fs.CosFileSystemに固定されます。                          |
| fs.AbstractFileSystem.cosn.impl     | org.apache.hadoop.fs.CosN          | AbstractFileSystem用のcosn実装クラスです。 org.apache.hadoop.fs.CosNに固定されます。                |
| fs.cosn.bucket.region               | フォーマット例：ap-beijing               | アクセスするバケットのリージョン情報を入力してください。列挙値については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)のリージョンの略称をご参照ください。例えば、ap-beijing、ap-guangzhouなどです。元の設定：fs.cosn.userinfo.regionと互換性があります。 |
| fs.cosn.tmp.dir                     | デフォルト/tmp/hadoop_cos                | 実際に存在するローカルディレクトリを設定してください。プロセス実行中に生成された一時ファイルは、一時的にここに保存されます。また、各ノードでこのディレクトリに十分なスペースと権限を割り当てることをお勧めします。 |



### 2. POSIXアクセスメソッド入力必須設定項目（推奨方式）

>?
>- POSIXアクセス方式は共通設定項目以外に、さらに以下の内容を追加する必要があります。POSIX アクセス方式の [その他のオプション設定項目](https://intl.cloud.tencent.com/document/product/1106/41965) から「fs.cosn.trsf.」 というプレフィックスを追加することでメタデータアクセラレーションバケットにアクセスすることができます。
>- 元のHadoop cosに関連する設定項目は今後適用されなくなることに注意してください。

| 設定項目                | 設定項目内容     | 説明 |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl | com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter                      |      メタデータバケットアクセス実装クラス                                             |
| fs.cosn.trsf.fs.ofs.impl                    | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter                |     メタデータバケットアクセス実装クラス                                                          |
| fs.cosn.trsf.fs.ofs.tmp.cache.dir           | フォーマット例：/data/emr/hdfs/tmp/posix-cosn/  |実際に存在するローカルディレクトリを設定してください。プロセス実行中に生成された一時ファイルは、一時的にここに保存されます。また、各ノードでこのディレクトリに十分なスペースと権限を割り当てることをお勧めします。例：`"/data/emr/hdfs/tmp/posix-cosn/"`                                                                      |
| fs.cosn.trsf.fs.ofs.user.appid              | フォーマット例：12500000000  | 入力必須。ユーザーappid |
| fs.cosn.trsf.fs.ofs.bucket.region           | フォーマット例：ap-beijing  | 入力必須。ユーザーbucketがregionに対応します |


### 3. S3プロトコルアクセスメソッド入力必須設定項目

S3プロトコルによるアクセス方式は以下の設定が必要です。その他のオプションについては、[Hadoop-cos 設定項目](https://intl.cloud.tencent.com/document/product/436/6884)をご参照ください。

| 設定項目                | 設定項目内容     | 説明 |
| ------------------------ | ------------------ | ---------------- |
| fs.cosn.posix_bucket.fs.impl         | org.apache.hadoop.fs.CosNFileSystem |      POSIXメソッドのアクセス設定は`com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter S3` プロトコルメソッドのアクセス設定は `org.apache.hadoop.fs.CosNFileSystem`、デフォルトはPOSIXメソッドでのアクセスです。                                        |


### 5. 注意事項
1. 古いhadoop cos jarパッケージを使用してメタデータアクセラレーションのバケットにアクセスすることはできません。
2. Hadoop cos ≤ 8.1.5バージョンのposix方式を使用してメタデータアクセラレーションのバケットへのアクセスが有効な場合は、コンソールでranger検証を無効にする必要があります。8.1.5以上のバージョンはコンソールでranger検証を有効にすることをサポートしています。

