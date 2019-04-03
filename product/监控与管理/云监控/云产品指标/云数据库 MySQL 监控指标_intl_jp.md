Tencent Cloud CMはTencentDB for MySQLインスタンスに以下の監視メトリックを提供します。

| メトリック名（日本語） | メトリック名（英語） | 単位 |ディメンション|
|---------|---------|---------|---------|
|スロークエリ数|slow_queries|回/分|uInstanceId|
|フルテーブルスキャン数|select_scan|回/秒|uInstanceId|
|クエリ数|select_count|回/秒|uInstanceId|
|アップデート数|com_update|回/秒|uInstanceId|
|削除数|com_delete|回/秒|uInstanceId|
|挿入数|com_insert|回/秒|uInstanceId|
|上書き数|com_replace|回/秒|uInstanceId|
|合計リクエスト数|queries|回/秒|uInstanceId|
|現在開いている接続数|threads_connected|個|uInstanceId|
|照合使用率|query_rate|%|uInstanceId|
|ディスク使用容量|real_capacity|MB|uInstanceId|
|ディスク上のサイズ|capacity|MB|uInstanceId|
|送信データ量|bytes_sent|MB/秒|uInstanceId|
|受信データ量|bytes_received|MB/秒|uInstanceId|
|容量使用率|volume_rate|%|uInstanceId|
|照合キャッシュヒット率|qcache_hit_rate|%|uInstanceId|
|照合キャッシュ使用率|qcache_use_rate|%|uInstanceId|
|テーブルロック待ち回数|table_locks_waited|回/秒|uInstanceId|
|一時的テーブル数|created_tmp_tables|回/秒|uInstanceId|
|innodbキャッシュヒット率|innodb_cache_hit_rate|%|uInstanceId|
|innodbキャッシュ使用率|innodb_cache_use_rate|%|uInstanceId|
|innodbディスク読み取り数|innodb_os_file_reads|回/秒|uInstanceId|
|innodbディスク書き込み数|innodb_os_file_writes|回/秒|uInstanceId|
|innodb fsync数|innodb_os_fsyncs|回/秒|uInstanceId|
|myisamキャッシュヒット率|key_cache_hit_rate|%|uInstanceId|
|myisamキャッシュ使用率|key_cache_use_rate|%|uInstanceId|
|CPU比率|cpu_use_rate|%|uInstanceId|
|メモリ使用量|memory_use|MB|uInstanceId|
|一時的ファイル数|created_tmp_files|回/秒|uInstanceId|
|メモリの一時的テーブル数|created_tmp_tables|回/秒|uInstanceId|
|既に開いているテーブル数|opened_tables|個|uInstanceId|
|待つ必要のあるテーブルロック数|table_locks_waited|回/秒|uInstanceId|
|提出数|com_commit|回/秒|uInstanceId|
|ロールバック数|com_rollback|回/秒|uInstanceId|
|作成済みスレッド数|threads_created|個|uInstanceId|
|実行するスレッド数|threads_running|個|uInstanceId|
|最大接続数|max_connections|個|uInstanceId|
|ディスクの一時的テーブル数|created_tmp_disk_tables|回/秒|uInstanceId|
|次の行を読み取るリクエスト数|handler_read_rnd_next|回/秒|uInstanceId|
|内部ロールバック数|handler_rollback|回/秒|uInstanceId|
|内部提出数|com_commit|回/秒|uInstanceId|
|InnoDB空白ページ数|innodb_buffer_pool_pages_free|個|uInstanceId|
|InnoDB空白ページ数|innodb_buffer_pool_pages_total|個|uInstanceId|
|InnoDB論理読み取り|innodb_buffer_pool_read_requests|回/秒|uInstanceId|
|InnoDB物理読み取り|innodb_buffer_pool_reads|回/秒|uInstanceId|
|InnoDB読み取り量|innodb_data_read|Byte/秒|uInstanceId|
|InnoDB合計読み取り量|innodb_data_reads|回/秒|uInstanceId|
|InnoDB合計書き込み量|innodb_data_writes|回/秒|uInstanceId|
|InnoDB書き込み量|innodb_data_written|Byte/秒|uInstanceId|
|InnoDB行削除量|innodb_rows_deleted|回/秒|uInstanceId| 
|InnoDB行挿入量|innodb_rows_inserted|回/秒|uInstanceId|
|InnoDB行アップデート量|innodb_rows_updated|回/秒|uInstanceId|
|InnoDB行読み取り量|innodb_rows_read|回/秒|uInstanceId|
|InnoDB行ロック取得の平均時間|innodb_row_lock_time_avg|ミリ秒|uInstanceId|
|InnoDB行ロック待ち数|innodb_row_lock_waits|回/秒|uInstanceId|
|キーキャッシュで使用されないブロック数|key_blocks_unused|個|uInstanceId|
|キーキャッシュで使用さたブロック数|key_blocks_used|個|uInstanceId|
|キーキャッシュのデータブロック読み取り数|key_read_requests|回/秒|uInstanceId|
|ディスクのデータブロック読み取り数|key_reads|回/秒|uInstanceId|
|データブロックがキーキャッシュに書き込まれた回数|key_write_requests|回/秒|uInstanceId|
|データブロックがディスクに書き込まれた回数|key_writes|回/秒|uInstanceId|


データベースの監視メトリックの使用方法の内容の詳細については、CM APIで[監視データAPIの読み取り](https://cloud.tencent.com/document/api/248/11006)を確認することができます。

