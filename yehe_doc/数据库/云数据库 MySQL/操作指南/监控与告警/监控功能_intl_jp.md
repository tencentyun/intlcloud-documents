ユーザーがインスタンスの動作情報を確認、理解しやすいように、TencentDB for MySQLは豊富なパフォーマンス監視機能項目と便利な監視機能（カスタマイズしたビュー、タイムコントラスト、監視項目の統合など）を提供しています。ユーザーは[TencentDB for MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス管理ページの**インスタンス監視**に入って確認します。
>?
>- Basic Cloud Monitor APIの[指標のモニタリングデータのプル](https://intl.cloud.tencent.com/document/product/248/33881)、[TencentDB for MySQLの監視指標](https://intl.cloud.tencent.com/document/product/248/11006)  によって、インスタンスの監視指標を取得します。
>- また、監視指標のために [Dashboardを作成](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10)して、指標のモニタリングデータも動的に解析できます。
- 単一インスタンスのテーブル数が100万を超えた場合は、データベースの監視に影響する恐れがあるため、単一インスタンスのテーブル数が100万を超えないようにテーブルの数を適切に管理してください。

## 監視をサポートするインスタンスタイプ
TencentDB for MySQLは、マスターインスタンス、読み取り専用インスタンス、ディザスタリカバリインスタンスおよびデータベースプロキシノードの監視をサポートし、各インスタンスのために独立した監視ビューを提供してクエリします。

## 監視タイプ
TencentDB for MySQLには、リソース監視、エンジン監視（通常）、エンジン監視（拡張）、デプロイ監視の4種類の監視タイプがあり、様々な監視タイプの指標を確認することで、インスタンスのパフォーマンスおよび作動状況を迅速かつ正確に理解できます。
>?TencentDB for MySQL単一ノードのクラウドディスクインスタンスでサポートされる監視の種類には、リソース監視とエンジン監視（共通）が含まれますが、エンジン監視（拡張）とデプロイ監視は現在サポートされていません。
>
- **リソース監視**：CPU、メモリ、ディスク、ネットワーク関連の監視データを提供します。
- **エンジン監視（通常）**：接続数、ロック情報、ホットスポットテーブル、スロークエリーなど関連する監視データを提供し、障害の診断やパフォーマンスの最適化を行いやすくします。
- **エンジン監視（拡張）**：さらに豊富なエンジン関連の監視指標を提供し、データベースの健全性に関する既存または潜在的な問題を最大限発見します。
- **デプロイ監視**：マスターマシンとスレーブマシンの遅延関連の監視指標を提供します。デプロイ監視はマスターマシンと待機マシンに分かれます。
 - インスタンスがマスターインスタンスの場合、インスタンスデプロイ監視の対象は、マスターインスタンスとその非表示スレーブインスタンスの間のリンクです。デプロイ監視は非表示スレーブインスタンスの IO、SQL スレッド状態を表示します。マスター/スレーブ遅延距離とマスター/スレーブ遅延時間は、マスターインスタンスとその非表示スレーブインスタンスの間のことを指します。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5LFE331_11.png)
 - インスタンスが読み取り専用インスタンスの場合、インスタンスデプロイ監視の対象は、マスターインスタンスと読み取り専用インスタンスの間のリンクです。デプロイ監視は読み取り専用インスタンスの IO、SQL スレッド状態を表示します。マスター/スレーブ遅延距離とマスター/スレーブ遅延時間は、読み取り専用インスタンスとマスターインスタンスの間のことを指します。
 - インスタンスがディザスタリカバリインスタンスの場合：
 a. ディザスタリカバリインスタンスデプロイ監視（マスター）の対象は、ディザスタリカバリインスタンスとマスターインスタンスの間のリンクです。デプロイ監視はディザスタリカバリインスタンスの IO、SQL スレッド状態を表示します。マスター/スレーブ遅延距離とマスター/スレーブ遅延時間は、ディザスタリカバリインスタンスとマスターインスタンスの間のことを指します。
    b. ディザスタリカバリインスタンスデプロイ監視（スレーブ）の対象は、ディザスタリカバリインスタンスとその非表示スレーブインスタンスの間のリンクです。デプロイ監視はディザスタリカバリインスタンスの IO、SQL スレッド状態を表示します。マスター/スレーブ遅延距離とマスター/スレーブ遅延時間は、ディザスタリカバリインスタンスとその非表示スレーブインスタンスの間のことを指します。

## 監視粒度
2018年08月11日から、TencentDB for MySQLの監視粒度は適応型ポリシーを実行しており、監視粒度のカスタマイズ選択はサポートしていません。監視粒度の適応型ポリシーは次のとおりです：

| タイムスパン | 監視粒度 | 適応型説明 | 保持時間 |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5s | タイムスパンは4時間以内、監視粒度は5秒 | 1日 |
| (4h, 2d] | 1min | タイムスパンが4時間を超え、2日以内の場合、監視粒度は1分に調整 | 15日 |
| (2d, 10d] | 5min | タイムスパンが2日を超え、10日以内の場合、監視粒度は5分に調整 | 31日 |
| (10d, 30d] | 1h | タイムスパンが10日を超え、30日以内の場合、監視粒度は1時間に調整 | 62日 |

>?現在のTencentDB for MySQLは最大で30日以内の監視データの確認に対応します。

## 監視指標
Tencent CloudのBasic Cloud Monitorは、インスタンスの面からTencentDB for MySQLのために次の監視指標を提供します。

>?MySQLの監視指標の使用方法の詳細については、Basic Cloud Monitor APIの[TencentDB for MySQLインターフェース](https://www.tencentcloud.com/document/product/248/48735)をご参照ください。

| 指標の中国語名 | 指標の英語名 | 単位 |指標の説明|
|---------|---------|---------|---------|
| 毎秒実行操作数 | qps | 回/秒 | データベースが毎秒実行するSQL数（insert、select、update、delete、replaceなど）、QPS指標はTencentDBインスタンスの実際の処理能力を主に表します |
| 毎秒実行するトランザクション数 | tps | 回/秒| データベースが毎秒伝送するトランザクション処理数 |
| スロークエリ数          |slow_queries | 回 | クエリ時間がlong_query_time秒を超えたクエリ回数 |
| 全テーブルのスキャン数       |select_scan | 回/秒 | 全テーブルの検索クエリ実行数 |
| クエリ数             | select_count | 回/秒 | 1秒あたりのクエリ数 |
| 更新数             | com_update | 回/秒 | 1秒あたりの更新数 |
| 削除数             | com_delete | 回/秒 | 1秒あたりの削除数 |
| 挿入数             | com_insert | 回/秒 | 1秒あたりの挿入数 |
| 上書き数             | om_replace | 回/秒 | 1秒あたりの上書き数 |
| 合計リクエスト数          | queries | 回/秒 | 実行するすべてのSQLステートメント。set、showなどを含む |
| 現在のオープン接続数 | threads_connected | 個  | 現在のオープン接続数 |
| 接続数利用率    | connection_use_rate | %  | 現在のオープン接続数/最大接続数   |
| クエリ使用率       | query_rate                | %  | 1秒あたりの実行オペランドQPS/推奨する1秒あたりのオペランド |
| ディスク総使用キャパシティ | capacity         | MB | MySQLデータディレクトリとbinlog、relaylog、undolog、errorlog、slowlogログキャパシティを含む |
| データ使用キャパシティ    | real_capacity | MB | MySQLデータディレクトリのみ含む。binlog、relaylog、undolog、errorlog、slowlogログキャパシティは含まない |
| ログ使用キャパシティ    | log_capacity  | MB   | binlog、relaylog、undolog、errorlog、slowlogログキャパシティのみを含む |
| ログファイル使用キャパシティ |  disk_log_used  | MB | MySQL binlog、relaylog、undologログキャパシティのみ含む |
| 一時ファイル使用キャパシティ | disk_tmp_used | MB | MySQL作動時に生成する一時ファイルのみ含む |
| ディスク利用率      | volume_rate     | %         | ディスク総使用キャパシティ/インスタンス購入キャパシティ         |
| プライベートネットワークアウトバウンドトラフィック      | bytes_sent       | Byte/秒 | 1秒あたりに送信するバイト数  |
| プライベートネットワークインバウンドトラフィック      | bytes_received | Byte/秒 | 1秒あたりに受信するバイト数  |
| クエリキャッシュヒット率 | qcache_hit_rate         | %     | クエリキャッシュヒット率 |
| クエリキャッシュ使用率 | qcache_use_rate       | %     | クエリキャッシュ使用率 |
| テーブルロック待機回数    | table_locks_waited | 回/秒 | 速やかに取得できないテーブルロック回数 |
| 一時テーブル数       | created_tmp_tables   | 回/秒 | 一時テーブル作成数 |
| innodbキャッシュヒット率  | innodb_cache_hit_rate  | %     | Innodbエンジンのキャッシュヒット率 |
| innodbキャッシュ使用率  | innodb_cache_use_rate | %     | Innodbエンジンのキャッシュ使用率 |
| innodbディスク読み取り数  | innodb_os_file_reads    | 回/秒 | Innodbエンジンの1秒あたりのディスクファイル読み取り回数 |
| innodbディスク書き込み数  | innodb_os_file_writes   | 回/秒 | Innodbエンジンの1秒あたりのディスクファイル書き込み数 |
| innodb fsync数量  | innodb_os_fsyncs         | 回/秒 | Innodbエンジンの毎秒fsync関数の呼び出し回数 |
| Innodb用に現在開いているテーブル数量 | innodb_num_open_files  | 個 | Innodbエンジン用に現在開いているテーブルの数量| 
| myisamキャッシュヒット率  | key_cache_hit_rate  | %   | myisamエンジンのキャッシュヒット率 |
| myisamキャッシュ使用率  | key_cache_use_rate | %   | myisamエンジンのキャッシュ使用率 |
| CPU使用率             | cpu_use_rate           | %   | アイドルタイムの超過を許可。CPU使用率が100%より大きいことがある |
| メモリ使用率               | memory use rate     | %   | アイドルタイムの超過を許可。メモリ使用率が100%より大きいことがある  |
| メモリ使用量                  | memory_use       | MB | アイドルタイムの超過を許可。実際のメモリ使用量が購入仕様より大きいことがある |
| 一時ファイル数            | created_tmp_tables   | 回/秒 | 1秒あたりに一時ファイルを作成する回数 |
| 開いているテーブル数         | opened_tables     | 個      | インスタンスのディメンション|開いているテーブル数 |
| 提出数                     | com_commit            | 回/秒 | 1秒あたりの提出回数 |
| ロールバック数                     | com_rollback           | 回/秒 | 1秒あたりのロールバック回数 |
| 作成済みのスレッド数         | threads_created      | 個 | 接続処理用に作成したスレッド数 |
| 実行中のスレッド数            | threads_running      | 個 | アクティブの（スリープ状態ではない）スレッド数 |
| 最大接続数               | max_connections     | 個 | 最大接続数 |
| ディスクの一時テーブル数         | created_tmp_disk_tables | 回/秒 | 1秒あたりにディスクの一時テーブルを作成する回数 |
| 次の行の読み取りリクエスト数         | handler_read_rnd_next    | 回/秒    | 1秒あたりの次の行の読み取りリクエスト回数 |
| 内部ロールバック数               | handler_rollback    | 回/秒| 1秒あたりにトランザクションがロールバックされる回数 |
| 内部提出数               | handler_commit     | 回/秒 | 1秒あたりにトランザクションが提出される回数 |
| InnoDBブランクページ数         | innodb_buffer_pool_pages_free  | 個  | Innodbエンジンメモリブランクページ数  |
| InnoDB総ページ数         | innodb_buffer_pool_pages_total  | 個  | Innodbエンジンのメモリ占用総ページ数  |
| InnoDBロジック読み取り        | innodb_buffer_pool_read_requests  | 回/秒  | Innodbエンジンが1秒あたりに完了したロジック読み取りリクエスト回数  |
| InnoDB物理的読み取り         | innodb_buffer_pool_reads  | 回/秒  |Innodbエンジンが1秒あたりに完了した物理的読み取りリクエスト回数  |
| InnoDB読み取り量         | innodb_data_read        | Byte/秒  | Innodbエンジンが1秒あたりに完了した読み取りデータバイト数  |
| InnoDB合計読み取り量      | innodb_data_reads      | 回/秒      | Innodbエンジンが1秒あたりに完了したデータ読み取り回数  |
| InnoDB合計書き込み量      | innodb_data_writes     | 回/秒       | Innodbエンジンが1秒あたりに完了したデータ書き込み回数  |
| InnoDB書き込み量         | innodb_data_written    | Byte/秒   | Innodbエンジンが1秒あたりに完了したデータ書き込みバイト数  |
| InnoDB行削除量      | innodb_rows_deleted   | 回/秒  | Innodbエンジンが1秒あたりに削除した行数  |
| InnoDB行挿入量      | innodb_rows_inserted  | 回/秒  | Innodbエンジンが1秒あたりに挿入した行数  |
| InnoDB行更新量      | innodb_rows_updated  | 回/秒  | Innodbエンジンが1秒あたりに更新した行数  |
| InnoDB行読み取り量      | innodb_rows_read       | 回/秒  | Innodbエンジンが1秒あたりに読み取った行数  |
| InnoDBが取得する行の平均ロック時間 | innodb_row_lock_time_avg  | ミリ秒  | Innodbエンジンが行をロックする平均時間  |
| InnoDB行ロック待機回数       | innodb_row_lock_waits        | 回/秒 | Innodbエンジンの1秒あたりの行ロック待機回数  |
| キーキャッシュ内で未使用のブロック数   | key_blocks_unused              | 個     | myisamエンジンが未使用のキーキャッシュブロック数  |
| キーキャッシュ内で使用したブロック数      | key_blocks_used                  | 個     | myisamエンジンが使用済みのキーキャッシュブロック数  |
| キーキャッシュ読み取りデータブロック数      |key_read_requests   | key_read_requests   | 回/秒 | myisamエンジンの1秒あたりのキーキャッシュブロック読み取り回数  |
| ハードディスク読み取りデータブロック数         | key_reads                | 回/秒 | myisamエンジンの1秒あたりのハードディスク読み取りデータブロック回数|
| データブロックキーバッファ書き込み数      | key_write_requests   | 回/秒 | myisamエンジンの1秒あたりのキーキャッシュブロック書き込み回数|
| データブロックディスク書き込み数         | key_writes                | 回/秒 | myisamエンジンの1秒あたりのハードディスクデータブロック書き込み回数|
| マスター・スレーブ遅延距離     | master_slave_sync_distance  | MB | マスターマシンとスレーブマシンbinlogの距離  |
| マスター・スレーブ遅延時間     | seconds_behind_master        | 秒   | マスターマシンとスレーブマシンの遅延時間  |
| IOスレッド状態       |	slave_io_running  |	状態値（0-Yes，1-No，2-Connecting）| IOスレッド実行状態     |
| SQLスレッド状態    |	slave_sql_running  |	状態値（0-Yes，1-No）                      | スレッド実行状態  |
