このドキュメントではMySQLのカーネルバージョンの更新手順について説明します。
>?
>- TencentDB for MySQLのアップデートについて、[カーネルマイナーバージョンのアップデート](https://intl.cloud.tencent.com/document/product/236/36816)をご参照ください。
>- マイナーバージョンをアップデートするときに、一部のマイナーバージョンのメンテナンスで選択できない場合があります。コンソールで選択できるマイナーバージョンを優先してください。

<dx-tabs>
::: MySQL 8.0カーネルマイナーバージョンの更新説明
<table>
<thead><tr><th>カーネルマイナーバージョン</th><th>の説明</th></tr></thead>
<tbody>

<tr>	
<td>20220831</td>
<td><ul><li>新特性</li><ul>
<li>MySQLバージョンのダイナミック設定をサポートします。</li>
<li>透過的な列を暗号化します。テーブル構築時にvarcharフィールドにencryption属性を指定すると、ストレージ側で列を暗号化します。この機能は2023年に製品化される予定です。</li>
<li>サードパーティのデータサブスクリプションツールを使用するときに、内部データの整合性照合SQLのサブスクリプションが原因で、データサブスクリプションツールにエラーが発生するという問題を解決しました。<dx-alert infotype="explain" title="说明">データベースインスタンスが移行、アップグレード、または障害後に再構成された後、システムはデータ整合性の照合を実行して、データの整合性を確保します。データベースの照合SQLは`statement`モードになります。一部のサードパーティのサブスクリプションツールでは、`statement`モードのSQLの処理時にエラーが発生する傾向があります。このバージョンのカーネルにアップデートした後、サードパーティのサブスクリプションツールは、内部データの整合性照合SQLを購読しません。</dx-alert></li>
<li>DDL操作とNO_WAIT | WAIT [n]機能をサポートします。MDLロックを取得できず、待機する必要がある直前にDDLをロールバックできるようにします。または、MDLロックの待機に指定された時間が費やされた場合、DDLはロールバックされます。</li>
<li>Fast Query Cache機能をサポートします。読み取りが多く、書き込みが少ないシナリオに対応します。書き込みが多く、読み取りが少ない場合、データが頻繁に更新される場合、またはクエリの結果セットが非常に大きい場合は、有効にすることをお勧めしません。</li>
<li>mtsデッドロック検出機能強化をサポートします。</li>
<li><a href="https://www.tencentcloud.com/document/product/236/52512">並列クエリをサポートします</a>。並列クエリ機能を有効にして大規模なクエリを自動的に識別し、並列クエリ機能を使用してマルチコアコンピューティングリソースを動員し、大規模なクエリの応答時間を大幅に短縮します。</li>
</ul>
<li>パフォーマンスの最適化</li><ul>
<li>トランザクションシステムのスナップショットのオーバーヘッドを最適化します。Copy Free Snapshotメソッドが採用され、トランザクションディレーがグローバルアクティブトランザクションhashから削除され、スナップショットの取得がスナップショット取得イベントのロジックタイムスタンプに最適化されます。sysbenchテストのread-writeシナリオ制限のパフォーマンスが11%向上します。</li>
<li>prepared statementプロセスでの権限チェックを最適化します。グローバルでは、1つの変数で権限のバージョン番号が示され、prepared statementは、prepareが完了した後にバージョン番号を記録し、実行中に権限のバージョン番号が変更されたかどうかを比較します。権限の変更がない場合は、権限のチェックをスキップします。そうでない場合は、権限を再確認し、バージョン番号を記録します。</li>
<li>スレッドプールの時間取得精度を最適化します。</li>
<li>記録されたoffsetの取得を最適化します。indexごとに記録されたoffsetがキャッシュされます。条件が満たされる場合は、キャッシュされたoffsetが直接使用されて、rec_get_offsets()関数を呼び出す計算オーバーヘッドが節約されます。</li>
<li>Parallel DDLを最適化します。<br>1. インデックスフィールドが小さい場合は、サンプリングメモリのサイズを小さくして、サンプリングの頻度を減らします。<br>2. Kチャネルのマージによるソートは、マージによるソートのラウンド数を効果的に減らすことができるため、IO数を減らすことができます。<br>3. 毎回、記録ごとにoffsetsを生成することを避けるために、記録を読み取るときに固定長のoffsetをキャッシュします。</li>
<li>undo log情報記録ロジックを最適化し、insertパフォーマンスを向上させます。</li>
<li>半同期をオンにするときのパフォーマンスを最適化し、半同期を有効にするときのパフォーマンスを向上させます。</li>
<li>監査パフォーマンスを最適化し、システムのオーバーヘッドを削減します。</li>
</ul>

<li>バグの修正</li><ul>
<li>Thread_memoryに異常な値が表示されることがある問題を修正しました。</li>
<li>バッチステートメント監査のシナリオでtimestampが正しくない問題を修正しました。</li>
<li>秒レベルでの列の変更に関連する問題を修正しました。</li>
<li>CREATE TABLE t1 AS SELECT ST_POINTFROMGEOHASH("0123", 4326)ステートメントでマスタースレーブが中断される問題を修正しました。</li>
<li>テーブルレベルが並列の場合にslaveリトライ例外が発生する問題を修正しました。</li>
<li>show slave hostsを実行するときにMalformed packetエラーが発生する問題を修正しました。</li>
<li>ごみ箱に関連する問題を修正しました。</li>
<li>ARMモデルでjemallocのアサインメカニズムがOOMをトリガーしやすい問題を修正しました。</li>
<li>truncate pfs accout tableによる統計無効化の問題を修正しました。</li>
<li>ごみ箱に外部キー制約がある場合、子テーブルが最初に復元され、次に親テーブルが復元されるという異常な状況を修正しました。</li>
<li>ログのsql_modeロギングに関する問題を修正しました。</li>
<li>低確率でCREATE DEFINERストアドプロシージャを実行するときに異常が発生する問題を修正しました。</li>
<li>公式Copy Free Snapshotに関連する問題を修正しました。</li>
<li>スレッドプールのパフォーマンスジッターの問題を修正しました。</li>
<li>hash join+union結果が空になることがある問題を修正しました。</li>
<li>メモリに関連する問題を修正しました。</li>
</ul>
</td>
</tr>	

<tr>	
<td>20220401</td>
<td><ul><li>バグの修正</li><ul>
<li>Parallel DDLのstage変数エラーによってFTSインデックス作成シーンでstage nullポインタにcrashが発生する問題を修正しました。</li>
<li>フルテキストインデックスの新規追加によってクラッシュが発生する可能性がある問題を修正しました。</li>
</ul></td>
</tr>	

<tr>	
<td>20220331</td>
<td><ul><li>バグの修正</li><ul>
<li>スレッドプール内のワイルドポインタの参照が解除されるとcrashが発生する問題を修正しました。</li>
</ul></td>
</tr>

<tr>	
<td>20220330</td>
<td>
<ul><li>新特性</li><ul>
<li>writeset並列レプリケーションはデフォルトでオンになっています。</li>
<li>I/O、メモリ使用率、SQLタイムアウトポリシーをユーザー単位で制御できる拡張リソースグループをサポートします。</li>
<li>UNDO時間範囲内の任意の時点のデータを問い合せるフラッシュバック問合せ機能をサポートします。</li>
<li>delete/insert/replace/updateのreturning構文をサポートし、このstatementが操作するデータ行を返します。</li>
<li>rowモードのgtidレプリケーション機能拡張をサポートします。</li>
<li>トランザクションロックの最適化機能をサポートします。</li>
<li>ごみ箱が拡張され、truncate tableとごみ箱内のテーブルの自動クリーンアップをサポートします。</li>
<li>parallel ddl機能をサポートし、索引の作成を必要とするDDL操作を3段階並列で高速化しました。</li>
<li>索引列のクイック変更機能をサポートします。</li>
<li>統計情報の自動収集とクロスマシン統計情報の収集をサポートします。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>binlog_order_commitsがオフになっている状態でトランザクションがコミットされたときのgtidのロック競合を最適化しました。</li>
<li>InnoDB起動フェーズをrsegsのシングルスレッド作成からマルチスレッド作成に変更することで、MySQL起動時間を最適化しました。</li>
</ul>

<li>バグの修正</li><ul>
<li>デッドロックまたはロックされて待機すると接続が切断され、トランザクションが終了しないという問題を解決しました。</li>
<li>innodb_row_lock_current_waitsなどの統計値に異常があるという不具合を修正しました。</li>
<li>監査プラグインにはuse databaseでのsql typeエラーがないという問題を修正しました。</li>
<li>大きなテーブルの非同期削除機能の中で、innodb_async_table_sizeより小さいテーブルもrenameされるとい問題を修正しました。</li>
<li>監査プラグインのエスケープ文字エラーの問題を修正しました。</li>
<li>列をすばやく変更した後にロールバックするという問題を修正しました。</li>
<li>trx_sys closeときにxa付きシーンでcrashが発生するという問題を修正しました。</li>
<li>merge derived tableのときにcrashが発生するという問題を修正しました。</li>
<li>writesetがオンになっている状態でbinlog_formatが修正されるという問題を修正しました。</li>
<li>hash scanにより、同じ行をA->B->A->Cで更新する場合の1032問題を修正しました。</li>
<li>Prepared Statementモードでソートされた索引が無効になるという問題を修正しました。</li>
<li>実体化された結果を消費するオペレータが実体化オペレータの戻り値パスに組み込まれる可能性があり、実行計画の理解と表示の問題につながります。</li>
<li>大きなテーブルの非同期削除の極端な状況での異常な動作を修正しました。</li>
<li>sql filterの設定時のエラーメッセージ表示異常の問題を修正しました。</li>
<li>解析ストレージプロシージャ構文のエラー表示問題を修正しました。</li>
<li>過去ヒストグラを使用できないという問題を修正しました。</li>
<li>SHOW SLAVE HOSTS(show replicas)のRole列表示の互換性問題を修正しました。</li>
<li>Item_in_subselect::single_value_transformerが列数エラーのときにcrashが発生するという問題を修正しました。</li>
<li>サブテーブルにvirtual columnと外部キー列が存在し、カスケード接続更新期間にメモリーリークによるインスタンスのcrash問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20211202</td>
<td>
<ul><li>新特性</li><ul>
<li>列のクイック変更機能をサポートします。</li>
<li>ヒストグラムの履歴バージョンの機能をサポートします。</li>
<li>物理テーブルのランダムサンプルを得るためのSQL2003 TABLESAMPLE（単一テーブル）をサポートします。</li>
<li>非予約語の追加:TABLESAMPLE BERNOULLI。</li>
<li>特定の入力フィールドのヒストグラムを作成するためのHISTOGRAM()関数を追加します。</li>
<li>compressedヒストグラムをサポートします。</li>
<li>SQLトラフィック制限の機能をサポートします。</li>
<li>MySQLクラスターロールの設定機能をサポートします。デフォルトのロールはCDB_ROLE_UNKNOWNです。</li>
<li>show replicasのコマンド実行結果に、ロールを表示するためのRole列を新規追加します。</li>
<li>proxyをサポートします。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>insert on duplicate key updateによるホットスポットの更新問題を改善しました。</li>
<li>eventの複数の同一binlog eventを集約することによって、hash scanの適用速度を引き上げます。</li>
<li>plan cacheが開いた状態でのスレッドプールモードでは、prepareステートメントによってチェックされるメモリが大幅に削減されます。</li>
</ul>

<li>バグの修正</li><ul>
<li>ホットスポット更新の最適化を有効にした後、パフォーマンスが不安定になる不具合を修正しました。</li>
<li>`select count(*)`並列スキャンが極端な場合に全テーブルをスキャンする可能性がある不具合を修正しました。</li>
<li>さまざまな場合に統計情報が0を読み込むことによる実行計画の変更とそれによる機能トラブルを修正しました。</li>
<li>queryが長時間にquery end状態となっている不具合を修正しました。</li>
<li>長いレコードで統計情報が著しく低く見積もられる不具合を修正しました。</li>
<li>Temptableエンジンを使用する際、選択された列のアグリゲート関数が255を超過する時にエラーが出るバグを修正しました。</li>
<li>json_table関数列の大文字・小文字を区別してしまう問題を修正しました。</li>
<li>表現式のreturn true時に早く戻るため、ウィンドウ関数が正確性の問題を引き起こすbugを修正しました。</li>
<li>derived condition pushdownがuser variables を含むときに下がり続けることによって引き起こされる正確性の問題を修正しました。</li>
<li>SQL filterがRule規則でnamespaceを付け加えないことによるcrashの不具合を修正しました。</li>
<li>並列処理や競合が多い場合にスレッドプールをオンにすると、QPSがジッターする不具合を修正しました。</li>
<li>マスター/スレーブbpの同期が極端な場合（ホストサーバーのファイルシステムが壊れている場合）にファイルハンドルリークの不具合を修正しました。</li>
<li>index mappingの不具合を修正しました。</li>
<li>統計情報のキャッシュ同期の不具合を修正しました。</li>
<li>updateステートメントまたはストレージ過程の実行時においてメッセージをクリアしていないこといよるcrashの不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20210830</td>
<td>
<ul><li>新特性</li><ul>
<li>プリロード行数制限機能をサポートしています。</li>
<li>プランキャッシュチェックの最適化機能をサポートしています。</li>
<li>ANALYZE構文（UPDATE HISTOGRAM c USING DATA 'json'）を拡張して、直接ヒストグラムを書き込む機能をサポートします。
</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>インデックスプルダウンの代わりにヒストグラムを使用して、評価エラーとI/Oのオーバーヘッドを削減します。この機能はデフォルトではオフになっています。</li>
</ul>

<li>バグの修正</li><ul>
<li>online-DDL期間中に統計情報がゼロになる可能性がある状況を修正しました。</li>
<li>スレーブのgenerated columnが更新されない状況を修正しました。</li>
<li>binlogが圧縮されたときにインスタンスがハングする不具合を修正しました。</li>
<li>新しく生成されたbinlogファイルのprevious_gtids eventでgtidが欠落する不具合を修正しました。</li>
<li>システム変数を変更するときにデッドロックが発生する恐れがあるという不具合を修正しました。</li>
<li>show processlistのスレーブsqlスレッドのinfoが正しく表示されない不具合を修正しました。</li>
<li>公式8.0.23にhash joinに関するbugfixを移植しました。</li>
<li>公式writesetに関するbugfixを移植しました。</li>
<li>公式8.0.24にクエリオプティマイザに関するbugfixを移植しました。</li>
<li>FAST DDLでflush listを最適化し、ページの同時実行性を解放するバグを修正しました。</li>
<li>大量のテーブルのインスタンスで、データディクショナリをアップグレードするときに、大量のメモリを消費する状況を最適化しました。</li>
<li>instant add columnの後に新しいプライマリキーを作成するシーンでクラッシュが起きる問題を修正しました。</li>
<li>フルテキストインデックスクエリでのメモリの増加によって生じるOOMの問題を修正しました。</li>
<li>show processlisによって返される結果セットのTIMEフィールドに-1が発生する問題を修正しました。</li>
<li>ヒストグラムの互換性により、テーブルが開かない場合があるという問題を修正しました。</li>
<li>Singletonヒストグラムを作成する際の浮動小数点の累積エラーを修正しました。</li>
<li>row形式のログのテーブル名に長い中国語文字が含まれるために発生するレプリケーションの中断という問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20210330</td>
<td>
<ul><li>新特性</li><ul>
<li>マスター/スレーブbp同期機能のサポート：HAが発生し、マスター/スレーブの切り替えが行われた後、スタンバイデータベースは通常、比較的長時間warmupする必要があり、ホットデータをbuffer poolにロードします。待機マシンのウォームアップを高速化するために、TXSQLはマスター/スレーブbp同期機能をサポートしています。</li>
<li>Sort Merge Join機能をサポートします。</li>
<li>FAST DDL機能をサポートします。</li>
<li>ユーザー側のcharacter_set_client_handshakeパラメータの照会をサポートし、現在値機能を表示します。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>スキャンflush listダーティーページの最適化：ダーティーメカニズムを最適化することにより、インデックス作成プロセスでのパフォーマンスのジッターによる問題が解消され、システムの安定性が向上します。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>offline_mode、cdb_working_modeパラメータを変更する際のデッドロックの問題を修正しました。</li>
<li>trx_sysのmax_trx_idの同時実行の永続化という問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20201230</td>
<td>
<ul><li>新特性</li><ul>
<li>公式<a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-19.html" target="_blank">8.0.19</a>、<a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-20.html" target="_blank">8.0.20</a>、<a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-21.html" target="_blank">8.0.21</a>、<a href="https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-22.html" target="_blank">8.0.22</a>の変更をマージします。</li>
<li>thread_handlingのスレッドモードまたは接続プールモードの動的設定をサポートしました。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>BINLOG LOCK_doneロックの競合を最適化し、書き込みパフォーマンスを向上させました。</li>
<li>Lock Free Hashを使用して、trx_sys mutexの競合を最適化し、パフォーマンスを向上させました。</li>
<li>redo logのディスクへのフラッシュを最適化しました。</li>
<li>buffer poolの初期化時間を最適化しました。</li>
<li>大きなテーブルdrop tableのAHIクリーンアップを最適化しました。</li>
<li>監査性能を最適化しました。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>innodb一時テーブルのクリーンアップによって引き起こされるパフォーマンスジッターの問題を修正しました。</li>
<li>コア数が多いインスタンスでのread onlyのパフォーマンス低下という問題を修正しました。</li>
<li>hash scanによって、1032エラーが発生する不具合を修正しました。</li>
<li>ホットスポット更新機能の同時実行によるセキュリティの問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20200630</td>
<td>
<ul><li>新特性</li><ul>
<li>大規模なテーブルの非同期削除可能：ファイルを非同期かつ低速にクリーンアップすることで、大規模なテーブルの削除によるサービスパフォーマンスのジッター現象を回避します。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットを提出</a>して申請する必要があります。</li>
<li>アイドルタスクを自動的にkillしてリソースの競合を減らすことをサポートします。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットを提出</a>して申請する必要があります。</li>
<li>透過的なデータ暗号化をサポートします。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>relay_log_posとmaster_log_posの間のチェックポイントに一貫性がないために切り替えが失敗するエラーを修正しました。</li>
<li>非同期でディスクにデータを保存することにより発生するデータファイルエラーを修正しました。</li>
<li>fsyncがEIOを返すことを繰り返してデッドループに陥ってしまうという不具合を修正しました。</li>
<li>フルテキストインデックスにおけるマルチバイト文字セットでのフレーズ検索（phrase search）に発生したクラッシュ問題を修正しました。</li>
</ul>
</td>
</tr>
</tbody></table>
:::
::: MySQL 5.7カーネルマイナーバージョンの更新説明
<table>
<thead><tr><th>カーネルマイナーバージョン</th><th>の説明</th></tr></thead>
<tbody>

<tr>	
<td>20220716</td>
<td>
<ul><li>新特性</li><ul>
<li>InnoDBの自動採番列永続化機能をサポートします。</li>
<li>メモリの正確な統計機能をサポートします。</li>
<li>Queryレベルのメモリ監視機能をサポートします。</li>
<li>ごみ箱機能をサポートします。</li>
<li>DDL並列処理機能をサポートします。</li>
<li>フラッシュバッククエリ機能をサポートします。</li>
<li>内部xaトランザクションの非同期ロールバック機能をサポートします。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>非同期の大きなテーブルの削除最適化<br>50GBとして定義されていた大きなテーブルは、パラメータinnodb_async_table_sizeを使用してより柔軟に制御できるようになりました。</li>
</ul>

<li>バグの修正</li><ul>
<li>alter tableのインデックス作成によるERROR 1878(HY000)：Temporary file write failureの報告を修正しました。</li>
<li>PFSメモリ監視でbuf/buf/poolが認識されない問題を修正しました。</li>
<li>returningステートメントが一部のシーンで権限チェック時に異常が発生する可能性がある問題を修正しました。</li>
<li>parserがステートメントのセミコロンを正しく処理しなかったためにエラーが報告される問題を修正しました。</li>
<li>監査ステートメント内の一重引用符がエスケープされていない問題を修正しました。</li>
<li>ARMプラットフォームでメモリ使用量が急激に増加する問題を修正しました。</li>
<li>writesetがオンになっている状態でbinlog_formatが変更されるとマスタとスレーブが一致しない問題を修正しました。</li>
<li>大量のスレッドが同時に終了するとCPUが高くなる問題を解決しました。</li>
<li>drop table partiton forceに関連するbugを修正しました。</li>
<li>binlog dumpが重くなり、インスタンスの再起動が遅くなる問題を解決しました。</li>
<li>create table like temporary tableがbinlogの文字セットを継承しないことでマスタ/スレーブの同期が失敗する問題を修正しました。</li>
<li>show detail processlistに不正な文字情報が表示される問題を修正しました。</li>
<li>スレッドプールが特定の状況で終了するときにthread_groupロックが解放されない問題を修正しました。</li>
<li>table並列レベルで親テーブルを更新すると、インスタンスの実行に異常が発生する問題を修正しました。</li>
<li>slaveで仮想列の計算にエラーが発生する問題を修正しました。</li>
<li>gtid_subsetが行レコードの実行後にnull_valueをfalseに設定しない問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20211230</td>
<td>
<ul><li>新特性</li><ul>
<li>公式<a href="https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-19.html" target="_blank">5.7.19</a>から<a href="https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-36.html" target="_blank">5.7.36</a>までの変更をマージします。</li>
<li>マスタとスレーブのbuffer pool同期は、HA以降の性能回復速度を高速化し、ネイティブモードと比較して性能回復速度を90秒程度減少させました。</li>
<li>backup lock機能を追加し、軽量なメタデータロックを提供し、バックアップ時のサービス可用性を向上させました。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>utf8/utf8mb4 my_charpos相関関数をインライン化し、read_writeシーンでのUTF_8相関関数のパフォーマンスを最適化しました。
<li>jemallocのバージョンが5.2.1にアップデードされました。</li>
<li>binlog rotateときのファイル番号の取得を最適化しました。</li>
<li>半同期のslave ioを最適化しました。</li>
<li>hash scanの集約を最適化しました。</li>
<li>大規模トランザクションのcrash recover起動時間を最適化しました。</li>
</ul>

<tr>	
<td>20211102</td>
<td>
<ul><li>新特性</li><ul>
<li>サードパーティのデータサブスクリプションツールを使用するときに、内部データの整合性照合SQLのサブスクリプションが原因で、データサブスクリプションツールにエラーが発生するという問題を解決しました。<dx-alert infotype="explain" title="说明">データベースインスタンスが移行、アップグレード、または障害後に再構成された後、システムはデータ整合性の照合を実行して、データの整合性を確保します。データベースの照合SQLは`statement`モードになります。一部のサードパーティのサブスクリプションツールでは、`statement`モードのSQLの処理時にエラーが発生する傾向があります。このバージョンのカーネルにアップデートした後、サードパーティのサブスクリプションツールは、内部データの整合性照合SQLを購読しません。</dx-alert></li>
</ul>
</td>
</tr>

<tr>	
<td>20211031</td>
<td>
<ul><li>新特性</li><ul>
<li>writesetレプリケーション機能をサポートしています。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>checkpointを積極的に推進し、バックアップの成功率を引き上げます。</li>
<li>hash scanインデックス選択の最適化。</li>
<li>ホットスポット更新のパフォーマンスの最適化はinsert on duplicate key updateをサポートします。</li>
</ul>

<li>バグの修正</li><ul>
<li>ホットスポットの更新をオンにすると、パフォーマンスが不安定になる不具合を修正しました。</li>
<li>instant ddlの後にupdate操作をロールバックするとcrashを引き起こす不具合を修正しました。</li>
<li>列の圧縮を有効にした後、create table selectステートメントが圧縮属性を継承しない不具合を修正しました。</li>
<li>skip-grant-tableオプションを有効にした後、show variables like 'tencent_root%’ステートメントがインスタンスのcrashを引き起こす不具合を修正しました。</li>
<li>read onlyモードでQuery Rewriterプラグインがcrashする不具合を修正しました。</li>
<li>パーティションテーブルでのhash scanの1032の不具合を修正しました。</li>
<li>mtsモードで最初の大きなトランザクションsbmが0になる不具合を修正しました。</li>
<li>slave_preserve_commit_order=ON，slave_transaction_retries=0のときのstop slaveがタイムアウトする不具合を修正しました。</li>
<li>いくつかのXAトランザクションのbugを修正しました。</li>
<li>default値を持つjsonフィールドを作成した後、show create時にSQLエラーがアセンブルされる不具合を修正しました。</li>
<li>トランザクションがブロックされた後、接続が切断されたトランザクションをロールバックできない不具合を修正しました。</li>
<li>長いレコードで、innodb persistentメソッドの統計情報が0になることがある不具合を修正しました。</li>
<li>8.0を移植して、ANALYZE TABLEで照会が蓄積されてしまう不具合を修正しました。</li>
<li>innodbの統計情報が、変更後にServer層に速やかに同期されない不具合を修正しました。</li>
<li>統計サンプリングのブロックにより書き込み時間が長くなり、クラッシュが引き起こされる不具合を修正しました(Bug#31889883)。</li>
<li>innodbの統計情報の更新処理で、一定の確率で0を読み込むことになる不具合を修正しました(BUG#105224)。</li>
<li>MVCCに発生する可能性のある複雑さがO(N^2)の挙動を修正しました（Bug#28825617）。</li>
<li>接続が解放されたときに、一時テーブルを閉じることによって引き起こされるbinlog rotateによるcrashを修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20210630</td>
<td>
<ul><li>新特性</li><ul>
<li>現在のslaveがリプレイしたbinlogタイムスタンプを表示するために、コマンドSHOW SLAVE DETAIL [FOR CHANNEL channel]を追加しました。</li>
<li>transaction_read_only/transaction_isolationパラメータをサポートします。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>hash scanの適用速度を最適化しました。slave側では、複数の同一のbinlog eventを集約することにより、hash scanの適用速度を引き上げます。</li>
</ul>

<li>バグの修正</li><ul>
<li>更新ステートメントによってトリガーされる一時テーブルのプライマリキーの重複、列が見つからない、列が長すぎるといった問題を修正しました。</li>
<li>DDLプロセスにおいて統計情報がゼロになる可能性がある問題を修正しました。</li>
<li>接続ステータス統計においてundo log size統計が不正確になる問題を修正しました。</li>
<li>metadata_locksテーブルの照会によるインスタンスcrashの問題を修正しました。</li>
<li>「of」を非予約語に変更しました。</li>
<li>動的に変更されたバージョン番号が新しい接続で無効と表示される問題を修正しました。</li>
<li>page_cache cleanningアクセスワイルドポインタの問題を修正しました。</li>
<li>alter tableステートメントを実行すると、「Incorrect key file for table」というエラーレポートが発生する場合がある問題を修正しました。</li>
<li>パーティションテーブルが大量のメモリを使用する問題を修正しました。</li>
<li>show processlisによって返される結果セットのTIMEフィールドに-1が発生する問題を修正しました。</li>
<li>slaveノードでのXAトランザクションレプリケーションロックの待機の問題を修正しました。</li>
<li>equal rangeクエリでのパーティションテーブルの誤ったロックの問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20210331</td>
<td>
<ul><li>新特性</li><ul>
<li>delete/insert/replaceのreturning構文をサポートします。このstatmentによって操作されるデータ行を返すことができます。そのうち、deleteステートメントは前のイメージデータを返し、insert/replaceは後のイメージデータを返します。</li>
<li>列圧縮機能のサポート：現在、行形式の圧縮とデータページの圧縮がありますが、これら2つの圧縮方法は、テーブル内のいくつかの大きなフィールドと他の多くの小さなフィールドを処理すると同時に、小さなフィールドの読み取りと書き込みを頻繁に行います。大きなフィールドへのアクセス頻度が低い場合、その読み取り/書き込みアクセスにより、コンピューティングリソースに無駄な浪費が多く発生します。列の圧縮により、アクセス頻度の低い大きなフィールドを圧縮できると同時に、フィールドの行全体のストレージスペースを削減でき、読み取り/書き込みアクセスの効率を引き上げます。</li>
<li>ユーザー側のcharacter_set_client_handshakeパラメータの照会をサポートし、現在値機能を表示します。</li>
<li>ログファイルが占有するpage cacheの自発的なクリーンアップをサポート：この機能は、スライディングウィンドウを使用し、posix_fadviseを介してログファイルが占有するpage cacheを自発的にクリーンアップし、オペレーティングシステムのメモリ負荷を軽減し、マシン全体の安定性を向上させます。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>CREATE INDEXの並列化：CREATE INDEXプロセスでは外部マージソートを実行する必要がありますが、これには時間がかかります。今回、並列外部マージソートアルゴリズムを導入し、CREATE INDEXの所要時間を50%以上削減させます。</li>
<li>スキャンflush listダーティーページの最適化：ダーティーメカニズムを最適化することにより、インデックス作成プロセスでのパフォーマンスのジッターによる問題が解消され、システムの安定性が向上します。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>メモリ漏洩の問題を修正しました。</li>
<li>8.0バージョンjsonの修正を移植して、jsonの使用の安定性を向上させます。</li>
<li>hash scanによって、1032エラーが発生する不具合を修正しました。</li>
<li>ホットスポット更新機能の同時実行によるセキュリティの問題を修正しました。</li>
<li>公式gcolバグの修正を一括移植しました。</li>
<li>一部のシナリオでdatetimeタイプと文字列の比較に失敗する問題を修正しました。</li>
<li>マスター/スレーブbp同期機能のファイルハンドラが解放されないバグを修正しました。</li>
<li>offline_modeを設定しながらの接続の新規作成によって引き起こされる可能性のあるデッドロックのbugを修正しました。</li>
<li>範囲の照会同時実行シナリオでのm_end_rangeの誤った設定によって引き起こされるcrashの問題を修正しました。</li>
<li>groupby jsonフィールドのtemporay tableの更新に時間がかかる問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20201231</td>
<td>
<ul><li>新特性</li><ul>
<li>SELECT FOR UPDATE/SHAREにNOWAITとSKIP LOCKEDの選択項目の使用をサポートしました。</li>
<li>thread_handlingのスレッドモードまたは接続プールモードの動的設定をサポートしました。</li>
<li>マスター/スレーブのbuffer poolの同期機能をサポートしました。</li>
<li>ユーザーの接続状態監視機能、監視項目には、同期・非同期IO、メモリ、ログ量、CPU時間、ロックにかかる時間などが含まれます。
</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>トランザクションのサブシステムを最適化し、並列処理のパフォーマンスを向上させました。</li>
<li>大規模トランザクションのcrash recover起動時間を最適化しました。</li>
<li>redo logのディスクへのフラッシュを最適化しました。</li>
<li>buffer poolの初期化時間を最適化しました。</li>
<li>utf8/utf8mb4の文字列効率を最適化しました。</li>
<li>監査性能を最適化しました。</li>
<li>gtid_purgedの設定がブランクでなければならないという制限を解除しました。</li>
<li>バックアップロックの最適化：LOCK TABLES FOR BACKUP、LOCK BINLOG FOR BACKUP、UNLOCK BINLOGという3つの新しいSQLステートメントを導入しました。FLUSH TABLES WITH READ LOCKのバックアップをロックする方法では、データベース全体でサービスが提供できなくなるのに比べ、これら3つのステートメントは軽量級のデータバックアップロックに用いられ、バックアップ中のデータアクセスをサポートします。これらのステートメントは、物理バックアップか論理バックアップかに関わらず、バックアップの一貫性の保護を実現するために使用できます。</li>
<li>大きなテーブルdrop tableの最適化。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>performance_schemaのクエリ時にハングする不具合を修正しました。</li>
<li>digest_add_token関数のoverflowの不具合を修正しました。</li>
<li>MySQLの公式truncate tableでibufアクセスによって引き起こされるcrashを修正しました。</li>
<li>left joinのステートメントにおいてconstの事前計算によって引き起こされるクエリの正確性に関する不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20200930</td>
<td>
<ul><li>パフォーマンスの最適化</li><ul>
<li>バックアップロックを最適化しました。FLUSH TABLES WITH READ LOCKのバックアップをロックする方法では、データベース全体でサービスの提供ができなくなりますが、このバージョンでは、軽量級のデータバックアップロック方法が提供されています。</li>
<li>大きなテーブルdrop tableを最適化しました。アダプティブハッシュの高速クリーンアップの最適化（innodb_fast_ahi_cleanup_for_drop_tableコントロール）により、大きなテーブルをdropするときに時間のかかるアダプティブハッシュインデックスのクリーンアップを大幅に短縮できます。
</li>
</ul>

<li>公式bugの修正</li><ul>
<li>MySQLの公式truncate tableでibufアクセスによって引き起こされるcrashを修正しました。</li>
<li>高速列作成をした後にコールドスタンバイをプルできないという不具合を修正しました。</li>
<li>innodbメモリテーブルオブジェクトの頻繁なリリースによって引き起こされるパフォーマンスの低下という不具合を修正しました。</li>
<li>left joinのステートメントにおいてconstの事前計算によって引き起こされるクエリの正確性に関する不具合を修正しました。</li>
<li>Ruleクラス名の競合によってcoreの問題を引き起こす、sqlトラフィック制限とquery rewriteプラグインを修正しました。</li>
<li>複数sessionでのinsert on duplicate key updateステートメントの同時更新という不具合を修正しました。</li>
<li>auto_increment_incrementの同時挿入によって引き起こされるduplicate key errorによる失敗という不具合を修正しました。</li>
<li>innodbメモリオブジェクトの削除がダウンタイムを引き起こす不具合を修正しました。</li>
<li>ホットスポット更新機能の同時実行によるセキュリティの問題を修正しました。</li>
<li>jemallocバージョンを5.2.1にアップグレードした後、スレッドプールが有効になり、coredumpがトリガーされるという不具合を修正しました。</li>
<li>fwriteでエラー処理が行われないために監査ログが不完全になる不具合を修正しました。</li>
<li>rootユーザーとして起動したときに、mysqld_safeがログを出力しない不具合を修正しました。</li>
<li>alter table exchange partitionによってddl logファイルが大きくなる不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20200701</td>
<td>
<ul><li>公式bugの修正</li><ul>
<li>INNOBASE_SHARE index mappingのエラーの不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20200630</td>
<td>
<ul><li>新特性</li><ul>
<li>SELECT FOR UPDATE/SHAREのステートメントにNOWAITとSKIP LOCKEDの選択項目の使用をサポートしました。</li>
<li>大量のトランザクションを最適化する機能をサポートし、大量のトランザクションによるマスターに対するスレーブの遅延、バックアップ失敗等の不具合を修正しました。</li>
<li>監査機能の最適化：非同期監査機能をサポートしました。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>digest_add_token関数のオーバーフローの不具合を修正しました。</li>
<li>insert blobによるインスタンスcrashの不具合を修正しました。</li>
<li>hash scanでevent中に同じ行に対する更新が発生してレコードが見つからず、マスター/スレーブのレプリケーション中断が起きる不具合を修正しました。</li>
<li>performance_schemaのクエリ時にハングする不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20200331</td>
<td>
<ul><li>新特性</li><ul>
<li>公式MySQLのバージョン5.7.22のJSONシリーズ関数を追加しました。</li>
<li>電子商取引の秒殺(seckill)ケースに基づく<a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">ホットスポットの更新</a>機能をサポートしています。</li>
<li><a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">SQLトラフィック制限</a>をサポートしています。</li>
<li>データ暗号化機能は、KMSカスタムキーの暗号化をサポートしています。</li>
</ul>

<li>バグの修正</li><ul>
<li>フルテキストインデックスにおけるマルチバイト文字セットでのフレーズ検索（phrase search）に発生したクラッシュ問題を修正しました。</li>
<li>同時実行数が多い場合、CATSロックスケジューリングモジュールに発生したクラッシュ問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20190830</td>
<td>
<ul><li>新特性</li><ul>
<li>binlogファイルが破損した場合にスキップして解析を続ける機能をサポートします。マスターインスタンスとbinlogの両方が破損した場合に、最大限にスレーブデータベースからデータを復元して利用します。</li>
<li>非GTIDモードからGTIDモードへのデータ同期をサポートします。</li>
<li>ユーザーがshow full processlistステートメントを使用して「ユーザースレッドのメモリ使用状況」を確認することをサポートします。</li>
<li>テーブル<a href="https://intl.cloud.tencent.com/document/product/236/35988" target="_blank">高速列作成機能</a>をサポートし、データをコピーせず、ディスク領域やディスクI/Oを消費せず、サービスのピーク時にもリアルタイムで変更できます。</li>
<li>AUTO_INCREMENTの永続化をサポートします。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>GRANTステートメントの列名に予約語がある場合にレプリケーションが中断するという不具合を修正しました。</li>
<li>パーティションテーブルで逆方向スキャンを実行するとSQLの実行効率が低下するという不具合を修正しました。</li>
<li>プライマリキーを含むテーブルの仮想インデックスのデータ不整合によって、クエリ結果の異常が発生するという不具合を修正しました。</li>
<li>InnoDBでプライマリキーを範囲検索するとデータが欠落するという不具合を修正しました。</li>
<li>スペースインデックスを持つテーブルでDDLを実行するによって引き起こされるクラッシュを修正しました。</li>
<li>binlogのサイズが大きすぎると、ハートビート情報内のファイルの長さがオーバーフローし、マスター/スレーブが中断するという不具合を修正しました。</li>
<li>eventを削除すると他のeventが時間通りに実行されなくなるという不具合を修正しました。</li>
<li>検索結果をまとめるとエラーが発生するという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20190615</td>
<td>
<ul><li>新特性</li><ul>
<li>透過的なデータ暗号化をサポートします。</li>
</ul>
</td>
</tr>

<tr>	
<td>20190430</td>
<td>
<ul><li>公式bugの修正</li><ul>
<li>サブクエリで長いテキスト機能を使用した場合のNULLポインタ参照の不具合を修正しました。</li>
<li>Hash Scanを実行するとマスター/スレーブが中断するという不具合を修正しました。</li>
<li>マスターデータベースのbinlogの切り替えによってslaveノードのI/Oスレッドが中断するという不具合を修正しました。</li>
<li>NAME_CONSTによって引き起こされるクラッシュを修正しました。</li>
<li>文字セットによる「illegal mix of collation」の問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20190203</td>
<td>
<ul><li>新特性</li><ul>
<li>大規模なテーブルの非同期削除可能：ファイルを非同期かつ低速にクリーンアップすることで、大規模なテーブルの削除によるサービスパフォーマンスのジッター現象を回避します。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットを提出</a>して申請する必要があります。</li>
<li>CATSのロックスケジューラをサポートします。</li>
<li>GTIDを有効にすると、トランザクション内の一時テーブルおよびCTS構文を作成・削除することができます。この機能を有効にするには<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
<li>暗黙的なプライマリキーをサポートします。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
<li>super権限以外のユーザーが他のユーザーのセッションを強制終了する機能をサポートします。cdb_kill_user_extraパラメータを使用して設定します。デフォルト値はroot@%です。</li>
<li>エンタープライズクラスの暗号化関数をサポートします。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>binlogキャッシュファイルの容量が不足している場合にレプリケーションが中断されるという不具合を修正しました。</li>
<li>fsyncがEIOを返すことを繰り返してデッドループに陥ってしまうという不具合を修正しました。</li>
<li>GTIDの欠番によってレプリケーションが中断され、再開できないという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20180918</td>
<td>
<ul><li>新特性</li><ul>
<li>アイドル状態のトランザクションを自動的にkillしてリソースの競合を減らすことをサポートします。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
<li>MemoryエンジンからInnoDBエンジンへの自動切り替え：グローバル変数cdb_convert_memory_to_innodbがONの場合、テーブルエンジンはテーブルの作成/変更時にMemoryからInnoDBに変換されます。</li>
<li>インデックスの非表示機能をサポートします。</li>
<li>Jemallocによるメモリ管理をサポートします。これにより、jlibcメモリ管理モジュールを置き換え、メモリ使用量を削減し、メモリ割り当て効率を向上させることができます。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>binlogのスイッチを最適化し、rotateのホールドロック時間を短縮させることで、システムパフォーマンスを向上させます。</li>
<li>Crash Recoveryの回復速度を向上させます。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>マスター/スレーブの切り替えによるeventの無効化の不具合を修正しました。</li>
<li>REPLAY LOG RECORDによって引き起こされるクラッシュを修正しました。</li>
<li>Lose index scansによってクエリ結果にエラーが発生するという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20180530</td>
<td>
<ul><li>新特性</li><ul>
<li>SQL監査機能をサポートします。</li>
<li>テーブルレベルの並列レプリケーションをサポートします。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>slaveインスタンスのロックを最適化し、slaveインスタンスの同期パフォーマンスを向上させます。</li>
<li>select...limitのプッシュダウンを最適化します。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>relay_log_posとmaster_log_posの間のチェックポイントに一貫性がないために切り替えが失敗するエラーを修正しました。</li>
<li>Crash on UPDATE ON DUPLICATE KEYによるCrashの不具合を修正しました。</li>
<li>JSONカラムのインポートによる「Invalid escape character in string.」のエラーを修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20171130</td>
<td>
<ul><li>新特性</li><ul>
<li> information_schema.metadata_locksビューをサポートし、現在のインスタンスにおけるMDLの付与及び待機ステータスを確認します。</li>
<li>ALTER TABLE NO_WAIT | TIMEOUTの構文をサポートし、DDL操作に待機タイムアウトを与えます。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
<li>スレッドプール機能をサポートします。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。
</ul>

<li>公式bugの修正</li><ul>
<li>bytes_dataに基づいてinnodb_buffer_pool_pages_dataを計算し、このパラメータのオーバーフローを回避します。</li>
<li>非同期モードで速度制限プラグインが使用できないという不具合を修正しました。</li>
</ul>
</td>
</tr>

</tbody></table>
:::
::: MySQL 5.6カーネルマイナーバージョンの更新説明
<table>
<thead><tr><th>カーネルマイナーバージョン</th><th>の説明</th></tr></thead>
<tbody>

<tr>	
<td>20220303</td>
<td>
<ul><li>Bugの修正</li><ul>
<li>大きなテーブルのrow_mysql_truncate_t::file_nameを非同期に削除するとき、mem_strdupによって割り当てられたメモリを使用すると、リリース異常が発生するという問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20220302</td>
<td>
<ul><li>Bugの修正</li><ul>
<li>sql_update.ccのメモリリークの問題を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20220301</td>
<td>
<ul><li>新特性</li><ul>
<li>スピン周期の動的設定をサポートします。動的パラメータinnodb_spin_wait_pause_multiplierによってスピン周期(0～100)を動的に調整できます。<br>当該パラメータは臨時調整に使用され、コンソールで固定への修正がサポートされません。</li>
<li>デッドロックループ情報のプリント機能をサポートします。<br>パラメータinnodb_print_dead_lock_loop_infoで有効にします。有効にした状態でデッドロックが発生した場合、show engine innodb statusを使用してデッドロックループ情報を確認できます。</li>
</ul>

<li>バグの修正</li><ul>
<li>slaveを再起動した後のmemoryテーブルに匿名GTIDトランザクションが発生するという不具合を修正しました。</li>
<li>root@localhost権限が失われることでアップデートに失敗するという不具合を修正しました。</li>
<li>innodb_row_lock_current_waitsなどの監視変数値に異常があるという不具合を修正しました。</li>
<li>監査プラグインのsql typeマッピングにエラーが発生するという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20211030</td>
<td>
<ul><li>新特性</li><ul>
<li>大規模トランザクションレプリケーションの最適化をサポートします。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>hash scanの適用速度を最適化しました。</li>
</ul>

<li>バグの修正</li><ul>
<li>大量のテーブルクエリでOOMが発生する不具合を修正しました。</li>
<li>innodb_thread_concurrecyを0に設定することで発生するデッドループの不具合を修正しました。</li>
<li>長いレコードで統計情報が0になる不具合を修正しました。</li>
<li>sbmジャンプの不具合を修正しました。</li>
<li>LOCK_binlog_end_pos hangの不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20210630</td>
<td>
<ul><li>新特性</li><ul>
<li>大規模トランザクションレプリケーションの最適化をサポートします。</li>
</ul>

<li>バグの修正</li><ul>
<li>index mergeがオンになっている場合のコピーの正確性の問題を修正しました。</li>
<li>rowモードでcdb_more_gtid_feature_supportedがオンになっている場合、create table selectの実行が中断されると、レプリケーションが中断される状況を修正しました。</li>
<li>max(id)がshow create tableの AUTO_INCREMENTより大きいというバグを修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20201231</td>
<td>
<ul><li>公式bugの修正</li><ul>
<li>hash scanによって、1032エラーが発生する不具合を修正しました。</li>
<li>rowフォーマットのreplace intoによって、マスター/スレーブのauto incrementの値が不一致になるという不具合を修正しました。</li>
<li>SQLステートメントの解析に要求されたメモリを解放しないことによって引き起こされるメモリリークを修正しました。</li>
<li>create table as selectのテーブル作成時に、sql mode検査をスキップする不具合を修正しました。</li>
<li>Insertステートメントがデフォルト値を挿入する時に、sql mode検査をスキップする不具合を修正しました。</li>
<li>バインドされたパラメータを使用してupdateステートメントを実行する時に、sql mode検査をスキップする不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20200915</td>
<td>
<ul><li>新特性</li><ul>
<li><a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">SQLトラフィック制限</a>の機能をサポートします。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>buffer poolの初期化アクセラレーションを最適化します。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>マスター/スレーブのrename tableがハングする不具合を修正しました。</li>
<li>event_schedulerの設定をdisableにした場合、cdb_skip_event_schedulerをon からoffに変更した際に、crashが発生する不具合を修正しました。</li>
<li>tencentroot最大リンク数にsrv_max_n_threadsがカウントされず、sync_wait_array関連のアサーションが失敗する不具合を修正しました。</li>
<li>他のクラウド製品のMySQL 5.6 とTencent MySQL 5.6 のシステムデータベース中のテーブル構造の一部が異なるため、マスター/スレーブの並列レプリケーションを行った際に、crashが発生する不具合を修正しました。</li>
<li>INSERT ON DUPLICATE KEY UPDATE THE WRONG ROWの不具合を修正しました。</li>
<li>index_mappingにエラーが起きる不具合を修正しました。</li>
<li>mtr失敗のバグの問題を修正しました。</li>
<li>hash scanでevent 中に、同じ行に対する更新が発生した時にレコードが見つからなくなり、マスター/スレーブのレプリケーション中断が起きる不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20190930</td>
<td>
<ul><li>新特性</li><ul>
<li>ユーザーはshow full processlistステートメントを使用して「ユーザースレッドのメモリ使用状況」を確認できます。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>スレーブデータベースのreplication filterによるgtid欠番の不具合を修正しました。</li>
<li>Binlogのサイズが大きすぎると、ハートビート情報内のファイルの長さがオーバーフローし、マスター/スレーブが中断するという不具合を修正しました。</li>
<li>文字セットによるillegal mix of collationエラーを修正しました。</li>
<li>Hash Scanを実行するとマスター/スレーブが中断するという不具合を修正しました。</li>
<li>NAME_CONSTの使用によって引き起こされるクラッシュを修正しました。</li>
<li>マスターデータベースのbinlogの切り替えによってslaveノードのI/Oスレッドが中断するという不具合を修正しました。</li>
<li>innodb_log_checusumによるバックアップに互換性がないという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20190530</td>
<td>
<ul><li>公式bugの修正</li><ul>
<li>RCモードでダーティデータが読み込まれるという不具合を修正しました。</li>
<li>一時テーブルを削除すると待機マシンの再生に失敗するという不具合を修正しました。</li>
<li>高並列処理でのデッドロックの不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20190203</td>
<td>
<ul><li>新特性</li><ul>
<li>大きなテーブルの非同期削除が可能：ファイルを非同期かつゆっくりとクリーンアップすることで、大きなテーブルの削除によるビジネスパフォーマンスの変動を回避します。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットを提出</a>して申請する必要があります。</li>
<li>super権限以外のユーザーが他のユーザーのセッションを強制終了する機能をサポートします。cdb_kill_user_extraパラメータを使用して設定します。デフォルト値はroot@%です。</li>
<li>GTIDを有効にすると、トランザクション内の一時テーブルおよびCTS構文を作成・削除することができます。この機能を有効にするには<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>パーティションテーブルのレプリケーションと再生を最適化することで、パーティションテーブルの再生速度を向上させます。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>一時的な空き容量が不足しているため、マスター/スレーブ間でデータが一致しないという不具合を修正しました。</li>
<li>ホットログレコードを更新するとハングアップするという不具合を修正しました。</li>
<li>並列レプリケーションでのSeconds_Behind_Master値に異常が発生するという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20180915</td>
<td>
<ul><li>新特性</li><ul>
<li>MEMORYエンジンからInnoDBエンジンへの自動切り替え：グローバル変数cdb_convert_memory_to_innodbがONの場合、テーブルエンジンはテーブルの作成/変更時にMEMORYからInnoDBに変換されます。</li>
<li>アイドル状態のトランザクションを自動的にkillしてリソースの競合を減らすことができます。この機能を有効化するには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>REPLAY LOG RECORDによって引き起こされるクラッシュを修正しました。</li>
<li>decimalの精度によるマスター／スレーブ間の時間データに不整合が生じる不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20180130</td>
<td>
<ul><li>新特性</li><ul>
<li>スレッドプール機能をサポートします。この機能を有効にするには、<a href="https://console.cloud.tencent.com/workorder/category" target="_blank">チケットをサブミット</a>して申請する必要があります。</li>
<li>slaveノードはレプリケーションフィルタリング条件の動的な変更をサポートします。</li>
</ul>

<li>パフォーマンスの最適化</li><ul>
<li>drop tableによるパフォーマンスのジッター。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>パスワード文字列の認証によるデータベースのcrashの不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20180122</td>
<td>
<ul><li>新特性</li><ul>
<li>SQL監査機能をサポートします。</li>
</ul>

<li>公式bugの修正</li><ul>
<li>整数がオーバーフローするという不具合を修正しました。</li>
<li>フルテキストインデックスにおけるクエリにエラーが発生するという不具合を修正しました。</li>
<li>レプリケーション中にslaveがcrashするという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20170830</td>
<td>
<ul><li>公式bugの修正</li><ul>
<li>非同期モードでbinlog速度制限が無効になるという不具合を修正しました。</li>
<li>buffer_poolステータスに異常が発生するという不具合を修正しました。</li>
<li>SEQUENCEと暗黙的なプライマリキーの競合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20170228</td>
<td>
<ul><li>公式bugの修正</li><ul>
<li>drop tableの文字コードのバグを修正しました。</li>
<li>replicate-wild-do-tableが小数点などの特殊文字を含むデータベースまたはテーブルを正しくフィルタリングできない不具合を修正しました。</li>
<li>スレーブデータベースからrotateイベントが発生した後にSQLスレッドが早く終了するという不具合を修正しました。</li>
</ul>
</td>
</tr>

<tr>	
<td>20161130</td>
<td>
<ul><li>パフォーマンスの最適化</li><ul>
<li>lock_logロックを分割し、lock logにかかる時間を短縮させ、並列処理のパフォーマンスを向上させます。</li>
<li>マスターデータベースのACKスレッドが独立して動作するようにして、応答時間が向上します。</li>
<li>ファントムリードを防ぐために、ACKを待機している間、ユーザースレッドを強制終了する機能を禁止します。</li>
<li>sync_binlog !=1の場合は、不要なlock_syncロックになることを修正しました。</li>
</ul>
</td>
</tr>

</tbody></table>
:::
</dx-tabs>
