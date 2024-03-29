## ユースケース
指定時間を超過したSQLステートメントクエリを「スロークエリ」といいます。対応するステートメントは「スロークエリステートメント」といい、データベース管理者(DBA)はスロークエリステートメントを分析し、スロークエリが生じた原因を探し出す過程を「スロークエリ分析」といいます。

コンソールの【操作ログ】ページで、インスタンスのスローログの詳細、エラーログの詳細、ロールバックログの表示およびスローログのダウンロードを行うことができます。コマンドラインインターフェイス(CLI)またはTencentDB APIを使用してデータベースログを閲覧しダウンロードすることもできます。詳細については、[スロークエリログのクエリ](https://intl.cloud.tencent.com/document/product/236/15845)および[バイナリログのクエリ](https://intl.cloud.tencent.com/document/product/236/15843)をご参照ください。

>?TencentDB for MySQL単一ノードクラウドディスクバージョンのインスタンスは現在、スローログのダウンロードおよびロールバック機能をサポートしていません。
>

#### MySQLスロークエリ関連の説明
- long_query_time：スロークエリの閾値パラメータで、精度はマイクロ秒クラスまででき、デフォルトは10sです。SQLステートメントの実行時間がこの数値を超過すると、スローログに記録されます。 
long_query_timeパラメータを調整すれば、元のスローログに影響することはありません。例えば、スローログの閾値パラメータが10sであれば、10sを超過したスローログが報告されます。この値を1に変更しても、元々報告していたログはそのまま表示されます。
- log_queries_not_using_indexes：未使用のインデックスの照会を記録するかどうかについてで、デフォルトはOFFです。

## 操作手順
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストのインスタンスIDまたは**操作**列の**管理**をクリックして、インスタンス管理ページに進みます。
2. インスタンス管理ページで、**操作ログ**画面を選択すると、インスタンスのスローログ明細、エラーログ明細、ロールバックログ、スローログダウンロードを選択、確認できます。
<table>
<thead><tr><th>機能項目</th><th>説明</th></tr></thead>
<tbody><tr>
<td>スローログの明細</td><td>1か月以内にデータベースで実行時間が10秒を超えたSQLステートメントを記録</td></tr>
<tr>
<td>スローログダウンロード</td><td>スローログダウンロードの提供</td></tr>
<tr>
<td>エラーログの明細</ td> <td>各起動とシャットダウンの詳細情報、および操作中のより深刻な警告とエラーメッセージをすべて記録します</ td> </ tr>
<tr>
<td>ロールバックログ</td><td>ロールバックタスクの実行状態と進捗を記録</td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/eb38248f51697df8b79798e02690f426.png"  style="margin:0;">

3. スローログのダウンロードページで、**操作**カラムの**ダウンロード**をクリックしてスローログをダウンロードします。
4. ポップアップしたダイアログボックスでダウンロード先をコピーし、[クラウドデータベースが存在するVPC内のCVM（Linux OS）にログイン](https://www.tencentcloud.com/document/product/213/10517)し、wgetコマンドを実行して、プライベートネットワークから高速でダウンロードすることをお勧めします。
>?
>- サイズが0KBのログはダウンロードできません。
>- **ローカルダウンロード**を選択して直接ダウンロードすることもできますが、時間がかかります。
>- wgetコマンド形式：wget -c 'ログファイルのダウンロードアドレス' -O カスタマイズファイル名.log
>
例：
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```

