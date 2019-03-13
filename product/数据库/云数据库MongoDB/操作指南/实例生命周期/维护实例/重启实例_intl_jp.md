## 説明　##
TencentDB for MongoDBのアーキテクチャによって決まりますが、インスタンスの再起動は、Mongosの再起動とMongodの再起動に分けられます。インスタンスの再起動によって接続が切断され、特に、Mongodを再起動するときにデータの書き込みがあると、rollbackを引き起こす可能性があるため、データが失われます。再起動中、TencentDB for MongoDBインスタンスは正常的なサービスを提供できなくなりますので、ビジネスに影響を与えないように事前に準備してください。現在、Mongodの再起動はホワイトリストの管理下にあります。必要な場合は、チケットを提出してご連絡ください。再起動は危険性の高い操作です。慎重に取り扱ってください。
## 操作ガイド ##
Tencent Cloudの公式Webサイトにログインし、[TencentDB for MongoDBコンソール](https://console.cloud.tencent.com/mongodb)にアクセスして、レプリカセットまたはシャードインスタンスリストに移動します。再起動するインスタンスを選択し、【再起動】ボタンをクリックして操作を実行してください。詳細は以下のとおりです。
![](https://main.qcloudimg.com/raw/f9970b086c8d84dee900e72e320f2fbf.png)
2番目の方法は、各インスタンスの【操作】-【その他】-【再起動】をクリックすることです。詳細は以下のとおりです。
![](https://main.qcloudimg.com/raw/712e6bc5b00ede03cccf0855affe0d22.png)
「再起動」をクリックすると、ポップアップは次のとおりです。
![](https://main.qcloudimg.com/raw/b6331e32eb64212ceb7fc4bed98ddff7.png)
再起動する必要があるコンポーネントを選択し、OKをクリックして、タスクが完了するのを待ちます。

