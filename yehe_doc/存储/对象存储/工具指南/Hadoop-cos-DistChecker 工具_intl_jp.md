## 機能説明

Hadoop-cos-DistCheckerは、移行したディレクトリの整合性を検証するためのツールです。ユーザーが`hadoop distcp`コマンドを使用してHDFSからCOSにデータを移行した後、MapReduceの並列機能に基づいて、Hadoop-cos-DistCheckerツールは**ソースディレクトリ**と**ターゲットディレクトリ**間の検証比較をすばやく実行することができます。

## 使用環境

- Hadoop-cos v5.8.2以降。詳細については、[hadoop-cos release](https://github.com/tencentyun/hadoop-cos/releases)をご参照ください。
- Hadooop MapReduceの実行環境。

> !
> - 自分でHadoopクラスターをビルドする場合、CRC64チェックデジットの取得をサポートするため、Hadoop-cos依存関係を最新バージョン（GitHub releaseバージョンは5.8.2以降）にする必要があります。
> - Tencent Cloud EMRスイートを使用している場合、2020年5月8日以降に作成されたクラスターには、このHadoop-cosバージョンのみが含まれます。それ以前に作成されたクラスターについては、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してお問い合わせください。

## 利用説明

Hadoop-cos-distcheckerは、Hadoop-cos（CosNファイルシステム）内のファイルのCRC64チェックサムを取得する必要があるため、ツールを実行する前に、設定項目fs.cosn.crc64.checksum.enabled をtrueに設定して、Hadoop-cosファイルのCRC64チェックサムの取得をサポートする必要があります。ツールの実行が完了したら、このオプションをfalseに戻し、CRC64チェックサムの取得を無効にします。

> !Hadoop-COSでサポートされているCRC64チェックサムはHDFSファイルシステムのCRC32Cチェックサムと互換性がないため、このツールを使用した後は、必ず上記の設定項目を無効状態に戻してください。戻さない場合、Hadoop-cosがファイルシステムのgetFileChecksumインターフェースが呼び出されるシナリオによっては、実行が失敗する恐れがあります。

### パラメータの概念

- **ソースファイルリスト**：ソースファイルパスリストとは、ユーザーが以下のコマンドを実行してエクスポートしたチェック対象のサブディレクトリとファイルのリストです。
```plaintext
hadoop fs -ls -R hdfs://host:port/{source_dir} | awk '{print $8}' > check_list.txt
```
 形式の例は次のとおりです。
```plaintext
/benchmarks/TestDFSIO
/benchmarks/TestDFSIO/io_control
/benchmarks/TestDFSIO/io_control/in_file_test_io_0
/benchmarks/TestDFSIO/io_control/in_file_test_io_1
/benchmarks/TestDFSIO/io_data
/benchmarks/TestDFSIO/io_data/test_io_0
/benchmarks/TestDFSIO/io_data/test_io_1
/benchmarks/TestDFSIO/io_write
/benchmarks/TestDFSIO/io_write/_SUCCESS
/benchmarks/TestDFSIO/io_write/part-00000
```
- **ソースディレクトリ**：ソースファイルのリストがあるディレクトリを指します。このディレクトリは通常、データを移行する際の`distcp`コマンドのソースパスにもなります。次に示すように、`hdfs://host:port/source_dir`はソースディレクトリです。
```plaintext
hadoop distcp hdfs://host:port/source_dir cosn://examplebucket-appid/dest_dir
```
 さらに、このパスは**ソースファイルパスリスト**の共通の親ディレクトリでもあります。例えば、上記のソースファイルリスト共通の親ディレクトリは、`/benchmarks`です。
- **ターゲットディレクトリ**：比較するターゲットディレクトリです。

### コマンドライン形式

Hadoop-cos-DistCheckerは、MapReduceジョブプログラムです。MapReduceジョブの送信プロセスに従えばOKです。

```plaintext
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App <ソースファイルリストの絶対パス> <ソースディレクトリの絶対パス表現> <ターゲットディレクトリの絶対パス表現> [optional parameters]
```

> ? Optional parametersは、Hadoopのオプションパラメータを示します。

#### 使用手順

以下では、ツールの使用手順を紹介する例として、` hdfs://10.0.0.3:9000/benchmarks`と`cosn://hdfs-test-1250000000/benchmarks`のチェックを例として取り上げます。

まず、次のコマンドを実行します。

```plaintext
hadoop fs -ls -R hdfs://10.0.0.3:9000/benchmarks | awk '{print $8}' > check_list.txt
```

![](https://main.qcloudimg.com/raw/a2a853be2646b6558983303de805c04e.png)
次のように、チェックするソースパスをcheck_list.txtファイルにエクスポートします。このファイルには、ソースファイルのパスリストが格納されています。
![](https://main.qcloudimg.com/raw/216d90b20d383e233e50f497e83c24c3.png)

次に、check_list.txtをHDFSに入れて、次のように実行します。

```plaintext
hadoop fs -put check_list.txt hdfs://10.0.0.3:9000/
```

![](https://main.qcloudimg.com/raw/e5b79519dfeac808b64f29e04c35e9a4.png)

最後に、Hadoop-cos-DistCheckerを実行し、`hdfs://10.0.0.3:9000/benchmarks`と`cosn://hdfs-test-1250000000/benchmarks`を比較して、出力結果を`cosn://hdfs-test-1250000000/check_result`のパスに保存します。コマンド形式は次のとおりです。

```shell
hadoop jar hadoop-cos-distchecker-2.8.5-1.0-SNAPSHOT.jar com.qcloud.cos.hadoop.distchecker.App hdfs://10.0.0.3:9000/check_list.txt hdfs://10.0.0.3:9000/benchmarks cosn://hdfs-test-1250000000/benchmarks cosn://hdfs-test-1250000000/check_result
```

![](https://main.qcloudimg.com/raw/8356bebae88dae96aaecf03ea202df0d.png)

Hadoop-cos-DistCheckerは、ソースファイルリストとソースディレクトリを読み込み、MapReduceジョブを実行して分散チェックを行い、最終的なチェックレポートを`cosn://examplebucket-appid/check_result`パスに出力します。

![](https://main.qcloudimg.com/raw/b49000f8613e41a659df31c19bdab2fa.png)

チェックレポートは次のとおりです。

```plaintext
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO       hdfs://10.0.0.3:9000/benchmarks/TestDFSIO,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control    hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0  hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_0,CRC64,1566310986176587838,1566310986176587838,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1  hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_control/in_file_test_io_1,CRC64,-6584441696534676125,-6584441696534676125,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data       hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_0,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_0,CRC64,3534425600523290380,3534425600523290380,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_data/test_io_1,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_data/test_io_1,CRC64,3534425600523290380,3534425600523290380,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write      hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write,None,None,None,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS     hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/_SUCCESS,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/_SUCCESS,CRC64,0,0,SUCCESS,'The source file and the target file are the same.'
hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000   hdfs://10.0.0.3:9000/benchmarks/TestDFSIO/io_write/part-00000,cosn://hdfs-test-1250000000/benchmarks/TestDFSIO/io_write/part-00000,CRC64,-4804567387993776854,-4804567387993776854,SUCCESS,'The source file and the target file are the same.'
```



## チェックレポート形式

チェックレポートは、次のような形式で表示されます。

```plaintext
check_list.txtのソースファイルパス、ソースファイルの絶対パス、ターゲットファイルの絶対パス、Checksumアルゴリズム、ソースファイルのchecksum値、ターゲットファイルのchecksum値、チェック結果、チェック結果の説明
```

これらのチェック結果は、以下7つのカテゴリーに分類されます。

- SUCCESS：ソースファイルとターゲットファイルの両方が存在し、整合性が取れていることを示します。
- MISMATCH：ソースファイルとターゲットファイルの両方が存在しますが、整合性が取れていないことを示します。
- UNCONFIRM：ソースファイルとターゲットファイルの整合性を確認できません。この状態は、COS上のファイルがCRC64チェックデジット機能がオンラインになる前に存在していたファイルである可能性があり、そのCRC64チェックサムを取得できないことが主な原因です。
- UNCHECKED：チェックされていません。この状態は、ソースファイルが読み込めないか、ソースファイルのchecksum値を取得できないことが主な原因です。
- SOURCE_FILE_MISSING：ソースファイルが存在しません。
- TARGET_FILE_MISSING：ターゲットファイルが存在しません。
- TARGET_FILESYSTEM_ERROR：ターゲットファイルシステムがCosNファイルシステムではありません。


## よくあるご質問

#### チェックレポートのCRC64値が負の値になるのはなぜですか。

CRC64の値が20ビットの値である可能性があり、Java long型の表現できる範囲を超えていますが、基になるバイトは同じであるため、long型をダンプすると負の数が表示されます。

