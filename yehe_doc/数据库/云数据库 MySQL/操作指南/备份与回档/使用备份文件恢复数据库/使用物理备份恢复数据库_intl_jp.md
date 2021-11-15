
## 操作シナリオ
>ストレージ容量を節約するために、TencentDB for MySQLの物理バックアップファイル及び論理バックアップファイルは、まずqpressで圧縮し、次にxbstreamでパッケージング（xbstreamはPerconaのパッケージング/アンパッケージングツール）して圧縮とパッケージングを実行します。
>
オープンソースソフトウェアPercona Xtrabackupは、データベースのバックアップ、復旧に使用できます。ここでは、XtraBackupツールを使用して、MySQL物理バックアップファイルを、その他のマスターマシン上で自ら構築したデータベースに復旧させる方法を紹介します。
- XtraBackupLinuxプラットフォームのみをサポートし、Windowsプラットフォームはサポートしません。
- Windowsプラットフォームでデータを復元する方法の詳細については、[コマンドラインツールによるデータの移行](https://intl.cloud.tencent.com/document/product/236/8464)をご参照ください。


## 前提条件
- XtraBackupツールをダウンロードしてインストールします。
アドレスのダウンロードについては、 [Percona XtraBackup公式サイト](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)を参照し、Percona XtraBackup 2.4.6以上のバージョンを選択してください。インストール方法の紹介は、[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)をご参照ください。
- サポートするインスタンスのバージョン：MySQL 2ノードおよび3ノード。
- データ暗号化機能が有効になっているインスタンスについては、物理バックアップを用いたデータベースの復旧はサポートされません。

## 操作手順
>?ここではCentOS OSのCloud Virtual Machine（CVM） とMySQL 5.7バージョンを例として説明します。
>
### 手順1：バックアップファイルのダウンロード
コンソールを介して、TencentDB for MySQLのデータバックアップ、ログバックアップをダウンロードできます。
>?デフォルトでは、各IPのリンクは10個に制限しており、各リンクのダウンロード速度は20Mbps～30Mbpsです。
>
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストのインスタンス名または「操作」の列の【管理】をクリックし、インスタンス管理画面に入ります。
2. インスタンス管理画面で、【バックアップの復旧】>【データバックアップリスト】のページを選択し、ダウンロードしたいバックアップを選択して、「操作」列の【ダウンロード】をクリックします。
3. ポップアップダイアログボックスで、ダウンロードアドレスをコピーして、[クラウドデータベースが存在するVPC内のCVM（Linuxシステム）にログイン](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)し、wgetコマンドを実行して、より効率的なイントラネットの高速ダウンロードを行うことをお勧めします。
>?
>- 【ローカルダウンロード】を選択して直接ダウンロードすることもできますが、時間がかかります。
>- wgetコマンド形式：wget -c 'バックアップファイルのダウンロードアドレス' -O カスタムファイル名.xb 
>
例：
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O ~/test.xb
```

### 手順2：データの復旧
#### 2.1 バックアップファイルのアンパッケージング
xbstreamコマンドを使用してバックアップファイルをターゲットディレクトリにアンパックします。
```
xbstream -x -C /data < ~/test.xb
```
>?
>- ここでのターゲットディレクトリは、`/data`を例として、実際の状況に基づき実際のパスに置き換えることができます。
>- `~/test.xb`をバックアップファイルに置き換えます。
>
展開した結果は、次のように示されます。
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

#### 2.2 バックアップファイルのアンパッケージング
1. 次のコマンドを使用して、qpressツールをダウンロードします。
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?wgetのダウンロードでエラーが表示された場合は、[quicklz](http://www.quicklz.com/) に進んでqpressツールをローカルにダウンロードした後、qpressツールをLinux CVMにアップロードできます。詳細については、[SCPによるLinux CVMへのファイルのアップロード](https://intl.cloud.tencent.com/zh/document/product/213/2133)をご参照ください。
2. 次のコマンドを使用して、qpressバイナリーファイルを解凍します。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. 以下のコマンドを使用して、対象ディレクトリ内の`.qp`を末尾とするすべてのファイルを解凍します。
```
xtrabackup --decompress --target-dir=/data
```
>?
>- `/data`をこれまでのバックアップファイルを保存する対象ディレクトリとします。実際の状況に基づき実際のパスに置き換えることができます。
>- Percona Xtrabackup2.4.6以上のバージョンで`--remove-original`オプションに対応します。
>- `xtrabackup`を解凍するとき、デフォルトではオリジナルの圧縮ファイルは削除されません。解凍後にオリジナルの圧縮ファイルを削除する場合は、上記のコマンドに`--remove-original`パラメータを追加します。
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

#### 2.3 バックアップファイルのprepare
バックアップを解凍後、次のコマンドを実行してapply log操作を行います。
```
xtrabackup --prepare  --target-dir=/data
```
実行後の結果に次の出力がある場合は、prepareが成功したことを示します。
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	
	
#### 2.4 設定ファイルの修正
1. 次のコマンドを実行して`backup-my.cnf`ファイルを開きます。
```
vi /data/backup-my.cnf
```
>- ここでの対象ディレクトリ`/data`を例として、実際の状況に基づき実際のパスに置き換えることができます。
>
2. バージョンの問題によるものは、解凍ファイル`backup-my.cnf`の次のパラメータに注意してください。
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

#### 2.5 ファイルのプロパティの修正
ファイルのプロパティを修正し、ファイルの所属がmysqlユーザーかどうかチェックします。
```
chown -R mysql:mysql /data
```
![](https://mc.qcloudimg.com/static/img/efbdeb20e1b699295c6a4321943908b2/4.png)

### 手順3：mysqldプロセスを始動してログイン認証します
1. mysqldプロセスを始動します。
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. クライアントがmysqlログイン認証します。
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## バックアップ関連の質問
詳細手順については、 [バックアップについてのよくあるご質問](https://intl.cloud.tencent.com/document/product/236/9036) と [バックアップ失敗の原因](https://intl.cloud.tencent.com/document/product/236/34394)をご参照ください。


