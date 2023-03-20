## 機能説明

COSDistCpは、MapReduceをベースとした分散ファイルコピーツールで、主にHDFSとCOS間のデータコピーに使用され、主に次のような機能を備えています。
- 長さ、CRCチェックサムに応じて、ファイルの増分移行とデータチェックを行います
- ソースディレクトリ内のファイルに対して正規表現でのフィルタリングを行います
- ソースディレクトリ内のファイルを解凍し、想定の圧縮形式に変換します
- 正規表現に基づいてテキストファイルを集約します
- ソースファイルとソースディレクトリのユーザー、グループ、拡張属性および時間を保持します
- アラートとPrometheusモニタリングを設定します
- ファイルサイズ分布の統計
- 読み込み帯域幅の速度制限

## 使用環境

#### システム環境

Linuxシステムをサポートしています。

#### ソフトウェア依存

Hadoop-2.6.0以降、Hadoop-COSプラグイン5.9.3以降。

### ダウンロードとインストール

#### COSDistCpjarパッケージの取得

- Hadoop 2.x ユーザーは、[cos-distcp-1.12-2.8.5.jarパッケージ](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-2.8.5.jar)をダウンロードし、jarパッケージの[MD5チェックサム](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-2.8.5-md5.txt)に基づき、ダウンロードしたjarパッケージが完全かどうかを確認します。
- Hadoop 3.xユーザーは、[cos-distcp-1.12-3.1.0.jarパッケージ](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-3.1.0.jar)をダウンロードし、jarパッケージの[MD5チェックサム](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-1.12-3.1.0-md5.txt)に基づき、ダウンロードしたjarパッケージが完全かどうかを確認します。

#### インストール説明

