## 機能の説明
スレッドプール（Thread_pool）は一定数のワークスレッドを用いて接続リクエストを処理するもので、通常はOLTPワークロードのシーンに比較的適しています。しかし、 リクエストにスロークエリが多い状況でスレッドプールの不足が発生すると、高遅延操作においてワークスレッドがブロックされ、新しいリクエストに迅速に応答できなくなり、システムのスループットが既存のone-thread-per-connection（Per_thread）方式より逆に低下する場合があります。

Per_thread方式とThread_pool方式にはそれぞれに長所と短所があり、システムは業務のタイプに応じて柔軟に切り替えを行う必要があります。残念ながら、現時点ではこの2種類の方式を切り替えるには、サーバーの再起動が必須です。通常、2種類の方式の切り替えニーズは業務のピーク時間帯に生じるため、その時点でのサーバー強制再起動は業務に重大な影響を与えます。

Per_thread方式とThread_pool方式の切り替えの柔軟性を高めるため、TencentDB for MySQLはスレッドプールの動的切り替えの最適化、すなわちデータベースサービスを再起動せずに、スレッドプールを動的にオンまたはオフにすることを可能にしました。

## サポートするバージョン
- カーネルバージョン MySQL 8.0 20201230およびそれ以降
- カーネルバージョン MySQL 5.7 20201230およびそれ以降

## ユースケース
パフォーマンスに敏感で、業務のタイプに応じて柔軟にデータベースの実行方式を調整する必要がある業務に適します。

## パフォーマンスへの影響
- pool-of-threadsをone-thread-per-connectionに切り替えるプロセス自体はqueryの堆積や、パフォーマンスへの影響をもたらしません。
- one-thread-per-connectionをpool-of-threadsに切り替えるプロセスは、その前にスレッドプールがスリープ状態にあるため、QPSが極めて高くかつストレスが持続的に高い状況下では、一定のリクエストの蓄積が存在する可能性があります。対処方法は次のとおりです。
  - 方法1：thread_pool_oversubscribeを適宜増大させるとともに、thread_pool_stall_limitを適宜小さくし、スレッドプールを迅速にアクティブ化します。堆積したSQLを消化後、状況に応じて上記の変更を元に戻します。
  - 方法2：SQLの蓄積が生じた際、業務トラフィックを一時的に数秒間停止または低下させ、pool-of-threadsが完全にアクティブ化されるのを待ってから、持続的な高ストレス業務トラフィックを再開させます。

## 利用説明
追加されたthread_handling_switch_modeはスレッドプール動的切り替え機能の制御に用います。オプション値およびその意味は次のとおりです。

| オプション値   | 意味                                               |
| -------- | -------------------------------------------------- |
| disabled | 方式の動的移動禁止                                   |
| stable    | 新しい接続のみ移動                                     |
| fast       | 新しい接続 + 新しいリクエストをすべて移動。デフォルトモード                      |
| sharp    | 現在アクティブな接続をkillし、ユーザーに強制的に再接続させることで、切り替えの効果を素早く発揮 |

`show threadpool status`に追加されたステータスは次のとおりです。
- connections_moved_from_per_threadは、Per_threadからThread_poolに移動したconnectionsの数を表します。
- connections_moved_to_per_threadは、Thread_poolからPer_threadに移動したconnectionsの数を表します。
- events_consumedは、各スレッドプールのワークスレッドで消費されたeventsの総数を表します。Thread_poolがPer_threadに移動した後は、eventsの総数はそれ以上増加しません。
- average_wait_usecs_in_queueは、各eventのqueueにおける平均待機時間を表します。

`show full processlist`に追加されたステータスは次のとおりです。
- Moved_to_per_threadは、その接続がPer_threadに移動した回数を表します。
- Moved_to_thread_poolは、その接続がThread_poolに移動した回数を表します.

## 関連パラメータステータス説明
スレッドプール関連パラメータの紹介：

