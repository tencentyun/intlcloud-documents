TencentDB for MySQLは、並列クエリー機能をサポートしています。コンソールまたはコマンドラインを通じて関連するパラメータを調整し、インスタンスの並列クエリー機能を有効または無効にすることができます。

##  前提条件
データベースバージョン：MySQL 8.0カーネルバージョン20220831以降。

## パラメータの説明
>?マスターインスタンスと読み取り専用インスタンスの両方が並列クエリー機能を有効にすることをサポートしますが、インスタンスのCPUコアの数は4以上である必要があります。

コンソールまたはコマンドラインを通じて、パラメータtxsql_max_parallel_worker_threadsとtxsql_parallel_degreeを0以外に調整することにより、現在のインスタンスの並列クエリー機能を有効にすることができます。推奨されるパラメータの関連情報と具体的な設定は次のとおりです。
**パラメータ情報**

| パラメータ | 変数タイプ | スコープ | デフォルト値 | 値の範囲 | 説明 |
|---------|---------|---------|---------|---------|---------|
| txsql_max_parallel_worker_threads | Integer | Global | {MIN(DBInitCpu,0)} | 0-{MAX(DBInitCpu-2,2)} | インスタンスノードが並列クエリーに使用できるスレッドリソースの総数。0に設定すると、使用できる並列スレッドがなく、並列クエリー機能をオフにすると見なされます。|
| txsql_parallel_degree | Integer | Global/session | 4 | 0 - 64 | 1つのステートメントの並列クエリーに使用できるスレッドの最大数（デフォルト並列度）。0に設定すると、並列クエリー機能をオフにすると見なされます。|

**推奨される設定**
- 並列度の仕様制限：txsql_parallel_degreeパラメータの値は、1つのステートメントの並列クエリーに使用されるスレッドの最大数、つまり、並列クエリーのデフォルト並列度を表します。並列度がインスタンスのCPUコア数の半分を超えないようにすることをお勧めします。安定性を確保するために、CPUコアが4未満の小規模なクラスターでは並列クエリー機能が無効になっています。コンソールまたはコマンドラインを使用して並列クエリーに関連するパラメータを調整することはできません。
- SQLステートメントは、並列クエリーを実行するときに、txsql_parallel_degreeによって設定された並列度をデフォルトで使用しますが、ユーザーはhintステートメントを通じて1つのSQLステートメントの並列クエリーの並列度を調整できます。詳細の説明については、[hintステートメント制御](https://www.tencentcloud.com/document/product/236/53410)をご参照ください。
- txsql_max_parallel_worker_threadsパラメーターの値は、インスタンスが並列クエリーで並列クエリーに使用できるスレッドの数を表します。txsql_max_parallel_worker_threads / txsql_parallel_degreeの値は、並列クエリーを同時に実行できるSQLステートメントの数を表します。
- txsql_max_parallel_worker_threadsとtxsql_parallel_degreeは、並列クエリー機能の有効と無効を共通で制御します。任意のパラメータが0に設定される場合は、並列クエリー機能を無効にすることを意味します。

TencentDB for MySQLはまた、並列クエリーの実行条件を設定するためのさまざまなパラメータを提供して、業務をカスタマイズし、業務の安定した運用を確保するのに便利です。設定後、データベースは、ステートメントの実行コスト、テーブルの行数、並列スケジュールを実行する1つのステートメントで使用されるメモリなどの条件を判断し、各SQLステートメントが並列クエリーを実行できるかどうかを確認します。関連するパラメータの説明は次のとおりです：

| パラメータ | 変数タイプ | スコープ | デフォルト値 | 値の範囲 | 説明 |
|---------|---------|---------|---------|---------|---------|
| innodb_txsql_parallel_partitions_per_worker | Integer | Global/Session |13 |0-256 |スライスされたデータの並列スキャンで、各スレッドによってスキャンされたパーティションの平均数。|
| txsql_optimizer_context_max_mem_size | Integer | Global/Session |{MIN(DBInitMemory*52429,8388608)} |0-{DBInitMemory*52429} |1つのステートメントが申請できる並列クエリースケジュール環境の最大メモリ制限。|
| txsql_parallel_cost_threshold | Integer | Global/Session |50000 |0-9223372036854476000 |並列実行コストのしきい値。実行コストがしきい値よりも高いステートメントのみが並列クエリーを実行します。|
| txsql_parallel_exchange_buffer_size | Integer | Global/Session |1048576 |65536-268435456 |データ交換バッファーのサイズ。|
| txsql_parallel_cost_threshold | Integer | Global/Session |5000 |0-9223372036854476000 |並列テーブルの行数のしきい値。行数がしきい値よりも多いテーブルのみを並列テーブルとして選択できます。|

>!
>- 並列クエリーなどのすべてのパラメータは、インスタンスを再起動する必要はなく、設定後、すぐ有効になります。
>- sessionスコープでマークされたパラメータは、このパラメータが1つのステートメントの設定をサポートすることを意味します。

### コンソールによる並列クエリーの有効化または無効化
MySQLコンソールを通じてインスタンスパラメータ設定ページに入り、関連するパラメータを設定することで、機能を有効または無効にすることができます。
- txsql_max_parallel_worker_threadsとtxsql_parallel_degreeを0以外に設定すると、並列クエリー機能を有効にすることを意味します。
- txsql_max_parallel_worker_threadsとtxsql_parallel_degreeのいずれか1つを0に設定すると、並列クエリー機能を無効にすることを意味します。

関連する実行条件パラメータを設定することもできます。コンソールパラメータ設定ページは、下図の通りです。詳細な操作方法については、[パラメータインスタンスの設定](https://intl.cloud.tencent.com/document/product/236/35793)をご参照ください。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/BgaK167_18.png)

### hintステートメントによる1つのSQLステートメントの並列実行方法の指定
TencentDB for MySQLは、1つのSQLステートメントに対して並列実行方法を指定することをサポートします。1つのSQLステートメントを設定する場合は、hintステートメントを使用して操作します。詳細の方法については、[hintステートメント制御](https://www.tencentcloud.com/document/product/236/53410)をご参照ください。

##  関連ドキュメント
- [並列クエリーの確認](https://www.tencentcloud.com/document/product/236/53411)
- [Hintステートメント制御](https://www.tencentcloud.com/document/product/236/53410)

