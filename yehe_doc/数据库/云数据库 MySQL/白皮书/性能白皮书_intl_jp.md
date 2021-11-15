### テストツール
sysbench 0.5は、データベースのベンチマーク性能をテストするツールです。 

ツールの変更手順：
sysbenchに付属のotlpスクリプトが変更されました。読み取り／書き込み比率が1：1に変更され、テストコマンドパラメーターoltp_point_selectsおよびoltp_index_updatesによって制御されます。このドキュメントのテストケースでは、4つのselectポイントと1つのupdateポイントが読み取り／書き込み比率4：1で含まれています。

#### ツールのインストール
このドキュメントのテストではSysbenchバージョン0.5を使用します。インストール方法は次のとおりです。
```
git clone https://github.com/akopytov/sysbench.git
git checkout 0.5
yum -y install make automake libtool pkgconfig libaio-devel
yum -y install mariadb-devel
./autogen.sh
./configure
make -j
make install
```
>?上記のインストール手順は、CentOS CVMインスタンスでの性能負荷テストに適用されます。他のOSにインストールする必要がある場合は、[Sysbench公式ドキュメント](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS)をご参照ください。  

## テスト環境

|タイプ|説明|
|--|--|
|インスタンス物理マシン|２ノード-単一マシンが最大488GBのメモリと6TBのディスクを備えたデータベースインスタンスをサポート|
|インスタンス仕様|現在メインストリームの構成仕様を販売（詳細は下記を参照 [テストケース](#cscs)）|
|クライアント構成| 4コアCPUと8GBメモリ|
|クライアント数|1～6（構成を高度化する場合は、それに応じてクライアント数を増やす必要あり）|
|ネットワーク環境|10ギガビットネットワークコンピュータルーム、ネットワーク遅延＜0.05ms|
|環境負荷|MySQLがインストールされているマシンの負荷が70％を超えている（非排他的インスタンスの場合）|

- クライアント仕様の説明：単一クライアントでのテストによってデータベースインスタンスの性能負荷を測定できるように、マシンにはハイスペックなクライアントマシンが使用されます。ロースペッククライアントの場合は、同時インスタンス負荷テストに複数のクライアントを使用して、データの合計を求めることをお勧めします。
- ネットワークレイテンシーの説明：テスト環境は、クライアントのマシンとデータベースインスタンスが同じアベイラビリティーゾーンにあるようにし、テスト結果がネットワーク環境の影響を受けないようにします。

### テスト方法
### 1. データベーステーブル構造のテスト
```
CREATE TABLE `sbtest1` ( 
`id` int(10) unsigned NOT NULL AUTO_INCREMENT, 
`k` int(10) unsigned NOT NULL DEFAULT '0', 
`c` char(120) NOT NULL DEFAULT '', 
`pad` char(60) NOT NULL DEFAULT '',
 PRIMARY KEY (`id`), KEY `k_1` (`k`) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8；
```

### 2. データ行フォーマットのテスト
```
id: 1
k: 20106885
c: 08566691963-88624912351-16662227201-46648573979-64646226163-77505759394-75470094713-41097360717-15161106334-50535565977
pad: 63188288836-92351140030-06390587585-66802097351-4928296184
```

### 3.  データ準備
```
sysbench --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --mysql-table-engine=innodb --test=tests/db/oltp.lua --oltp_tables_count=20 --oltp-table-size=10000000  --rand-init=on prepare
```

データ準備パラメータの説明：
- `--test=tests/db/oltp.lua`は、tests/db/oltp.lua スクリプトを呼び出してoltpテストを行うことを示しています。
- `--oltp_tables_count=20`は、テストに使用されるテーブル数が20であることを示しています。
- `--oltp-table-size=10000000`は、各テストテーブルに入力されるデータが1,000万行であることを示しています。
- `--rand-init=on`は、各テストテーブルがランダムデータで入力されていることを示しています。
  

### 4. 性能負荷テストのコマンド
```
sysbench --mysql-host=xxxx --mysql-port=xxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua --oltp_tables_count=xx --oltp-table-size=xxxx --num-threads=xxx --oltp-read-only=off --rand-type=special --max-time=600 --max-requests=0 --percentile=99 --oltp-point-selects=4 run
```

性能負荷テストパラメータの説明：
- `--test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua`は、/root/sysbench_for_z3/sysbench/tests/db/oltp.lua スクリプトを呼び出してoltpテストを行うことを示しています。
- `--oltp_tables_count=20`は、今回のテストに使用されるテーブルの数が20であることを示しています。
- `--oltp-table-size=10000000` は、今回のテストテーブルに入力されるデータが1,000万行であることを示しています。
- `--num-threads=128`は、今回のテストのクライアントの並列接続数が28であることを示しています。
- `--oltp-read-only=off`は、読み取り専用テストモデルが無効になり、読み取り／書き込みの混合モデルが使用されることを示しています。
- `--rand-type=special` は、ランダムモデルが特定であることを示しています。
- `--max-time=1800`は、今回のテストの実行時間を示しています。
- `--max-requests=0`は、総リクエスト数を制限せず、max-time によってテストされることを示しています。
- `--percentile=99`は、サンプリング率を設定することを示しています。デフォルトは95%です。ここでは、長いリクエストの1%が破棄され、残りの99%から最大値が求められることを意味します。
- `--oltp-point-selects=4`は、oltpスクリプトのsqlテストコマンドで、selectオペレーションの回数は4であること示しています。デフォルト値は1です。

### 5. シナリオモデル
このドキュメントでは、sysbenchのluaスクリプトを使用し、4つのselectポイントのクエリ、1つのupdate（インデックス列）に変更され、読み取り／書き込み比率は4：1です。
最大構成タイプの場合、データシナリオにパラメータチューニングモデルが追加されます。テスト結果は、次の[テスト結果](#document_test_result)をご参照ください。


<span id="cscs"></span>
### テストパラメータ

|インスタンス仕様|ストレージ容量|テーブル数|テーブル行数|データセットサイズ|並列数|実行時間（分）|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1コア1GB|200GB| 4|2000万|19GB|128|30|
|1コア2GB|200GB| 4 | 4000万| 38GB|128|30|
|2コア4GB|200GB|8|4000万|76GB|128|30|
|4コア8GB|200GB|15|4000万|142GB|128|30|
|4コア16GB|400GB|25|4000万|238GB|128|30|
|8コア32GB|700GB|25|4000万|238GB|128|30|
|16コア64GB|1TB|40|4000万|378GB|256|30|
|16コア96GB|1.5TB|40|4000万|378GB|128|30|
|16コア128GB|2TB|40|4000万|378GB|128|30|
|24コア244GB|3TB|60|4000万|567GB|128|30|
|48コア488GB|6TB|60|4000万|567GB|128|30|
|48コア488GB（最適化）|6TB|60|1000万|140GB|128|30|

<span id="document_test_result"></span>
## テスト結果

|インスタンス仕様|ストレージ容量|データセット|クライアント数|単一クライアント並列数|QPS|TPS|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1コア1GB|200GB|19GB|1|128|1757|97|
|1コア2GB|200GB| 38GB|1|128|3016|167|
|1コア2GB|200GB| 38GB|1|128|3016|167|
|4コア8GB|200GB|142GB|1|128|6551|1310|
|4コア16GB|400GB|238GB|1|128|11098|2219|
|8コア32GB|700GB|238GB|2|128|20484|3768|
|16コア64GB|1TB|378GB|2|128|36395|7279|
|16コア96GB|1.5TB|378GB|3|128|56464|11292|
|16コア128GB|2TB|378GB|3|128|81752|16350|
|24コア244GB|3TB|567GB|4|128|98528|19705|
|48コア488GB|6TB|567GB|6|128|142246|28449|
|48コア488GB（最適化）|6TB|140GB|6|128|245509|46304|
