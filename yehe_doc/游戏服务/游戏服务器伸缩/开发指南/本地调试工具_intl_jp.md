## GSE Localの説明

GSE Localは、ゲームサーバーホスティングサービスGSEを個別に起動できるコマンドラインツールです。GSE Localは、さらにサーバープロセスの初期化、ヘルスチェック、API呼び出しと応答のためのランタイム実行中のログも提供します。

GSE Localの使用は、GSEホスティングサービスの起動とローカルデバイスでのゲーム統合テストに限定されます。このツールを使用することで、ゲームのデバッグ時間が大幅に短縮され、反復型開発の効率が向上します。これを使用しない場合、新規生成された各ゲームパッケージをGSEにアップロードし、サーバーフリートをゲームをホストするように構成する必要があります。

GSEを介して、次の内容を検証できます。
*ゲームサーバーが、GSEサーバー開発キットと適切に統合され、GSEサービスと適正に通信し、新規ゲームセッションを開始し、新規プレイヤーを受け入れ、実行ステータスを報告しているか。
* ゲームクライアントがGSE関連のTencentCloudのAPIと適切に統合され、既存のゲームセッションの情報を取得し、新規ゲームセッションを開始し、プレイヤーをゲームに参加させ、ゲームセッションに接続できているか。




## GSE Localの設定


