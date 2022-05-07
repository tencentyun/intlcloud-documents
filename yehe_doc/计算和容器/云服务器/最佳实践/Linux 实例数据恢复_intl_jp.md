## 概要
このドキュメントでは、CentOS 8.0を搭載したTencent Cloud CVMを例として取り上げ、オープンソースツール[Extundelete](https://sourceforge.net/projects/extundelete/)を使用して誤って削除されたデータをすばやくリカバーする方法について説明します。
Extundeleteは、誤って削除されたファイルシステムタイプext3およびext4のファイルのリカバーをサポートしますが、具体的なリカバーの度合いは、削除後に書き込みによって上書きされるかどうか、メタデータがjournalに保存されるかどうかなどの要因に関連しす。データのリカバーを必要とするファイルシステムがシステムディスクにあり、常にサービスプロセスまたはシステムプロセスがファイルを書き込んでいる場合、リカバーの可能性は低くなります。

<dx-alert infotype="explain" title="">
Tencent Cloudは、[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)、[カスタマイズイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)および[Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6222)などのデータストレージ方法を提供しています。データセキュリティを向上させるために、定期的にデータバックアップを行うことをお勧めします。
</dx-alert>




## 準備作業
データリカバーに関連する操作を実行する前に、次の準備を完了してください：
- 問題が発生するときに初期状態にリカバーできるために、[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)および[カスタマイズイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)を参照してデータをバックアップしてください。
- 関連するサービスプログラムを停止し、ファイルシステムへのデータの書き込みを続行します。データディスクをリカバーする必要がある場合、最初にデータディスクで`umount`操作を実行できます。


## 操作手順

1. 次の2つの方法を使用して、Extundeleteをインストールします：
<dx-tabs>
::: コンパイルされたバイナリプログラムをダウンロードします（推奨）
1. 次のコマンドを実行して、コンパイルされたバイナリプログラムを直接ダウンロードできます。
```
wget https://github.com/curu/extundelete/releases/download/v1.0/extundelete
```
2. 次のコマンドを実行して、ファイルの権限を付与します。
```
chmod a+x extundelete
```
:::
::: 手動によるコンパイルとインストール

<dx-alert infotype="explain" title="">
この手順では、CentOS 7 OSを例として取り上げます。手順はシステム環境によって異なります。実際のリファレンスドキュメントに従って操作してください。
</dx-alert>



1. 次のコマンドを実行して、Extundeleteに必要な依存関係とライブラリをインストールします。
```shell
yum install libcom_err e2fsprogs-devel
```
```shell
yum install gcc gcc-c++ 
```
2. 次のコマンドを実行して、Extundeleteソースコードをダウンロードします。
```
wget https://github.com/curu/extundelete/archive/refs/tags/v1.0.tar.gz
```
3. 次のコマンドを実行して、v1.0.tar.gzファイルを解凍します。
```
tar  xf v1.0.tar.gz
```
4. 次のコマンドを実行して、コンパイルしてインストールします。
```
cd extundelete-1.0
```
```
./configure
```
```
make
```
5. 次のコマンドを実行して、srcディレクトリに入り、コンパイルされたExtundeleteファイルを表示できます。
```
cd ./src
```
:::
</dx-tabs>
2. 次のコマンドを実行して、データのリカバーを試みます。
```
./extundelete  --restore-all  /dev/対応するディスク
```
リカバーされたファイルは同じレベルのディレクトリの`RECOVERED_FILES`フォルダにあります。必要なファイルがあるかどうかを確認してください。


