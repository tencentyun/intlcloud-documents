## 概要
メタデータアクセラレーターはTencent Cloud COS（Cloud Object Storage）サービス向けにハイパフォーマンスなファイルシステム機能をご提供します。メタデータアクセラレーターの基盤にはCloud HDFSの優れたメタデータ管理機能を採用し、ユーザーがファイルシステムのセマンティクスによってCOSサービスにアクセスできるようサポートします。システム設計指標は100GBレベルの帯域幅、10万レベルのQPSおよびミリ秒レベルの遅延を実現可能です。バケットでメタデータアクセラレーターを有効にすることで、ビッグデータ、ハイパフォーマンスコンピューティング、機械学習、AIなどのシーンに幅広く応用できます。メタデータアクセラレーターの詳細な説明に関しては、[メタデータアクセラレーター](https://intl.cloud.tencent.com/document/product/436/43305)をご参照ください。

COSはメタデータアクセラレーションサービスによってHadoopファイルシステムのセマンティクスを提供しているため、[Hadoop Distcpツール](https://intl.cloud.tencent.com/document/product/436/38863)を利用すると、Cloud Object Storage（COS）と他のHadoopファイルシステム間の双方向データマイグレーションを便利に行うことができます。ここではHadoop DistcpツールによってローカルHDFS内のファイルをCOSのメタデータアクセラレーションバケットに移す方法について重点的にご説明します。

## 移行環境の準備

### マイグレーションツールの準備


1. 下の表にあるjarパッケージツールをダウンロードし、マイグレーションクラスターの送信先マシンのローカルディレクトリ下に配置します（例：/data01/jars）。

<b>Tencent Cloud EMR環境</b>
 
**インストール説明**

<table>
<thead>
<tr><th>jarパッケージファイル名</th><th>説明</th><th>ダウンロードアドレス</th></tr>
</thead>
<tbody>
<tr>
<td>cos-distcp-1.12-3.1.0.jar</td>
<td>COSDistCp関連パッケージです。データをCOSNにコピーします</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/38863">COSDistCpツール</a>をご参照ください</td>
</tr>
<tr>
<td>chdfs_hadoop_plugin_network-2.8.jar</td>
<td>OFSプラグイン</td>
<td><a href="https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar">クリックしてダウンロード</a></td>
</tr>
</tbody>
</table>


<b>自作Hadoop/CDHなどの環境</b>

**ソフトウェア依存**

Hadoop-2.6.0およびそれ以上のバージョン、Hadoop-COSプラグイン8.1.5およびそれ以上のバージョンとし、またcos_api-bundleプラグインのバージョンはHadoop-COSバージョンに対応するものとします。詳細については、<a href="https://github.com/tencentyun/hadoop-cos/releases">COSN github releases</a>でご確認ください。

**インストール説明**

Hadoop環境下で、次のプラグインをインストールします。
<table>
<thead>
<tr><th>jarパッケージファイル名</th><th>説明</th><th>ダウンロードアドレス</th></tr>
</thead>
<tbody>
<tr>
<td>cos-distcp-1.12-3.1.0.jar</td>
<td>COSDistCp関連パッケージです。データをCOSNにコピーします</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/38863">COSDistCpツール</a>をご参照ください</td>
</tr>
<tr>
<td>chdfs_hadoop_plugin_network-2.8.jar</td>
<td>OFSプラグイン</td>
<td><a href="https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar">クリックしてダウンロード</a></td>
</tr>
<tr>
<td>Hadoop-COS</td>
<td>Version >= 8.1.5</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6884">Hadoop-COSツール</a>をご参照ください</td>
</tr>
<tr>
<td>cos_api-bundle</td>
<td>バージョンはHadoop-COSに対応している必要があります</td>
<td><a href="https://github.com/tencentyun/hadoop-cos/releases">クリックしてダウンロード</a></td>
</tr>
</tbody>
</table>

>!
>- Hadoop-cosは、バージョン8.1.5以降、`cosn://bucketname-appid/`メソッドによるメタデータアクセラレーションバケットへのアクセスをサポートしています。
>- メタデータアクセラレーション機能は、バケット作成時にのみオンにすることができ、一度オンにするとオフにすることはできません。お客様のビジネスシーンに応じて、オンにするかどうか慎重にご検討ください。また、旧バージョンのHadoop-cosパッケージは、メタデータアクセラレーション機能がオンになっているバケットには正常にアクセスできませんのでご注意ください。

2. メタデータアクセラレーションバケットを作成し、メタデータアクセラレーションバケットのHDFSプロトコルを設定します。詳細な手順については、[メタデータアクセラレーターを有効にしたバケットへのHDFSプロトコルを使用したアクセス](https://intl.cloud.tencent.com/document/product/436/46198)の、「バケットの作成とHDFSプロトコルの設定」の章をご参照ください。
3. マイグレーションクラスター`core-site.xml`を変更し、変更完了後にすべてのノード上に送信して設定します。データの移行のみの場合は、ビッグデータコンポーネントの再起動は必要ありません。
<table>
<thead>
<tr><th>key</th><th>value</th><th>設定ファイル</th><th>説明</th></tr>
</thead>
<tbody>
<tr>
<td>fs.cosn.trsf.fs.ofs.impl</td>
<td>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</td>
<td>core-site.xml</td>
<td>COSN実装クラス。入力必須です</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.AbstractFileSystem.ofs.impl</td>
<td>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</td>
<td>core-site.xml</td>
<td>COSN実装クラス。入力必須です</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.tmp.cache.dir</td>
<td>形式は/data/emr/hdfs/tmp/のようになります</td>
<td>core-site.xml</td>
<td>一時ディレクトリ。入力必須です。MRSの各ノードにはすべて作成し、十分なスペースと権限を保証する必要があります</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.user.appid</td>
<td>お客様のCOS bucketに対応するappid</td>
<td>core-site.xml</td>
<td>入力必須</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.ranger.enable.flag</td>
<td>false</td>
<td>core-site.xml</td>
<td>入力必須、falseかどうか確認</td>
</tr>
<tr>
<td>fs.cosn.trsf.fs.ofs.bucket.region</td>
<td>bucketに対応するregion</td>
<td>core-site.xml</td>
<td>入力必須です。オプション値：eu-frankfurt（フランクフルト）、ap-chengdu（成都）、ap-singapore（シンガポール）</td>
</tr>
</tbody>
</table>
4. マイグレーションクラスターがプライベートネットワークを経由してメタデータアクセラレーションバケットにアクセス可能かどうかを検証します。詳細な手順については、[メタデータアクセラレーターを有効にしたバケットへのHDFSプロトコルを使用したアクセス](https://intl.cloud.tencent.com/document/product/436/46198)の、「コンピューティングクラスターを設定してCOSにアクセス」の章をご参照ください。マイグレーションクラスターを送信して、COSに正常にアクセスできるかどうかを検証します。



## 既存データの移行

### 1. 移行ディレクトリの決定

通常、データ移行はまずHDFSストレージデータの移行から開始します。ソースHDFSクラスターの移行対象のディレクトリを選定し、ターゲット側とソース側のパスは同一にします。以下に示します。

HDFSパス`hdfs:///data/user/target`を`cosn://{bucketname-appid}/data/user/target`に移行したいと仮定します。

移行の過程で、ソース側ディレクトリのファイルが変更されないようにするため、HDFSのスナップショット機能を使用し、先に移行対象のディレクトリのスナップショットを作成します。現在の日付をスナップショットのファイル名とします。

```shell
hdfs dfsadmin -disallowSnapshot hdfs:///data/user/
hdfs dfsadmin -allowSnapshot hdfs:///data/user/target
hdfs dfs -deleteSnapshot hdfs:///data/user/target {現在の日付}
hdfs dfs -createSnapshot hdfs:///data/user/target {現在の日付}
```

成功の例：
![](https://qcloudimg.tencent-cloud.cn/raw/b96ef1500668c059909eb1ced5744a3f.png)

スナップショットを使用したくない場合は、ソース側のtargetファイルを直接移行することができます。

### 2. COSDistCpを使用して移行

COSDistCpタスクを起動し、ファイルをソースHDFSからターゲットCOSバケットにコピーします。

COSDistCpはMapReduceタスクであり、MapReduceタスクのプリントログにはMRタスクの実行が成功したかどうかが表示されます。失敗した場合はYARNページを確認し、ログまたはエラー情報をCOSに提供してトラブルシューティングを行うことができます。COSDistCpツールによる移行タスクの実行は次のいくつかの手順に分かれています。
（1）一時ディレクトリの作成
（2）COSDistCpタスクの実行
（3）失敗したファイルの再移行

#### （1）一時ディレクトリの作成

```shell
hadoop fs -libjars /data01/jars/chdfs_hadoop_plugin_network-2.8.jar -mkdir cosn://bucket-appid/distcp-tmp
```

#### （2）COSDistCpタスクの実行

```shell
nohup hadoop jar /data01/jars/cos-distcp-1.10-2.8.5.jar -libjars  /data01/jars/chdfs_hadoop_plugin_network-2.8.jar --src=hdfs:///data/user/target/.snapshot/{現在の日付}  --dest=cosn://{bucket-appid}/data/user/target   --temp=cosn://bucket-appid/distcp-tmp/ --preserveStatus=ugpt  --skipMode=length-checksum --checkMode=length-checksum --cosChecksumType=CRC32C --taskNumber 6 --workerNumber 32 --bandWidth 200 >> ./distcp.log &
```

パラメータの説明は次のとおりです。実際の状況に応じて調整できます。
- --taskNumber=VALUE コピープロセス数を指定します。例：--taskNumber=10。
-  --workerNumber=VALUE コピースレッド数を指定します。COSDistCpは、各コピープロセスでこのパラメータサイズのコピースレッドプールを作成します。例：--workerNumber=4。
-  --bandWidth 移行する各ファイルの読み込み帯域幅を制限します。単位はMB/s、デフォルトは-1で、読み込み帯域幅は制限しません。例：--bandWidth=10。
- --cosChecksumType=CRC32C、デフォルトではCRC32Cを使用しますが、HDFSクラスターはCOMPOSITE_CRC32チェックをサポートする必要があり、Hadoop バージョン3.1.1+に依存します。HDFSのバージョンが3.1.1より低い場合は、このパラメータを--cosChecksumType=CRC64に変更する必要があります。

>!COSDistCpでは移行の総帯域幅制限計算式は、taskNumber x workerNumber x bandWidthとなります。workerNumberを1に設定し、パラメータtaskNumberによる移行の同時実行数の制御、およびパラメータbandWidthによる単一の同時実行帯域幅の制御を行うことができます。

コピータスクの終了時に、タスクログによってファイルのコピーに関する統計情報が出力されます。関連するカウンターは次のとおりです。
このうち、FILES_FAILEDは失敗の数を表します。FILES_FAILEDの統計項目がない場合は、すべての移行が成功したことになります。
```
CosDistCp Counters
        BYTES_EXPECTED=10198247
        BYTES_SKIPPED=10196880
        FILES_COPIED=1
        FILES_EXPECTED=7
        FILES_FAILED=1
        FILES_SKIPPED=5

```

具体的な出力結果統計項目の説明は次のとおりです。

| 統計項目          | 説明                                               |
| --------------- | -------------------------------------------------- |
|  BYTES_EXPECTED  | ソースディレクトリの統計に基づいてコピーが必要なファイルの合計サイズ。単位：バイト   |
|  FILES_EXPECTED  | ディレクトリファイルを含む、ソースディレクトリの統計に基づいてコピーが必要なファイル数   |
| BYTES_SKIPPED   | 長さまたはチェックサム値が等しく、コピーされないファイルサイズの合計。単位：バイト |
| FILES_SKIPPED   | 長さまたはチェックサム値が等しく、コピーされないソースファイル数               |
| FILES_COPIED    |  コピーに成功したソースファイル数                                 |
| FILES_FAILED    | コピーに失敗したソースファイル数                                 |
| FOLDERS_COPIED  | コピーに成功したディレクトリ数                                   |
| FOLDERS_SKIPPED | スキップしたディレクトリ数                                       |


#### （3）失敗したファイルの再移行

COSDistCpツールはファイルの移行効率の問題の大部分を解決することができるほか、`--delete`パラメータによってHDFSとCOSのデータを完全に一致させることもできます。

`--delete`パラメータを使用する場合は、`--deleteOutput=/xxx(カスタム)`パラメータを含める必要があります。ただし`--diffMode`パラメータを含めることはできません。

```shell
nohup hadoop jar /data01/jars/cos-distcp-1.10-2.8.5.jar -libjars /data01/jars/chdfs_hadoop_plugin_network-2.8.jar --src=--src=hdfs:///data/user/target/.snapshot/{現在の日付} --dest=cosn://{bucket-appid}/data/user/target --temp=cosn://bucket-appid/distcp-tmp/ --preserveStatus=ugpt --skipMode=length-checksum --checkMode=length-checksum --cosChecksumType=CRC32C --taskNumber 6 --workerNumber 32 --bandWidth 200 --delete --deleteOutput=/dele-xx >> ./distcp.log &
```

実行完了後、HDFSとCOSの差分データは`trash`ディレクトリに移動し、`/xxx/failed`ディレクトリ下に移動ファイルリストが生成されます。`trash`ディレクトリ下のデータの削除には`hadoop fs -rm URL`または`hadoop fs -rmr URL`を用いることができます。

## 増分の移行

各回の移行が完了した後に、更新された増分データが存在し、その移行も必要な場合は、データの移行がすべて完了するまで、全量移行の手順を繰り返し実行します。

