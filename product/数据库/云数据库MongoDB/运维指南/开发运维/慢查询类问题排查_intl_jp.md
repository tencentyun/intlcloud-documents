MongoDBを使用するときにリクエストの遅延が明らかに長くなると判明したとき、次のステップでトラブルシューティングできます。<br>
1. インスタンスのリクエスト遅延監視指標に異常があるかどうかをチェックしてください。
インスタンスの監視データをチェックします。下図に示すように、時間遅延監視指標は主にリクエストがアクセス層に到着した時点から処理を完了した後にクライアントに戻すまでの時間を反映します。リクエストの時間遅延が高い場合、mongodにスローログが存在するかチェックする必要があります。
![](https://main.qcloudimg.com/raw/d67c9fad80b03829168fbd92ad095378.png)

 参考手順は次のとおりです。<br>
2. 現在のmongodにスローログが存在するかどうかを確認します。
[TencentDB for MongoDBコンソール](https://console.cloud.tencent.com/mongodb)にログインし、インスタンスのスローログを確認し、下図に示すように、抽象クエリを選択してください。
![](https://main.qcloudimg.com/raw/19a7b1568cf38f6b493cb5088cfdff93.png)
command、COLLSCAN、IXSCAN、keysExamined、docsExaminedなどのキーワードに注意してください。その他のログについては、[MongoDB公式サイト](https://docs.mongodb.com/manual/reference/log-messages/index.html)を参照してください。
以下のキーワードに注意してください。
 - commandはスローログに記録される操作を指し示します。
 - COLLSCANはこのクエリによる全テーブルスキャン、IXSCANは索引スキャンを示します。その他のフィールドの記述については、[MongoDB公式サイト](https://docs.mongodb.com/manual/reference/explain-results/index.html)を参照してください。<br>
 - keysExaminedは索引スキャンエントリを示し、docsExaminedはドキュメントスキャンエントリを示します。keysExaminedとdocsExaminedが多いほど、索引が作成されていない可能性または索引の差別が小さい可能性が高くなります。索引の作成フィールドを確認してください。<br>
 
 
3. フォアグラウンドでの索引の作成によりリクエストがロックされるかどうかを確認してください
業務のクリエに使用される索引に問題が存在しない場合、現時点で業務の忙しい時間帯にフォアグラウンドの索引作成操作を行ったかどうかを確認してください。1つのセットに索引を作成するときにフォアグラウンド方式（backgroundの値がfalse）がデフォルト方式であれば、この操作が他のすべての操作をフォアグラウンドの索引作成完了までブロックします。バックグラウンド方式で索引を作成する場合、索引を作成する期間に、MongoDBが依然として読み取り・書き込み操作サービスを正常に提供できますが、バックグラウンドの索引作成方式にも欠点があります。すなわち、バックグラウンド方式の索引作成は索引作成時間を長くする場合があります。具体的な索引作成オプションについては、[MongoDB公式サイト](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/)を参照してください。<br>
currentOpコマンドで現在索引を作成する進捗を確認できます。具体的なコマンドを次に示します。

  
	db.currentOp(
        {
          $or: [
            { op: "command", "query.createIndexes": { $exists: true } },
            { op: "insert", ns: /\.system\.indexes\b/ }
          ]
        }
        )
戻り値は下図のとおりです。msgフィールドが現在索引を作成する進捗を示し、locksフィールドがこの操作のロックタイプを示します。その他のロックについては、[MongoDB公式サイト](https://docs.mongodb.com/v3.2/reference/database-profiler/)を参照してください。<br>
![](https://main.qcloudimg.com/raw/355b6c06539ad6a5e3980b90bd200bf0.png)
![](https://main.qcloudimg.com/raw/155583329a2eb2a99575a2b5ce0b8647.png)<br>

4. mongos負荷が高いかどうかをチェックします。
時間遅延監視指標は、主にリクエストがアクセス層に到着した時点から処理を完了した後にクライアントに戻すまでの時間を反映します。mongodにスロー操作がないと確認したがリクエストの時間遅延が高いと確認した場合、mongos負荷が高いことが原因である可能性があります。mongos負荷が高くなる原因がさまざまあります。例えば、業務が一瞬で大量の接続を確立することによりmongos負荷が高くなる可能性があるか、または、複数のシャードのデータをまとめる必要があるのでmongos負荷が高くなる可能性があります。この場合、mongosを再起動します。下図のように、mongosの再起動はコンソールで実行できます。<br>
![](https://main.qcloudimg.com/raw/0ab109e9a0adad49c3d96660132ea290.png)
> !mongosの再起動によってインスタンスのすべての接続が再起動の一瞬で中断されます。業務を再接続するとよいので、業務に影響し続ける可能性がありません。