Hadoop環境において、[Hadoop-COS](https://intl.cloud.tencent.com/document/product/436/6884) をインストールすると、直接COSDistCpツールを実行できます。

Hadoop-COSプラグインがインストールおよび設定されていない環境のユーザーの場合、Hadoopのバージョンに従って、対応するバージョンのCOSDistCp jar、Hadoop-COS jar、cos_api-bundle jarパッケージをダウンロードし（jarパッケージのダウンロードアドレスは上記参照）、Hadoop-COS関連のパラメータを指定してコピータスクを実行します。jarパッケージアドレスにはローカルjarの存在するアドレスを入力する必要があります。

```plaintext
hadoop jar cos-distcp-${version}.jar \
-libjars cos_api-bundle-${version}.jar,hadoop-cos-${version}.jar \
-Dfs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider \
-Dfs.cosn.userinfo.secretId=COS_SECRETID \
-Dfs.cosn.userinfo.secretKey=COS_SECRETKEY \
-Dfs.cosn.bucket.region=ap-guangzhou \
-Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
-Dfs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
--src /data/warehouse \
--dest cosn://examplebucket-1250000000/warehouse
```


## 原理の説明

COSDistCpはMapReduceフレームワークをベースとして実装されています。これはマルチプロセス+マルチスレッドのアーキテクチャで、ファイルのコピー、データのチェック、圧縮、ファイル属性の保持およびコピーの再試行を行うことができます。COSDistCpは、デフォルトでターゲットの同名の既存ファイルを上書きします。ファイルの移行またはチェックに失敗した場合、対応するファイルのコピーが失敗し、移行に失敗したファイル情報が一時ディレクトリに記録されます。ソースディレクトリにファイルが追加されたり、内容が変更されたりした場合、skipModeやdiffModeモードを使用して、ファイルの長さまたはCRCチェック値を比較することによって、データチェックサムとファイルの増分移行を行うことができます。


## パラメータの説明

hadoopユーザーの下でコマンド`hadoop jar cos-distcp-${version}.jar --help`を使用すると、COSDistCpでサポートされているパラメータオプションを確認することができます。ここで`${version}`はバージョン番号です。以下は現在のバージョンのCOSDistCpのパラメータの説明です。


|                プロパティキー                | 説明                                                                                                                                                                                                                  |              デフォルト値              | 入力必須かどうか |
|:---------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------:|:----:|
|              --help               | COSDistCpでサポートされているパラメータオプションを出力します<br> 例：--help                                                                                                                                                                                  |               なし               |  いいえ   |
|          --src=LOCATION           | コピーのソースディレクトリを指定します。これはHDFSまたはCOSパスにすることができます<br> 例：--src=hdfs://user/logs/                                                                                                                                                          |               なし               |  はい   |
|          --dest=LOCATION          | コピーのターゲットディレクトリを指定します。これは、HDFSまたはCOSパスにすることができます<br> 例：--dest=cosn://examplebucket-1250000000/user/logs                                                                                                                                |               なし               |  はい   |
|       --srcPattern=PATTERN        | 正規表現を指定して、ソースディレクトリにあるファイルをフィルタリングします。<br>例：`--srcPattern='.*\.log$'`<br>**注意：記号`*`がshellによって解釈されるのを避けるために、パラメータをシングルクォーテーションで囲む必要があります**                                                                                                                      |               なし               |  いいえ   |
|        --taskNumber=VALUE         | コピープロセス数を指定します。例：--taskNumber=10                                                                                                                                                                                          |              10               |  いいえ   |
|       --workerNumber=VALUE        | コピースレッド数を指定します。COSDistCpは、各コピープロセスでこのパラメータサイズのコピースレッドプールを作成します<br>例：--workerNumber=4                                                                                                                                                      |               4               |  いいえ   |
|      --filesPerMapper=VALUE       | Mapper入力ファイル1ファイルあたりの行数を指定します<br>例：--filesPerMapper=10000                                                                                                                                                                    |            500000             |  いいえ   |
|         --groupBy=PATTERN         | テキストファイルを集約するための正規表現を指定します</br>例：--groupBy='.\*group-input/(\d+)-(\d+).\*'                                                                                                                                                   |               なし               |  いいえ   |
|        --targetSize=VALUE         | ターゲットファイルのサイズをMB単位で指定します。--groupByとともに使用します</br>例：--targetSize=10                                                                                                                                                             |               なし               |  いいえ   |
|        --outputCodec=VALUE        | 出力ファイルの圧縮方法を指定します。gzip、lzo、snappy、none、keepを選択できます。このうち、</br> 1. keepは、元のファイルの圧縮方法を維持します。<br>2. noneは、ファイルの拡張子に従ってファイルを解凍します。</br>例：--outputCodec=gzip </br>**注意：ファイル /dir/test.gzipと/dir/test.gzがあり、出力形式をlzoに指定する場合は、最終的に1つのファイル/dir/test.lzoだけが維持されます** |             keep              |  いいえ   |
|         --deleteOnSuccess         | ソースファイルのターゲットディレクトリへのコピーが成功したら、直ちにソースファイルを削除するよう指定します</br>例：--deleteOnSuccess，</br>**注意：1.7以降のバージョンではこのパラメータは提供されませんので、データ移行が成功し、--diffModeを使用してチェックを行った後、ソースファイルシステムのデータを削除することをお勧めします**                                                                                                |             false             |  いいえ   |
| --multipartUploadChunkSize=VALUE  | Hadoop-COSプラグインがファイルをCOSに転送するときのチャンクサイズを指定します。COSがサポートするチャンクの最大数は10000で、ファイルサイズに応じてチャンクサイズをMB単位で調整できます。デフォルトは8MBです</br>例：--multipartUploadChunkSize=20                                                                                              |              8MB              |  いいえ   |
|     --cosServerSideEncryption     | ファイルがCOSにアップロードされる際に、暗号化・復号アルゴリズムとしてSSE-COSを使用するように指定します</br>例：--cosServerSideEncryption                                                                                                                                                   |             false             |  いいえ   |
|      --outputManifest=VALUE       | コピーが完了した際、ターゲットディレクトリにそのコピーのターゲットファイルの情報リスト（GZIP圧縮）が発行されるように指定します</br>例：--outputManifest=manifest.gz                                                                                                                                        |               なし               |  いいえ   |
|     --requirePreviousManifest     | 増分をコピーする場合は、--previousManifest=VALUEパラメータを指定する必要があります</br>例：--requirePreviousManifest                                                                                                                                           |             false             |  いいえ   |
|    --previousManifest=LOCATION    | 前回のコピーで生成されたターゲットファイルの情報<br>例：--previousManifest=cosn://examplebucket-1250000000/big-data/manifest.gz                                                                                                                        |               なし               |  いいえ   |
|        --copyFromManifest         | --previousManifest=LOCATIONとともに使用すると、--previousManifest内のファイルをターゲットファイルシステムにコピーできます<br>例：--copyFromManifest                                                                                                                    |             false             |  いいえ   |
|       --storageClass=VALUE        | COSタイプを指定します。オプション値は、STANDARD、STANDARD_IA、ARCHIVE、DEEP_ARCHIVE、INTELLIGENT_TIERINGです。サポートされているストレージタイプと概要については、[ストレージタイプの概要](https://intl.cloud.tencent.com/document/product/436/30925)をご参照ください                                                       |               なし               |  いいえ   |
|    --srcPrefixesFile=LOCATION     | ローカルファイルを指定します。ファイルの各行には、コピーする必要のあるソースディレクトリが含まれます</br>例：--srcPrefixesFile=file:///data/migrate-folders.txt                                                                                                                                 |               なし               |  いいえ   |
|          --skipMode=MODE          | ファイルをコピーする前に、ソースファイルとターゲットファイルが同じかどうかをチェックし、同じであればスキップします。none（チェックしない）、length（長さ）、checksum（CRC値）、length-mtime(長さ+mtime値)、length-checksum（長さ+CRC値）が選択可能です</br>例：--skipMode=length                                                                    |        length-checksum        |  いいえ   |
|         --checkMode=MODE          | ファイルコピー完了時に、ソースファイルとターゲットファイルが同じかどうかをチェックします。none（チェックしない）、length（長さ）、checksum（CRC値）、length-checksum（長さ+mtime値）、length-checksum（長さ+ CRC値）が選択可能です</br>例：--checkMode=length-checksum                                                          |        length-checksum        |  いいえ   |
|          --diffMode=MODE          | ソースディレクトリとターゲットディレクトリの差分ファイルリストを指定して取得します。length（長さ）、checksum（CRC値）、length-checksum（長さ+mtime値）、length-checksum（長さ+CRC値）が選択可能です</br>例：--diffMode=length-checksum                                                                             |               なし               |  いいえ   |
|       --diffOutput=LOCATION       | diffModeのHDFS出力ディレクトリを指定します。この出力ディレクトリは、必ず空である必要があります<br/>例：--diffOutput=/diff-output                                                                                                                                                  |               なし               |  いいえ   |
|      --cosChecksumType=TYPE       | Hadoop-COSプラグインが使用するCRCアルゴリズムを指定します。オプション値はCRC32CとCRC64です<br/>例：--cosChecksumType=CRC32C                                                                                                                                      |            CRC32C             |  いいえ   |
|      --preserveStatus=VALUE       | ソースファイルのuser、group、permission、xattr、timestampsのメタ情報をターゲットファイルにコピーするかどうかを指定します。オプション値は、ugpxt（user、group、permission、xattr、timestampsの英語頭文字）です<br/>例：--preserveStatus=ugpt                                                           |               なし               |  いいえ   |
|          --ignoreSrcMiss          | ファイルリストには存在しても、コピー時には存在しないファイルを無視します                                                                                                                                                                                               |             false             |  いいえ   |
|    --promGatewayAddress=VALUE     | MapReduceタスクによって実行されるCounterデータがプッシュされるPrometheus PushGatewayのアドレスとポートを指定します                                                                                                                                                     |               なし               |  いいえ   |
| --promGatewayDeleteOnFinish=VALUE | タスクが完了したら、Prometheus PushGatewayのJobNameのメトリクスコレクションを削除するよう指定します</br>例：--promGatewayDeleteOnFinish=true                                                                                                                           |             true              |  いいえ   |
|    --promGatewayJobName=VALUE     | Prometheus PushGatewayに報告するJobNameを指定します</br>例：--promGatewayJobName=cos-distcp-hive-backup                                                                                                                          |               なし               |  いいえ   |
|    --promCollectInterval=VALUE    | MapReduceタスクのCounter情報を収集する間隔をms単位で指定します</br>例：--promCollectInterval=5000                                                                                                                                            |             5000              |  いいえ   |
|         --promPort=VALUE          | Prometheusメトリクスを外部に公開するサーバーポートを指定します <br>例：--promPort=9028                                                                                                                                                            |               なし               |  いいえ   |
|      --enableDynamicStrategy      | タスクの動的割り当てポリシーを指定して、移行速度の速いタスクがより多くのファイルを移行できるようにします。</br>**注意：このモードには一定の制限があります。例えば、プロセスに異常が発生した場合、タスクカウンターは不正確になります。移行の完了後、--diffModeを使用してデータチェックを行ってください** </br>例：--enableDynamicStrategy                                                                                |             false             |  いいえ   |
|        --splitRatio=VALUE         | Dynamic Strategyの分割比を指定します。splitRatio値が大きいほど、タスクの粒度は小さくなります</br>例：--splitRatio=8                                                                                                                                              |               8               |  いいえ   |
|         --localTemp=VALUE         | Dynamic Strategyによって生成されたタスク情報ファイルが保存されているローカルフォルダを指定します</br>例：--localTemp=/tmp                                                                                                                                                       |             /tmp              |  いいえ   |
|  --taskFilesCopyThreadNum=VALUE   | Dynamic Strategyのタスク情報ファイルをHDFSにコピーする際の同時実行性を指​​定します </br>例：--taskFilesCopyThreadNum=32                                                                                                                                        |              32               |  いいえ   |
|        --statsRange=VALUE         | 統計の区間範囲を指定します</br>例：---statsRange=0,1mb,10mb,100mb,1gb,10gb,inf                                                                                                                                                        | 0,1mb,10mb,100mb,1gb,10gb,inf |  いいえ   |
|         --printStatsOnly          | 移行するファイルサイズの分布情報のみ統計が行われ、データは移行されません</br>例：--printStatsOnly                                                                                                                                                                       |               なし               |  いいえ   |
|            --bandWidth            | 移行する各ファイルの読み込み帯域幅を制限します。単位はMB/s、デフォルトは-1で、読み込み帯域幅は制限しません。</br>例：--bandWidth=10                                                                                                                                                          |               なし               |  いいえ   |
|             --jobName             | 移行タスクの名前を指定します。</br>例：--jobName=cosdistcp-to-warehouse                                                                                                                                                                  |               なし               |  いいえ   |
|   --compareWithCompatibleSuffix   | --skipModeと--diffModeパラメータを使用する場合、ソースファイルの拡張子gzipをgzに変換するかどうか、lzopファイルの拡張子をlzoに変換するかどうかを判断します。</br>例：--compareWithCompatibleSuffix                                                                                                    |               なし               |  いいえ   |
|             --delete              | ソースディレクトリとターゲットディレクトリのファイルの一致性を保証します。ソースディレクトリにはなく、ターゲットディレクトリにはあるファイルを独立したtrashディレクトリ下に移動させ、同時にファイルリストを生成します。</br>注意：--diffModeパラメータは同時に使用できません                                                                                                                           |    なし   |  いいえ   |
|          --deleteOutput           | deleteのHDFS出力ディレクトリを指定します。このディレクトリは必ず空でなければなりません<br/>例： --deleteOutput=/dele-output                                                                                                                                                   |  なし   |  いいえ   |

## ユースケース

### helpオプションの確認

パラメータ`--help`によりコマンドを実行し、COSDistCpでサポートされているパラメータを確認します。次に例を示します。

```plaintext
hadoop jar cos-distcp-${version}.jar --help
```
上記コマンドにおいて`${version}`はCOSDistCpのバージョン番号です。例えば、バージョン1.0のCOSDistCp jarパッケージ名はcos-distcp-1.0.jarとなります。

### 移行するファイルサイズ分布に関する情報の統計を行います

パラメータ`--printStatsOnly`と`--statsRange=VALUE`によりコマンドを実行すると、移行するファイルのサイズ分布に関する情報が出力されます。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /wookie/data --dest cosn://examplebucket-1250000000/wookie/data --printStatsOnly  --statsRange=0,1mb,10mb,100mb,1gb,10gb,inf

Copy File Distribution Statistics:
Total File Count: 4
Total File Size: 1190133760
| SizeRange         | TotalCount          | TotalSize           |
| 0MB ~ 1MB         | 0(0.00%)            | 0(0.00%)            |
| 1MB ~ 10MB        | 1(25.00%)           | 1048576(0.09%)      |
| 10MB ~ 100MB      | 1(25.00%)           | 10485760(0.88%)     |
| 100MB ~ 1024MB    | 1(25.00%)           | 104857600(8.81%)    |
| 1024MB ~ 10240MB  | 1(25.00%)           | 1073741824(90.22%)  |
| 10240MB ~ LONG_MAX| 0(0.00%)            | 0(0.00%)            |
```

### 移行するファイルのソースディレクトリとターゲットディレクトリを指定します

パラメータ`--src`と`--dest`によりコマンドを実行します。次に例を示します。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse
```


COSDistCpは、コピーが失敗したファイルをデフォルトで5回再試行します。それでも失敗した場合、失敗したファイル情報を/tmp/${randomUUID}/output/failed/ディレクトリに書き込みます。ここで${randomUUID}は、ランダム文字列です。失敗したファイル情報を記録した後、COSDistcpは残りのファイルの移行を続行しますが、一部のファイルが失敗したために移行タスクが失敗することはありません。移行タスクが完了すると、COSDistcpはカウンター情報（タスクがマシンへ送信され、MapReduceタスクの提出側INFOログの出力が設定されたことを確認してください）を出力し、移行に失敗したファイルが存在するかどうかを判断します。存在した場合は、タスクを送信したクライアントに異常が報告されます。

出力ファイルには、次のようなソースファイル情報が含まれます。
1. ソースファイルのリストに存在しますが、コピー時にソースファイルが存在しないため、SRC_MISSと記録されます
2. その他の原因によるコピーの失敗は、すべてCOPY_FAILEDと記録されます

copyコマンドを再実行して、増分移行を行うことができます。次のコマンドによって、MapReduceタスクのログを取得し、ファイルコピーに失敗した原因を特定します。ここでapplication_1610615435237_0021は、アプリケーションIDです。
```plaintext
yarn logs -applicationId application_1610615435237_0021 > application_1610615435237_0021.log
```

### Countersの確認 

コピータスクの終了時に、ファイルのコピーに関する統計情報が出力されます。関連するカウンターは次のとおりです。

```plaintext
CosDistCp Counters
        BYTES_EXPECTED=10198247
        BYTES_SKIPPED=10196880
        FILES_COPIED=1
        FILES_EXPECTED=7
        FILES_FAILED=1
        FILES_SKIPPED=5
```

ファイルコピーの統計情報は次のとおりです。

|  統計項目   |  説明  |
| -----|-----|
|  BYTES_EXPECTED  | ソースディレクトリの統計に基づいてコピーが必要なファイルの合計サイズ。単位：バイト   |
|  FILES_EXPECTED  | ディレクトリファイルを含む、ソースディレクトリの統計に基づいてコピーが必要なファイル数   |
|  BYTES_SKIPPED  | 長さまたはチェックサム値が等しく、コピーされないファイルサイズの合計。単位：バイト  |
|  FILES_SKIPPED  | 長さまたはチェックサム値が等しく、コピーされないソースファイル数  |
|  FILES_COPIED  | コピーに成功したソースファイル数   |
|  FILES_FAILED  | コピーに失敗したソースファイル数   |
|  FOLDERS_COPIED  | コピーに成功したディレクトリ数   |
|  FOLDERS_SKIPPED  | スキップしたディレクトリ数   |


### コピープロセス数と各コピープロセスのコピースレッド数を指定します

パラメータ`--taskNumber`と`--workersNumber`によってコマンドを実行します。COSDistCpはマルチプロセス+マルチスレッドのコピーアーキテクチャを使用しており、次のことが可能です。
- `--taskNumber`でコピーするプロセス数を指定します
- `--workerNumber`で各コピープロセスにおけるコピースレッド数を指定します

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse --taskNumber=10 --workerNumber=5
```

### 同じチェックサムを持つファイルをスキップし、増分移行を実行します

パラメータ`--skipMode`によりコマンドを実行します。同じ長さとチェックサムを持つソースとターゲットファイルのコピーをスキップします。デフォルト値はlength-checksumです。
```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse  --skipMode=length-checksum
```

`--skipMode`オプションは、ファイルをコピーする前に、ソースファイルとターゲットファイルが同じかどうかをチェックして、同じであればスキップします。none（チェックしない）、length（長さ）、checksum（CRC値）、length-checksum（長さ+CRC値）が選択可能です。

ソースとターゲットのファイルシステムのチェックサムアルゴリズムが異なる場合、ソースファイルを読み込んで新しいチェックサムを計算します。ソースがHDFSの場合、HDFSソースがCOMPOSITE-CRC32Cチェックサムアルゴリズムをサポートしているかどうかは、次のように確認することができます。

```plaintext
hadoop fs  -Ddfs.checksum.combine.mode=COMPOSITE_CRC -checksum /data/test.txt
/data/test.txt  COMPOSITE-CRC32C        6a732798
```

### 移行完了後のデータチェックおよび増分移行

パラメータ`--diffMode`と`--diffOutput`によりコマンドを実行します。
- `--diffMode`のオプション値はlengthとlength-checksumです。
 - `--diffMode=length`は、ファイルサイズが同じかどうかによって、差分ファイルのリストを取得することを表します。
 - `--diffMode=length-checksum`、ファイルサイズとCRCチェックサムが同じかどうかによって、差分ファイルのリストを取得することを表します。
- `--diffOutput`は、diff操作の出力ディレクトリを指定します。
ターゲットファイルシステムがCOSで、ソースファイルシステムのCRCアルゴリズムが異なる場合、COSDistCpはソースファイルをプルしてターゲットファイルシステムのCRCを計算し、同じCRCアルゴリズム値を比較します。以下の例では、移行が完了した後、--diffModeパラメータを使用して、ファイルサイズとCRC値に基づきソースファイルとターゲットファイルが同じであることをチェックしています。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

上記のコマンドの実行が成功すると、ソースファイルシステムのファイルリストを基準にカウンター情報（タスクがマシンへ送信され、MapReduceタスクの提出側INFOログの出力が設定されたことを確認してください）が出力されます。このカウンター情報を基に、ソースとターゲットが同じであるか分析することができます。カウンター情報の説明は、次のとおりです。

1. ソースファイルとターゲットファイルが同じ場合、SUCCESSと記録されます
2. ターゲットファイルが存在しない場合、DEST_MISSと記録されます
3. ソースディレクトリのリストに存在しますが、チェック時にソースファイルが存在しないため、SRC_MISSと記録されます
4. ソースファイルとターゲットファイルのサイズが異なる場合、LENGTH_DIFFと記録されます
5. ソースファイルとターゲットファイルのCRCアルゴリズムの値が異なる場合、CHECKSUM_DIFFと記録されます
6. 読み込み権限が不十分であるなどの要因により、diff操作が失敗した場合、DIFF_FAILEDと記録されます
7. ソースがディレクトリ、ターゲットがファイルの場合、TYPE_DIFFと記録されます

また、COSDistcpは、HDFSの`/tmp/diff-output/failed`ディレクトリ（1.0.5および以前のバージョンでは/tmp/diff-output）に差分ファイルリストを発行します。次のコマンドを使用して、SRC_MISS以外の差分ファイルリストを取得することができます。

```plaintext
hadoop fs -getmerge /tmp/diff-output/failed diff-manifest
grep -v '"comment":"SRC_MISS"' diff-manifest |gzip > diff-manifest.gz
```

次のコマンドを実行し、差分ファイルリストに基づいて増分移行を実行します。

```plaintext
hadoop  jar cos-distcp-${version}.jar --taskNumber=20 --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --previousManifest=file:///usr/local/service/hadoop/diff-manifest.gz --copyFromManifest
```
増分移行が完了したら、再度--diffModeパラメータ付きのコマンドを実行し、ファイルが同じであることをチェックします。

### ソースファイルとターゲットファイルのCRCが同じであるかチェックします

パラメータ`--checkMode`によりコマンドを実行します。ファイルのコピーが完了したときに、ソースファイルとターゲットファイルの長さとチェックサムが同じであることをチェックします。デフォルト値はlength-checksumです。

非COSファイルシステムからCOSに同期する場合やソースのCRCアルゴリズムがHadoop-COSのCRCアルゴリズムと一致しない場合、コピー中にCRCが計算され、コピー完了時にターゲットCOSファイルのCRCを取得し、算出されたソースファイルのCRCと照合します。

```plaintext
hadoop jar cos-distcp-${version}.jar   --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --checkMode=length-checksum
```
>! --groupByが指定されておらず、outputCodecがデフォルト値の場合に有効になります。


### 単一ファイルの読み込み帯域幅を制限します

パラメータ`--bandWidth`によりコマンドを実行します。単位はMBです。移行した各ファイルの読み込み帯域幅を10MB/sに制限します。次に例を示します。

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --bandWidth=10
```

### 複数ディレクトリの同期

ローカルファイル（srcPrefixes.txtなど）を新規作成し、このファイルに移行が必要なディレクトリの絶対パスを追加します。これらのディレクトリ間に親子関係は必要なく、追加すれば、次の例に示すように、catコマンドで確認することができます。

```plaintext
cat srcPrefixes.txt 
/data/warehouse/20181121/
/data/warehouse/20181122/
```

`--srcPrefixesFile`パラメータを使用してこのファイルを指定し、移行コマンドを実行します。

```plaintext
hadoop jar  cos-distcp-${version}.jar --src /data/warehouse  --srcPrefixesFile file:///usr/local/service/hadoop/srcPrefixes.txt --dest  cosn://examplebucket-1250000000/data/warehouse/ --taskNumber=20
```

- 入力ファイルの正規表現でのフィルタリング

パラメータ`--srcPattern`でコマンドを実行すると、`/data/warehouse/`ディレクトリにある.logで終わるログファイルのみを同期します。次に例を示します。

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse --srcPattern='.*\.log$'
```
.tempまたは.tmpで終わるファイルは移行されません。
```
 hadoop jar cos-distcp-${version}.jar --src /data/warehouse/ --dest cosn://examplebucket-1250000000/data/warehouse/ --srcPattern='.*(?<!\.temp|\.tmp)$'
```

### Hadoop-COSのファイルチェックとタイプの指定

パラメータ`--cosChecksumType`によりコマンドを実行します。デフォルトはCRC32Cで、オプションはCRC32CとCRC64です。

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --cosChecksumType=CRC32C
```

### COSファイルのストレージタイプの指定

パラメータ`--storageClass`によりコマンドを実行します。次に例を示します。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest-2020-01-10.gz --storageClass=STANDARD_IA
```


### ターゲットファイルの圧縮タイプの指定

パラメータ`--outputCodec`によりコマンドを実行します。このパラメータを使用すると、HDFS内のデータをリアルタイムに圧縮してCOSにバックアップし、ストレージコストを節約することができます。パラメータのオプション値は、keep、none、gzip、lzop、snappyです。noneオプションはターゲットファイルを非圧縮状態で保存し、keepはオリジナルファイルの圧縮状態を維持します。次に例を示します。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse/logs --dest cosn://examplebucket-1250000000/data/warehouse/logs-gzip --outputCodec=gzip
```

>! keepオプションを除いて、まずファイルを解凍し、それからターゲットの圧縮タイプに変換します。そのためkeepオプション以外では、圧縮パラメータなどの不整合により、ターゲットファイルがソースファイルと一致しないことがありますが、解凍後のファイルは同じになります。--groupByが指定されておらず、--outputCodecがデフォルトの場合は、--skipModeで増分の移行を行い、--checkModeでデータチェックを行うことができます。
>

### ソースファイルの削除

パラメータ`--deleteOnSuccess`によりコマンドを実行し、`/data/warehouse`ディレクトリ内のファイルをHDFSからCOSに同期してから、直ちにソースディレクトリ内の対応するファイルを削除します。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --deleteOnSuccess
```

>! このオプションを指定すると、ファイルが移行されるたびに対応するソースファイルが直ちに削除されます。全体の移行が完了した後、ソースファイルを削除する必要はありませんので、ご注意ください。1.7以降のバージョンでは、このパラメータは提供されません。
>

### ターゲットリストファイルの発行と最終リスト出力ファイルの指定

パラメータ`--outputManifest`と`--previousManifest`によりコマンドを実行します。

- `--outputManifest`このオプションは、まずローカルでgzip圧縮されたmanifest.gzを発行し、移行が成功したときに`--dest`で指定されたディレクトリに移動させます。
- `--previousManifest`は前回の`--outputManifest`出力ファイルを指定します。COSDistCpは、同じサイズのファイルをスキップします。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest  cosn://examplebucket-1250000000/data/warehouse/ --outputManifest=manifest.gz --previousManifest= cosn://examplebucket-1250000000/data/warehouse/manifest-2020-01-10.gz
```

>! 上記のコマンドの増分移行では、サイズが変更されたファイルのみを同期できますが、ファイル内容が変更されたファイルは同期できません。ファイルの内容が変更される可能性がある場合は、 --diffModeの使用例を参照して、ファイルのCRCに基づいて変更されたファイルのリストを決定してください。
>


### 移行タスクの割り当てポリシーを動的割り当てに指定

ごく少量の非常に大きなファイル、多数の小さなファイル、移行用マシンの負荷が変化する場合などのように、ファイルサイズが極端に分かれている場合は、enableDynamicStrategy`を使用して、タスクの動的割り当てポリシーを有効にすると、実行速度の速いタスクがより多くのファイルを移行できるようになり、タスクの実行時間が短縮されます。

```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse    --dest  cosn://examplebucket-1250000000/data/warehouse --enableDynamicStrategy
```
移行完了後の移行データのチェックを行います。
```
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

>! このモードには一定の制限があります。例えば、プロセス例外が発生した場合、タスクカウンターはカウントが不正確になる可能性があります。移行完了後に--diffModeを使用してデータをチェックしてください。
>

### ファイルのメタ情報のコピー

パラメータ`--preserveStatus`によりコマンドを実行し、ソースファイルまたはソースディレクトリのuser、group、permission、timestamps（modification timeとaccess time）をターゲットファイルまたはターゲットディレクトリにコピーします。このパラメータは、HDFSからCHDFSへファイルをコピーするときに有効になります。
例：
```plaintext
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --preserveStatus=ugpt
```


### Prometheusモニタリングの設定

Yarnの管理画面では、すでに移行が完了したファイル数、バイト数などの情報を含む、COSDistcp移行タスクのカウンターを確認することができます。移行タスクカウンターの曲線の推移をより見やすくするためには、prometheus.ymlを設定してクロールタスクを追加するといった簡単な設定だけで、Prometheus + GrafanaモニタリングシステムでCOSDistcp移行タスクのカウンターを表示させることができます。

```plaintext
- job_name: 'cos-distcp-hive-backup'
    static_configs:
      - targets: ['172.16.16.139:9028']
```

パラメータ`--promPort=VALUE`によりコマンドを実行し、現在のMapReduceタスクのカウンターを外部に公開します

```plaintext
hadoop jar cos-distcp-${version}.jar  --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --promPort=9028
```

事例の[Grafana Dashboard](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/COSDistcp-Grafana-Dashboard.json)をダウンロードしてインポートすると、Grafanaは次のように表示されます。
![COSDistcp-Grafana](https://staticintl.cloudcachetci.com/yehe/backend-news/2Rc8914_2.png)


### ファイルコピー失敗時のアラート
パラメータ`--completionCallbackClass`でコールバッククラスパスを指定してコマンドを実行します。COSDistCpはコピータスクが完了すると、収集したタスク情報をパラメータとしてコールバック関数を実行します。ユーザー定義のコールバック関数については、以下のインターフェースを実装する必要がありますので、[コールバックのサンプルコードのダウンロード](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-distcp/cos-distcp-alarm-1.0.jar)に移動してください。

```plaintext
package com.qcloud.cos.distcp;
import java.util.Map;
public interface TaskCompletionCallback {
/**
 * @description: When the task is completed, the callback function is executed
 * @param jobType Copy or Diff
 * @param jobStartTime  the job start time
 * @param errorMsg  the exception error msg
 * @param applicationId the MapReduce application id
 * @param: cosDistCpCounters the job 
*/

void doTaskCompletionCallback(String jobType, long jobStartTime, String errorMsg, String applicationId, Map<String, Long> cosDistCpCounters);

/**
 *  @description: init callback config before execute
 */
void init() throws Exception;
}
```

COSDistCpは、内部でBCMのアラートを統合し、タスクに異常が発生したり、ファイルコピーに失敗したりした場合にアラートを実行します。

```plaintext
export alarmSecretId=SECRET-ID
export alarmSecretKey=SECRET-KEY
export alarmRegion=ap-guangzhou
export alarmModule=module
export alarmPolicyId=cm-xxx
hadoop jar cos-distcp-1.4-2.8.5.jar \
-Dfs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider \
-Dfs.cosn.userinfo.secretId=SECRET-ID \
-Dfs.cosn.userinfo.secretKey=SECRET-KEY \
-Dfs.cosn.bucket.region=ap-guangzhou \
-Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
-Dfs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
--src /data/warehouse \
--dest cosn://examplebucket-1250000000/data/warehouse/ \
--checkMode=checksum \
--completionCallbackClass=com.qcloud.cos.distcp.DefaultTaskCompletionCallback
```

上記コマンドのalarmPolicyIdは、BCMアラートポリシーであり、BCMコンソールで作成と設定ができます（アラート管理 > アラート設定 > カスタムメッセージ）。



## よくあるご質問
### COSDistcpを使用したHDFSデータの移行にはどのような段階があり、どのように移行パフォーマンスを調整してデータの正確性を確保すればよいですか。
COSDistcpでは各ファイルの移行完了ごとに、checkModeに基づいて、移行したファイルに対してチェックが行われます。
```
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse --taskNumber=20
```
また、移行が完了したら、以下のコマンドを実行し、ソースとターゲットの差分ファイルリストを確認することができます。
```
hadoop jar cos-distcp-${version}.jar --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse/ --diffMode=length-checksum --diffOutput=/tmp/diff-output
```

### Hadoop-COSが設定されていない環境で、COSDistCpを実行するにはどうすればいいですか。

Hadoop-COSプラグインが設定されていない環境のユーザーの場合、Hadoopのバージョンに従って、対応するバージョンのCOSDistCp jarパッケージをダウンロードし、Hadoop-COS関連のパラメータを指定してコピータスクを実行します。

```plaintext
hadoop jar cos-distcp-${version}.jar \
-Dfs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider \
-Dfs.cosn.userinfo.secretId=COS_SECRETID \
-Dfs.cosn.userinfo.secretKey=COS_SECRETKEY \
-Dfs.cosn.bucket.region=ap-guangzhou \
-Dfs.cosn.impl=org.apache.hadoop.fs.CosFileSystem \
-Dfs.AbstractFileSystem.cosn.impl=org.apache.hadoop.fs.CosN \
--src /data/warehouse \
--dest cosn://examplebucket-1250000000/warehouse
```

### コピー結果に、一部のファイルのコピーに失敗したと表示されます。どうすればよいですか。

COSDistCpは、ファイルコピー中に発生した IOExceptionに対して5回再試行します。5回目のコピーも失敗した場合は、失敗したファイル情報を`/tmp/${randomUUID}/output/failed/`ディレクトリに書き込みます。ここで、${randomUUID}はランダムな文字列です。コピーが失敗する一般的な原因としては、次のようなものがあります。
1. コピーリストにソースファイルは存在しますが、コピー時にソースファイルが存在しないため、SRC_MISSと記録されます。
2. タスクを開始したユーザーが、ソースファイルの読み込みやターゲットファイルへの書き込みの権限を持っていないことなどが原因で、COPY_FAILEDと記録されます。

ログ情報にソースファイルが存在しないことが記録されており、ソースファイルを実際に無視できる場合は、次のコマンドを使用して、SRC_MISS以外の差分ファイルのリストを取得することができます。
```plaintext
hadoop fs -getmerge /tmp/${randomUUID}/output/failed/ failed-manifest
grep -v '"comment":"SRC_MISS"' failed-manifest |gzip > failed-manifest.gz
```
SRC_MISS以外に失敗したファイルがある場合は、 `/tmp/${randomUUID}/output/logs/`ディレクトリにまとめられた例外ログ情報と、yarnアプリケーションなどのプルアプリケーションログに基づいて原因を診断することができます。次のコマンドを使用できます。
```plaintext
yarn logs -applicationId application_1610615435237_0021 > application_1610615435237_0021.log
```
ここでapplication_1610615435237_0021は、アプリケーションIDです。

### COSDistCpは、ネットワークの異常などが発生した場合、不完全なファイルのコピーは生成されますか。

COSDistCpは、ネットワークの異常、ソースファイルの欠落、権限不足などの場合、ターゲット側とソース側で同じサイズのファイルを発行することはできません。
- COSDistCpのバージョンが1.5以下の場合、COSDistCpはターゲット側で生成されたファイルの削除を試みます。削除に失敗した場合は、コピータスクを再実行してこれらのファイルを上書きするか、不完全なファイルを手動で削除する必要があります。
- COSDistCp 1.5以降のバージョンで、実行環境のHadoop COSプラグインバージョンが5.9.3以降の場合、COSDistCpはCOSへのコピーが失敗すると、abortインターフェースを呼び出してアップロード中のリクエストを終了させるようにします。そのため異常が発生しても、不完全なファイルは発行されません。
- COSDistCp 1.5以降のバージョンで、実行環境のHadoop COSプラグインバージョンが5.9.3未満の場合は、5.9.3以降のバージョンにアップグレードすることをお勧めします。
- COS以外のターゲット側では、COSDistCpはターゲットファイルの削除を試みます。

### COSバケットに、目に見えず完了していないアップロードファイルがあり、ストレージ容量を占有しています。どうすればよいですか。
マシンの異常やプロセスのKillなどの要因により、COSバケット内でフラグメントファイルがストレージ容量を占有する場合があります。この場合、公式ウェブサイトの[ライフサイクルドキュメント](https://intl.cloud.tencent.com/document/product/436/14605)を参照して、フラグメントの削除ルールを設定し、クリーンアップを行うことができます。

### 移行プロセスでは、メモリオーバーフローとタスクタイムアウトが発生した場合、どのようにパラメータチューニングを行いますか。
移行プロセスでは、COSDistcpとCOSへのアクセスとCHDFSのツールは、 自身のロジックに基づき、メモリの一部を占有します。メモリオーバーフローとタスクタイムアウトを防ぐため、下の例のようにしてMapReduceタスクのパラメータ調整をすることができます。
```
hadoop jar cos-distcp-${version}.jar -Dmapreduce.task.timeout=18000 -Dmapreduce.reduce.memory.mb=8192 --src /data/warehouse --dest cosn://examplebucket-1250000000/data/warehouse  
```
そのうち、タスクのタイムアウト時間mapreduce.task.timeoutを18000秒に調整することで、大容量のファイルをコピーするとき、タスクタイムアウトの発生を防ぐことができます。Reduceプロセスのメモリ容量mapreduce.reduce.memory.mbサイズを8GBに調整することで、メモリオーバーフローを防ぐことができます。

### 専用回線の移行で、どのように移行タスクの移行帯域幅をコントロールしますか。
COSDistcpでは移行の総帯域幅制限計算式は、taskNumber * workerNumber * bandWidthです。workerNumberを1に設定し、パラメータtaskNumberによる移行の同時実行数のコントロール、およびパラメータbandWidthによる単一の同時実行帯域幅のコントロールができます。



