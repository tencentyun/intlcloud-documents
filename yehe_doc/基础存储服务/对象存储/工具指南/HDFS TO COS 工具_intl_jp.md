## 機能説明
HDFS TO COSツールは、HDFSからTencent Cloud COSにデータをコピーするときに使います。|

## 使用環境
#### システム環境
LinuxまたはWindowsシステム。

#### ソフトウェア依存
JDK 1.7または1.8。 

#### インストールと設定
環境のインストールと設定の詳細については、[Javaのインストールと設定](https://intl.cloud.tencent.com/document/product/436/10865)をご参照ください。

## 設定方法
1. Hadoop-2.7.2以降のバージョンをインストールします。具体的なインストール手順については、[Hadoopのインストールとテスト](https://intl.cloud.tencent.com/document/product/436/10867)をご参照ください。
2. [GitHub](https://github.com/tencentyun/hdfs_to_cos_tools)からHDFS TO COSツールをダウンロードし、解凍してください。
3. 同期するHDFSクラスターのcore-site.xmlをconfフォルダにコピーします。このうちcore-site.xmlには、NameNodeの設定情報が含まれています。
4. 設定ファイルcos_info.confを編集して、バケット(Bucket)、リージョン(Region)およびAPIキー情報を保存します。このうちバケット名は、ユーザー定義の文字列と、システムが発行したAPPID文字列をハイフンで連結することで構成されます（例：examplebucket-1250000000）。
5. コマンドラインパラメータで設定ファイルの場所を指定します。デフォルトの場所はconf/cos_info.confです。
>!コマンドラインパラメータのパラメータが設定ファイルと重複している場合は、コマンドラインが優先されます。

## 利用方法

>?以下は、Linuxを例とした使用方法です。

### ヘルプの確認

```
./hdfs_to_cos_cmd -h
```


### ファイルのコピー

- HDFSからCOSにコピーします。COSにすでに同名のファイルが存在する場合、元のファイルは上書きされます。

```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
-  HDFSからCOSにコピーします。COSにすでに同名で同じ長さのファイルが存在する場合、アップロードは無視されます（1回目のコピー後、再度コピーする場合に適用されます）。

```
./hdfs_to_cos_cmd --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/ -skip_if_len_match
```
Hadoop上でファイルサマリーを計算するとオーバーヘッドが大きくなるため、ここでは長さのみを判断しています。

- HDFSからCOSにコピーします。HDFSにHarディレクトリ（Hadoop Archiveアーカイブファイル）が存在する場合、--decompress_harパラメータを指定することでharファイルを自動的に解凍できます。

```
./hdfs_to_cos_cmd --decompress_har --hdfs_path=/tmp/hive --cos_path=/hdfs/20170224/
```
--decompress_harパラメータを指定しない場合、デフォルトで通常のHDFSディレクトリがコピーされます。すなわち、.harディレクトリ内のindexやmasterindexなどのファイルがそのままコピーされるということです。

### ディレクトリ情報

```shell
conf : 設定ファイル。core-site.xmlとcos_info.confを保存するときに使います
log  : ログディレクトリ
src  : Javaソースプログラム
dep  : 発行した実行可能なJARパッケージをコンパイルします
```

## 質問とヘルプ

#### 設定情報について

バケット(Bucket)、リージョン(Region)、APIキー情報など、入力された設定情報が正しいことを確認してください。このうちバケット名は、ユーザー定義の文字列と、システムが発行したAPPID文字列をハイフンが連結することで構成されます（例：examplebucket-1250000000）。また、マシンの時刻が北京の時刻と一致していることを確認してください（1分程度の差は正常です）。差が大きい場合は、マシンの時刻をリセットしてください。

#### DataNodeについて
DataNodeについては、コピープログラムが配置されているマシンも接続できることを確認してください。NameNodeには接続するパブリックネットワークIPがありますが、取得したblockが配置されているDateNodeマシンはプライベートネットワークIPであり、直接接続することはできません。したがって、NameNodeとDataNodeの両方にアクセスできるように、Hadoopのいずれかのノードで同期プログラムを実行することをお勧めします。

#### 権限について
Hadoopコマンドを使用してファイルをダウンロードし、正常かどうかチェックしてから、同期ツールを使用してHadoopのデータサポートを同期してください。

#### ファイルの上書きについて
COSにすでに存在するファイルについては、デフォルトで再送信と上書きが行われます。ユーザーが明示的に-skip_if_len_matchを指定しない限り、ファイルの長さが同じである場合、アップロードはスキップされます。

#### cos pathについて
cos pathのデフォルトはディレクトリであり、最終的にHDFSからコピーされるファイルはこのディレクトリに保存されます。


#### Tencent Cloud EMR HDFSからのデータのコピーについて
Tencent Cloud EMR HDFSからCOSにデータをコピーする場合、高性能のDistcpツールを使用することをお勧めします。[HadoopファイルシステムとCOS間のデータ移行](https://intl.cloud.tencent.com/document/product/436/34076)をご参照ください。