| パラメータ名                          | 動的         | タイプ | デフォルト            | パラメータ値範囲                  | 説明                             |
| ------------------------------- | ------------ | ---- | --------------- | --------------------------- | ------------------------------- |
| thread_pool_idle_timeout        | Yes          | uint | 60              | [1, UINT_MAX]               | workerスレッドが処理すべきネットワークイベントがない場合に破棄されるまでの最長の待機時間（単位は秒） |
| thread_pool_oversubscribe       | Yes          | uint | 3               | [1,1000]                    | 1つのワークグループ内の最大許容worker数                          |
| thread_pool_size                | Yes          | uint | 現在のマシンのCPU数 | [1,1000]                    | スレッドグループ数                  |
| thread_pool_stall_limit         | Yes          | uint | 500             | [10, UINT_MAX]              | この時間（単位はミリ秒）ごとに1回、timerスレッドが全スレッドグループに対するトラバースを行います。<br>スレッドグループにlistenerがない場合や、優先度付きキューが空ではなく、かつ新たなIOネットワークイベントがない場合は、スレッドグループがstall状態にあると判断し、timerスレッドがウェイクアップを行うかまたは新たなworkerスレッドを作成し、そのスレッドグループのストレスを緩和します |
| thread_pool_max_threads         | Yes          | uint | 100000          | [1,100000]                  | スレッドプール内の全workerスレッドの総数                               |
| thread_pool_high_prio_mode      | Yes, session | enum | transactions    | transactions\statement\none | 高優先度キューの実行方式であり、次の3種類があります。<li>transactions：すでにトランザクションを開始している1つのSQLで、かつthread_pool_high_prio_ticketsが0ではないもののみ、高優先度キューに入ることができます。各接続はthread_pool_high_prio_ticketsプールで優先キューに入れられた後、一般キューに移動します<li>statement：すべての接続が高優先度キューに入れられます<li>none：statementに反し、すべての接続が低優先度キューに入れられます</li> |
| thread_pool_high_prio_tickets   | Yes, session | uint | UINT_MAX        | [0, UINT_MAX]               | transactions実行方式において、各接続に与えられるticketsのサイズ        |
| threadpool_workaround_epoll_bug | Yes          | bool | false           | true/false                  | linux2.x中のepoll bugを回避したかどうか。このbugはlinux3では修復されています          |

`show threadpool status`コマンドによって表示される関連ステータスの紹介：

| ステータス名                            | 説明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| groupid                               | スレッドグループID                                                     |
| connection_count                | スレッドグループのユーザー接続数                                             |
| thread_count                      | スレッドグループ内のワークスレッド数                                           |
| havelistener                       | スレッドグループに現在listenerが存在するか                                   |
| active_thread_count               | スレッドグループ内のアクティブworker数                                       |
| waiting_thread_count              | スレッドグループ内の待機中のworker数（wait_beginをコールしたworker）         |
| waiting_threads_size              | スレッドグループ内の、処理を必要とするネットワークイベントがなく、スリープ状態でウェイクアップ待機中のworker数（thread_pool_idle_timeout秒待機後に自動的に破棄） |
| queue_size                             | スレッドグループの一般優先度キューの長さ                                     |
| high_prio_queue_size              | スレッドグループの高優先度キューの長さ                                       |
| get_high_prio_queue_num           | スレッドグループ内でイベントを高優先度キューから取り出した総回数                     |
| get_normal_queue_num              | スレッドグループ内でイベントを一般優先度キューから取り出した総回数                   |
| create_thread_num                  | スレッドグループ内のworkerスレッド作成総数                                 |
| wake_thread_num                    | スレッドグループ内でwaiting_threadsキューからウェイクアップしたworkerの総数              |
| oversubscribed_num                | スレッドグループ内のworkerが、スレッドグループが現在oversubscribed状態にあることを発見し、スリープに入る準備をした回数 |
| mysql_cond_timedwait_num     | スレッドグループ内のworkerがwaiting_threadsキューに入った総回数                |
| check_stall_nolistener             | スレッドグループでtimerスレッドによるcheck_stallチェック中に発見されたlistenerなしの総回数   |
| check_stall_stall                     | スレッドグループでtimerスレッドによるcheck_stallチェック中にstall状態と判定された総回数  |
| max_req_latency_us                | スレッドグループ内のユーザー接続がキュー内で待機した最長時間（単位はミリ秒）             |
| conns_timeout_killed               | スレッドグループ内のユーザー接続が、クライアントから新しいメッセージがない時間が閾値（net_wait_timeout）を超えたためにkillされた総回数 |
| connections_moved_in               | 他のスレッドグループからこのスレッドグループに移動した接続の総数                         |
| connections_moved_out             | このスレッドグループから他のスレッドグループに移動した接続の総数                         |
| connections_moved_from_per_thread | one-thread-per-connection方式からこのスレッドグループに移動した接続の総数      |
| connections_moved_to_per_thread     | このスレッドグループからone-thread-per-connection方式に移動した接続の総数    |
| events_consumed                          | スレッドグループが処理したeventsの総数                                     |
| average_wait_usecs_in_queue       | スレッドグループ内の全eventsのキュー内平均待機時間                     |



