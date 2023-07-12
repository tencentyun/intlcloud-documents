## 概要

CDH (Cloudera's Distribution, including Apache Hadoop)は、業界で流行りのHadoopディストリビューションです。このドキュメントでは、CDH環境でTencent Cloud COSNストレージサービスを使用して、ビッグデータの計算とストレージの分離を実現し、フレキシブルかつ低コストのビッグデータソリューションを提供する方法についてご説明します。

>? COSNはHadoop-COSファイルシステムの略称です。
>

COSNビッグデータコンポーネントのサポートは次のとおりです：

| コンポーネント名 | COSNビッグデータコンポーネントのサポート状況 | サービスコンポーネントの再起動の要否                       |
| -------- | ----------------------- | -------------------------------------------- |
| Yarn     | サポート                     | NodeManagerの再起動                           |
| Hive     | サポート                     | HiveServerおよびHiveMetastoreの再起動           |
| Spark    | サポート                     | NodeManagerの再起動                           |
| Sqoop    | サポート                     | NodeManagerの再起動                           |
| Presto   | サポート                     | HiveServer、HiveMetastore、およびPrestoの再起動           |
| Flink    | サポート                 | いいえ                                         |
| Impala   | サポート                    | いいえ                                        |
|  EMR   |  サポート                      |       いいえ                                        |
|自作のコンポーネント  |  フォローアップサポート                    |   なし                                         |
| HBase    | 推奨しない                   | なし                                         |


## バージョンの依存関係

依存するコンポーネントのバージョンは次のとおりです：

- CDH 5.16.1
- Hadoop 2.6.0


## 利用方法

### ストレージ環境の設定

1. CDH管理ページにログインします。
2. 下図に示すとおり、**設定** > *サービス範囲** > **高度**を選択して、コードセグメントの高度な設定ページに進みます：
   ![](https://main.qcloudimg.com/raw/ee096f8e123efd393e1c8a610dd06ff2.png)
3. Cluster-wide Advanced Configuration Snippet(Safety Valve) for core-site.xmlのコードボックスに、COSN設定を入力します。
```
<property>
<name>fs.cosn.userinfo.secretId</name>
<value>AK***</value>
</property>
<property>
<name>fs.cosn.userinfo.secretKey</name>
<value></value>
</property>
<property>
<name>fs.cosn.impl</name>
<value>org.apache.hadoop.fs.CosFileSystem</value>
</property>
<property>
<name>fs.AbstractFileSystem.cosn.impl</name>
<value>org.apache.hadoop.fs.CosN</value>
</property>
<property>
<name>fs.cosn.bucket.region</name>
<value>ap-shanghai</value>
</property>
```
以下は、入力必須のCOSN設定項目です（core-site.xmlに追加する必要があります）。COSNのその他の設定については、[Hadoopツール](https://intl.cloud.tencent.com/document/product/436/46199)ドキュメントをご参照ください。
<table>
<thead>
<tr><th>COSN設定項目</th><th>値</th><th>意味</th></tr>
</thead>
<tbody>
<tr>
<td>fs.cosn.userinfo.secretId</td>
<td>AKxxxx</td>
<td>アカウントのAPIキー情報</td>
</tr>
<tr>
<td>fs.cosn.userinfo.secretKey</td>
<td>Wpxxxx</td>
<td>アカウントのAPIキー情報</td>
</tr>
<tr>
<td>fs.cosn.bucket.region</td>
<td>ap-shanghai</td>
<td>ユーザーバケットが配置されているリージョン</td>
</tr>
<tr>
<td>fs.cosn.impl</td>
<td>org.apache.hadoop.fs.CosFileSystem</td>
<td>org.apache.hadoop.fs.CosFileSystemとして修正されたFileSystemに対するcosnの実装クラス</td>
</tr>
<tr>
<td>fs.AbstractFileSystem.cosn.impl</td>
<td>org.apache.hadoop.fs.CosN</td>
<td>org.apache.hadoop.fs.CosNとして修正されたAbstractFileSystemに対するcosnの実装クラス</td>
</tr>
</tbody>
</table>
4. HDFSサービスを操作し、「クライアント設定のデプロイ」をクリックします。この時点で、上記のcore-site.xmlの設定がクラスター内のマシンに更新されます。
5. COSNの最新のSDKパッケージをCDH HDFSサービスのjarパッケージパス下に配置します。実際の値に従って置き換えてください。次に例を示します：
```
cp hadoop-cos-2.7.3-shaded.jar /opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/hadoop-hdfs/
```
>! クラスター内の各マシンは、SDKパッケージを同じ場所に配置してください。
>

<span id=1></span>

### データマイグレーション

Hadoop Distcpツールを使用して、CDH HDFSデータをCOSにマイグレーションします。詳細については、[HadoopファイルシステムとCOS間のデータマイグレーション](https://intl.cloud.tencent.com/document/product/436/34076)をご参照ください。

### ビッグデータスイートはCOSNを使用する

#### 1. MapReduce

**操作手順**

（1）[データマイグレーション](#1)章に従って、HDFSの関連設定を行い、COSNのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）CDHシステムのホームページでYARNを見つけてNodeManagerサービスを再起動します（TeraGen コマンドを再起動する必要はありませんが、TeraSortは内部ビジネスロジックのためにNodeMangerを再起動する必要があります。NodeManagerサービスを一律に再起動することをお勧めします）。

**事例**

以下に、Hadoop標準テストでのTeraGenとTeraSortの例を示します：

```
hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar teragen  -Dmapred.job.maps=500  -Dfs.cosn.upload.buffer=mapped_disk -Dfs.cosn.upload.buffer.size=-1 1099 cosn://examplebucket-1250000000/terasortv1/1k-input

hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar terasort -Dmapred.max.split.size=134217728 -Dmapred.min.split.size=134217728 -Dfs.cosn.read.ahead.block.size=4194304 -Dfs.cosn.read.ahead.queue.size=32 cosn://examplebucket-1250000000/terasortv1/1k-input  cosn://examplebucket-1250000000/terasortv1/1k-output
```

>?`cosn://    schema`の後をユーザーのビッグデータサービスのバケットパスに置き換えてください。

####  2. Hive

##### 2.1 MRエンジン

**操作手順**

（1）[データマイグレーション](#1)章に従って、HDFSの関連設定を行い、COSNのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）CDHメインページでHIVEサービスを見つけ、Hiveserver2およびHiverMetastoreのロールを再起動します。

**事例**

例えば、あるユーザーの実際のサービスクエリーでは、Hiveコマンドラインを実行してLocationを1つ作成し、COSNのパーティションテーブルとします。

```plaintext
CREATE TABLE `report.report_o2o_pid_credit_detail_grant_daily`(
  `cal_dt` string,
  `change_time` string,
  `merchant_id` bigint,
  `store_id` bigint,
  `store_name` string,
  `wid` string,
  `member_id` bigint,
  `meber_card` string,
  `nickname` string,
  `name` string,
  `gender` string,
  `birthday` string,
  `city` string,
  `mobile` string,
  `credit_grant` bigint,
  `change_reason` string,
  `available_point` bigint,
  `date_time` string,
  `channel_type` bigint,
  `point_flow_id` bigint)
PARTITIONED BY (
  `topicdate` string)
ROW FORMAT SERDE
  'org.apache.hadoop.hive.ql.io.orc.OrcSerde'
STORED AS INPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcInputFormat'
    OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat'
LOCATION
  'cosn://examplebucket-1250000000/user/hive/warehouse/report.db/report_o2o_pid_credit_detail_grant_daily'
TBLPROPERTIES (
  'last_modified_by'='work',
  'last_modified_time'='1589310646',
  'transient_lastDdlTime'='1589310646')
```

sql照会を実行します。

```
select count(1) from report.report_o2o_pid_credit_detail_grant_daily;
```

観察結果は次のとおりです：
![](https://main.qcloudimg.com/raw/28a566e5f08d7cbbeb4893b851565c01.png)

##### 2.2 Tezエンジン

Tezエンジンは、COSNのjarパッケージをTezの圧縮パッケージにインポートする必要があります。以下は、apache-tez.0.8.5を例として説明しています：

**操作手順**

（1）CDHクラスターによってインストールされたtezパッケージを見つけて、解凍します。例：/usr/local/service/tez/tez-0.8.5.tar.gz。
（2）COSNのjarパッケージを解凍したディレクトリ下に配置し、次に圧縮したパッケージを再圧縮して出力します。
（3）tez.lib.urisで指定されたパス下に、新しい圧縮パッケージをアップロードします（以前にパスがある場合は、直接置き換えてください）。
（4）CDHメインページでHIVEを見つけて、hiveserverおよびhivemetastoreを再起動します。

#### 3. Spark

**操作手順**

（1）[データマイグレーション](#1)章に従って、HDFSの関連設定を行い、COSNのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）NodeManagerサービスを再起動します。

**事例**

例として、COSNによるSpark example word countテストの実施を取り上げます。

```
spark-submit  --class org.apache.spark.examples.JavaWordCount --executor-memory 4g --executor-cores 4  ./spark-examples-1.6.0-cdh5.16.1-hadoop2.6.0-cdh5.16.1.jar cosn://examplebucket-1250000000/wordcount
```

実行結果は次のとおりです。
![](https://main.qcloudimg.com/raw/90e847c279f948af89ac670e43cd0b31.png)


#### 4. Sqoop

**操作手順**

（1）[データマイグレーション](#1)章に従って、HDFSの関連設定を行い、COSNのSDK jarパッケージをHDFSの対応するディレクトリに配置します。

（2）COSNのSDKjarパッケージをsqoopディレクトリ下に配置する必要もあります（例：/opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/sqoop/）。

（3）NodeManagerサービスを再起動します。

**事例**

例として、MYSQLテーブルのCOSへのエクスポートを取り上げます。[リレーショナルデータベースとHDFSのインポート・エクスポート](https://intl.cloud.tencent.com/document/product/1026/31157)ドキュメントを参照し、テストを実施してください。

```
sqoop import --connect "jdbc:mysql://IP:PORT/mysql" --table sqoop_test --username root --password 123**  --target-dir cosn://examplebucket-1250000000/sqoop_test
```

実行結果は次のとおりです：
![](https://main.qcloudimg.com/raw/4164c207304ba75eb8be42045f7f1394.png)


#### 5. Presto

**操作手順**

（1）[データマイグレーション](#1)章に従って、HDFSの関連設定を行い、COSNのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）COSNのSDK jarパッケージをprestoディレクトリ下に配置する必要もあります（例：/usr/local/services/cos_presto/plugin/hive-hadoop2）。
（3）prestoはhadoop common下のgson-2.*.*.jarをロードしないため、gson-2.*.*.jarもprestoディレクトリ下に配置してください（例： /usr/local/services/cos_presto/plugin/hive-hadoop2、COSNのみがgsonに依存します）。
（4）HiveServer、HiveMetaStoreおよびPrestoサービスを再起動します。

**事例**

例として、HIVEによってLocationをCOSとして作成したテーブルクエリーを取り上げます：

```
select * from cosn_test_table where bucket is not null limit 1;
```

>? cosn_test_tableはlocationがcosn schemeのテーブルです。

確認結果は次のとおりです：
![](https://main.qcloudimg.com/raw/b83d2aaf490edebbe3d9cc936c5bcce3.png)
