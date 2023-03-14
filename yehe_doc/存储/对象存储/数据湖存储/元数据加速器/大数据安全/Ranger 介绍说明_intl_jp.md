## 背景

COS Ranger ServiceはTencent Cloudのストレージ/コンピューティング分離アーキテクチャからリリースされた、ビッグデータ権限管理ソリューションです。細粒度、Hadoop Rangerとの互換性、プラガブルというメリットを備え、ビッグデータコンポーネントとクラウドホスティングストレージの権限を一元管理したいユーザーにとって役立ちます。具体的なアーキテクチャソリューションおよび説明については、[COS Ranger権限システムソリューション](https://intl.cloud.tencent.com/document/product/436/39144)をご参照ください。

COS Ranger Serviceはリリース以来、幅広くご利用いただいていますが、お客様の業務が多岐にわたり、背景も複雑なことから、いくつかの疑問も生じています。ここでRangerに関する説明、バージョンの詳細および注意事項について整理しておきます。

## バージョンの紹介

### 関連コンポーネント

主な関連コンポーネントには、Ranger-Plugin、COS Ranger Server、COS Ranger Client（Hadoop-Ranger-Client）、COSN Ranger Interfaceがあります。

#### Ranger-Plugin

Rangerプロトコル（詳細は[Apache公式ドキュメント](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=53741207)をご参照ください）に基づいて、Rangerサーバー用のサービス定義プラグインを提供します。これらはRanger側のCOSサービスの説明を提供するもので、このプラグインをデプロイすると、ユーザーはRangerの制御ページでCOSの権限ポリシー（例えばpath、bucket、user、groupなどのアクセスポリシー設定）を入力できるようになります。  

#### COS Ranger Server

このサービスはRangerのクライアントを統合し、Rangerサーバーから権限ポリシーを定期的に同期し、クライアントからの認証リクエストを受信した後、ローカルで権限チェックを行います。同時に、HadoopでのDelegationTokenの発行や更新などのインターフェースを提供します。

EMR環境でのデフォルトのインストールディレクトリは/usr/local/service/cosranger/libです。例えばパッケージ名がcos-ranger-service-5.1.2-jar-with-dependencies.jarの場合、5.1.2がcos ragner serverのバージョン番号です。

#### COS Ranger Client

Hadoop sdkプラグインは、core-site.xmlファイル内でそれを動的にロードするように設定することで、権限チェックのリクエストをCOS Ranger Serviceに転送します。  

EMR環境でのデフォルトのインストールディレクトリは/usr/local/service/hadoop/share/hadoop/common/libです。例えばパッケージ名がhadoop-ranger-client-for-hadoop-2.8.5-5.0.jarの場合、2.8.5がhadoopのバージョン番号、5.0がそのパッケージのバージョン番号です。

#### COSN Ranger Interface

このプラグインはCOS Ranger ClientおよびCOS Ranger Clientパブリックデータによる定義およびインターフェース定義を行います。

EMR環境でのデフォルトのインストールディレクトリは/usr/local/service/hadoop/share/hadoop/common/libです。例えばパッケージ名がcosn-ranger-interface-1.0.4.jarの場合、1.0.4がCOSN Ranger Interfaceのバージョン番号です。

上記のjarパッケージはすべて[Github](https://github.com/tencentyun/cos-ranger-service)から取得できます。impala、prestoなどの他のコンポーネントに対応するCOS Ranger ClientパッケージについてはEMRチームにお問い合わせください。  

EMRコンソールでRangerおよびcosrangerコンポーネントを購入すると、上記のコンポーネントは自動的にインストールされます。ご自身でインストールする場合は、[CHDFS Ranger権限システムソリューション](https://intl.cloud.tencent.com/document/product/1106/41973)をご参照ください。

### バージョン説明 

バージョン全体は、コアアーキテクチャの違いによって大きく2つに分けられます。**zookeeperサービスディスカバリに依存する**バージョンと**zookeeperサービスディスカバリに依存しない**バージョンです。COS Ranger Serverが提供するサービスは、COS Ranger Clientの呼び出しに用いられます。  
- COS Ranger ClientがzookeeperによってCOS Ranger Serverのサービスアドレスを検出する場合は、zookeeperアドレスを設定する必要があり、これが**zookeeper依存バージョン**の特性です。
- COS Ranger Clientがzookeeperに依存せずCOS Ranger Serverのサービスを検出する場合は、qcloud.object.storage.ranger.service.addressを設定してCOS Ranger Serverサービスアドレスを直接指定する必要がありますが、zookeeperに依存してCOS Ranger Serverサービスを検出する必要はありません。これが**zookeeper非依存バージョン**の特性です。

### バージョン対応関係

| コンポーネント | zookeeperサービスディスカバリに依存する | zookeeperサービスディスカバリに依存しない |
| ---- | --- | ---- |
|COS Ranger Server| v5.0.9およびそれ以前のバージョン| v5.1.1およびそれ以降のバージョン|
|COS Ranger Client |  v3.9およびそれ以前のバージョン| v4.1およびそれ以降のバージョン|
|COSN Ranger Interface | バージョンv1.0.3| バージョンv1.0.4およびそれ以降|

>! **zookeeperサービスディスカバリに依存しない**バージョンを使用する場合、COS Ranger Serverはv5.1.1以降（**v5.1.2**を推奨）、COS Ranger Clientはv4.1以降（**v5.0**を推奨）がそれぞれ必須となり、かつCOSN Ranger Interfaceはv1.0.4およびそれ以降が必須となります。
>

### バージョン互換性関係

バージョン対応関係は上記の2つの分類に従ってマッチングすることが可能ですが、お客様の多くは背景が複雑で、必ずしも上記の2分類に従って分けられるとは限らないため、各コンポーネント間の互換性関係を下表に列記します。各行の記載は互換可能であることを表します。

| COS Ranger Clientバージョン   | COS Ranger Serverバージョン  | COSN Ranger Interfaceバージョン| zookeeperサービスディスカバリに依存するかどうか  |
|  -----------------------|  ----------------------  | ------------------------ | ------|
|   version ≤ v3.9       |    version ≤ v5.0.9     |       v1.0.3             |  はい |
|   version ≤ v3.9       |    version ≥ v5.1.1     |       v1.0.4             |  はい |
|   version ≥ v4.1       |    version ≥ v5.1.1     |       v1.0.4             |  いいえ |
|   version ≥ v5.0       |    version ≤ v5.0.9     |       v1.0.4             |  はい |
|   version ≥ v5.0       |    version ≥ v5.1.1     |       v1.0.4             |  いいえ |


>!
> - COS Ranger Client v5.0はすべてのバージョンのCOS Ranger Serverとの間に互換性を有します。
> - COS Ranger Client v4.1はv 5.1.1およびそれ以降のバージョンのCOS Ranger Serverとのみ互換性を有します。
> - COS Ranger Client v3.xもすべてのバージョンのCOS Ranger Serverとの間に互換性を有しますが、zookeeperに依存しなければCOS Ranger Serverサービスを検出できません（zookeeper依存バージョンの問題点についてはこの後に説明します）。
> - COS Ranger ClientとCOSN Ranger Interfaceパッケージは同一のディレクトリ下に配置し、hadoop sdkプラグインによる動的ロードが行えるようにする必要があります。
> 

### 利用説明

- メタデータアクセラレーションバケットとCHDFSファイルシステムは公式サイトのコンソールでRanger検証をオンにする必要があります。
- **zookeeperサービスディスカバリに依存する**バージョンを使用する場合、core-site.xmlにはqcloud.object.storage.zk.addressを設定し、valueはzookeeperアドレス（コンマで区切る）とする必要があります。
- COS Ranger Serverはバージョンv5.1.1およびv5.1.2を使用し、COS Ranger Clientはバージョンv3.xを使用した場合も、やはり登録と検出はzookeeerに依存しますので、core-site.xmlにはqcloud.object.storage.zk.addressを設定し、valueはzookeeperアドレス（例えば10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181のように、コンマで区切る）とする必要があります。
- **zookeeperサービスディスカバリに依存しない**バージョンを使用する場合、core-site.xmlにはqcloud.object.storage.ranger.service.addressを設定し、valueはCOS Ranger Serverサービスアドレス（例えば127.0.0.1:9999,128.0.0.1:9999のように、コンマで区切る）とする必要があります。
- ofsプロトコルを使用してアクセスする場合、core-site.xmlはfs.ofs.ranger.enable.flagをtrueに設定する必要があります。
- cosnプロトコルを使用してアクセスする場合、core-site.xmlにはfs.cosn.credentials.providerを設定し、org.apache.hadoop.fs.auth.RangerCredentialsProviderに設定する必要があります。

### 設定項目の説明

| 設定項目 | 説明 | 例  |
| --- | --- | --- |
| qcloud.object.storage.zk.address | COS Ranger Serverに登録するzkアドレス | 10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181  |
| qcloud.object.storage.ranger.service.address | COS Ranger Server RPCサービスアドレス | 127.0.0.1:9999,128.0.0.1:9999 |
| fs.ofs.ranger.enable.flag | ofsプロトコルを使用する場合のRangerスイッチ | true |
| fs.cosn.credentials.provider | cosnプロトコルを使用する場合のRanger認証クラスパス | org.apache.hadoop.fs.auth.RangerCredentialsProvider |
| fs.cosn.posix.bucket.use_ofs_ranger.enabled | chdfs ranger認証設定を有効にするかどうか| デフォルトではfalse、すなわちCOSN Ranger認証です。<br>trueに設定すると、chdfs ranger認証となります<br>説明：この項目はhadoop-cos v8.1.7およびそれ以降のバージョンで追加された設定項目です  |


### 設定項目表

| コンポーネントのバージョン | 設定項目 |
| --- | --- |
| cos ranger verser ≤ v5.0.9<br> cos ranger client ≤ v3.9 OR = v5.0<br> ofsプロトコルによるアクセス| qcloud.object.storage.zk.address<br> fs.ofs.ranger.enable.flag |
| cos ranger verser ≤ v5.0.9<br> cos ranger client ≤ v3.9 OR = v5.0<br> cosnプロトコルによるアクセス| qcloud.object.storage.zk.address<br> fs.cosn.credentials.provider |
| cos ranger verser = v5.1.1 OR = v5.1.2<br> cos ranger client ≥ v4.1<br> ofsプロトコルによるアクセス|qcloud.object.storage.ranger.service.address<br> fs.ofs.ranger.enable.flag|
| cos ranger verser = v5.1.1 OR = v5.1.2<br> cos ranger client ≥ v4.1<br> cosnプロトコルによるアクセス|qcloud.object.storage.ranger.service.address<br> fs.cosn.credentials.provider|

>!
> - cosnプロトコルを使用してメタデータアクセラレーションバケットにアクセスし、なおかつchdfs ranger認証を有効にしたい場合は、fs.cosn.posix.bucket.use_ofs_ranger.enabledをtrueに設定し、かつhadoop-cosのバージョンをv8.1.7以上にしてください。
> - 上記の設定を追加または調整した場合、YARNのResourceManager/NodeManager、HiveのHiveMetaStore/HiveServer2、ImpalaおよびPresto下のアプリケーションなどのビッグデータコンポーネントはすべて再起動する必要があります。
> 

### 推奨バージョン

| コンポーネント | バージョン番号 |
| ---| ---|
| cos-ranger-server| >= v5.1.2 |
| cos-ranger-client| >= v5.0   |
| cosn-ranger-interface| >= v1.0.4|


### 推奨説明

上記のバージョンを推奨する理由は次のとおりです。

- zookeeperをリーダー選出のみに使用し、サービスの登録と検出を行わなければ、ビッグデータ作業時のzookeeperの負荷は大幅に軽減されます。各ビッグデータ作業の際、大量のtaskがzookeeperにアクセスしてCOS Ranger Serverサービスディスカバリを行うと、zookeeperの負荷が高まり、他のビッグデータコンポーネントの安定性にも影響するためです。
- バージョンV5.0のhadoop-ranger-clientパッケージは旧バージョンのCOS Ranger Serverパッケージとの間に互換性を有し、以前からのユーザーがCOS Ranger Serverをアップグレードする上で役立ちます。
- COS Ranger Server 5.1.2より前のバージョンでは、取得したleader IPとleader latchのIPが一致しない状況が発生する可能性があります。また、今後COS Ranger Serverのzkに登録する情報が簡略化されるため、後で拡張またはアップグレードを行う際に役立ちます。
- いくつかのbugが修正されています。


## 認証に関するよくあるご質問

### IOException: init fs.ofs.ranger.client.impl failedというエラーが発生しました。どのように対処すればよいですか。

- Caused by: java.io.IOException: invalid zk address nullの場合は、core-site.xmlにqcloud.object.storage.zk.addressを設定し、valueはzookeeperアドレス（例えば10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181のように、コンマで区切る）とする必要があります。
- Caused by: java.io.IOException: ranger client is null, maybe ranger server for qcloud object storage is not deployed!の場合、次の質問を参考にしてください。

### ranger client is null, maybe ranger server for qcloud object storage is not deployed!というエラーが発生しました。どのように対処すればよいですか。

このエラーの主な原因には次のいくつかが挙げられます。
- hadoop-ranger-clientパッケージのバージョンがv3.8およびそれ以下の場合、zookeeper watchが失われたことが原因の可能性があります。v5.0へのアップグレードをお勧めします。
- 設定項目qcloud.object.storage.zk.addressまたはqcloud.object.storage.ranger.service.addressを確認します。
- COS Ranger Serverサービスおよびプロセスが正常かどうかを確認します。

### Expect ranger service addresses: [127.0.0.1:6080,128.0.0.1:6080], but actual ranger service addressというエラーが発生しました。どのように対処すればよいですか。

![エラー画像](https://qcloudimg.tencent-cloud.cn/raw/5cc5ce4451bbe5bfe91835befd1a49db.png)

- このエラーの原因は、メタデータアクセラレーションバケットまたはCHDFS公式サイトのコンソールでRanger検証をオンにしているのに、クライアントでRanger検証をオンにしていないことによるものです。
- ofsプロトコルを使用してアクセスする場合、core-site.xmlはfs.ofs.ranger.enable.flagをtrueに設定する必要があります。
- cosnプロトコルを使用してアクセスする場合、core-site.xmlにはfs.cosn.credentials.providerを設定し、org.apache.hadoop.fs.auth.RangerCredentialsProviderに設定する必要があります。

### RangerQcloudObjectStorageClientクラスが見つからないのですが、どのように対処すればよいですか。

![エラー画像](https://qcloudimg.tencent-cloud.cn/raw/6558d81d1269320c53379c44c7f254ca.png)

- cosn-ranger-interfaceパッケージがない場合は、[Github](https://github.com/tencentyun/cos-ranger-service)のcosn-ranger-interfaceディレクトリ下から取得できます。
- その他の関連クラスが見つからない場合は、cosn-ranger-interfaceパッケージおよびhadoop-ranger-clientパッケージが存在するか、バージョンはマッチしているか、正しいパスに配置されているかを確認してください。
- その他の関連クラスが見つからない場合にもう一つ考えられるのは、パッケージのshadeパスの問題です。この場合はこちらで調査と対処を行えるよう、お問い合わせいただく必要があります。

### NoSuchMethodErrorと表示されましたが、どのように対処すればよいですか。

![エラー画像](https://qcloudimg.tencent-cloud.cn/raw/4b3fdbf027180095ca32292d54a05279.jpg)

このエラーの原因は、元々そのメソッドがあったものの、ロードされたクラス内にはないことによるものです。このような状況が起こる原因には主に次の2つがあります。

- バージョンのイテレーションにより、旧バージョンのパッケージにはなかったこのメソッドが新バージョンで追加されたためです。
- 他のパッケージの同名のクラスをロードした可能性もあります。

/usr/local/serviceで次のコマンドを実行します。
```
find . -name "*.jar" -exec grep -Hls "org/apache/hadoop/fs/cosn/ranger/client/RangerQcloudObjectStorageClientImpl" {} \;
```
関連のパッケージを見つけて削除します。他のクラスの場合は、上記のコマンドのクラスパスを変更すれば解決します。

### java.lang.ClassCastException org.apache.hadoop.fs.cosn.ranger.protocol.ClientQCloudObjectStorageProtocolProtos$GetSTSRequest cannot be cast to com.google.protobuf.Messageというエラーが発生しました。どのように対処すればよいですか。

この種のエラーに類似したものに、パッケージ汚染の問題があります。マシン上に旧バージョンのパッケージが存在し、protobufプロトコルが一致しないことが原因で起こります。下記のalluxioパッケージの汚染問題と基本的には同じです。  

/usr/local/serviceで次のコマンドを実行します。
```
find . -name "*.jar" -exec grep -Hls "org/apache/hadoop/fs/cosn/ranger/protocol/ClientQCloudObjectStorageProtocolProtos" {} \;
```
関連のパッケージを見つけて削除します。他のクラスの場合は、上記のコマンドのクラスパスを変更すれば解決します。

### Ranger policyを変更しても有効になりませんが、どのように対処すればよいですか。

- chdfsの場合は、COS Ranger Serverの設定ファイルranger-chdfs-security.xmlの中の設定項目ranger.plugin.chdfs.policy.pollIntervalMsの値を小さくします（単位はミリ秒）。
- cosnの場合は、COS Ranger Serverの設定ファイルranger-cos-security.xmlの中の設定項目ranger.plugin.cos.policy.pollIntervalMsの値を小さくします（単位はミリ秒）。

### Ranger policyのポリシーにgroupを設定しても有効になりませんが、どのように対処すればよいですか。

userを設定した場合は有効になったのであれば、groupの同期の問題についてEMRチームに確認する必要があります。それ以外の場合は弊社までお問い合わせください。

### Ranger policyのストレージパスポリシールール設定にはどのように対処すればよいですか。

RangerのPathチェックルールはとてもシンプルで、主に文字列マッチングとなっています。ファイル/a/b/cがあり、設定したpolicyのpathルールが**/a/**である場合、**/a**または**/a/**へのアクセスはどちらも不可となります。これはsdkがアクセスパスの末尾の**/**を削除することで、最終的にRanger側に到達したパスが**/a**に変わるため、**/a/**にマッチしなくなるためです。**/a/b**または**/a/b/c**にアクセスした場合は、これらの2つのpathのプレフィックス部分はpolicy内のpathルール**/a/**にマッチします。

### HiveでCOSNまたはOFSパスを指定してテーブル作成を行う際、HiveAccessControlExceptionと表示されましたが、どのように対処すればよいですか。

![エラー画像](https://qcloudimg.tencent-cloud.cn/raw/928c7f08b597170da831dcca0e7edc42.png)

hiveのURLに対するチェックを許可する必要があります。rangerコンソールのhive内の設定でurlの権限を許可する必要があります。

![Ranger Admin](https://qcloudimg.tencent-cloud.cn/raw/8db0474e6ec152f92b61c98f6ac5d83c.png)

>! エラーログの形式にご注意ください。このエラーの大半はRangerサービスから報告されており、大多数の場合はranger adminで設定した権限に誤りがあります。

### kerberosのspark送信タスクでHiveAccessControlExceptionと表示されましたが、どのように対処すればよいですか。

アプリケーションは他のセキュリティHadoopファイルシステムとのインタラクションを行う必要があるため、起動時にURIをSparkに明示的に提供する必要があります。設定パラメータspark.kerberos.access.hadoopFileSystems=cosn://bucket-appid,ofs://f4mxxxxxxxx-Xxxx.chdfs.ap-guangzhou.myqcloud.comについては[Spark公式ドキュメント](https://spark.apache.org/docs/latest/security.html)をご参照ください。

### SPARKの削除テーブルがごみ箱に入らないのですが、どのように対処すればよいですか。

Sparkのcreate tableでLocationを指定することは、外部テーブルの作成と等価であり、外部テーブルの削除によってデータを削除することはできません。[Spark公式ドキュメントの説明](https://spark.apache.org/docs/latest/sql-migration-guide.html#upgrading-from-spark-sql-16-to-20)をご参照ください。

>? hive on mrの場合は、drop tableは削除できます。
>

### HiveでINSERTステートメントを実行するとAccessControlExceptionと表示されましたが、どのように対処すればよいですか。

HiveのデフォルトエンジンはMapReduceです。yarn-site.xmlファイルに次の設定項目を追加します。
```
<property>
    <name>mapreduce.job.hdfs-servers</name>
    <value>
        ofs://f4mxxxxxxx-XXXX,cosn://bucketname-appid,${fs.defaultFS}
    </value>
</property>
```
hiveエンジンがtezの場合は、tez-site.xmlファイルに設定項目tez.job.fs-serversを追加します。valueの値は上記と同様です。

beelineでhiveに接続している場合は、hiveserver2を再起動して新しいyarn-site設定をロードする必要があります。

### OFSアクセスエラーが発生しましたが、どのように対処すればよいですか。

![ofsアクセスエラー](https://qcloudimg.tencent-cloud.cn/raw/006df64050758fb2e4551d68335b94dd.png)

エラーがofsバックエンドから返されている場合、rangerを有効化した後にposixを無効化する必要があります。操作は次のとおりです。

- CHDFSコンソール

- COS bucket設定


### YARNコマンドラインでタスクを送信すると、renew token failedと表示されましたが、どのように対処すればよいですか。

yarnコマンドラインの実行の際は、-Dmapreduce.job.send-token-confパラメータが必要です。

### cosrangerを自作するにはどうすればよいですか。

[COS Ranger権限システムソリューション](https://intl.cloud.tencent.com/document/product/436/39144)、[CHDFS Ranger権限システムソリューション](https://intl.cloud.tencent.com/document/product/1106/41973)をご参照ください。

### Tencent Cloud EMRでRangerを有効化するにはどうすればよいですか。

emrコンソールでRangerおよびcosrangerコンポーネントを購入すると、ご自身でデプロイを行う手間が省けます。  
- chdfsの場合は、core-site.xmlに設定項目fs.ofs.ranger.enable.flagを追加し、trueに設定します。
- cosnの場合は、core-site.xmlに設定項目fs.cosn.credentials.providerを追加し、次のように設定します。
org.apache.hadoop.fs.auth.RangerCredentialsProvider

### NodeCache NULLポインタに異常が発生しましたが、どのように対処すればよいですか。

hadoop-ranger-clientのバージョンを確認し、v3.8であればv5.0へのアップグレードをお勧めします。その他の場合はお問い合わせください。
このエラーの原因は、ビッグデータ作業の際に同時実行性が比較的高いためにzookeeperの負荷が高まり、zookeeper watchが失われたことによるものです。

### cosrangerを有効化した後、hadoop fsコマンドでjava.lang.IllegalArgumentException: Failed to specify server's Kerberos principal nameと表示されましたが、どのように対処すればよいですか。

- core-site.xmlに設定項目qcloud.object.storage.kerberos.principalを追加します。
- hdfsクラスターのエラーであれば、core-site.xmlに設定項目dfs.namenode.kerberos.principalを追加します。
