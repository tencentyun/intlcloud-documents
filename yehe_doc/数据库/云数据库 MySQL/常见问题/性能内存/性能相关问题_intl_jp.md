### MySQLインスタンスのストレージスペースの使用状況をどのように表示しますか。
 [DBbrainコンソール](https://console.cloud.tencent.com/dbbrain)にログインし、左側のナビゲーションウィンドウで【Performance Optimization】を選択し、上の対応するデータベースを選択して、【 Space Analysis 】ページを選択します。 
スペース分析ページには、過去1週間の1日あたり増加率、ディスク領域の空き容量、使用可能な予定日数、および過去1週間のディスク領域使用傾向表を表示できます。また、インスタンス内のデータベースの各テーブルの占有領域の詳細と断片化の状態も表示できます。
![](https://main.qcloudimg.com/raw/612e0641f7c2c09c6d5f820d56d8f1e4.png)

### TencentDB for MySQLインスタンスの完全なSQL実行トラックを分析するにはどうすればよいですか。
[DBbrainコンソール](https://console.cloud.tencent.com/dbbrain)にログインし、左側のナビゲーションウィンドウで【Performance Optimization】を選択し、上の対応するデータベースを選択して、【Audit Log Analysis】ページを選択します。
1. ビューの右上にある【Create Analysis Task】をクリックし、時間帯を選択して【OK】をクリックします。
2. タスクリストで【View SQL Analysis】をクリックし、SQL分析ページに進みます。
[](https://main.qcloudimg.com/raw/fbf88dd9624dd0378e13902f3f8b7157.png)
3. SQL分析ページでは、SQL Type、Host、UserまたはSQL Codeディメンションのビューを選択できます。また、時間帯を選択してビューを伸縮させて特定の時点のデータを表示できます。
![](https://main.qcloudimg.com/raw/e20326e6719f18a5dac27bec64fa1182.png)
4. SQLテンプレートの特定の行をクリックすると、右側にSQL文の詳細がポップアップ表示されます。 
 - 分析ページでは、特定のSQL文を表示、コピーできます。提示された最適化アドバイスまたは説明に従ってSQL文を最適化します。
 - 統計ページでは、Host、User、SQL CodeディメンションにおけるこのSQLの統計分析および実行時間トラックを表示できます。

### MySQLインスタンスに障害や異常が発生した場合、最適化を実行するにはどうすればよい​ですか。
1. [DBbrainコンソール](https://console.cloud.tencent.com/dbbrain)にログインし、左側のナビゲーションウィンドウで【Performance Optimization】を選択し、上の対応するデータベースを選択して、【Exception Diagnosis 】ページを選択します。
2. 「Diagnosis Prompt」バーには、レベル、開始時間、診断項目、継続時間など、診断イベント履歴の概要情報が表示されます。DBbrainでは、インスタンスの健康チェックが定期的に行われます。
![](https://main.qcloudimg.com/raw/fe0dd650bb834eb093e7964917da758e.png)
3. 【View Details】または「Diagnosis Prompt」バーの診断項目をクリックすると、診断詳細ページに進みます。ビューで「診断イベント」をクリックすると、イベントの概要、現象の説明、インテリジェント分析および専門家のアドバイスなど、このイベントの詳細が表示されます。専門家のアドバイスに基づいて最適化することで、データベースの異常を解決し、インスタンスの性能を向上させることができます。
 ![](https://main.qcloudimg.com/raw/576a445b12b249f278d50cbe89ab238e.png)

### MySQLヘルスレポートをどのように定期的に取得しますか。
1. [DBbrainコンソール](https://console.cloud.tencent.com/dbbrain)にログインし、左側のナビゲーションウィンドウで【Performance Optimization】を選択し、上の対応するデータベースを選択して、【Health Report】ページを選択すると、選択した時間帯のヘルススコアの傾向と問題の概要が表示されます。 
- レポートの時間範囲を設定し、【ヘルスレポートの作成】をクリックすると、タスクの完了後にその時間帯のヘルスレポートを表示またはダウンロードできます。  
- 【 Regular Generation Settings】をクリックして、ヘルスレポートの自動生成期間を設定できます。 
 ![](https://main.qcloudimg.com/raw/0cf1ac4dd76a106cde20f854086c38f7.png)

### MySQLのスローログをどのように表示、最適化しますか。
1. [DBbrainコンソール](https://console.cloud.tencent.com/dbbrain)にログインし、左側のナビゲーションウィンドウで【Performance Optimization】を選択し、上の対応するデータベースを選択して、【Slow SQL Analysis】ページを選択します。「SQL Analysis」バーには、インスタンスのスロークエリ数とCPU使用率が表示されます。
2. SQL統計グラフのスロークエリをクリックまたは選択すると、下に集約SQLテンプレートと実行情報が表示されます。各列のデータは正順または逆順のソートをサポートしています。右側のかかる時間の分布には、選択した時間帯におけるSQLのかかる時間の全体的な分布が表示されます。
 ![](https://main.qcloudimg.com/raw/c937f9639acc557e9cb58eb885f36805.png)
3. 集約されたSQLテンプレートの特定の行をクリックすると、右側にSQLの最適化アドバイスと統計情報が表示されます。最適化アドバイスに応じてSQLを変更するか、適切なインデックスを追加することで、SQLの実行効率、データベースの性能が向上します。
 

### MySQLがタスクを実行するときにデッドロックになるのはなぜですか。
同時発生する操作がロック待機をもたらすためで、正常な現象です。

### MySQLの中国語データに文字化けが生じるのはなぜですか。
TencentDB for MySQLにデータを保存する場合は、[MySQLコンソール](https://console.cloud.tencent.com/cdb) にログインし、インスタンス詳細画面に入ってそのインスタンスのデフォルトの文字セットをご確認ください。プログラム作成時に`character_set_client`、`character_set_results`、および`character_set_connection`をTencentDBインスタンスと同じ文字セットに設定します。そうしないと、保存したデータに中国語が含まれている場合、中国語データに文字化けが生じます。
例えば、TencentDBインスタンスのデフォルトの文字セットはutf8です。インスタンスに接続するプログラムを作成するときは、中国語のデータを保存する前に、次のステートメントを実行する必要があります。
```
SET NAMES 'utf8';
```

### MySQLへの接続数が最大値に達した場合の問題の一般的な理由と解決策は何ですか。
- sleepスレッド数が多い場合は、コンソールでwait_timeoutおよびinteractive_timeoutパラメータ値を低く調整することをお勧めします。
- スロークエリのスタックの場合、long_query_timeパラメーターはデフォルトで10秒で、1s - 2sに変更してから、スロークエリログを観察することをお勧めします。
- sleepスレッド数が少なく、スロークエリもスタックしていない場合は、コンソールでmax_connectionsパラメータ値を大きく調整することをお勧めします。

### MySQLのCPU使用率が高くなってしまう原因と解決策は何ですか。
- スロークエリのスタックの場合は、インスタンスモニターでスロークエリと全表スキャンを確認して、スロークエリログ（コンソールでダウンロード可能）を参照して、分析と最適化を実行してください。モニターにスロークエリがなく、全表スキャンだけがある場合は、コンソールでlong_query_timeの値を1s-2sに変更し、TencentDB for MySQLをしばらく使用した後、スロークエリを再度分析することをお勧めします。
- スロークエリがスタックしていない場合は、インスタンスモニターでメモリ使用率を確認してください。インスタンスの仕様を超えていて、かつディスクの読み込み/書き込み量が明らかに増えていれば、メモリにボトルネックが発生しているので、メモリをアップグレードすることをお勧めします。

### ユーザーが普段に注意を払わなければならないインスタンスの監視メトリックは何ですか。
CPU使用率、メモリ使用率、ディスク領域使用率。実際の状況に応じて [アラームを設定](https://intl.cloud.tencent.com/document/product/236/8457)できます。アラームが表示された場合、適切な措置を講じてアラームを削除することができます

### 複数のインスタンスの容量使用状況はどのように確認しますか。
- [DBbrainコンソール](https://console.cloud.tencent.com/dbbrain)にログインし、インスタンスの概要で、アカウントの下にあるインスタンスの概要情報を表示します。
- または、[getmonitordata](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=GetMonitorData&SignVersion=)インターフェースを使用して、複数のインスタンスの容量使用状況を表示します。
