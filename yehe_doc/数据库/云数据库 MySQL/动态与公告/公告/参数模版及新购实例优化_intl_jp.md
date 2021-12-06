
TencentDB for MySQLは2021年11月22日より、パラメータ関連の機能と出荷フローの最適化を開始します。今回の最適化には、パラメータテンプレートの作成、パラメータの比較、パラメータテンプレートの適用、パラメータの変更などの機能や変更可能なパラメータおよび新規購入インスタンスの最適化の更新が含まれます。

>?このパラメータ関連機能と出荷フローの最適化を事前に体験する必要がある場合は、2021年9月27日以降、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してベータ版テストへの参加を申請することができます。
パラメータ関連機能は、2ノードおよび3ノードのMySQL 5.6、MySQL 5.7およびMySQL8.0バージョンにのみ適用できます。

## 新規購入インスタンスの最適化
既存の新規購入インスタンスフローと比較して、初期化プロセスをキャンセルしました。新規購入ページは、文字セットの選択、テーブル名の大文字・小文字の区別、データベースアクセスポートの入力およびrootパスワードをサポートしています。

詳細については[MySQLインスタンスの作成](https://intl.cloud.tencent.com/document/product/236/43472)をご参照ください。

## パラメータ関連の最適化
### パラメータアプリケーション
一部のパラメータは、式による定義をサポートしています。このようなパラメータは仕様の変更に応じて変更される可能性があるため、データベースは常に最適な設定で実行されます。
式構文に関するサポートについては、下表をご参照ください。

| サポートカテゴリー | 説明 | サンプル |
| ------ | ------------------------------------------------------------ | --------------------- |
| 変数   | <li>DBinitMemory：インスタンス仕様のメモリサイズ、整数型。例えば、インスタンス仕様のメモリサイズが4000MBの場合、DBinitMemoryの値は4000です。<li>DBInitCpu：インスタンス仕様のCPUコアの数、整数型。TencentDB for MySQLのinnodb_buffer_pool_sizeパラメータの設定は、必ずメモリサイズの50%～90%に保つようにしてください。設定値が90%より大きい場合、自動的に90%に設定されます。設定値が50%未満の場合、自動的に50%に設定されます。 | {DBinitMemory*786432} |
| 演算子 | 式構文：{}パッケージを使用します。<li>除算演算子（/）：被除数を除数で除し、整数型の商を返します。計算結果が小数の場合、整数部分は切り捨てられます。小数はサポートされていません。例えば、システムは{MIN(DBInitMemory/4+500,1000000)}をサポートし、{MIN(DBInitMemory\*0.25+500,1000000)}をサポートしていません。<li>乗算演算子(*)：2つの乗数を互いに乗じて、整数型の積を返します。計算結果が小数の場合、整数部分は切り捨てられます。小数演算はサポートしていません。 |  -                     |
| 関数   | <li>関数MAX()、整数またはパラメータ式リストの最大値を返します。<li>関数MIN()は、整数型またはパラメータ式リストの最小値を返します。</li> | {MAX(DBInitCpu/2,4)}  |

パラメータ設定の詳細については、[インスタンスのパラメータ設定](https://intl.cloud.tencent.com/document/product/236/35793)をご参照ください。

### パラメータテンプレートの作成
パラメータテンプレートを作成する際に、既存の1種類のテンプレートが2つのテンプレート（高性能パラメータテンプレート/高安定パラメータテンプレート）に変更され、既存のテンプレートタイプオプションが追加されます。
<img src="https://main.qcloudimg.com/raw/a93abb9d05b05c0018c46d5efa027221.png"  style="zoom:90%;">

各テンプレートパラメータの比較：

|   差分パラメータ名           | デフォルトテンプレート                 | 高性能パラメータテンプレート       | 高安定性テンプレート            |
| -------------------- | ------------------------- | ------------------------ | -------------------------- |
| innodb_read_io_threads          | 12            | {MAX(DBInitCpu/2,4)}              | {MAX(DBInitCpu/2,4)}             |
| innodb_write_io_threads         | 12            | {MAX(DBInitCpu/2,4)}              | {MAX(DBInitCpu/2,4)}                |
| max_connections       | 800    | {MIN(DBInitMemory/4+500,100000)} | {MIN(DBInitMemory/4+500,100000)} |
| table_definition_cache                 | 768                       | {MAX(DBInitMemory*512/1000,2048)} | {MAX(DBInitMemory*512/1000,2048)} |
| table_open_cache                       | 2000                      | {MAX(DBInitMemory*512/1000,2048)} | {MAX(DBInitMemory*512/1000,2048)} |
| table_open_cache_instances             | 16                        | {MIN(DBInitMemory/1000,16)}       | {MIN(DBInitMemory/1000,16)}       |
| innodb_disable_sort_file_cache         | OFF                       | OFF                               | ON                    |
| innodb_log_compressed_pages            | ON                        | OFF                               | ON                   |
| innodb_print_all_deadlocks             | OFF                       | OFF                               | ON                    |
| sync_binlog                            | 0                         | 1000                              | 1                                 |
| thread_handling                        | one-thread-per-connection | pool-of-threads                   | one-thread-per-connection         |
| innodb_flush_redo_using_fdatasync      | FALSE                     | TRUE                   | FALSE                 |
| innodb_fast_ahi_cleanup_for_drop_table | FALSE                     | TRUE        | FALSE                             |
| innodb_adaptive_hash_index             | FALSE                     | TRUE                   | FALSE                      |
| innodb_table_drop_mode                 | SYNC_DROP                 | ASYNC_DROP             | SYNC_DROP         |
| innodb_flush_log_at_trx_commit         | 2                         | 2                                 | 1                                 |

パラメータテンプレートの詳細については、[パラメータテンプレートの使用](https://intl.cloud.tencent.com/document/product/236/31906)をご参照ください。

### 設定可能なパラメータの追加

| パラメータ名                                               |  MySQL 5.6  | MySQL 5.7  | MySQL 8.0  |
| ------------------------------------------------ | -------- | ---- | ---- |
| character_set_client                           |     -            |  &#10003;    |  -    |
| default_password_lifetime                   |      -          |  &#10003;    |  &#10003;    |
| innodb_alter_table_default_algorithm   |      -          |  &#10003;    |   -   |
| innodb_async_truncate_size                |      -          |  &#10003;    |  &#10003;    |
| innodb_async_truncate_work_enabled  |     -          | &#10003;     |    -  |
| innodb_buffer_pool_instances              |  &#10003; |  &#10003;   |  &#10003;   |
| innodb_buffer_pool_size                      |  &#10003; |  &#10003;   |  &#10003;   |
| innodb_default_row_format                  |       -         | &#10003;     | &#10003;    |
| innodb_fast_ahi_cleanup_for_drop_table |     -        |      -             | &#10003;     |
| innodb_flush_redo_using_fdatasync     |       -         | &#10003;     | &#10003;    |
| innodb_page_cleaners                         |       -        | &#10003;     | &#10003;     |
| innodb_table_drop_mode                     |      -         |      -             | &#10003;     |
| innodb_temp_tablespace_fast_cleanup |       -        |       -            | &#10003;     |
| internal_tmp_mem_storage_engine       |       -        |      -            | &#10003;    |
| slave_net_timeout                               |  &#10003; | &#10003;     |   -   |
| slave_parallel_type                             |  &#10003; |          -        |  -    |
| slave_parallel_workers                        |  &#10003; | &#10003;   |&#10003;    |
| sort_buffer_size                                  |  &#10003; |    -              |  -    |
| temptable_use_mmap                          |           -      |      -            | &#10003;    |
| thread_handling                                  |   &#10003; | &#10003;   |&#10003;   |
| thread_handling_switch_mode             |        -          |         -          | &#10003;   |
| thread_pool_oversubscribe                  |   &#10003; | &#10003;    |&#10003;    |
| thread_pool_size                                |        -          | &#10003;    | &#10003;   |
| tx_isolation                                        |          -        | &#10003;    | &#10003;    |

### 各テンプレートのパフォーマンステスト
テスト結果は次のとおりです。
![](https://qcloudimg.tencent-cloud.cn/raw/0f1aadfa080a43281fd98bea342812e6.png)
![](https://qcloudimg.tencent-cloud.cn/raw/29c6c04452626abe48e32c8370fe3aef.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3ed85cff088505c9f6979c42d5aadf20.png)
。

### デフォルトのパラメータテンプレートを保持する方法
新しいパラメータシステムがオンラインになった後、デフォルトのパラメータテンプレートは高性能パラメータテンプレートと高安定性テンプレートに置き換えられます。新しいパラメータシステムがオンラインになる前に、パラメータテンプレートを作成することで、デフォルトのパラメータテンプレート設定を保持することができます。[パラメータテンプレートの使用](https://intl.cloud.tencent.com/document/product/236/31906)をご参照ください。

### パラメータの比較
異なるテンプレート間でパラメータを比較する機能を提供し、異なるテンプレート間のパラメータの違いを確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/8529618ea8427864dea55f10b675ecb4.png)
パラメータテンプレートページの**比較**をクリックし、ポップアップウィンドウで比較するテンプレートを選択します。同じバージョンのデータベーステンプレートのみがサポートされています。 結果は以下をご参照ください。
<img src="https://qcloudimg.tencent-cloud.cn/raw/aad046642c7bec92ccacfda616887781.png"  style="zoom:80%;">

## お問い合わせ
ご不明な点がございましたら、[お問い合わせ](https://console.cloud.tencent.com/workorder/category)までお気軽にご連絡ください。長年にわたりTencent Cloudをご愛顧いただき、厚く御礼申し上げます。Tencent Cloudは、よりコストパフォーマンスの高い製品を引き続きご提供して参ります。

