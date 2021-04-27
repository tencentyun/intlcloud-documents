ユーザーがインスタンスの動作情報を確認、理解しやすいように、TencentDB for MySQLは豊富なパフォーマンス監視機能項目と便利な監視機能（カスタマイズしたビュー、タイムコントラスト、監視項目の統合など）を提供しています。ユーザーは [TencentDB for MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス管理ページの【インスタンス監視】に入って確認します。
>?
>- Basic Cloud Monitor APIの[指標のモニタリングデータのプル](https://intl.cloud.tencent.com/document/product/248/39306)、[TencentDB for MySQLの監視指標](https://intl.cloud.tencent.com/zh/document/product/248/11006)  によって、インスタンスの監視指標を取得します。
>- また、監視指標のために [Dashboardを作成](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10)して、指標のモニタリングデータも動的に解析できます。
- 単一インスタンスのテーブル数が100万を超えた場合は、データベースの監視に影響する恐れがあるため、単一インスタンスのテーブル数が100万を超えないようにテーブルの数を適切に管理してください。

## 監視をサポートするインスタンスタイプ
TencentDB for MySQLは、マスターインスタンス、読み取り専用インスタンス、ディザスタリカバリインスタンスの監視をサポートし、各インスタンスのために独立した監視ビューを提供してクエリーします。

## 監視タイプ
TencentDB for MySQLには、リソース監視、エンジン監視（通常）、エンジン監視（拡張）、デプロイ監視の4種類の監視タイプがあり、様々な監視タイプの指標を確認することで、インスタンスのパフォーマンスおよび作動状況を迅速かつ正確に理解できます。
- **リソース監視**：CPU、メモリ、ディスク、ネットワーク関連の監視データを提供します。
- **エンジン監視（通常）**：接続数、ロック情報、ホットスポットテーブル、スロークエリーなど関連する監視データを提供し、障害の診断やパフォーマンスの最適化を行いやすくします。
- **エンジン監視（拡張）**：さらに豊富なエンジン関連の監視指標を提供し、データベースの健全性に関する既存または潜在的な問題を最大限発見します。
- **デプロイ監視**：マスターマシンとスレーブマシンの遅延関連の監視指標を提供します。デプロイ監視はマスターマシンと待機マシンに分かれます。
 - マスターマシンのデプロイ監視：監視インスタンスがマスターインスタンスのとき、マスターインスタンスはどのインスタンスのスレーブにもならないため、そのマスターマシンでのレプリケーション関連の監視データは無効となり、この時のIOスレッドとSQLスレッドは起動状態にはなりません。監視インスタンスがディザスタリカバリインスタンスか読み取り専用インスタンスのときのみ、関連するレプリケーション関連の監視データは有効になり、IOスレッド、SQLスレッドは起動状態になります。

 - 待機マシンのデプロイ監視：2ノード、3ノードのマスターインスタンスとディザスタリカバリインスタンスは、デフォルトではマスター／スレーブアーキテクチャです。従って、監視インスタンスがマスターインスタンスかディザスタリカバリインスタンスである場合でのみ、スレーブでのレプリケーション関連の監視データは有効になります。マスターインスタンス、ディザスタリカバリインスタンスと非表示のスレーブノードとの間の距離遅延と時間を反映するのに用いられるので、スレーブに関連する監視データにご注意ください。マスターインスタンスやディザスタリカバリインスタンスに障害が発生した場合、監視インスタンス対象の非表示スレーブノードは速やかにマスターインスタンスにアップグレードできます。

![](https://main.qcloudimg.com/raw/183cebeb93cdeaca2dedeb228ab8f0be.png)

## 監視粒度
2018年08月11日から、TencentDB for MySQLの監視粒度は適応型ポリシーを実行しており、監視粒度のカスタマイズ選択はサポートしていません。監視粒度の適応型ポリシーは次のとおりです。

| タイムスパン | 監視粒度 | 適応型説明 | 保持時間 |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5s | タイムスパンは4時間以内、監視粒度は5秒 | 1日 |
| (4h, 2d] | 1min | タイムスパンが4時間よりも長く2日以内の場合、監視粒度は1分に調整 | 15日 |
| (2d, 10d] | 5min | タイムスパンが2日よりも長く10日以内の場合、監視粒度は5分に調整 | 31日 |
| (10d, 30d] | 1h | タイムスパンが10日よりも長く30日以内の場合、監視粒度は1時間に調整 | 62日 |

>?現在のTencentDB for MySQLは最大で30日以内の監視データの確認に対応します。

## 監視指標
Tencent CloudのBasic Cloud Monitorは、インスタンスの面からTencentDB for MySQLのために次の監視指標を提供します。

>?クラウドデータベースの監視指標に係る使用方法の詳細は、Basic Cloud Monitor APIの [TencentDB for MySQLインターフェース](https://intl.cloud.tencent.com/zh/document/product/248/11006)をご参照ください。

| 指標の中国語名 | 指標の英語名 | 単位 |指標の説明|
|---------|---------|---------|---------|
| 毎秒実行操作数 | qps | 回/秒 | データベースが毎秒実行するSQL数（insert、select、update、delete、replaceなど）、QPS指標はTencentDBインスタンスの実際の処理能力を主に表します |
| 毎秒実行するトランザクション数 | tps | 回/秒| データベースが毎秒伝送するトランザクション処理数 |
| スロークエリー数 |slow_queries | 回 | クエリー時間がlong_query_time秒を超えたクエリー回数 |
| 全テーブルのスキャン数 |select_scan | 回/秒 | 全テーブルの検索クエリー実行数 |
| クエリー数 | select_count | 回/秒 | 毎秒のクエリー数 |
| 更新数 | com_update | 回/秒 | 毎秒の更新数 |
| 削除数 | com_delete | 回/秒 | 毎秒の削除数 |
| 挿入数 | com_insert | 回/秒 | 毎秒の挿入数 |
| 上書き数 | com_replace | 回/秒 | 毎秒の上書き数 |
| 合計リクエスト数 | queries | 回/秒 | 実行するすべてのSQLステートメント。set、showなどを含む |
| 現在のオープン接続数 | threads_connected | 個 | 現在のオープン接続数 |
| 接続数利用率 | connection_use_rate | % | 現在のオープン接続数/最大接続数   |
| クエリー使用率 | query_rate | % | 毎秒の実行操作数QPS/推奨する毎秒操作数 |
| ディスク総使用キャパシティ | capacity | MB | MySQLデータディレクトリとbinlog、relaylog、undolog、errorlog、slowlogログキャパシティを含む |
| データファイル使用キャパシティ | real_capacity | MB | MySQLデータディレクトリのみ含む。binlog、relaylog、undolog、errorlog、slowlogログキャパシティは含まない |
| ログファイル使用キャパシティ |  disk_log_used  | MB | MySQL binlog、relaylog、undolog、errorlog、slowlogログキャパシティのみ含む |
| 一時ファイル使用キャパシティ | disk_tmp_used | MB | MySQL作動時に生成する一時ファイルのみ含む |
| プライベートネットワークアウトバウンドトラフィック | bytes_sent       | Byte/秒 | 毎秒送信するバイト数 |
| プライベートネットワークインバウンドトラフィック | bytes_received | Byte/秒 | 毎秒受信するバイト数 |
| ディスク利用率 | volume_rate     | % | ディスク総使用キャパシティ/インスタンス購入キャパシティ |
| クエリーキャッシュヒット率 | qcache_hit_rate  | % | クエリーキャッシュヒット率 |
| クエリーキャッシュ使用率 | qcache_use_rate | % | クエリーキャッシュ使用率 |
| テーブルロック待機回数 | table_locks_waited | 回/秒 | 速やかに取得できないテーブルロック回数 |
| 一時テーブル数 | created_tmp_tables   | 回/秒 | 一時テーブル作成数 |
| innodbキャッシュヒット率 | innodb_cache_hit_rate  | % | Innodbエンジンのキャッシュヒット率 |
| innodbキャッシュ使用率 | innodb_cache_use_rate | % | Innodbエンジンキャッシュ使用率 |
| innodbディスク読み取り数 | innodb_os_file_reads    | 回/秒 | Innodb エンジンの毎秒ディスクファイル読み取り数 |
| innodbディスク書き込み数 | innodb_os_file_writes   | 回/秒 | Innodbエンジンの毎秒ディスクファイル書き込み数 |
| innodb fsync数量  | innodb_os_fsyncs         | 回/秒 | Innodbエンジンの毎秒fsync関数の呼び出し回数 |
| Innodb用に現在開いているテーブル数量 | innodb_num_open_files  | 個 | Innodbエンジン用に現在開いているテーブルの数量|
| myisamキャッシュヒット率 | key_cache_hit_rate  | % | myisamエンジンのキャッシュヒット率 |
| myisamキャッシュ使用率 | key_cache_use_rate | % | myisamエンジンのキャッシュ使用率 |
| CPU使用率 | cpu_use_rate     | % | アイドルタイムの超過を許可。CPU使用率が100%より大きいことがある |
|メモリ使用率   |memory use rate| % | アイドルタイムの超過を許可。メモリ使用率が100%より大きいことがある  |
| メモリ使用量     |memory_use       | MB | アイドルタイムの超過を許可。実際のメモリ使用量が購入仕様より大きいことがある |
| 一時ファイル数 | created_tmp_tables   | 回/秒 | 毎秒の一時ファイル作成数 |
| 開いているテーブル数 | opened_tables     | 個      | インスタンスのディメンション|
| 提出数 | com_commit  | 回/秒 | 毎秒の提出数 |
| ロールバック数 | com_rollback | 回/秒 | 毎秒のロールバック数 |
| 作成済みのスレッド数 | threads_created  | 個 | 接続処理用に作成したスレッド数 |
| 実行中のスレッド数    | threads_running  | 個 | アクティブの（スリープ状態ではない）スレッド数 |
| 最大接続数       | max_connections | 個 | 最大接続数 |
| ディスクの一時テーブル数 | created_tmp_disk_tables | 回/秒 | 毎秒のディスクの一時テーブル作成数 |
| 次の行の読み取りリクエスト数 | handler_read_rnd_next    | 回/秒 | 毎秒の次の行の読み取りリクエスト数 |
| 内部ロールバック数 | handler_rollback | 回/秒 |毎秒トランザクションがロールバックされる回数 |
| 内部提出数 | handler_commit  | 回/秒 | 毎秒のトランザクション提出数 |
|InnoDBブランクページ数|innodb_buffer_pool_pages_free|個|Innodbエンジンメモリブランクページ数|
|InnoDB総ページ数|innodb_buffer_pool_pages_total|個|Innodbエンジンのメモリ占用総ページ数|
|InnoDBロジック読み取り|innodb_buffer_pool_read_requests|回/秒|Innodbエンジンが毎秒完了したロジック読み取りリクエスト回数|
|InnoDB物理的読み取り|innodb_buffer_pool_reads|回/秒|Innodbエンジンが毎秒完了した物理的読み取りリクエスト回数|
|InnoDB読み取り量|innodb_data_read|Byte/秒|Innodbエンジンが毎秒完了した読み取りデータバイト数|
|InnoDB合計読み取り量|innodb_data_reads|回/秒|Innodbエンジンが毎秒完了したデータ読み取り回数|
|InnoDB合計書き込み量|innodb_data_writes|回/秒|Innodb エンジンが毎秒完了したデータ書き込み回数|
|InnoDB書き込み量|innodb_data_writes|Byte/秒|Innodbエンジンが毎秒完了したデータ書き込みバイト数|
|InnoDB行削除量|innodb_rows_deleted|回/秒|Innodbエンジンが毎秒削除した行数|
|InnoDB行挿入量|innodb_rows_inserted|回/秒|Innodbエンジンが毎秒挿入した行数|
|InnoDB行更新量|innodb_rows_updated|回/秒|Innodbエンジンが毎秒更新した行数|
|InnoDB行読み取り量|innodb_rows_read|回/秒|Innodbエンジンが毎秒読み取った行数|
|InnoDBが取得する行の平均ロック時間|innodb_row_lock_time_avg|ミリ秒|Innodbエンジンが行をロックする平均時間|
|InnoDB行ロック待機回数|innodb_row_lock_waits|回/秒|Innodbエンジンの毎秒の行ロック待機回数|
|キーキャッシュ内で未使用のブロック数|key_blocks_unused|個|myisamエンジンが未使用のキーキャッシュブロック数|
|キーキャッシュ内で使用したブロック数|key_blocks_used|個|myisamエンジンが使用済みのキーキャッシュブロック数|
|キーキャッシュ読み取りデータブロック数|key_read_requests|回/秒|myisamエンジンの毎秒のキーキャッシュブロック読み取り数|
|ハードディスク読み取りデータブロック数|key_reads|回/秒|myisamエンジンの毎秒のハードディスク読み取りデータブロック数|
|データブロックキーバッファ書き込み数|key_write_requests|回/秒|myisamエンジンの毎秒のキーキャッシュブロック書き込み数|
|データブロックディスク書き込み数|key_writes|回/秒|myisamエンジンの毎秒のハードディスクデータブロック書き込み回数|
|マスターマシンとスレーブマシンとの遅延距離|master_slave_sync_distance|MB|マスターマシンとスレーブマシンbinlogの距離|
|マスターマシンとスレーブマシンとの遅延時間|	seconds_behind_master|	秒|マスターマシンとスレーブマシンとの遅延時間|
|IOスレッドの状態|	slave_io_running|	状態値（0-Yes，1-No，2-Connecting）|IOスレッド作動状態|
|SQLスレッド状態|	slave_sql_running|	状態値（0-Yes，1-No）|SQLスレッド作動状態|

