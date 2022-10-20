## ユースケース
>ストレージ容量を節約するために、TencentDB for MySQLの物理バックアップファイル及び論理バックアップファイルは、qpressで圧縮してから、xbstreamでパッケージング（xbstreamはPerconaのパッケージング/アンパッケージングツール）されます。

TencentDB for MySQLは、[論理バックアップ](https://intl.cloud.tencent.com/document/product/236/37796)をサポートしています。ユーザはコンソールで手動でバックアップを実行し論理バックアップファイルを生成し、インスタンス全体または一部のデータベーステーブルの論理バックアップファイルをダウンロードすることができます。本書では、論理バックアップファイルを使用し手動で復元する方法を説明します。

- ここで紹介する復元方法はLinuxプラットフォームのみで使用でき、Windowsプラットフォームでは使用できません。
- Windowsでデータを復元する方法の詳細については、[コマンドラインツールによるデータの移行](https://intl.cloud.tencent.com/document/product/236/8464)をご参照ください。
- サポートするインスタンスのバージョン：MySQL 2ノードおよび3ノード。

## 操作手順
### 手順1：バックアップファイルをダウンロードします
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストのインスタンスIDまたは**操作**列の**管理**をクリックして、インスタンス管理ページに進みます。
2. インスタンス管理画面で、**バックアップ・復元**>**データバックアップリスト**のページを選択し、ダウンロードするバックアップを選択して、**操作**列の**ダウンロード**をクリックします。
3. ポップアップしたダイアログボックスでダウンロード先をコピーし、[クラウドデータベースが存在するVPC内のCVM (Linux OS)にログイン](https://intl.cloud.tencent.com/document/product/213/10517)し、wgetコマンドを実行して、プライベートネットワークから高速でダウンロードすることをお勧めします。
>?
>- **ローカルダウンロード**を選択して直接ダウンロードすることもできますが、時間がかかります。
>- wgetコマンドの形式：wget -c 'バックアップファイルのダウンロード先' -O カスタムファイル名.xb
>
例：
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### 手順2：バックアップファイルをアンパッケージングします
xbstreamを使用してバックアップファイルを解凍します。
>? xbstreamツールのダウンロード先については、[Percona XtraBackup公式サイト](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)をご参照ください。Percona XtraBackup 2.4.6以降のバージョンを使用してください。インストール方法については、[Percona XtraBackup 2.4](https://docs.percona.com/percona-xtrabackup/2.4/installation/yum_repo.html)をご参照ください。
>
```
xbstream -x < test0.xb
```
>?`test0.xb`がお客様のバックアップファイルに置き換えられます。
>
展開した結果は、次の図に示します。
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

### 手順3：バックアップファイルの解凍
1. 次のコマンドを実行し、qpressツールをダウンロードします。
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar
```
>?wgetダウンロード中にエラーが発生した場合、[qpressツールをダウンロード](https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar)をクリックしqpressツールをローカルにダウンロードした後、Linux CVMにアップロードしてください。詳しくは、[SCPでLinux CVMにファイルをアップロード](https://intl.cloud.tencent.com/document/product/213/2133)をご参照ください。
>
2. 次のコマンドを実行し、qpressバイナリーファイルを解凍します。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. qpressを使用してバックアップファイルを解凍します。
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>?解凍時間にもとづき、拡張子が`.sql.qp`のバックアップファイルを見つけ、そのファイル名で`cdb-jp0zua5k_backup_20191202182218`を置き換えてください。
>
解凍後は下図に示すようになります：
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### 手順4：バックアップファイルをターゲットデータベースにインポートします
次のコマンドを実行し、sqlファイルをターゲットデータベースにインポートします：
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>?
>- 本書では、ローカルの3306ポートにMySQLをインポートすることを例として説明します。必要に応じて置き換えてください。
>- `cdb-jp0zua5k_backup_20191202182218.sql`を、qpressを使用し解凍されたsqlファイルで置き換えます。

