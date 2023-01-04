
## ユースケース
>ストレージ容量を節約するために、TencentDB for MySQLの物理バックアップファイル及び論理バックアップファイルは、まずqpressで圧縮し、次にxbstreamでパッケージング（xbstreamはPerconaのパッケージング/アンパッケージングツール）して圧縮とパッケージングを実行します。
>
オープンソースソフトウェアPercona Xtrabackupは、データベースのバックアップと復元に使用されます。このドキュメントでは、XtraBackupツールを使用して、MySQLの物理バックアップファイルを別のホスト上の自己構築データベースに復元する方法について説明します。
- XtraBackupツールはLinuxプラットフォームのみに対応し、Windowsプラットフォームに対応していません。
- Windowsでデータを復元する方法の詳細については、[コマンドラインツールによるデータの移行](https://intl.cloud.tencent.com/document/product/236/8464)をご参照ください。

##  前提条件
- XtraBackupツールをダウンロードしてインストールします。
 - MySQL 5.6/5.7の場合、[ダウンロード先](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)からPercona XtraBackup2.4.6以降のバージョンをご利用ください。インストール方法については、[Percona XtraBackup 2.4ガイド](https://docs.percona.com/percona-xtrabackup/2.4/installation/yum_repo.html)をご参照ください。
 - MySQL 8.0の場合、[ダウンロード先](https://www.percona.com/downloads/Percona-XtraBackup-LATEST/#)からPercona XtraBackup 8.0.22-15以降のバージョンをご利用ください。インストール方法については、[Percona XtraBackup 8.0ガイド](https://docs.percona.com/percona-xtrabackup/8.0/installation/yum_repo.html)をご参照ください。
- サポートするインスタンスのバージョン：MySQL 2ノードおよび3ノード。
- 透過的データ暗号化(TDE)機能が有効になっているインスタンスでは、物理バックアップを使用したデータベースの復元がサポートされていません。

>?ここではCentOS OSのCloud Virtual Machine (CVM)とMySQL 5.7バージョンを例として説明します。
>

## 手順1：[バックアップファイルのダウンロード](id:XZBFWJ)
MySQLインスタンスのデータバックアップ、ログバックアップはコンソールからダウンロードできます。
>?デフォルトでは、各IPのリンクは10個に制限しており、各リンクのダウンロード速度は20Mbps～30Mbpsです。

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

## 手順2：バックアップの復号化キーをダウンロードします（この手順は、バックアップの暗号化機能が有効になっている場合にのみ必要です）。
コンソールからTencentDB for MySQLのデータバックアップの復号化キーをダウンロードできます。
>?データベースのバックアップごとに個別に復号化キーが生成されるため、バックアップの暗号化機能を有効にしている場合は、バックアップファイルをダウンロードするときに復号化キーとともにダウンロードして保存してください。

1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストのインスタンスIDまたは**操作**列の**管理**をクリックして、インスタンス管理ページに進みます。
2. インスタンス管理画面で、**バックアップ復元** > **データバックアップリスト**のページを選択し、ダウンロードしたいバックアップに対応する復号化キーを選択して、**操作**列の**キーをダウンロード**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/743b8d691a006b99cb25591bb2100b07.png)
3. 表示されたダイアログボックスで、キーを保存する必要があるファイルパスを選択し、**ダウンロード**をクリックします。

## 手順3：データの復元
### 3.1 バックアップファイルのアンパッケージング
xbstreamコマンドを使用してバックアップファイルをターゲットディレクトリにアンパックします。
```
xbstream -x --decrypt=AES256 --encrypt-key-file=<キーファイルのバックアップ> --parallel=2  -C /data/mysql < /data/test.xb
```
>?
>- 本書では、ターゲットディレクトリは、`/data/mysql`をデータファイルとしてストレージを復元します。必要に応じて、実際のパスで置き換えてください。
>- `/data/test.xb`をバックアップファイルで置き換えます。
>
展開した結果は、次の図に示したとおりです：
<img src="https://qcloudimg.tencent-cloud.cn/raw/f981522847f38b10bfe0a59c7234b7ba.png"  style="zoom:80%;">

### 3.2 バックアップファイルの解凍
1. 次のコマンドを使用して、qpressツールをダウンロードします。
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar
```
>?wgetダウンロード中にエラーが発生した場合、[qpressツールをダウンロード](https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar)をクリックしqpressツールをローカルにダウンロードした後、Linux CVMにアップロードしてください。詳しくは、[SCPでLinux CVMにファイルをアップロード](https://intl.cloud.tencent.com/document/product/213/2133)をご参照ください。
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
>- `/data/mysql`はこの前バックアップファイルを保存するターゲットディレクトリです。必要に応じて実際のパスで置き換えてください。
>- Percona Xtrabackupは2.4.6以降のバージョンで`--remove-original`オプションをサポートします。
>- `xtrabackup`は、デフォルトでは解凍時に元のファイルを削除しません。解凍後に元のファイルを削除する場合、上記のコマンドに`--remove-original`パラメータを指定してください。
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

### 3.3 バックアップファイルのPrepare
バックアップファイルが解凍された後、下記のコマンドを実行して「apply log」処理を行います。
```
xtrabackup --prepare  --target-dir=/data/mysql
```
実行した後、結果に下記の出力が含まれている場合は、準備が成功したことを示します。
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
		
### 3.4 設定ファイルの修正
1. 次のコマンドを実行し、ファイル`backup-my.cnf`を開きます。
```
vi /data/mysql/backup-my.cnf
```
>?本書では、ターゲットディレクトリ`/data/mysql`を例として説明します。必要に応じて、実際のパスで置き換えてください。
>
2. バージョン問題が原因で、解凍ファイル`backup-my.cnf`で下記のパラメータをコメントアウトしてください。
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

 ![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### 3.5 ファイルのプロパティの修正
ファイルプロパティを変更し、ファイルがmysqlユーザーによって所有されているかどうかを確認します。
```
chown -R mysql:mysql /data/mysql
```
![](https://mc.qcloudimg.com/static/img/efbdeb20e1b699295c6a4321943908b2/4.png)

## 步骤4：mysqldプロセスを起動し、ログイン検証を実行
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

