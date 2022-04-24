このドキュメントでは、MySQL性能テストツールSysBenchと、Cloud Virtual Machine（CVM）インスタンスでのSysBenchのインストール方法をご説明します。

## SysBench ツールの説明
SysBenchはプラットフォームを超えて使用可能かつマルチスレッドをサポートしているモジュール化基準テストツールです。ハイロードのデータベースを実行する際におけるシステムの関連パラメータをテストするために使用されます。複雑なデータベース基準設定やデータベースのインストールをせずに、データベースシステムの性能を迅速に把握することが可能です。

## SysBenchテストモデル
 - SysBenchの標準OLTPでは、読み取りと書き込みのケースにおいて、1つのトランザクションに18個の読み取り/書き込みSQLが含まれます。
 - SysBenchの標準OLTPでは、読み取りのみのケースにおいて、1つのトランザクションに14個の読み取りSQLが含まれます（主キーポイントクエリー10件、範囲クエリ4件）。
 - SysBenchの標準OLTPでは、書き込みのみのケースにおいて、1つのトランザクションに4個の書き込みSQLが含まれます（UPDATE 2件、DETELE 1件、INSERT 1件）。

## SysBenchパラメータ説明
| パラメータ     | 説明 | 
|---------|---------|
| db-driver | データベースエンジン  | 
| mysql-host | MySQLインスタンス接続アドレス  |
| mysql-port | MySQLインスタンス接続ポート  |
| mysql-user | MySQLインスタンスアカウント  |
| mysql-password | MySQLインスタンスアカウントに対応するパスワード  |
| mysql-db | 	MySQLインスタンスデータベース名 |
| table_size| テストテーブルサイズ  |
|tables | テストテーブル数 |
| events | テストリクエスト数 |
| time | テスト時間 |
| threads | テストスレッド数 |
| percentile | カウントされるパーセンタイル。デフォルト値は95%、すなわち95%の状況におけるリクエストの実行時間 |
| report-interval | テスト進捗レポートを出力する間隔秒数Nを表す。0はテスト進捗レポートの出力を終了し、最終的なレポート結果のみを出力することを表す |
| skip-trx | トランザクションをスキップしますか。<br>1：はい<br>0：いいえ |

## インストール方法
負荷テストではSysBench 1.0.20を使用します。詳細については、[Sysbench 公式ドキュメント](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS)をご参照ください。
1. CVMインスタンスでは、次のコマンドを実行してSysBenchをインストールしてください。
```
yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql
git clone https://github.com/akopytov/sysbench.git
## GitからSysBenchをダウンロードする
cd sysbench
## SysBenchディレクトリを開く
git checkout 1.0.20
## SysBench 1.0.20に切り替える
./autogen.sh
## autogen.shを実行する
./configure --prefix=/usr --mandir=/usr/share/man
make
##コンパイル
make install
```
2．次のコマンドを実行してクライアントを構成してください。この操作により、カーネルがすべてのCPUでデータパケットを処理すると同時に、各CPU間のコンテキスト切り替えを減少できます。
```
sudo sh -c 'for x in /sys/class/net/eth0/queues/rx-*; do echo ffffffff>$x/rps_cpus; done'
sudo sh -c "echo 32768 > /proc/sys/net/core/rps_sock_flow_entries"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt"
sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-1/rps_flow_cnt"
```
>?ffffffffは32個のCPU使用を表す（1つのfは、4つのCPUを表す）。

