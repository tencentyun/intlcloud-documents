## 操作シナリオ
>ストレージスペースを節約するために、MySQLの物理バックアップファイル及び論理バックアップファイルは、まずqpressにて圧縮され、つぎにxbstreamにてパッケージングされて（xbstreamはPerconaのパッケージング/アンパッケージングツールです）圧縮とパッケージングを実行します。
>
オープンソースソフトウェアPercona Xtrabackupは、データベースのバックアップと復元に使用されます。このドキュメントでは、XtraBackupツールを使用して、MySQLの論理バックアップファイルを別のホスト上の自己構築データベースに復元する方法について説明します。
- XtraBackupツールはLinuxプラットフォームのみに対応し、Windowsプラットフォームに対応していません。
- Windowsでデータを復元する方法の詳細については、[コマンドラインツールによるデータの移行](https://intl.cloud.tencent.com/document/product/236/8464)をご参照ください。

## 前提条件
- XtraBackupツールをダウンロードしてインストールします。
  XtraBackupツールは[Percona XtraBackup公式ウェブサイト](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)からダウンロードでき、Percona XtraBackup 2.4.6及びその以降のバーションを選択してください。ツールのインストール方法の詳細については、[Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)をご参照ください 。
- サポートするインスタンスのバージョン：MySQL 5.5、5.6、5.7の高可用性エディションとファイナンスエディション。

##　操作手順
### 手順1：バックアップファイルのダウンロード
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス名又は操作列の【管理】をクリックして、【インスタンス管理】ページに入ります。
2. 【インスタンス管理】ページで、【バックアップと復元】>【データバックアップリスト】ページを選択し、ダウンロードするバックアップを選択し、操作列で【ダウンロード】をクリックします。
3. ポップアップダイアログボックスで、ダウンロードアドレスをコピーして、TencentDBインスタンスと同じVPCの（Linux）CVMインスタンスにログインし、wgetコマンドを実行して、プライベートネットワークで高速、高効率のダウンロードを行うことをお勧めします。　
>
>- 【ローカルダウンロード】を選択して直接ダウンロードすることもできますが、時間がかかります。
>- wgetコマンド形式：wget -c ‘バックアップファイルのダウンロードアドレス’ -O カスタムファイル名.xb
>
例：
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### 手順2：バックアップファイルのアンパッケージング
xbstreamを使用してバックアップファイルを解凍します。
```
xbstream -x < test0.xb
```
>`test0.xb`はユーザのバックアップファイルに置き換えられます。
>
展開した結果は、次の図に示します。
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

### 手順3：バックアップファイルの解凍
1. 次のコマンドを使用して、qpressツールをダウンロードします。
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
>wgetダウンロードにエラーが発生した場合は、[quicklz](http://www.quicklz.com/)からqpressツールをローカルまでダウンロードした後、qpressツールをLinux CVMインスタンスにアップロードしてください。詳細については、[SCPを通じてファイルをLinux CVMにアップロード](https://intl.cloud.tencent.com/document/product/213/2133)をご参照ください。
2. 次のコマンドを使用して、qpressバイナリーファイルを解凍します。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. qpressを使用してバックアップファイルを解凍します。
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>解凍時間に応じて、拡張子が`.sql.qp`のバックアップファイルを見つけ、そのファイル名を`cdb-jp0zua5k_backup_20191202182218`に置き換えてください。
>
解凍した結果は、次の図に示します。
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### ステップ4：バックアップファイルをターゲットデータベースにインポート
次のコマンドを実行して、sqlファイルをターゲットデータベースにインポートします。
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>
>- このドキュメントでは、ローカルの3306ポートにインポートされたMySQLを例として説明します。ユーザーが実際の状況に応じて置き換えることができます。
>- `cdb-jp0zua5k_backup_20191202182218.sql`を、qpressによって実際に解凍されたsqlファイルに置き換えます。
