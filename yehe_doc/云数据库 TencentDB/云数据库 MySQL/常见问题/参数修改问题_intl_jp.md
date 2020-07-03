### MySQLの構成パラメーターをどのように変更しますか？
- **MySQLコンソールによる方法**
[MySQLコンソール](https://console.cloud.tencent.com/cdb)でインスタンス名をクリックして管理ページに進み、【データベースの管理】＞【パラメーターの設定】を選択し、そのうち一般的なvar\_nameは以下の変数を含みます。
<table class="t">
<tbody><tr>
<th>変数
</th><th>説明
</th></tr>
<tr>
<td> character_set_server
</td><td>サーバーのデフォルト文字セット
</td></tr>
<tr>
<td> connect_timeout
</td><td>接続タイムアウト
</td></tr>
<tr>
<td> long_query_time
</td><td>この時間を超えるクエリはスロークエリです
</td></tr>
<tr>
<td> max_allowed_packet
</td><td>最大パック長
</td></tr>
<tr>
<td> max_connections
</td><td>最大接続数
</td></tr>
<tr>
<td> sql_mode
</td><td>現在のサーバーのSQLモード
</td></tr>
<tr>
<td> table_open_cache
</td><td>すべてのスレッドで開いているテーブルの個数で、この数値が大きくなるとmysqldの開くことを要求されたファイルの記述子個数が増えます。
</td></tr>
<tr>
<td> wait_timeout
</td><td>非インタラクティブ接続のタイムアウト時間
</td></tr></tbody></table>

- **phpMyAdminコンソールによる方法**
phpMyAdminによりMySQLにログインした後、上のメニュー中の【変数】をクリックし、下の変数リストで変更する必要のある変数に対応する【編集】をクリックし、それを変更後、【保存】をクリックします。
![](https://main.qcloudimg.com/raw/214fec618ff4e166c6e4d747be3fea0b.png)

その他の構成パラメータはコンソールの【データベースの管理】＞【パラメーターの設定】ページで確認することができます。

### MySQLで日本語クエリをどのように設定しますか？
MySQLは現在、日本語文字をサポートしていません。

### MySQLのタイマー機能の有効化をどのように設定しますか？
[MySQLコンソール](https://console.cloud.tencent.com/cdb)でインスタンス名をクリックして管理ページに入り、【データベースの管理】＞【パラメーターの設定】ページを選択し、パラメーターの設定でevent_schedulerのパラメータの設定をONにします。

### MySQLのタイムアウト接続設定が短すぎますが、どのように時間を増やしますか？
[MySQLコンソール](https://console.cloud.tencent.com/cdb)でインスタンス名をクリックして管理ページに進み、【データベースの管理】＞【パラメーターの設定】ページを選択し、パラメーターの設定でwait_timeoutパラメーターを変更します。

### MySQLはどのようにgroup_concat_max_lenパラメーターを調整しますか？
[MySQLコンソール](https://console.cloud.tencent.com/cdb)でインスタンス名をクリックして管理ページに進み、【データベースの管理】＞【パラメーターの設定】ページを選択し、パラメーターの設定でgroup_concat_max_lenパラメーターを変更します。

###　MySQL全テーブルスキャンのSQLステートメントはどうやって見つけられますか？
デフォルトは全テーブルスキャンのステートメントを記録しません。MySQLコンソールの【パラメーター設定】でlog_queries_not_using_indexesパラメーターをONに設定することができますが、あまり長くONにしないで下さい。

### CDBのデフォルト文字セットコードはどのように変更しますか？
CDBはMySQLデータベースと同じで、デフォルトの文字セットのエンコード形式はLATIN1、即ちISO-8859-1エンコード形式です。開発者はCDBコンソールでServer端末のデータベース文字セットを修正することができます。現在、LATIN1 、GBK、UTF8 、UTF8MB4の4種類の文字セットの設定をサポートしています。

CDBはデフォルトの文字セットのエンコード設定をサポートしていますが、当社ではお客様のテーブル作成時に、テーブルのエンコードを明示的に指定し、かつ接続確立時に接続するエンコードを指定することをお勧めします。これにより、お客様のアプリケーションがより優れた移植性を有します。デフォルトの文字セットの説明および変更方法は、<a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">使用制限</a>をご参照ください。CDBコンソールで文字セットを変更することができます。
