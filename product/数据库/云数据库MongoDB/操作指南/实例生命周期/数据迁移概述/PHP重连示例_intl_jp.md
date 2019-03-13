##　説明

TencentDB for MongoDBデータベースサービスは単純なmongodアクセスを提供しておらず、ユーザーにはCLB IPが与えられ、このIPの後にはmongosのような一連のルーティングアクセスレイヤに接続されます。
クライアントドライバーは、CLB IPを介してアクセスサーバーと長時間の接続を確立します。接続が長期間アクティブであれば、私たちはそれに干渉しませんが、長時間の接続が1日以上アイドル状態であれば（この時間はバージョンの最適化で調整されます）、ルーティングアクセスレイヤはこの接続を解除します。
一般に、クライアントドライバーは自動再接続プロセスを実装していますが、一部の言語ドライバーは実装されていません。自動再接続を実装していない言語ドライバーの場合、ユーザーが解除された接続を使用してTencentDB for MongoDBサービスと通信しようとすると、「Remote server has closed the connection」などのエラーメッセージが表示されるため、手動で再接続する必要があります。これはPHP再接続のdemoです。

## PHP mongoドライバーに基づく再接続の実装
```
<?php

function getConnection() {
    $connection = false;
    $uri = 'mongodb://rwuser:1234567a@10.66.148.142:27017/admin?authMechanism=MONGODB-CR';
    $maxRetries = 5;
    for( $counts = 1; $counts <= $maxRetries; $counts++ ) {
        try {
            $connection = new MongoClient($uri);
        } catch( Exception $e ) {
     // あるいは、必要に応じて次のcatchコードラインを使用します。「\」に注意してください。これは、一部のフレームワークがネームスペースを使用する場合に必要です。
     // } catch( \Exception $e ) {
            continue;
        }
        break;
    }
    return $connection;
}

$connection = getConnection();

if($connection) {
		$db = $connection->testdb;
		$collection = $db->testcollection;

		$one = $collection->findOne();

		var_dump($one);
}
```


