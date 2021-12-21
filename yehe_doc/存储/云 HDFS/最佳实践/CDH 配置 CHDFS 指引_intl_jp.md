## 概要

CDH(Cloudera's Distribution, including Apache Hadoop)は、業界で流行りのHadoopディストリビューションです。ここでは、CDH環境でTencent Cloud CHDFSサービスを使用して、ビッグデータの計算とストレージの分離を実現し、フレキシブルかつ低コストのビッグデータソリューションを提供する方法についてご説明します。

CHDFSビッグデータコンポーネントのサポートは次のとおりです。

| コンポーネント名 | CHDFSビッグデータコンポーネントのサポート状況 | サービスコンポーネントの再起動の要否                       |
| -------- | ------------------------ | ------------------------------------------ |
| Yarn     | サポート                     | NodeManagerの再起動                           |
| Yarn     | サポート                     | NodeManagerの再起動                           |
| Hive     | サポート                     | HiveServerおよびHiveMetastoreの再起動           |
| Spark    | サポート                     | NodeManagerの再起動                           |
| Sqoop    | サポート                     | NodeManagerの再起動                           |
| Presto   | サポート                     | HiveServerおよびHiveMetastoreとPrestoの再起動 |
| Flink    | サポート                 | いいえ                                         |
| Impala   | サポート                    | いいえ                                        |
|  EMR   |  サポート  | いいえ                                        |
|セルフビルドコンポーネント  |  フォローアップサポート  |  なし                                         |
| HBase    | 推奨しない                   | なし                                         |


## バージョンの依存関係

依存するコンポーネントのバージョンは次のとおりです。

- CDH 5.16.1
- Hadoop 2.6.0


## 使用方法

### ストレージ環境の設定

1. CDH管理ページにログインします。
2. 下図に示すとおり、**設定** > *サービス範囲** > **高度**を選択して、コードセグメントの高度な設定ページに進みます。
   ![](https://main.qcloudimg.com/raw/09f053f2c0feaf4451d9bc4c70cb501d.png)
3. Cluster-wide Advanced Configuration Snippet(Safety Valve)for core-site.xmlのコードボックスに、CHDFS設定を入力します。

```
<property>
<name>fs.AbstractFileSystem.ofs.impl</name>
<value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
</property>
<property>
<name>fs.ofs.impl</name>
<value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
</property>
<!--ローカルcacheの一時ディレクトリ。データの読み取りと書き込みの場合、メモリcacheが不足すると、ローカルディスクに書き込まれます。このパスが存在しない場合は、自動的に作成されます-->
<property>
<name>fs.ofs.tmp.cache.dir</name>
<value>/data/emr/hdfs/tmp/chdfs/</value>
</property>
<!--appId-->      
<property>
<name>fs.ofs.user.appid</name>
<value>1250000000</value>
</property>
```

以下は、入力必須のCHDFS設定項目です（core-site.xmlに追加する必要があります）。CHDFSの他の設定については、[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)をご参照ください。

| CHDFS設定項目                   | 値                                               | 意味                                                         |
| ------------------------------ | ------------------------------------------------ | ------------------------------------------------------------ |
| fs.ofs.user.appid              | 1250000000                                       | ユーザーappid                                                   |
| fs.ofs.tmp.cache.dir           | /data/emr/hdfs/tmp/chdfs/                        | ローカルcacheの一時ディレクトリ                                        |
| fs.ofs.impl                    | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter | chdfsのileSystemに対する実装クラスは、com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapterに固定されます |
| fs.AbstractFileSystem.ofs.impl | com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter       | chdfsのAbstractFileSystemに対する実装クラスは、com.qcloud.chdfs.fs.CHDFSDelegateFSAdapterに固定されます |

4. HDFSサービスを操作し、「クライアント設定のデプロイ」をクリックします。この時点で、上記のcore-site.xmlの設定がクラスター内のマシンに更新されます。
5. CHDFSの最新のSDKパッケージをCDH HDFSサービスのjarパッケージパス下に配置します。実際の値に従って置き換えてください。次に例を示します。

```
cp chdfs_hadoop_plugin_network-2.0.jar /opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/hadoop-hdfs/
```

>!クラスター内の各マシンは、SDKパッケージを同じ場所に配置する必要があります。


<span id=1>

### データマイグレーション

Hadoop Distcpツールを使用して、CDH HDFSデータをCHDFSに移行します。詳細については、以下をご参照ください
[ネイティブHDFSデータのTencent Cloud CHDFSへの移行](https://intl.cloud.tencent.com/document/product/1106/41970)。

### ビッグデータスイートによるCHDFSの使用

#### 1. MapReduce

**操作手順**

（1）[データマイグレーション]#1)の章に従って、HDFSの関連設定を行い、CHDFSのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）CDHシステムのホームページでYARNを見つけてNodeManagerサービスを再起動します（TeraGen コマンドを再起動する必要はありませんが、TeraSortは内部ビジネスロジックのためにNodeMangerを再起動する必要があります。NodeManagerサービスを一律に再起動することをお勧めします）。

**事例**

以下に、Hadoop標準テストでのTeraGenとTeraSortの例を示します。

```
hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar teragen -Dmapred.map.tasks=4 1099 cosn://examplebucket-1250000000/teragen_5/

hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar terasort  -Dmapred.map.tasks=4 cosn://examplebucket-1250000000/teragen_5/ cosn://examplebucket-1250000000/result14
```

>?`ofs://     schema`の後ろを、ユーザーCHDFSのマウントポイントパスに置き換えてください。


####  2. Hive

##### 2.1 MRエンジン

**操作手順**

（1）[データマイグレーション](#1)の章に従って、HDFSの関連設定を行い、CHDFSのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）CDHメインページでHIVEサービスを見つけ、Hiveserver2およびHiverMetastoreのロールを再起動します。

**事例**

例えば、あるユーザーの実際の業務の照会では、Hiveコマンドラインを実行してLocationを1つ作成し、CHDFSのパーティションテーブルとします。

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

観察の結果は次のとおりです。
![](https://main.qcloudimg.com/raw/28a566e5f08d7cbbeb4893b851565c01.png)

##### 2.2 Tezエンジン

Tezエンジンは、CHDFSのjarパッケージをTezの圧縮パッケージにインポートする必要があります。以下は、apache-tez.0.8.5を例として説明しています。

**操作手順**

（1）CDHクラスターによってインストールされたtezパッケージを見つけて、解凍します。例：/usr/local/service/tez/tez-0.8.5.tar.gz。
（2）CHDFSのjarパッケージを解凍したディレクトリ下に置き、圧縮したパッケージを再圧縮して出力します。
（3）tez.lib.urisで指定されたパス下に、新しい圧縮パッケージをアップロードします（以前にパスがある場合は、直接置き換えてください）。
（4）CDHメインページでHIVEを見つけて、hiveserverおよびhivemetastoreを再起動します。

#### 3. Spark

**操作手順**

（1）[データマイグレーション](#1)の章に従って、HDFSの関連設定を行い、CHDFSのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）NodeManagerサービスを再起動します。

**事例**

例として、CHDFSによるSpark example word countテストの実施を取り上げます。

```
spark-submit  --class org.apache.spark.examples.JavaWordCount --executor-memory 4g --executor-cores 4  ./spark-examples-1.6.0-cdh5.16.1-hadoop2.6.0-cdh5.16.1.jar cosn://examplebucket-1250000000/wordcount
```

実行結果は次のとおりです。
![](https://main.qcloudimg.com/raw/5070c17e6db105f7b1d20c609f334b60.png)


#### 4. Sqoop

**操作手順**

（1）[データマイグレーション](#1)の章に従って、HDFSの関連設定を行い、CHDFSのSDK jarパッケージをHDFSの対応するディレクトリに配置します。

（2）CHDFSのSDKjarパッケージもsqoopディレクトリ下に配置する必要があります（例：/opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/sqoop/）。

（3）NodeManagerサービスを再起動します。

**事例**

例として、MYSQLテーブルのCHDFSへのエクスポートを取り上げます。[リレーショナルデータベースとHDFSのインポート・エクスポート](https://intl.cloud.tencent.com/document/product/1026/31157)ドキュメントをご参照ください。

```
sqoop import --connect "jdbc:mysql://IP:PORT/mysql" --table sqoop_test --username root --password 123  --target-dir cosn://examplebucket-1250000000/sqoop_test
```

実行結果は次のとおりです。
![](https://main.qcloudimg.com/raw/3b27f8417460e8edfa7f8f11cbef3f4f.png)


#### 5. Presto

**操作手順**

（1）[データマイグレーション](#1)の章に従って、HDFSの関連設定を行い、CHDFSのSDK jarパッケージをHDFSの対応するディレクトリに配置します。
（2）CHDFSのSDK jarパッケージもprestoディレクトリ下に配置する必要があります（例：/usr/local/services/cos_presto/plugin/hive-hadoop2）。
（3）prestoはhadoop common下のgson-2.*.*.jarをロードしないため、gson-2.*.*.jarもprestoディレクトリ下に配置する必要があります（例： /usr/local/services/cos_presto/plugin/hive-hadoop2、CHDFSのみがgsonに依存します）。
（4）HiveServer、HiveMetaStoreおよびPrestoサービスを再起動します。

**事例**

例として、HIVEによってLocationをCHDFSとして作成したテーブルの照会を取り上げます。

```
select * from chdfs_test_table where bucket is not null limit 1;
```

>?chdfs_test_tableはlocationがofs schemeのテーブルです。

確認の結果は次のとおりです。
![](https://main.qcloudimg.com/raw/c5dc086fefbc32ad116e91524e7102ad.png)