GSE Localは、Windows、LinuxおよびMacで実行でき、GSEがサポートする言語で使用できます。ローカルデバッグツールのインストールパッケージは次のとおりです。
- [Windowsローカルデバッグツールのダウンロード](https://gselocal-1301007756.cos.ap-nanjing.myqcloud.com/gse-local/gselocal-master-windows-amd64.exe)
- [Linuxローカルデバッグツールのダウンロード](https://gselocal-1301007756.cos.ap-nanjing.myqcloud.com/gse-local/gselocal-master-linux-amd64)
- [Macローカルデバッグツールのダウンロード](https://gselocal-1301007756.cos.ap-nanjing.myqcloud.com/gse-local/gselocal-master-darwin-amd64)


>?以下のサンプルコードは、Linuxおよびmacosオペレーティングシステムに適しています。Windowsオペレーティングシステムでcurlコマンドを実行する場合は、gitbashコマンドラインツールを使用することをお勧めします。
>

<span id="test"></span>
## ゲームサーバーのテスト

ゲームサーバーのみをテストする必要がある場合は、curlを直接使用してゲームクライアントのGSEローカルサービスに対する呼び出しをシミュレートできます。このようにしてゲームサーバーが期待どおりに次の操作を実行するかどうかを検証します。
1. 起動プロセス中に、ゲームサーバーは、GSEにサーバーがゲームサーバーセッションをホストする準備ができていることを通知します（ProcessReadyを呼び出します）。
2. 実行時にゲームサーバーは、1分毎に、実行状況をGSEに送信します（onHealthCheakコールバックを使用します）。
3. ゲームサーバーはリクエストに応答し、新規ゲームセッションを立ち上げます（onStartGameServerSessionコールバックをトリガーし、コールバックでactivateGameServerSessionを呼び出します）。

### 手順1：GSE Localの起動

コマンドプロンプトウィンドウを開き、gselocal_windows、gselocal_linuxまたはgselocal_macディレクトリに移動してプログラムを実行します。このテキストでは、Macを例に説明します。ローカルで `./gselocal_mac` を起動すると、プログラムは自動的にGSEローカルに接続されます。
端末で次のコマンドを入力します。
```
./gselocal_mac
```
コマンドプロンプトウィンドウに次の情報が表示された場合は、起動が成功したことを意味します。
```
{"level":"info","ts":"2020-10-20T09:16:09.364+0800","msg":"start grpc v3 server success"}
```



### 手順2：ゲームサーバーの起動

プログラミングツールまたはコマンドラインツールでゲームプロセスを開始します。ゲームプロセスが開始されると、ProcessReadyが呼び出され、プロセスがセッションをホストする準備ができていることが表示されると同時に、次のログ情報が出力されます。
```
Getting process ready, LogPath: System.String[], ClientPort: 3237, GrpcPort: 6224
Process ready succeed, resp: { }
Server Start On Locolhost:6224
```
Gse Localは、ProcessReadyリクエストを受け取り、ログ情報を出力し、ヘルスチェックを実行します。
```
{"level":"info","ts":"2020-10-20T09:27:03.172+0800","msg":"ProcessReady Info is","pid":"41688","requestId":"3b38495b38bc4ef8a59ae8****a8256d","info":"clientPort:3237 grpcPort:6224 "}
{"level":"info","ts":"2020-10-20T09:27:03.172+0800","msg":"set runner success","pid":"41688","processUUID":"527bf89b-d128-4b5d-bfea-****3d22ede7"}
{"level":"info","ts":"2020-10-20T09:28:03.276+0800","msg":"onHealthCheck received","pid":"41688","health":true}
{"level":"info","ts":"2020-10-20T09:29:03.256+0800","msg":"onHealthCheck received","pid":"41688","health":true}
{"level":"info","ts":"2020-10-20T09:30:03.261+0800","msg":"onHealthCheck received","pid":"41688","health":true}
```




### 手順3：curlを使用してデバッグし、ゲームサーバーセッションとプレイヤーセッションを作成

ローカルでcurlを使用してクライアント呼び出しをシミュレートします。具体的なパラメータについては [TencentCloud APIインターフェース](https://intl.cloud.tencent.com/document/product/1055/37120)をご参照ください。

<span id="test1"></span>
#### ゲームサーバーセッションの作成

Localについては、FleetIdパラメータを任意の有効な文字列 `(^fleet-\S+)`に設定できます。次のコマンドを実行しFleetIdパラメータを設定します。
```
curl -d '{"Action":"CreateGameServerSession", "FleetId":"fleet-1235", "MaximumPlayerSessionCount":5}' http://127.0.0.1:8080/capi
```

LocalコマンドプロンプトウィンドウのログメッセージにはGSEローカルがonStartGameServerSession コールバックをゲームサーバーに送信したことが表示されます。ゲームサーバーセッションの作成に成功した場合、ゲームサーバーはActivateGameServerSessionを呼び出して応答します。ログメッセージは次のとおりです。
```
{"level":"info","ts":"2020-10-20T09:37:08.580+0800","msg":"API to use: GSE.CreateGameServerSession, with input","req":"FleetId:<value:\"fleet-1235\" > MaximumPlayerSessionCount:<value:5 > "}
{"level":"info","ts":"2020-10-20T09:37:08.580+0800","msg":"Reserved process: 41688 for GameServerSession: qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
{"level":"info","ts":"2020-10-20T09:37:08.580+0800","msg":"start to call StartGameSessionByGrpc to game server","gameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
{"level":"info","ts":"2020-10-20T09:37:08.597+0800","msg":"onGameSessionActivate received","pid":"4****","gameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe","requestId":"de1a678dea364db4b487ff84ad****31"}
{"level":"info","ts":"2020-10-20T09:37:08.598+0800","msg":"call StartGameSessionByGrpc to game server success","gameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
```

#### ゲームサーバーセッションの確認

curlコマンドを介して、GSEはゲームサーバーセッションIDを含むゲームサーバーセッションオブジェクトを渡します。新規ゲームサーバーセッションのステータスが“Activating”であることに注意してください。ゲームサーバーセッションが ActivateGameServerSession を呼び出すと、ステータスが“Active”に変更されます。変更されたステータスを表示する場合は、curlを使用して DescribeGameServerSessions を呼び出し、次のコマンドを実行してください。
```
curl -d '{"Action":"DescribeGameServerSessions", "FleetId":"fleet-1235"}' http://127.0.0.1:8080/capi
```
確認の結果は次のとおりです。
```
{"Response":{"GameServerSessions":[{"AvailabilityStatus":"Enable","CreationTime":"2020-10-20T01:37:08Z","CreatorId":"","CurrentCustomCount":0,"CurrentPlayerSessionCount":0,"DnsName":"","FleetId":"fleet-1235","GameProperties":[],"GameServerSessionData":"","GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-2fa56a09bffe","InstanceType":"localhost","IpAddress":"127.0.0.1","MatchmakerData":"","MaxCustomCount":0,"MaximumPlayerSessionCount":5,"Name":"","PlayerSessionCreationPolicy":"ACCEPT_ALL","Port":3237,"Status":"ACTIVE","StatusReason":"","TerminationTime":null,"Weight":0}],"NextToken":"","RequestId":"s1603158295201357000"}}
```

<span id="test4"></span>
##  ゲームサーバーとクライアントのテスト

### 前提条件
[ゲームサーバーテスト](#test) が完了していること。

### 手順1：プレイヤーの追加
次のコマンドを実行し、プレイヤーを追加します。 GameServerSessionId は[ゲームサーバーセッションの作成](#test1) でインターフェースから返送されるGameServerSessionIdです。
```
curl -d '{"Action":"JoinGameServerSession", "GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe", "PlayerId":"k****111"}' http://127.0.0.1:8080/capi
```

Localコマンドプロンプトウィンドウのログメッセージには、ゲームサーバーが新規プレイヤーの接続を検証するためにAcceptPlayerSessionリクエストを送信したことが表示されます。
```
{"level":"info","ts":"2020-10-20T10:03:43.096+0800","msg":"API to use: GSE.JoinGameServerSession, with input","req":"GameServerSessionId:\"qcs::gse:local::gameserversession/fleet-****/gssess-c648654a-293b-4f1f-b71f-****6a09bffe\" PlayerId:\"ka****11\" "}
{"level":"info","ts":"2020-10-20T10:03:43.096+0800","msg":"Creating player session with id: kadin111 for gameServersessionId: qcs::gse:local::gameserversession/fleet-****/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
{"level":"info","ts":"2020-10-20T10:03:43.096+0800","msg":"Created player session with PlayerId: kadin111 and PlayerSessionId: psess-56dd6f48-08d4-4a11-9330-****09784977"}
```

### 手順2：プレイヤーセッションのクエリー

DescribePlayerSessionsを呼び出し、プレイヤーセッションをクエリーします。プレイヤーセッションの初期状態は「Reserved」です。
- クライアントが1分以内にゲームサーバーへの接続に成功すると、ステータスは「Active」に変更されます。
- 1分経過してもクライアントがゲームサーバーに接続しない場合、ステータスは「TIMEDOUT」に変更されます。

```
curl -d '{"Action":"DescribePlayerSessions", "GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-2fa56a09bffe", "PlayerId":"kadin111"}' http://127.0.0.1:8080/capi
```
クエリーの結果：
```
{"Response":{"NextToken":"","PlayerSessions":[{"CreationTime":"2020-10-20T02:03:43Z","DnsName":"","FleetId":"fleet-****","GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe","IpAddress":"127.*.*.1","PlayerData":"","PlayerId":"ka****11","PlayerSessionId":"psess-56dd6f48-08d4-4a11-9330-****09784977","Port":3237,"Status":"TIMEDOUT","TerminationTime":"1970-01-01T00:00:00Z"}],"RequestId":"s16031596094****2000"}}% 
```

### 手順3：クライアントプレイヤーのサーバーへの接続

ゲームセッションとプレイヤーセッションを作成した後、ゲームセッションとの直接接続が確立されます。クライアントプレイヤーは `localhost：port` を使用して接続します。

Localコマンドプロンプトウィンドウのログメッセージには、ゲームサーバーが新規プレイヤーの接続を検証するためにAcceptPlayerSessionリクエストを送信したことが表示されます。curlを使用してDescribePlayerSessionsを呼び出す場合、プレイヤーセッションのステータスは「Reserved」から 「Active」に変更される必要があります。


### 手順4：検証レポートの GSEへの送信
ゲームサーバーがゲームとプレイヤーのステータスをGSEサービスに送信中であることを検証します。GSEにプレイヤーのニーズを管理させ、メトリックスを正しく報告する必要があり、ゲームサーバーは各種ステータスをGSEに送信する必要があります。またローカルが以下のアクションに関連するイベントを記録していることを検証します。さらにcurlを使用してステータスの変更を追跡することもできます。
* **プレイヤーのゲームセッションからの切断**
GSE LocalログメッセージはゲームサーバーがRemovePlayerSessionを呼び出したことを表示する必要があります。DescribePlayerSessions() に対するステータスが「Active」から「Completed」に変更されます。またDescribeGameServerSessionsを呼び出してゲームセッションの現在のプレイヤー数が1人減少したことをチェックすることもできます。
* **ゲームセッションの終了**
GSE Localログメッセージにはゲームサーバーが TerminateGameServerSession を呼び出したことが表示されます。DescribeGameServerSessionsに対するステータスが「Active」から「Terminated」（または「Terminating」）に変更されます。
* **サーバープロセスの終了**
GSE Localログメッセージには、ゲームサーバーがProcessEndingを呼び出したことが表示されます。

## ゲームクライアントのGSEサービスに対する呼び出しのテスト

[ゲームサーバーのテスト](#test)と[ゲームサーバーとクライアントのテスト] (#test4)では、ゲームセッションとプレイヤーセッションのAPIを呼び出します。これらはすべてcurlを使用してGSE Localを呼び出しますが、ゲームサービスにおいて呼び出す場合は、コードを使用して呼び出すことができます。ローカルデバッグでは `http://127.0.0.1:8080/capi` を呼び出してゲームサービスが正常に実行されているかどうかを検証する必要があり、次のAPIの呼び出しを行うことができます。
- [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)
- [DescribeGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37136)
- [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)
- [JoinGameServerSessionBatch](https://intl.cloud.tencent.com/document/product/1055/39130)
- [DescribePlayerSessions](https://intl.cloud.tencent.com/document/product/1055/37135)

Localコマンドプロンプトウィンドウでは、CreateGameServerSessionを呼び出す場合に限り、ログメッセージが表示されます。ログメッセージには、GSEローカルがゲームセッションを開始するタイミング（onStartGameServerSession コールバック）が提示され、ゲームサーバーがそれを呼び出せば、ActivateGameServerSessionの取得に成功することが表示されます。その他APIの呼び出しステータスについては、上記のcurlを使用して表示できます。

##  その他説明

GSE Localを使用する場合は、次の点に注意してください。
1. GSE Webサービスとは異なり、Localはサーバーのステータスを追跡せずに、onProcessTerminateコールバックを開始します。 またLocalはゲームサーバーが実行状態レポートの記録を停止するだけです。
2. Tencent Cloud Development Toolkitに対する呼び出しでは、FleetIdは検証されません。このパラメータは任意の有効な文字列 `(`(^fleet-\S+)` に設定できるからです。
3. Localを使用して作成されたゲームセッションIDは異なる構造となります。それらIDには文字列localが含まれ、具体的な例は次のとおりです。
```
arn:gse:local::gamesession/fleet-****/gsess-56961f8e-db9c-4173-97e7-****82f0daa6
```




