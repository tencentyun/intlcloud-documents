このドキュメントでは、並列クエリー機能でサポートされるステートメントのシナリオと制限されたシナリオを紹介します。

[](id:JRYJCJ1)
## 互換性のあるステートメントのシナリオ
TencentDB for MySQLは、以下の特徴を持つSQLステートメントの並列クエリー処理を実装しており、より機能的なシナリオを徐々に改善しています。
- 単一テーブルスキャンの場合：全テーブルスキャン、インデックススキャン、インデックス範囲スキャン、インデックスREFクエリーなどの順方向および逆方向のスキャンをサポートします。
- 複数テーブル結合の場合：Nested Loop JoinアルゴリズムおよびSemi Join、Anti Join、Outer Joinなどの結合タイプをサポートします。
- サブクエリーの場合: derived tableの並列処理をサポートします。
- データ型の場合：整数データ、文字データ、浮動小数点データ、時間型データ、およびオーバーフロー型データ（実行時のサイズ制限あり）など、複数のデータ型のクエリーをサポートします。
- 共通の演算子と関数は、原則として制限されません。
- アグリゲート関数は、COUNT/SUM/AVG/MIN/MAXをサポートします。
- UNION/UNION ALLクエリーをサポートします。
- traditional（デフォルト形式）、json、およびtreeという3つのEXPLAIN形式をサポートします。

## 制限されたシナリオ
TencentDB for MySQLの並列クエリー機能は、次のシナリオをサポートしていません。

<table>
<thead><tr><th>制限項目</th><th>制限説明</th></tr></thead>
<tbody>
<tr>
<td rowspan="6">ステートメントの互換性制限</td>
<td>非クエリ ステートメントは、INSERT ... SELECTおよびREPLACE ... SELECTを含む並列クエリーをサポートしません。</td></tr>
<tr><td>stored programのクエリーステートメントは並列処理できません。</td></tr>
<tr><td>prepared statementのクエリーステートメントは並列処理できません。</td></tr>
<tr><td>シリアライズ可能な隔離レベルのトランザクション内のクエリーステートメントは、並列処理できません。</td></tr>
<tr><td>select for update/share lockなどのロックされた読み取りステートメントは、並列処理できません。</td></tr>
<tr><td>CTEは、並列処理できません。</td></tr>
<tr>
<td rowspan="5">テーブル/インデックスの互換性制限</td>
<td>クエリーテーブルがシステムテーブル/一時テーブル/非Innodbテーブルの場合は、並列処理できません。</td></tr>
<tr><td>キャパシティインデックスは、並列処理できません。</td></tr>
<tr><td>全文索引は、並列処理できません。</td></tr>
<tr><td>パーティションテーブルは、並列処理できません。</td></tr>
<tr><td>スキャン方式がindex_mergeのテーブルは、並列処理できません。</td></tr>
<tr>
<td rowspan="13">表現式/Fieldの互換性制限</td>
<td>Generated Column 、BLOB、TEXT、JSON、BITおよびGEOMETRY フィールドを含むテーブルは、並列処理できません。</td></tr>
<tr><td>BIT_AND、BIT_OR、BIT_XORタイプのアグリゲート関数は、並列処理できません。</td></tr>
<tr><td>Aggregation(distinct)、例えばSUM(DISTINCT)、COUNT(DISTINCT)などのアグリゲート関数は、並列処理できません。</td></tr>
<tr><td>GISに関連する関数（SP_WITHIN_FUNC、ST_DISTANCEなど）は、並列処理できません。</td></tr>
<tr><td>ユーザーのカスタマイズ関数は、並列処理できません。</td></tr>
<tr><td>jsonに関連する関数（json_length，json_type、JSON_ARRAYAGGなど）は、並列処理できません。</td></tr>
<tr><td>XMLに関連する関数（xml_str）は、並列処理できません。</td></tr>
<tr><td>ユーザーロックに関連する関数（is_free_lock、is_used_lock、release_lock、release_all_locks、get_lock）は、並列処理できません。</td></tr>
<tr><td>sleep関数、random関数、GROUP_CONCAT関数、set_user_var関数、weight_string関数は、並列処理できません。</td></tr>
<tr><td>一部の統計に関する関数（STD/STDDEV/STDDEV_POP，VARIANCE/VAR_POP/VAR_SAMP）は、並列処理できません。</td></tr>
<tr><td>サブクエリーは、並列処理できません。</td></tr>
<tr><td>window関数は、並列処理できません。</td></tr>
<tr><td>rollupは、並列処理できません。</td></tr>
</tbody></table>	

[互換性のあるステートメントの並列クエリー](#JRYJCJ1)でステートメントが並列クエリーされているかどうかを問い合わせるほか、並列クエリーの実行計画を表示し、スレッドの稼働状況クエリーを表示することもできます。詳細については、[並列クエリーの表示](https://www.tencentcloud.com/document/product/236/53411)をご参照ください。

