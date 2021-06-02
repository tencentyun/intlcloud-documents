### TencentDB for MySQLインスタンスの設定パラメータをどのように変更しますか。
- **MySQLコンソールによる方法**
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンス名をクリックして管理ページに進み、【データベース管理】>【パラメータ設定】を選択します。通常、var_nameには次の変数が含まれています。
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

- **phpMyAdminコンソールによる方法**
phpMyAdminによりTencentDB for MySQLインスタンスにログインした後、トップメニューの【変数】をクリックし、下の変数リストで変更する必要のある変数に対応する【編集】をクリックし、それを変更後、【保存】をクリックします。
![](https://main.qcloudimg.com/raw/214fec618ff4e166c6e4d747be3fea0b.png)

その他の設定パラメータはTencentDB for MySQLコンソールの【データベース管理】＞【パラメータ設定】ページで確認することができます。

### MySQLで中国語クエリをどのように設定しますか。
MySQLは現在、中国語をサポートしていません。

### MySQLでスケジューラー機能を有効にするにはどうすればよいですか。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンス名をクリックして管理ページに進み、【データベース管理】>【パラメータ設定】ページを選択し、パラメータ設定でevent_schedulerパラメータをONに設定します。

### MySQLのタイムアウト接続設定が短すぎますが、どのように時間を増やしますか。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンス名をクリックして管理ページに進み、【データベース管理】>【パラメータ設定】ページを選択し、パラメータ設定でwait_timeoutパラメータを変更します。

### MySQLのgroup_concat_max_lenパラメータをどのように変更しますか。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)で、インスタンス名をクリックして管理ページに進み、【データベース管理】>【パラメータ設定】ページを選択し、パラメータ設定でgroup_concat_max_lenパラメータを変更します。

###　MySQLでフルテーブルスキャンのSQLステートメントはどうやって見つけられますか。
デフォルトはフルテーブルスキャンのステートメントを記録しません。MySQLコンソールの【パラメータ設定】でlog_queries_not_using_indexesパラメータをONに設定することができますが、ONにする時間を長すぎないようにしてください。

### MySQLのデフォルトの文字セットはどのように変更しますか。
MySQLのデフォルトの文字セットはUTF8です。現在、LATIN1、GBK、UTF8、UTF8MB4の4種類の文字セットを設定することができます。

MySQLはデフォルトの文字セットの設定をサポートしますが、テーブルを作成するとき、テーブルのエンコーディングを明示的に指定し、接続の確立時に接続のエンコーディングを指定することをお勧めします。これにより、お客様のアプリケーションがより優れた移植性を有します。MySQLのデフォルトの文字セットの説明および変更方法については、<a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">使用制限</a>をご参照するか、[コンソール](https://console.cloud.tencent.com/cdb)で文字セットを変更することもできます。　　

### lower_case_table_namesパラメータの変更に失敗してしまいます。どうすればよいですか。
コンソールからパラメータlower_case_table_namesを変更できます：1に設定し、大文字と小文字を区別しません。 次の2つの点に注意する必要があります。
- このパラメーターを変更すると、データベースが再起動されます。
- インスタンスのデータベース、テーブルがすべて小文字であるかどうか確認する必要があります。大文字のデータベーステーブル名がある場合は、それらをすべて小文字に変更してからパラメータを変更する必要があります。変更しない場合、エラーが報告されます。- 
- バージョン8.0ではこのパラメータを修正できません。バージョン8.0では、デフォルトで大文字と小文字が区別されます。

