
## 操作シナリオ
>ストレージスペースを節約するために、MySQLの物理バックアップファイル及び論理バックアップファイルは、まずqpressにて圧縮され、つぎにxbstreamにてパッケージングされて（xbstreamはPerconaのパッケージング/アンパッケージングツールです）圧縮とパッケージングを実行します。
>
オープンソースソフトウェアPercona Xtrabackupは、データベースのバックアップと復元に使用されます。このドキュメントでは、XtraBackupツールを使用して、MySQLの物理バックアップファイルを別のホスト上の自己構築データベースに復元する方法について説明します。
- XtraBackupはLinuxプラットフォームのみに対応し、Windowsプラットフォームに対応していません。
- Windowsでデータを復元する方法の詳細については、[コマンドラインツールによるデータの移行](https://intl.cloud.tencent.com/document/product/236/8464)をご参照ください。


## 前提条件
- XtraBackupツールをダウンロードしてインストールします。
XtraBackupツールは[Percona XtraBackup公式ウェブサイト](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)からダウンロードでき、Percona XtraBackup 2.4.6及びその以降のバーションを選択してください。ツールのインストール方法の詳細については、[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)をご参照ください 。
- サポートするインスタンスのバージョン：MySQL 5.5、5.6、5.7の高可用性エディションとファイナンスエディション。
- データ暗号化が有効になっているインスタンスでは、物理バックアップを使用したデータベースの復元がサポートされていません。

##　操作手順
### 手順1：バックアップファイルのダウンロード
MySQLインスタンスのデータバックアップ、ログバックアップはコンソールからダウンロードできます。
>各IPには、デフォルトで最大10個のダウンロードリンクを設定でき、リンクあたりのダウンロード速度は最大で20～30 Mpbsです。
>
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス名又は操作列の【管理】をクリックして、【インスタンス管理】ページに入ります。
2. 【インスタンス管理】ページで、【バックアップと復元】>【データバックアップリスト】ページを選択し、ダウンロードするバックアップを選択し、操作列で【ダウンロード】をクリックします。
3. ポップアップダイアログボックスで、ダウンロードアドレスをコピーして、TencentDBインスタンスと同じVPCの（Linux）CVMインスタンスにログインし、wgetコマンドを実行して、プライベートネットワークで高速、高効率のダウンロードを行うことをお勧めします。　
>
>- 【ローカルダウンロード】を選択して直接ダウンロードすることもできますが、時間がかかります。
>- wgetコマンド形式：wget -c ‘バックアップファイルのダウンロードアドレス’ -O カスタムファイル名.xb 
>
例：
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O ~/test.xb
```

### 手順2：バックアップファイルのアンパッケージング
1. xbstreamコマンドを使用して、バックアップファイルを保存先ディレクトリにアンパッケージングします。
```
xbstream -x -C /data < ~/test.xb
```
>
>- このドキュメントでは、保存先ディレクトリを`/data`としますが、ユーザが実際の状況に応じて実際のパスに置き換えることができます。
>- `~/test.xb`はユーザのバックアップファイルに置き換えられます。
>
展開した結果は、次の図に示します。
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

### 手順3：バックアップファイルの解凍
1. 次のコマンドを使用して、qpressツールをダウンロードします。
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
> wgetダウンロードにエラーが発生した場合は、[quicklz](http://www.quicklz.com/)からqpressツールをローカルまでダウンロードした後、qpressツールをLinux CVMインスタンスにアップロードしてください。詳細については、[SCPを通じてファイルをLinux CVMにアップロード](https://intl.cloud.tencent.com/document/product/213/2133)をご参照ください。
2. 次のコマンドを実行して、qpressバイナリーファイルを解凍します。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. 次のコマンドを実行して、ターゲットディレクトリの下にある`.qp`で終わるすべてのファイルを解凍します。
```
xtrabackup --decompress --target-dir=/data
```
>
>- `/data`は、バックアップファイルが保存されていたターゲットディレクトリです。実際の状況に応じて、実際のパスに置き換えることもできます。
>- `--remove-original`オプションは、Percona Xtrabackupの2.4.6及びその以降のバージョンでのみサポートされています。
>- `xtrabackup`については、デフォルトでは解凍中に元のファイルを削除しません。解凍した後に元のファイルを削除したい場合、上記のコマンドに`--remove-original`パラメータを追加することができます。
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

### 手順4：バックアップファイルの準備
バックアップファイルが解凍された後、下記のコマンドを実行して「apply log」処理を行います。
```
xtrabackup --prepare  --target-dir=/data
```
実行した後、結果に下記の出力が含まれている場合は、準備が成功したことを示します。
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	

### 手順5：コンフィギュレーションファイルの変更
1. 次のコマンドを実行して、ファイル`backup-my.cnf`を開きます。
```
vi /data/backup-my.cnf
```
>このドキュメントでは、保存先ディレクトリを`/data`としますが、実際の状況に応じて、実際のパスに置き換えることができます。
>
2. バージョン問題のため、解凍されたファイル`backup-my.cnf`で次のパラメーターをコメント化する必要があります。
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 
 
![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### 手順6:ファイルプロパティの変更
ファイルプロパティを変更し、ファイルがmysqlユーザーによって所有されているかどうかを確認します。
```
chown -R mysql:mysql /data
```
![](https://main.qcloudimg.com/raw/2c2bfcad8c8bdac9385e70d975bec56a.png)

### ステップ7：mysqldプロセスを起動しログイン検証を実行
1. mysqldプロセスを起動します。
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. 検証のためにmysqlクライアントにログインします。
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## バックアップに関するよくある質問
[バックアップに関するよくある質問](https://intl.cloud.tencent.com/document/product/236/9036)及び[バックアップ失敗の原因](https://intl.cloud.tencent.com/document/product/236/34394)をご参照ください。
