ここでは主に、GooseFSのスピーディーなデプロイ、デバッグに関するガイドをご提供します。ローカルマシン上にGooseFSをデプロイし、Cloud Object Storage（COS）をリモートストレージとして使用する手順のガイドをご提供します。具体的な手順は次のとおりです。


##  前提条件

GooseFSを使用する前には、次の準備作業が必要です。

1. COSサービスでバケットを1つ作成してリモートストレージとします。操作ガイドについては、[コンソールクイックスタート](https://intl.cloud.tencent.com/document/product/436/32955)をご参照ください。
2. [Java 8またはそれより上のバージョン](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)をインストールします。
3. [SSH](https://www.ssh.com/ssh/)をインストールします。SSHによってLocalHostに接続し、リモートログインを行えることを確認します。
4. CVMサービスでインスタンスを1台購入します。操作ガイドについては、[CVMの購入](https://www.tencentcloud.com/document/product/213/2753)をご参照ください。ディスクがすでにインスタンスにマウントされていることを確認します。

## GooseFSのダウンロードと設定

1. ローカルディレクトリを新規作成し、そのディレクトリ下に進み（必要に応じて他のディレクトリも選択できます）、公式リポジトリからGooseFSインストールパッケージをローカルにダウンロードします。インストールパッケージのGithubアドレスは[goosefs-1.4.0-bin.tar.gz](https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-1.4.0-bin.tar.gz)です。
```
$ cd /usr/local
$ mkdir /service
$ cd /service
$ wget https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-1.4.0-bin.tar.gz
```
2. 次のコマンドを実行して、インストールパッケージを解凍し、解凍後にインストールパッケージディレクトリに入ります。
```shell
$ tar -zxvf goosefs-1.4.0-bin.tar.gz
$ cd goosefs-1.4.0
```
解凍すると、goosefs-1.4.0、すなわちGooseFSのホームディレクトリが得られます。以下では`${GOOSEFS_HOME}`がこのディレクトリの絶対パスを表します。
3. `${GOOSEFS_HOME}/conf`のディレクトリ下に`conf/goosefs-site.properties`の設定ファイルを作成します。GooseFSはAIとビッグデータという2つのシナリオ向けの設定テンプレートを提供しており、上記のうち任意の内蔵テンプレートを使用できます。その後編集モードに進み、設定を変更します。
（1）AIシナリオテンプレートの使用に関するその他の情報については、GooseFS AIシナリオ本番環境設定の実践をご参照ください。
```shell
$ cp conf/goosefs-site.properties.ai_template conf/goosefs-site.properties
$ vim conf/goosefs-site.properties
```
（2）ビッグデータシナリオテンプレートの使用に関するその他の情報については、GooseFSビッグデータシナリオ本番環境設定の実践をご参照ください。
```shell
$ cp conf/goosefs-site.properties.bigdata_template conf/goosefs-site.properties
$ vim conf/goosefs-site.properties
```
4. 設定ファイル`goosefs-site.properties`内で次の設定項目を調整します。
```shell
# Common properties
# Masterノードhost情報の調整
goosefs.master.hostname=localhost
goosefs.master.mount.table.root.ufs=${goosefs.work.dir}/underFSStorage

# Security properties
# 権限設定の調整
goosefs.security.authorization.permission.enabled=true
goosefs.security.authentication.type=SIMPLE

# Worker properties
# workerノード設定の調整、ローカルキャッシュメディア、キャッシュパスおよびキャッシュ容量サイズの指定
goosefs.worker.ramdisk.size=1GB
goosefs.worker.tieredstore.levels=1
goosefs.worker.tieredstore.level0.alias=SSD
goosefs.worker.tieredstore.level0.dirs.path=/data
goosefs.worker.tieredstore.level0.dirs.quota=80G


# User properties
# ファイル読み取り書き込みキャッシュポリシーの指定
goosefs.user.file.readtype.default=CACHE
goosefs.user.file.writetype.default=MUST_CACHE
```

>!パス`goosefs.worker.tieredstore.level0.dirs.path`のパラメータを設定する前に、このパスを新規作成する必要があります。

## GooseFSの有効化

1. GooseFSを有効化する前に、GooseFSディレクトリ下で次の起動コマンドを実行する必要があります。
```shell
$ cd /usr/local/service/goosefs-1.4.0
$ ./bin/goosefs-start.sh all
```
これらのコマンドを実行すると、次のようなページが表示されます。

<img width="881" alt="image" src="https://qcloudimg.tencent-cloud.cn/raw/7b7f7f6ea02d36853ed7851023cfb8af.png">

このコマンドの実行が完了すると、`http://localhost:9201`および`http://localhost:9204`にアクセスして、MasterとWorkerの実行状態をそれぞれ確認できるようになります。

## GooseFSを使用してCOS（COSN）またはTencent Cloud HDFS（CHDFS）をマウント

GooseFSでCOS（COSN）またはTencent Cloud HDFS（CHDFS）をGooseFSのルートパス上にマウントしたい場合は、先に`conf/core-site.xml`設定の中でCOSNまたはCHDFSの必須設定項目を指定する必要があります。これには次に示すように、`fs.cosn.impl`、`fs.AbstractFileSystem.cosn.impl`、および`fs.cosn.userinfo.secretId`と`fs.cosn.userinfo.secretKey`などが含まれますが、これらに限定されません。

```xml

<!-- COSN related configurations -->
<property>
  <name>fs.cosn.impl</name>
  <value>org.apache.hadoop.fs.CosFileSystem</value>
</property>


<property>
   <name>fs.AbstractFileSystem.cosn.impl</name>
   <value>com.qcloud.cos.goosefs.CosN</value>
</property>


<property>
    <name>fs.cosn.userinfo.secretId</name>
    <value></value>
</property>


<property>
    <name>fs.cosn.userinfo.secretKey</name>
    <value></value>
</property>


<property>
    <name>fs.cosn.bucket.region</name>
    <value></value>
</property>


<!-- CHDFS related configurations -->
<property>
   <name>fs.AbstractFileSystem.ofs.impl</name>
   <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>


<property>
   <name>fs.ofs.impl</name>
   <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>


<property>
   <name>fs.ofs.tmp.cache.dir</name>
   <value>/data/chdfs_tmp_cache</value>
</property>


<!--appId-->      
<property>
   <name>fs.ofs.user.appid</name>
   <value>1250000000</value>
</property>

```

>?
>- COSNの完全な設定については、[Hadoopツール](https://intl.cloud.tencent.com/document/product/436/6884)をご参照ください。
>- CHDFSの完全な設定については、[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)をご参照ください。

次に、Namespaceを作成してCOSまたはCHDFSをマウントする方法および手順についてご説明します。

1. ネームスペース（namespace）を作成してCOSをマウントします。
```shell
$ goosefs ns create myNamespace cosn://bucketName-1250000000/ \
--secret fs.cosn.userinfo.secretId=AKXXXXXXXXXXX \
--secret fs.cosn.userinfo.secretKey=XXXXXXXXXXXX \
--attribute fs.cosn.bucket.region=ap-xxx \
```
>! 
> - COSNをマウントするnamespaceを作成する際は、必ず`–-secret`パラメータを使用してアクセスキーを指定し、なおかつ`--attribute`を使用してHadoop-COS（COSN）のすべての入力必須パラメータを指定しなければなりません。具体的な入力必須パラメータについては、[Hadoopツール](https://intl.cloud.tencent.com/document/product/436/6884)をご参照ください。
> - Namespaceを作成する際、読み取り書き込みポリシー（rPolicy/wPolicy）を指定しない場合は、デフォルトで設定ファイル内の指定のread/write typeを使用するか、またはデフォルト値（CACHE/CACHE_THROUGH）を使用します。
>
Tencent Cloud HDFSのマウントに用いるnamespaceも同様に作成できます。
```shell
goosefs ns create MyNamespaceCHDFS ofs://xxxxx-xxxx.chdfs.ap-guangzhou.myqcloud.com/ \
--attribute fs.ofs.user.appid=1250000000
--attribute fs.ofs.tmp.cache.dir=/tmp/chdfs
```
2. 作成に成功すると、クラスター内に作成したすべてのnamespaceを`ls`コマンドによってリストアップすることができます。
```shell
$ goosefs ns ls
namespace	      mountPoint	       ufsPath                     	 creationTime                wPolicy      	rPolicy	     TTL	   ttlAction
myNamespace    /myNamespace   cosn://bucketName-125xxxxxx/3TB  03-11-2021 11:43:06:239      CACHE_THROUGH   CACHE        -1      DELETE
myNamespaceCHDFS /myNamespaceCHDFS ofs://xxxxx-xxxx.chdfs.ap-guangzhou.myqcloud.com/3TB 03-11-2021 11:45:12:336 CACHE_THROUGH   CACHE  -1  DELETE
```
3. 次のコマンドを実行し、namespaceの詳細情報を指定します。
```shell
$ goosefs ns stat myNamespace

NamespaceStatus{name=myNamespace, path=/myNamespace, ttlTime=-1, ttlAction=DELETE, ufsPath=cosn://bucketName-125xxxxxx/3TB, creationTimeMs=1615434186076, lastModificationTimeMs=1615436308143, lastAccessTimeMs=1615436308143, persistenceState=PERSISTED, mountPoint=true, mountId=4948824396519771065, acl=user::rwx,group::rwx,other::rwx, defaultAcl=, owner=user1, group=user1, mode=511, writePolicy=CACHE_THROUGH, readPolicy=CACHE}
```

メタデータ内に記録する情報には次のものが含まれます。

| 番号 | パラメータ                   | 説明 |
| ---- | ---------------------- | ----- |
| 1    | name                   | namespaceの名前 |
| 2    | path                   | namespaceのGooseFSにおけるパス |
| 3    | ttlTime                | namespace下のディレクトリおよびファイルのttl期間 |
| 4    | ttlAction              | namespace下のディレクトリおよびファイルのttl処理動作。FREEとDELETEの2つの処理動作があり、デフォルトではFREE |
| 5    | ufsPath                | namespaceのufs上でのマウントパス |
| 6    | creationTimeMs         | namespaceの作成時間。単位はミリ秒|
| 7    | lastModificationTimeMs | namespace下のディレクトリおよびファイルの最終変更時刻。単位はミリ秒|
| 8    | persistenceState       | namespaceの永続化の状態 |
| 9    | mountPoint             | namespaceがマウントポイントかどうか。常にtrue |
| 10   | mountId                | namespaceのマウントポイントID |
| 11   | acl                    | namespaceのアクセス制御リスト |
| 12   | defaultAcl             | namespaceのデフォルトのアクセス制御リスト |
| 13   | owner                  | namespaceのowner |
| 14   | group                  | namespaceのownerが所属するgroup |
| 15   | mode                   | namespaceのPOSIX権限 |
| 16   | writePolicy            | namespaceの書き込みポリシー |
| 17   | readPolicy             | namespaceの読み取りポリシー |


## GooseFSを使用してTable内のデータをプリフェッチ

1. GooseFSはHive Table内のデータのGooseFSへのプリフェッチをサポートしています。プリフェッチの前に関連のDBをGooseFSにバインドしておく必要があります。関連のコマンドは次のとおりです。
```shell
$ goosefs table attachdb --db test_db hive thrift://
172.16.16.22:7004 test_for_demo
```
>! コマンド内のthriftには実際のHive Metastoreのアドレスを入力する必要があります。
>
2. DBの追加が完了すると、現在バインドしているDBとTableの情報をlsコマンドによって確認できるようになります。
```shell
$ goosefs table ls test_db web_page

OWNER: hadoop
DBNAME.TABLENAME: testdb.web_page (
   wp_web_page_sk bigint,
   wp_web_page_id string,
   wp_rec_start_date string,
   wp_rec_end_date string,
   wp_creation_date_sk bigint,
   wp_access_date_sk bigint,
   wp_autogen_flag string,
   wp_customer_sk bigint,
   wp_url string,
   wp_type string,
   wp_char_count int,
   wp_link_count int,
   wp_image_count int,
   wp_max_ad_count int,
)
PARTITIONED BY (
)
LOCATION (
   gfs://172.16.16.22:9200/myNamespace/3000/web_page
)
PARTITION LIST (
   {
   partitionName: web_page
   location: gfs://172.16.16.22:9200/myNamespace/3000/web_page
   }
)
```
3. loadコマンドによってTable内のデータをプリフェッチします。
```shell
$ goosefs table load test_db web_page
Asynchronous job submitted successfully, jobId: 1615966078836
```
 Table内のデータのプリフェッチは非同期タスクのため、タスクIDが返されます。goosefs job stat &lt;Job Id>コマンドによってプリフェッチ作業の実行進捗状況を確認できます。ステータスが"COMPLETED"になると、プリフェッチのプロセス全体が完了しています。

## GooseFSを使用したファイルのアップロードおよびダウンロード操作

1. GooseFSはほとんどのファイルシステムの操作コマンドをサポートしています。現在サポートしているコマンドのリストは次のコマンドによって照会できます。
```shell
$ goosefs fs
```
2. `ls`コマンドによってGooseFS内のファイルをリストアップすることができます。ルートディレクトリ下のすべてのファイルをリストアップする方法について、以下の例で示します。
```shell
$ goosefs fs ls /
```
3. `copyFromLocal`コマンドによって、データをローカルからGooseFSにコピーできます。
```shell
$ goosefs fs copyFromLocal LICENSE /LICENSE
Copied LICENSE to /LICENSE
$ goosefs fs ls /LICENSE
-rw-r--r--  hadoop         supergroup               20798       NOT_PERSISTED 03-26-2021 16:49:37:215   0% /LICENSE
```
4. `cat`コマンドによってファイルの内容を確認できます。
```shell
$ goosefs fs cat /LICENSE                                                                         
Apache License
Version 2.0, January 2004
http://www.apache.org/licenses/
TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION
...
```
5. GooseFSはデフォルトでローカルディスクを基盤ファイルシステムとして使用します。デフォルトのファイルシステムパスは`./underFSStorage`であり、`persist`コマンドによってファイルをローカルファイルシステムに永続的に保存することができます。
```shell
$ goosefs fs persist /LICENSE
persisted file /LICENSE with size 26847
```

## GooseFSを使用したファイルのアップロードおよびダウンロード操作のアクセラレーション

1. ファイルの保存ステータスをチェックし、ファイルがキャッシュ済みかどうかを確認します。ファイルのステータスが`PERSISTED`であれば、ファイルはすでにメモリ内にあることを表し、ファイルのステータスが`NOT_PERSISTED`であれば、ファイルはメモリ内にないことを表します。
```shell
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 NOT_PERSISTED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
```
2. ファイル内に単語「tencent」がいくつあるかを集計し、操作にかかった時間を計算します。
```shell
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c tencent
889
real	0m22.857s
user	0m7.557s
sys	0m1.181s
```
3. このデータをメモリ内にキャッシュすると、照会速度を効果的に向上させることができます。詳細な例は次のとおりです。
```shell
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 
ED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c tencent
889
real	0m1.917s
user	0m2.306s
sys	 0m0.243s
```
 このように、システム処理の遅延が1.181sから0.243sに減少し、スピードが10倍向上しました。

## GooseFSの無効化

次のコマンドによってGooseFSを無効化できます。
```shell
$ ./bin/goosefs-stop.sh local
```
