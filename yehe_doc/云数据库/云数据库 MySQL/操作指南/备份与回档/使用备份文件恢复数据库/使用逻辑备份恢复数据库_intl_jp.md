## 操作シナリオ
>ストレージ容量を節約するために、TencentDB for MySQLの物理バックアップファイル及び論理バックアップファイルは、まずqpressで圧縮し、次にxbstreamでパッケージング（xbstreamはPerconaのパッケージング/アンパッケージングツール）して圧縮とパッケージングを実行します。

TencentDB for MySQLは、[論理バックアップ](https://intl.cloud.tencent.com/document/product/236/37796) 方式をサポートしています。ユーザーはコンソールから手動でバックアップを行って論理バックアップファイルを生成し、全インスタンスまたは一部のデータベーステーブルの論理バックアップファイルをダウンロードすることができます。このドキュメントでは論理バックアップファイルを使用した手動による復元についてご紹介します。

- ここで紹介する復旧方法はLinuxプラットフォームにのみに適用されます。現在Windowsプラットフォームをサポートしていません。
- Windowsプラットフォームでデータを復元する方法の詳細については、[コマンドラインツールによるデータの移行](https://intl.cloud.tencent.com/document/product/236/8464)をご参照ください。
- サポートするインスタンスのバージョン：MySQL 2ノードおよび3ノード。

## 操作手順
### 手順1：バックアップファイルのダウンロード
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストのインスタンス名または「操作」の列の【管理】をクリックし、インスタンス管理画面に入ります。
2. インスタンス管理画面で、【バックアップの復旧】>【データバックアップリスト】のページを選択し、ダウンロードしたいバックアップを選択して、「操作」列の【ダウンロード】をクリックします。
3. ポップアップダイアログボックスで、ダウンロードアドレスをコピーして、[クラウドデータベースが存在するVPC下のCVM（Linuxシステム）にログイン](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)し、wgetコマンドを実行して、より効率的なイントラネットの高速ダウンロードを行うことをお勧めします。
>?
>- 【ローカルダウンロード】を選択して直接ダウンロードすることもできますが、時間がかかります。
>- wgetコマンド形式：wget -c 'バックアップファイルのダウンロードアドレス' -O カスタムファイル名.xb
>
例：
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### 手順2：バックアップファイルのアンパッケージング
xbstreamを使用してバックアップファイルを解凍します。
>? xbstream ツールのダウンロードアドレスについては、 [Percona XtraBackup公式サイト](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)を参照し、Percona XtraBackup 2.4.6 およびそれ以上のバージョンを選択してください。インストール方法の紹介は、 [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)をご参照ください。
```
xbstream -x < test0.xb
```
>?`test0.xb`をバックアップファイルに置き換えます。
>
展開した結果は、次のように示されます。
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

### 手順3：バックアップファイルの解凍
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
3. qpressを使用してバックアップファイルを解凍します。
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>?解凍時間にもとづき、拡張子が`.sql.qp`のバックアップファイルを見つけ、そのファイル名を`cdb-jp0zua5k_backup_20191202182218`に置き換えてください。
>
解凍した結果は、次のように示されます。
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### 手順4：バックアップファイルをターゲットデータベースにインポート
次のコマンドを実行して、sqlファイルをターゲットデータベースにインポートします。
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>?
>- このドキュメントでは、ローカルの3306ポートにインポートされたMySQLを例として説明します。ユーザーが実際の状況に応じて置き換えることができます。
>- `cdb-jp0zua5k_backup_20191202182218.sql`を、qpressによって実際に解凍されたsqlファイルに置き換えます。
