## 操作シナリオ
本節では、ローカルにダウンロードした物理バックアップファイルを使って他のホストでデータベースを復元する方法について説明します。

## 操作手順
### バックアップファイルのダウンロード
詳細手順の確認：[バックアップダウンロード](https://intl.cloud.tencent.com/document/product/236/7274)

### バックアップファイルの展開
1. バックアップファイルは、 qpressにて圧縮され、xbstreamを持って展開します（xbstreamはPerconaの圧縮・展開ツールの1つである）。そのために、バックアップファイルをダウンロードした後に、まずxbstream を使って展開する必要があります。xbstream ツールについては、 Percona XtraBackup公式サイトからダウンロードするか、或いはバイナリーパッケージを直接ダウンロードできます。
 - [Percona XtraBackup 公式サイトからダウンロード・インストール](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)
  Percona XtraBackup 2.4.6 及びその以降のバージョンをご使用ください。インストール方法については、[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)をご参照ください。
 - バイナリーパッケージのインストール
  [XtraBackup-download](https://www.percona.com/downloads/Percona-XtraBackup-2.4/Percona-XtraBackup-2.4.13/binary/tarball/percona-xtrabackup-2.4.13-Linux-x86_64.libgcrypt145.tar.gz)  からOSバージョンに対応するXtraBackupバイナリーパッケージをダウンロードします。
>現在、Windows OSでは、XtraBackupツールがサポートされません。XtraBackupツールは、Linux OSでのみ、サポートされています。
2. XtraBackupをインストールした後に、 xbstream コマンドを使って、バックアップファイルをターゲットディレクトリに展開します。
```
xbstream -x -C /data < ~/test.xb
```
展開した結果は、次の図に示す。
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

### バックアップファイルの解凍
バックアップファイルは、quicklzアルゴリズムによって圧縮されているため、解凍する必要があります。[qpressツールをダウンロード](http://www.quicklz.com/)する必要があります。ダウンロードした後、下記のコマンドでqpressバイナリーファイルを解凍します。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
qpressコマンドでターゲットディレクトリの下にある「.qp」で終わるすべてのファイルを解凍します。
```
xtrabackup --decompress --target-dir=/data
```
>
>- 「xtrabackup --decompress」は qpress ツールを呼び出します。「--decompress」パラメータを使用する前に、qpressをインストールする必要があります。
>- 「--remove-original」オプションは、Percona Xtrabackupの2.4.6及びその以降のバージョンでのみ、サポートされています。
>- 「xtrabackup」については、デフォルトでは解凍した時に最初の圧縮ファイルを削除しません。解凍した後に最初の圧縮ファイルを削除したい場合、上記のコマンドに「--remove-original」`パラメータを追加することができます。
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

###  Prepare バックアップファイル
バックアップを解凍した後に、下記のコマンドを実行してapply log 処理を行います。
```
xtrabackup --prepare  --target-dir=/data
```
実行した後、結果に下記の出力が含まれていれば、 prepare に成功したことを示します。
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	

### 構成ファイルの変更
バージョン問題のため、解凍ファイル backup-my.cnfから下記のパラメータをコメントアウトしてください。
- innodb_checksum_algorithm
- innodb_log_checksum_algorithm
- innodb_fast_checksum
- innodb_page_size 
- innodb_log_block_size
- redo_log_version 

![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### ファイルプロパティ変更
ファイルプロパティを変更し、ファイルが mysqlユーザーに属することをチェックします。
```
chown -R mysql:mysql /data
```
![](https://mc.qcloudimg.com/static/img/efbdeb20e1b699295c6a4321943908b2/4.png)

### mysqldプロセスの起動・ログイン検証
1.  mysqldプロセスを起動します。
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. クライアントはmysqlにログインして検証します。
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

>
>- 復元が終了した後、テーブルmysql.userには TencentDBで作成したユーザーがないため、新規作成する必要があります。
>- ユーザーを新規作成する前に、下記の SQLを実行してください。
```
delete from mysql.db where user<>'root' and char_length(user)>0;
delete from mysql.tables_priv where user<>'root' and char_length(user)>0;
flush privileges;
```
