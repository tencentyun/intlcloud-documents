TXRocksは、Tencent TXSQLチームがRocksDBに基づいて開発したトランザクション型ストレージエンジンであり、さらにストレージスペースを節約し、書き込みの拡大率が低いという利点を併せ持っています。

## 製品紹介
TXRocksは、Tencent TXSQLチームがRocksDBに基づいて開発したトランザクション型ストレージエンジンであり、RocksDB LSM Treeストレージ構造により、InnoDBページの半分格納と断片化の無駄を減らすと同時に、コンパクトな形式のストレージを使うことができます。そのため、TXRocksはInnoDBと近い性能を維持するの前提の下で、ストレージ空間はInnoDBによりも半分以上節約することができ、さらにトランザクションの読み書きパフォーマンスが要求され、大量のデータを保存するビジネスに最適です。

##  前提条件
データベースのバージョンはMySQL 5.7、8.0で、アーキテクチャは2ノードでなければなりません。

## TencentDB for MySQLインスタンスの購入（RocksDBエンジン）
TencentDB for MySQL[購入ページ](https://buy.Intl.cloud.tencent.com/cdb)でインスタンスを購入するときに、エンジンとしてRocksDBを選択することができます。他のパラメータ項目について、[MySQLインスタンスを作成](https://intl.cloud.tencent.com/document/product/236/37785)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/4b309a61ecac3520e27160da7143c224.png)
>?RocksDBはkey-valueストレージエンジンであり、効率的な書き込み能力と高圧縮ストレージとして知られています。現時点で、エンジンとしてRocksDBを選択することをサポートしているのはMySQL 5.7、8.0だけです。

## RocksDBテーブルの作成
インスタンスを作成する際に、デフォルトのエンジンをRocksDBと設定する場合、テーブル作成時のデフォルトエンジンはRocksDBです。デフォルトエンジンは、以下のコマンドで確認できます：
```
show variables like '%default_storage_engine%';
```
![](https://qcloudimg.tencent-cloud.cn/raw/3bb1550d5995cece7cec2712ad62c5d0.png)
デフォルトエンジンはRocksDBである場合は、テーブル作成ステートメントではストレージエンジンの指定が許可されません。
![](https://qcloudimg.tencent-cloud.cn/raw/f4cb2efa27e236fb26a78971a8725cbd.png)
テーブルが正常に作成された後、その後の使用方法はInnoDBと同様に、データはRocksDBエンジンに格納されます。

## エンジン機能の制限
TXRocksは、次の表に示すように、エンジン機能にいくつかの制限があります：
<table>
<thead><tr><th>機能分類</th><th>機能項目</th><th>TXRocks制限</th></tr></thead>
<tbody>
<tr>
<td>DDL</td><td>Online DDL</td><td>サポートされません。例えば、ALTER TABLE ... ALOGRITHM=INSTANT機能をサポートしません。Partition 管理操作ではCOPYアルゴリズムだけをサポートします。</td></tr>
<tr>
<td rowspan="5">SQL機能</td>
<td>外部キー</td><td>外部キー（Foreign Key）がサポートされません</td></tr>
<td>パーティションテーブル</td><td>パーティションテーブル（Partition）がサポートされません</td></tr>
<td>生成列</td><td>生成列（Generated Columns）がサポートされません</td></tr>
<td>明示的なDefault表現式</td><td>サポートされません。例えば、CREATE TABLE t1（c1 FLOAT DEFAULT(RAND())）ENGINE=ROCKSDB; が失敗して、'Specited storage engine' is not supported for default value expressions.が表示されます</td></tr>
<td>暗号化テーブル</td><td>暗号化テーブルをサポートしません</td></tr>
<tr> 
<td rowspan="3">インデックス</td>
<td>空間インデックス</td><td>空間インデックス（Spatial Index）、空間データ型（GEOMETRY、POINT等）をサポートしません</td></tr>
<tr> 
<td>フルテキストインデックス</td><td>フルテキストインデックス(Fulltext Index)をサポートしません</td></tr>
<td>多値インデックス</td><td>多値インデックス(multi-valued index)をサポートしません</td></tr>
<tr>
<td rowspan="4">レプリケーション</td>
<td>グループレプリケーション</td><td>グループレプリケーション(Group Replication)をサポートしません</td></tr>
<td>binlog形式</td><td>ROW形式をサポートしますが、stmtまたはmixed形式をサポートしません</td></tr>
<td>クローンプラグイン</td><td>クローンプラグイン(Clone Plugin)をサポートしません</td></tr>
<td>トランスポータブル表領域</td><td>トランスポータブル表領域(Transportable Tablespace)をサポートしません</td></tr>
<tr>
<td rowspan="5">トランザクションとロック</td>
<td>LOCK NOWAITとSKIP LOCKED</td><td>LOCK NOWAITとSKIP LOCKEDをサポートしません</td></tr>
<td>ギャップロック</td><td>ギャップロック(Gap Lock)をサポートしません</td></tr>
<td>Savepoint</td><td>Savepointをサポートしません</td></tr>
<td>LOBフィールドの一部更新</td><td>LOBフィールドの一部更新をサポートしません</td></tr>
<td>XAトランザクション</td><td>使用をお勧めしません</td></tr>
</tbody></table>	

## パラメータの説明
>?TencentDB for MySQLインスタンスを作成する際には、RocksDB をデフォルトストレージエンジンとして選択でき、下の表のパラメータの説明に基づいて自社の業務に合わせたパラメータテンプレートを調整することができます。

#### MySQL 5.7に関するパラメータリスト

| パラメータ名称 | 再起動が必要かどうか | デフォルト値 | 許容値 | 説明 |
|---------|---------|---------|---------|---------|
| rocksdb_use_direct_io_for_flush_and_compaction | はい | ON | ON/OFF | compactionのときにDIOを使用するかどうかを指定します。|
| rocksdb_flush_log_at_trx_commit | いいえ | 1 | 0/1/2 | ログをディスクに書き込むタイミングを制御します。<br>innodb_flush_log_at_trx_commitと同様に、トランザクションがコミットされたときに同期するかどうかを指定します。<li>0の場合、トランザクションがコミットされるときに同期しません。<li>1の場合、トランザクションがコミットされるたびに同期します。<li>2の場合、1秒ごとに一回同期します。</li>  |
| rocksdb_lock_wait_timeout | いいえ | 1 | 1-1073741824 | ロックの待ち時間超過時間（秒）。|
| rocksdb_deadlock_detect | いいえ | ON | ON/OFF | デッドロック検出スイッチです。オンにすると、すべてのデッドロック情報はmysqldエラーログに記録されます。|
| rocksdb_manual_wal_flush | はい | ON | ON/OFF | rocksdb_max_total_wal_sizeよりも大きなWALの場合、一番旧いWALファイルを確実に削除するよう、RocksDBは強制的に列ファミリデータをディスクに書き込みます。|

#### MySQL 8.0関連パラメータリスト

| パラメータ名称 | 再起動が必要かどうか | デフォルト値 | 許容値 | 説明 |
|---------|---------|---------|---------|---------|
| rocksdb_flush_log_at_trx_commit | いいえ | 1 | 0/1/2 | ログをディスクに書き込むタイミングを制御します。<br>innodb_flush_log_at_trx_commitと同様に、トランザクションがコミットされたときに同期するかどうかを指定します。<li>0の場合、トランザクションがコミットされるときに同期しません。<li>1の場合、トランザクションがコミットされるたびに同期します。<li>2の場合、1秒ごとに一回同期します。</li>|
| rocksdb_lock_wait_timeout | いいえ | 1 | 1-1073741824 | ロックの待ち時間超過時間（秒）。|
| rocksdb_merge_buf_size | いいえ | 524288(=512K) | 100-18446744073709551615 | セカンダリインデックスの作成時に使用されるmerge-sort bufferのサイズ。|
| rocksdb_merge_combine_read_size | いいえ | 8388608 (=8M) | 524288(=512K)-18446744073709551615 | セカンダリインデックスの作成時に使用されるマルチパスのためのメモリの大きさ。|
| rocksdb_deadlock_detect | いいえ | ON | ON/OFF | デッドロック検出スイッチ。|
| rocksdb_manual_wal_flush | はい | ON | ON/OFF | rocksdb_max_total_wal_sizeよりも大きなWALの場合、一番旧いWALファイルを確実に削除するよう、RocksDBは強制的に列ファミリデータをディスクに書き込みます。|

## RocksDB エンジンモニタリング項目
下の表はRocksDBのエンジンモニタリングメトリックです。

| メトリック | 説明 |
|---------|---------|
| rocksdb_bytes_read | ディスク読み取り数 |
| rocksdb_bytes_written | ディスク書き込み数 |
| rocksdb_block_cache_bytes_read | データブロック読み取り数 |
| rocksdb_block_cache_bytes_write | データブロック書き込み数 |
| rocksdb_wal_log_capacity | WAL書き込みログのサイズ |

