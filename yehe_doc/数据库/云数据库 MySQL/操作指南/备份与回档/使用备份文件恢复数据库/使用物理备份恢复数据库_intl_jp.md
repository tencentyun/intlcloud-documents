
## 概要
>ストレージ容量を節約するために、TencentDB for MySQLの物理バックアップファイル及び論理バックアップファイルは、まずqpressで圧縮し、次にxbstreamでパッケージング（xbstreamはPerconaのパッケージング/アンパッケージングツール）して圧縮とパッケージングを実行します。
>
オープンソースソフトウェアPercona Xtrabackupは、データベースのバックアップと復元に使用されます。このドキュメントでは、XtraBackupツールを使用して、MySQLの物理バックアップファイルを別のホスト上の自己構築データベースに復元する方法について説明します。
- XtraBackupツールはLinuxプラットフォームのみに対応し、Windowsプラットフォームに対応していません。
- Windowsでデータを復元する方法の詳細については、[コマンドラインツールによるデータの移行](https://intl.cloud.tencent.com/document/product/236/8464)をご参照ください。

## 前提条件
- XtraBackupツールをダウンロードしてインストールします。
 - MySQL 5.6、5.7の場合は、Percona XtraBackup 2.4.6以降のバージョンを選択してください。[ダウンロードアドレス](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)。インストール手順については、[Percona XtraBackup 2.4ガイド](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)をご参照ください。
 - MySQL 8.0の場合は、Percona XtraBackup 8.0.22-15以降のバージョンを選択してください。[ダウンロードアドレス](https://www.percona.com/downloads/Percona-XtraBackup-LATEST/#)。インストール手順については、[Percona XtraBackup 8.0ガイド](https://www.percona.com/doc/percona-xtrabackup/8.0/installation.html)をご参照ください。
- サポートするインスタンスのバージョン：MySQL 2ノードおよび3ノード。
- データ暗号化が有効になっているインスタンスでは、物理バックアップを使用したデータベースの復元がサポートされていません。

## 操作手順
>?ここではCentOS OSのCloud Virtual Machine（CVM） とMySQL 5.7バージョンを例として説明します。
>
### 手順1：バックアップファイルのダウンロード
MySQLインスタンスのデータバックアップ、ログバックアップはコンソールからダウンロードできます。
>?デフォルトでは、各IPのリンクは10個に制限しており、各リンクのダウンロード速度は20Mbps～30Mbpsです。
>
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストのインスタンスIDまたは**操作**列の**管理**をクリックして、インスタンス管理ページに進みます。
2. インスタンス管理画面で、**バックアップ・復元**>**データバックアップリスト**のページを選択し、ダウンロードしたいバックアップを選択して、**操作**列の**ダウンロード**をクリックします。
3. ポップアップダイアログボックスで、ダウンロードアドレスをコピーして、[クラウドデータベースが存在するVPC内のCVM（Linuxシステム）にログイン ](https://intl.cloud.tencent.com/document/product/213/10517)し、wgetコマンドを実行して、より効率的なプライベートネットワークの高速ダウンロードを行うことをお勧めします。
>?
>- **ローカルダウンロード**を選択して直接ダウンロードすることもできますが、時間がかかります。
>- wgetコマンド形式：wget -c 'バックアップファイルのダウンロードアドレス' -O カスタムファイル名.xb 
>
例：
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O /data/test.xb
```

### 手順2：データの復旧
#### 2.1 バックアップファイルのアンパッケージング
xbstreamコマンドを使用してバックアップファイルをターゲットディレクトリにアンパックします。
```
xbstream -x --parallel=2  -C /data/mysql < /data/test.xb
```
>?
>- このドキュメントのターゲットディレクトリは、`/data/mysql`をデータファイルとして復元し、ストレージします。実情に応じて実際のパスに置き換えることができます。
>- `/data/test.xb`をバックアップファイルに置き換えます。
>
展開した結果は、次の図に示します。
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

#### 2.2 バックアップファイルのアンパッケージング
1. 次のコマンドを使用して、qpressツールをダウンロードします。
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10. http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?wgetのダウンロードにエラーが発生した場合は、[quicklz](http://www.quicklz.com/) からqpressツールをローカルにダウンロードした後、qpressツールをLinux CVMインスタンスにアップロードしてください。詳細については、[SCPによるLinux CVMへのファイルのアップロード](https://intl.cloud.tencent.com/document/product/213/2133)をご参照ください。
>
2. 次のコマンドを実行して、qpressバイナリーファイルを解凍します。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. 次のコマンドを実行して、ターゲットディレクトリの下にある`.qp`で終わるすべてのファイルを解凍します。
```
xtrabackup --decompress --target-dir=/data/mysql
```
>?
>- `/data/mysql`をこれまでのバックアップファイルをストレージするターゲットディレクトリとします。実情に応じて実際のパスに置き換えることができます。
>- `--remove-original`オプションは、Percona Xtrabackupの2.4.6及びその以降のバージョンでのみサポートされています。
>- `xtrabackup`については、デフォルトでは解凍中に元のファイルを削除しません。解凍した後に元のファイルを削除したい場合、上記のコマンドに`--remove-original`パラメータを追加することができます。
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

#### 2.3 バックアップファイルのprepare
バックアップファイルが解凍された後、下記のコマンドを実行して「apply log」処理を行います。
```
xtrabackup --prepare  --target-dir=/data/mysql
```
実行した後、結果に下記の出力が含まれている場合は、準備が成功したことを示します。
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
		
#### 2.4 設定ファイルの修正
1. 次のコマンドを実行して、ファイル`backup-my.cnf`を開きます。
```
vi /data/mysql/backup-my.cnf
```
>?このドキュメントではターゲットディレクトリ`/data/mysql`を例として、実情に応じて実際のパスに置き換えることができます。
>
2. バージョン問題のため、解凍されたファイル`backup-my.cnf`で次のパラメーターをコメント化する必要があります。
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

 ![](https://qcloudimg.tencent-cloud.cn/raw/6d56154cb19d16b56520199290a0c574.png)

#### 2.5 ファイルのプロパティの修正
ファイルプロパティを変更し、ファイルがmysqlユーザーによって所有されているかどうかを確認します。
```
chown -R mysql:mysql /data/mysql
```
![](https://qcloudimg.tencent-cloud.cn/raw/12fbe7f70fefa19fd7af5ac2f95bfdb8.png)

### ステップ3：mysqldプロセスを起動しログイン検証を実行
1.  mysqldプロセスを起動します。
```
mysqld_safe --defaults-file=/data/mysql/backup-my.cnf --user=mysql --datadir=/data/mysql &
```
2. 検証のためにmysqlクライアントにログインします。
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## バックアップに関するよくある質問
[バックアップに関するよくある質問](https://intl.cloud.tencent.com/document/product/236/9036)及び[バックアップ失敗の原因](https://intl.cloud.tencent.com/document/product/236/34394)をご参照ください。
