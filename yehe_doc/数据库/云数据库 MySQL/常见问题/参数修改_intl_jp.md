### TencentDB for MySQLインスタンスの設定パラメータをどのように変更しますか？
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンスIDをクリックして管理ページに進み、**データベース管理**> **パラメータ設定**を選択します。そのうちのよく見られるvar\_nameには、次の変数が含まれます：
<table>
<tbody><tr>
<th>変数</th><th>説明</th></tr>
<tr>
<td>character_set_server</td><td>サーバーのデフォルト文字セット</td></tr>
<tr>
<td>connect_timeout</td><td>接続タイムアウト</td></tr>
<tr>
<td>long_query_time</td><td>この時間を超えるクエリはスロークエリです</td></tr>
<tr>
<td>max_allowed_packet</td><td>最大パケット長</td></tr>
<tr>
<td>max_connections</td><td>最大接続数</td></tr>
<tr>
<td>sql_mode</td><td>現在のサーバーのSQLモード</td></tr>
<tr>
<td>table_open_cache</td><td>すべてのスレッドの開いているテーブルの数。この値を増やすと、mysqldが必要とするファイル記述子の数が増えます</td></tr>
<tr>
<td>wait_timeout</td><td>サーバーが非対話型接続でのアクティビティを待機してから閉じるまでの秒数</td></tr>
</tbody></table>

その他の設定パラメータは、コンソールの**データベース管理**> **パラメータ設定**ページで確認できます。

### MySQLで中国語クエリをどのように設定しますか？
MySQLは現在、中国語をサポートしていません。

### MySQLでスケジューラー機能を有効にするにはどうすればよいですか？
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンスIDをクリックして管理ページに進み、**データベース管理**> **パラメータ設定**ページを選択します。パラメータ設定でevent_schedulerパラメータをONに設定します。

### MySQLのタイムアウト接続設定が短すぎますが、どのように時間を増やしますか？
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンスIDをクリックして管理ページに進み、**データベース管理**> **パラメータ設定**ページを選択します。パラメータ設定でwait_timeoutパラメータを変更します。

### MySQLのgroup_concat_max_lenパラメータをどのように変更しますか？
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンスIDをクリックして管理ページに進み、**データベース管理**> **パラメータ設定**ページを選択します。パラメータ設定でgroup_concat_max_lenパラメータを変更します。

###　MySQLでフルテーブルスキャンのSQLステートメントはどのようにして見つけられますか？
デフォルトでは、全表スキャンのステートメントは記録されません。TencentDB for MySQLのMySQLコンソールの**パラメータ設定**でlog_queries_not_using_indexesパラメータをONに設定できますが、長時間開いたままにしないようご注意ください。

### MySQLのデフォルトの文字セットはどのように変更しますか？
MySQLのデフォルトの文字セットはUTF8です。現在、LATIN1、GBK、UTF8、UTF8MB4の4種類の文字セットを設定することができます。

MySQLはデフォルトの文字セットの設定をサポートしますが、テーブルを作成するとき、テーブルのエンコーディングを明示的に指定し、接続の確立時に接続のエンコーディングを指定することをお勧めします。これにより、お客様のアプリケーションがより優れた移植性を有します。MySQLのデフォルトの文字セットの説明および変更方法については、<a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">使用制限</a>をご参照するか、[コンソール](https://console.cloud.tencent.com/cdb)で文字セットを変更することもできます。　　

### クラウドデータベースの文字セットソートルールを表示する方法。
TencentDB for MySQLでは、一部のユーザーがデフォルトの文字セットをセルフ設定するよう、インスタンスの作成時に文字セットのソートルールを設定できます。インスタンス文字セットは、システムデータのソートルール（つまり、大文字と小文字の属性区別、アクセント記号の属性区別、バイナリかどうか）を提供します。データベースのソートルールの選択により、データベース内の関連する操作の結果に影響します。
show collationコマンドを使用すると、文字セットルールを表示できます。
**事例**：
```
show collation where charset ='utf8mb4';
```
**ソートルールについて**

| ソートルールオプション | 説明 | 
|---------|---------|
| _CS | 大文字と小文字を区別します。| 
| _CI | 大文字と小文字を区別しません。| 
| _AS | アクセント文字と非アクセント文字を区別します。例えば、「a」と「ấ」は異なる文字です。| 
| _AI | アクセントを区別しません。| 
| _BIN | バイナリ。| 

**文字セット接尾辞について**

| インスタンス文字セット接尾辞 | 説明 | 
|---------|---------|
|_CI_AI|大文字と小文字、アクセント記号を区別しません。|
|_CI_AS|大文字と小文字を区別しませんが、アクセント記号を区別します。|
|_CS_AI|大文字と小文字を区別しますが、アクセント記号を区別しません。|
|_CS_AS|大文字と小文字、アクセント記号を区別します。|

### lower_case_table_namesパラメータの変更に失敗してしまいます。どうすればよいですか。
コンソールからパラメータlower_case_table_namesを変更できます：1に設定し、大文字と小文字を区別しません。 次の2つの点に注意してください：
- このパラメーターを変更すると、データベースが再起動されます。
- インスタンスのデータベース、テーブルがすべて小文字であるかどうか確認する必要があります。大文字のデータベーステーブル名がある場合は、それらをすべて小文字に変更してからパラメータを変更する必要があります。変更しない場合、エラーが報告されます。
- バージョン8.0ではこのパラメータを修正できません。バージョン8.0では、デフォルトで大文字と小文字が区別されます。

大文字のテーブルがあるかどうか調べます：
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
大文字のデータベースがあるかどうか調べます。
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```
