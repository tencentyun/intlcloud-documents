
### MongoDB接続切断は、どのように操作しますか？
[接続例](https://cloud.tencent.com/document/product/240/3563)を参照して、認証の問題を排除してください。

### MongoDBは「Remote server has closed the connection」という情報を表示する場合は？
まず[接続例](https://cloud.tencent.com/document/product/240/3563)を参照して、認証の問題を排除してください。接続できてもこの問題が解決しない場合は、再接続メカニズムを実装する必要があります。詳細については、[再接続例](https://cloud.tencent.com/document/product/240/4980)を参照してください。

### WiredTiger 3.2にはロックテーブルの問題がありますが、クラウドバージョンのMongoDBにも同様の問題がありますか？
具体的な問題に従って分析する必要があります。たとえば、デフォルトのインデックス作成では確実にグローバルロックが追加され、また、ユーザーはfsynclockコマンドを実行する場合もロックされます。
ロックはデータベースの機能です。同時アクセスに関する一連の問題に対処するには、ビジネスの通常の実行に影響を与えない限り、通常のロックが必須です。

### MongoDBはどのバージョンのドライバーを選ぶべきですか？
最新のバージョンを使用することをお勧めします。例えば、PHPはmongo-1.6以上を選択できます。
 
### MongoDBはどんな言語接続方式を提供しますか？
TencentDB for MongoDBは、Shell、PHP、Node.js、Java、Pythonなどの複数の言語接続方式を提供します。詳細は、[接続例](https://cloud.tencent.com/document/product/240/3563)を参照してください。

### TencentDB for MongoDBバージョンではどの言語のクライアント接続がサポートされていますか？
TencentDB for MongoDBバージョンはMongoDBのクライアント接続と完全に互換性があります。公式のMongoDBバージョンがサポートされているクライアントである限り、TencentDB for MongoDBは全部サポートします。たとえば、C、C++、c＃、java、node.js、python、php、perlなどです。詳細については、[MongoDBの公式ドキュメント](https://docs.mongodb.org/ecosystem/drivers/)を参照してください。

### shellでTencentDB for MongoDBを接続する方法は？
詳細については、[Shellの接続例](https://cloud.tencent.com/doc/product/240/3978)を参照してください。

### ビジネスプログラムでMongoDBに接続するURIは何ですか？
詳細については、[接続例](https://cloud.tencent.com/doc/product/240/3563)を参照してください。

### meteorなどの各種類のフレームワークとクラスライブラリで、TencentDB for MongoDBに接続できないのですが、どうすれば対処できますか？
一般的には、接続方式とURIのつなぎ合わせエラーです。まず確認してください。

### PHPでMongoDBの最大接続数を設定する方法は？
MongoDBドライバー（[PHP公式Webサイトのドキュメント](http://php.net/manual/en/set.mongodb.php)）は、接続URLでmaxPoolSizeパラメータを構成することで接続数を制御できます。
MongoDBドライバー（[PHP公式Webサイトのドキュメント](http://php.net/manual/en/set.mongodb.php)）は、Mongo::setPoolSize() 方法を通して接続数を設定できます。詳細については、[MongoPool::setSize](http://php.net/manual/en/mongopool.setsize.php)を参照してください。
 

### MongoDB接続数の制限は何ですか？
![イメージの説明](//bot1024-1253841380.file.myqcloud.com/3defdf809c3d11e7bd8b525400a3183e.png)
接続数の上限は、ノードレベルではなく、インスタンスレベルのものです。詳細については、[制限の説明](https://cloud.tencent.com/document/product/240/622)を参照してください。
 
### MongoDBを手動で再接続する方法は？
TencentDB for Mongoデータベースサービスは単純なmongodアクセスを提供しておらず、ユーザーにはCLB IPが与えられ、このIPの後にはmongosのような一連のルーティングアクセスレイヤに接続されます。
クライアントドライバーは、CLB IPを介してアクセスサーバーと長時間の接続を確立します。接続が長期間アクティブであれば、Tencent Cloudはそれに干渉しませんが、長時間の接続が1日以上アイドル状態であれば（この時間はバージョンの最適化で調整されます）、ルーティングアクセスレイヤはこの接続を解除します。
一般に、クライアントドライバーは自動再接続プロセスを実装していますが、一部の言語ドライバーは実装されていません。自動再接続を実装していない言語ドライバーの場合、ユーザーが解除された接続を使用してTencentDB for MongoDBサービスと通信しようとすると、「Remote server has closed the connection」などのエラーメッセージが表示されるため、手動で再接続する必要があります。これはPHP再接続のdemoです。

**PHP mongoドライバーに基づく再接続の実装** 
![イメージの説明](//bot1024-1253841380.file.myqcloud.com/aa398f929c4211e79a34525400a3183e.png)


### mongooseを使ってTencentDB for MongoDBに接続する方法は？
mongooseがTencentDB for MongoDBに接続するパラメータは以下の通りです。

``` 
var dbUri = " mongodb:// " + user + " : " +password + " @ " +host + ":" +port + " / " + dbName;

var opts = {
　　auth：｛
　　　　authMechanism : ' MONDODB-CR'
      ｝
}；
var connection = mongodb.createConnection(dbUri, opts);
```

### MongoDBは外部ネットワーク接続をサポートしますか？
MongoDBは現在プライベートネットワーク接続のみをサポートしています。接続方式は、[接続例](https://cloud.tencent.com/document/product/240/3563)を参照してください。
現在、外部ネットワークアクセスをサポートしていません。ローカルにMongoDBに接続したい場合は、MongoDBと同じアカウントと同じプライベートネットワークサーバーをポートとして、転送して実装できます。
 

