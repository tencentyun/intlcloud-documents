## 概要

PostgreSQLは、拡張性と標準への準拠に焦点を重点に置いたオープンソースオブジェクトのリレーショナルデータベース管理システムです。PostgreSQLは、エンタープライズの複雑なSQL処理用のOLTPオンライントランザクション処理シナリオであり、NoSQLデータタイプ（JSON/XML/hstore）をサポートし、GIS（Geographic Information SystemまたはGeo－Information system）地理情報処理をサポートし、信頼性とデータ整合性の点で高い評判を得ています。インターネットのWebサイト、ロケーションアプリケーションシステム、複雑なデータオブジェクト処理などのアプリケーションシナリオに適しています。

このドキュメントでは、CentOS 7のCVMインスタンスでのPostgreSQLの構築方法について説明します。

## ソフトウェアのバージョン
このドキュメントで作成されたPostgreSQLの構成およびバージョンの使用方法は次のとおりです：
- Linux：Linux OSです。このドキュメントではCentOS 7.6を例として説明します。
- PostgreSQL：リレーショナルデータベース管理システムです。このドキュメントでは、PostgreSQL 9.6を例として説明します。


##  前提条件
- 2つのCVMインスタンスが作成されています（1つのCVMインスタンスがマスターノードとして機能し、もう1つのCVMインスタンスがスレーブノードとして機能します）。
- 具体的な手順については、[購入ページでのインスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
- 新しく作成された2つのCVMインスタンスは、セキュリティグループルールが構成されています。ポート5432がオープンされています。
具体的な手順については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。

## 操作手順

### マスターノードの設定

1. マスターノードインスタンスにログインします。
2. 次のコマンドを実行して、すべてのパッケージ、システムバージョン、カーネルをアップグレードします。
```
yum update -y
```
3. 次のコマンドを順番に実行して、PostgreSQLをインストールします。
このドキュメントでは、PostgreSQL 9.6バージョンを例として説明しますが、必要に応じてその他のバージョンを選択することもできます。
```
wget --no-check-certificate https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
```
rpm -ivh pgdg-redhat-repo-latest.noarch.rpm
```
```
yum install postgresql96-server postgresql96-contrib -y
```
```
/usr/pgsql-9.6/bin/postgresql96-setup initdb
```
4. 次のコマンドを実行して、サービスを起動します。
```
systemctl start postgresql-9.6.service
```
5. 次のコマンドを実行して、起動時に自動的にサービスを開始するように設定します。
```
systemctl enable postgresql-9.6.service 
```
6. 次のコマンドを実行して、postgresユーザーにログインします。
```
su - postgres
```
7. 次のコマンドを実行して、PostgreSQLインタラクティブ端末に入ります。
```
psql
```
8. 次のコマンドを実行して、ユーザーpostgresのパスワードを設定して、セキュリティを強化します。
```
ALTER USER postgres WITH PASSWORD '自定义密码';
```
9. 次のコマンドを実行して、データベースのアカウントを作成し、パスワード、ログイン権限、バックアップ権限を設定します。
```
create role アカウント名 login replication encrypted password 'カスタマイズパスワード';
```
このドキュメントでは、次のコマンドを実行して、データベースアカウント`replica`およびパスワード`123456`の作成を例として説明します。
```
create role replica login replication encrypted password '123456';
```
10. 次のコマンドを実行して、アカウントが正常に作成されたかどうかを確認します。
```
SELECT usename from pg_user;
```
次の結果が返された場合、正常に作成されたことを示します。
```
usename  
----------
postgres
replica
(2 rows)
```
11. 次のコマンドを実行して、権限が正常に作成されたかどうかを確認します。
```
SELECT rolname from pg_roles;
```
次の結果が返された場合、正常に作成されたことを示します。
```
rolname      
-------------------
pg_signal_backend
postgres
replica
(3 rows)
```
12. 「**\q**」を入力し、**Enter**を押して、SQL端末を終了します。
13. 「**exit**」を入力し、**Enter**を押して、PostgreSQLを終了します。
14. 次のコマンドを実行して、`pg_hba.conf`設定ファイルを開き、`replica`ユーザーホワイトリストを設定します。
```
vim /var/lib/pgsql/9.6/data/pg_hba.conf
```
15. **i**を押して編集モードに切り替え、`IPv4 local connections`セクションに次の2行を追加します：
```
host    all             all             <スレーブノードのVPC IPv4セグメント>          md5     #VPCセグメントでmd5パスワード認証接続を許可する
host    replication     replica         <スレーブノードのVPC IPv4セグメント>          md5     #ユーザーがreplicationデータベースによってデータを同期することを許可する
```
例えば、データベースアカウントが`replica`で、スレーブノードのVPC IPv4セクションが`xx.xx.xx.xx/16`である場合、`IPv4 local connections`セクションに次の内容を追加します。
```
host    all             all             xx.xx.xx.xx/16         md5
host    replication     replica         xx.xx.xx.xx/16         md5
```
16. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
17. 次のコマンドを実行して、`postgresql.conf`ファイルを開きます。
```
vim /var/lib/pgsql/9.6/data/postgresql.conf
```
18. **i**を押して編集モードに入り、次のパラメータをそれぞれ見つけて、パラメータを次のように変更します：
```
listen_addresses = '*'   #モニタリングされているプライベートネットワークIPアドレス
max_connections = 100    #接続の最大数です。スレーブデータベースのmax_connectionsはマスターデータベースより大きくする必要がある
wal_level = hot_standby  #ホットバックアップモードを有効にする
synchronous_commit = on  #同期レプリケーションを有効にする
max_wal_senders = 32     #同期プロセスの最大数
wal_sender_timeout = 60s #ストリーミングレプリケーションホストがデータを送信するためのタイムアウト時間
```
19. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
20. 次のコマンドを実行して、サービスを再起動します。
```
systemctl restart postgresql-9.6.service
```

### スレーブノードの設定

1. スレーブノードインスタンスにログインします。
2. 次のコマンドを実行して、すべてのパッケージ、システムバージョン、カーネルをアップグレードします。
```
yum update -y
```
3. 次のコマンドを順番に実行して、PostgreSQLをインストールします。
```
wget --no-check-certificate https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
```
rpm -ivh pgdg-redhat-repo-latest.noarch.rpm
```
```
yum install postgresql96-server postgresql96-contrib -y
```
4. 次のコマンドを実行して、pg_basebackupベースバックアップツールを使用して、バックアップディレクトリを生成します。
```
pg_basebackup -D /var/lib/pgsql/9.6/data -h <マスターノードのパブリックネットワークIP> -p 5432 -U replica -X stream -P
```
メッセージに従って、データベースアカウントに対応するパスワードを入力し、**Enter**を押します。次の結果が返された場合、正常にバックアップされたことを示します。
```
Password: 
24526/24526 kB (100%), 1/1 tablespace
```
5. 次のコマンドを実行して、master設定の関連ファイルをコピーします。
```
cp /usr/pgsql-9.6/share/recovery.conf.sample /var/lib/pgsql/9.6/data/recovery.conf
```
6. 次のコマンドを実行して、`recovery.conf`ファイルを開きます。
```
vim /var/lib/pgsql/9.6/data/recovery.conf
```
7. **i**を押して編集モードに切り替え、次のパラメータをそれぞれ見つけて、パラメータを次のように変更します：
```
standby_mode = on     #このノードをスレーブデータベースとして宣言する
primary_conninfo = 'host=<マスターノードのパブリックネットワークIP> port=5432 user=データベースのアカウント password=データベースのパスワード' #マスターデータベースの接続情報に対応する
recovery_target_timeline = 'latest' #ストリーミングレプリケーションは最新のデータに同期する
```
8. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
9. 次のコマンドを実行して、`postgresql.conf`ファイルを開きます。
```
vim /var/lib/pgsql/9.6/data/postgresql.conf
```
10. **i**を押して編集モードに切り替え、次のパラメータをそれぞれ見つけて、パラメータを次のように変更します：
```
max_connections = 1000             #接続の最大数です。スレーブデータベースのmax_connectionsはマスターデータベースより大きくする必要がある
hot_standby = on                   # ホットバックアップを有効にする
max_standby_streaming_delay = 30s  # ストリーミングバックアップの最大遅延
wal_receiver_status_interval = 1s  # スレーブノードがそのステータスをマスターノードに報告する最大間隔
hot_standby_feedback = on          # データのレプリケーションにエラーがある場合、マスターに報告する
```
11. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
12. 次のコマンドを実行して、データディレクトリのグループと所有者を変更します。
```
chown -R postgres.postgres /var/lib/pgsql/9.6/data
```
13. 次のコマンドを実行して、サービスを起動します。
```
systemctl start postgresql-9.6.service
```
14. 次のコマンドを実行して、起動時に自動的にサービスを開始するように設定します。
```
systemctl enable postgresql-9.6.service
```

### デプロイの検証
次の手順を実行して、正常にデプロイされたかどうかを確認できます：
1. 次のコマンドを実行して、ノードからディレクトリをバックアップします。
```
pg_basebackup -D /var/lib/pgsql/96/data -h <マスターノードのパブリックネットワークIP> -p 5432 -U replica -X stream -P
```
データベースのパスワードを入力し、**Enter**を押して、次の結果が返された場合は、正常にバックアップされたことを示します。
```
Password: 
24526/24526 kB (100%), 1/1 tablespace
```
2. マスターノードで、次のコマンドを実行して、senderプロセスを表示します。
```
ps aux |grep sender
```
![](https://qcloudimg.tencent-cloud.cn/raw/bc610cf837b18158a8d0ddd89d5d87ae.png)
3. スレーブノードで、次のコマンドを実行して、receiverプロセスを表示します。
```
ps aux |grep receiver
```
次の結果が返された場合は、receiverプロセスを正常に表示できることを示します。
![](https://qcloudimg.tencent-cloud.cn/raw/13c908ae7d83ff8d5099f2c488b40046.png)
4. マスターノードでは、次のコマンドを順番に実行して、PostgreSQLインタラクティブ端末に入り、マスターデータベースでスレーブデータベースのステータスを表示します。
```
su - postgres
```
```
psql
```
```
select * from pg_stat_replication;
```
次の結果が返された場合は、スレーブデータベースのステータスを正常に表示できることを示します。
![](https://qcloudimg.tencent-cloud.cn/raw/c38c6faf64af66188df0e944b335353a.png)

