
## gRPCのインストール
1. 前提条件： インストールするNodejsのバージョンがv12.16.0以上であること。
2. gRPCをインストールします。
<dx-alert infotype="explain" title="">
具体的な手順については、[gRPC Nodejsインストールの説明](https://github.com/grpc/grpc/tree/master/examples/node)をご参照ください。
</dx-alert>


## サービスの定義

gRPCは、protocol buffersを利用してサービスの定義を実現します。1つのRPCのサービスに､パラメータとリターンタイプによってリモートの呼び出しが可能なメソッドが指定されます。
<dx-alert infotype="explain" title="">
サービスを定義したprotoファイルを提供していますので、[protoファイル](https://intl.cloud.tencent.com/document/product/1055/37419)からダウンロードしてご利用ください。ご自身で生成する必要はありません。
</dx-alert>



## gRPCコードの生成 
1. サービスを定義した後、 protocol bufferコンパイラprotocを利用して、クライアントとサーバーのコードを生成します（gRPCがサポートする任意の言語）。 
2. 生成するコードには、クライアントのstubとサーバーに実装したい抽象インターフェースが含まれています。
3. gRPCコードを生成します。
    Nodejsバージョンは、grpc/proto-loaderを使用して直接pbファイルをローディングします。gRPC-nodejsコードを生成する必要はありません。

## ゲームプロセス統合の流れ
![](https://main.qcloudimg.com/raw/96018551bc88c71a02333b1f197b3111.png)

#### Game Serverコールバックインターフェースのリスト

| インターフェース名 | インターフェース機能|
|-----|----|
|[OnHealthCheck](https://intl.cloud.tencent.com/document/product/1055/37422)| ヘルスチェック|
|[OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423)|ゲームサーバーセッションの受け入れ|
|[OnProcessTerminate](https://intl.cloud.tencent.com/document/product/1055/37424)|ゲームプロセスの終了|

####  Game Serverアクティブコールインターフェースのリスト

| インターフェース名 | インターフェース機能 |
|-----|----|
|[ProcessReady](https://intl.cloud.tencent.com/document/product/1055/37426)|プロセス準備完了|
|[ActivateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37427)|ゲームサーバーセッションのアクティベート|
|[AcceptPlayerSession](https://intl.cloud.tencent.com/document/product/1055/37428)|プレイヤーセッションの受け入れ|
|[RemovePlayerSession](https://intl.cloud.tencent.com/document/product/1055/37429)|プレイヤーセッションの削除|
|[DescribePlayerSessions](https://intl.cloud.tencent.com/document/product/1055/37430)|プレイヤーセッションリストの取得|
|[UpdatePlayerSessionCreationPolicy](https://intl.cloud.tencent.com/document/product/1055/37431)|プレイヤーセッション作成ポリシーの更新|
|[TerminateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37432)|ゲームサーバーセッションの終了|
|[ProcessEnding](https://intl.cloud.tencent.com/document/product/1055/37434)|プロセス終了|
|[ReportCustomData](https://intl.cloud.tencent.com/document/product/1055/37435)|カスタムデータ報告|

#### その他

 リクエストmeta。ゲームプロセスがgRPCを利用して、Game Serverアクティブコールインターフェースを呼び出すときは、gRPCリクエストのmetaに2つのフィールドを追加する必要があります。

| フィールド      | 意味                                      | タイプ   |
| --------- | ----------------------------------------- | ------ |
| pid       | 現在のゲームプロセスのpid                         | string |
| requestId | 現在のリクエストのrequestId。一意のタグを使いリクエスト | string |

 1. 通常は、サーバーの初期化後、プロセスが対外的にサービス提供可能かセルフチェックします。Game ServerがProcessReadyインターフェースを呼び出して、プロセスの準備が完了し、ゲームサーバーセッションのホスティングの準備ができたことをGSEに通知します。GSEはこれを受信した後、サーバーインスタンスのステータスを「アクティブ」に変更します。
```
function ProcessReady(param) {
		console.log("ProcessReady.request", param);
		getGseGrpcSdkServiceClient().ProcessReady({
				//ログパス
				logPathsToUpload: param.logPathsToUpload,
				//ポート設定
				clientPort: param.clientPort,
				grpcPort: param.grpcPort
		}, getMetadata(), function (err, response) {
				//準備完了。対外的にサービス提供可能
				console.log('ProcessReady.response:', err, response);
		});
}
```
 2. プロセス準備完了後、GSEがOnHealthCheckインターフェースを呼び出し、Game Serverに対してヘルスチェックを実施します。1分ごとに1回検査し、連続3回失敗するとそのプロセスを異常と判定し、ゲームサーバーセッションをこのプロセスにアサインしません。
```
function OnHealthCheck(call, callback) {
		console.log("OnHealthCheck.request", call.request);

		callback(null, {healthStatus: gsesdkClient.IsProcessHealth() });
}
```
 3. Clientが [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)インターフェースを呼び出して、ゲームサーバーセッションを作成し、このゲームサーバーセッションを1つのプロセスにアサインしたため、GSEがトリガーされて当該プロセスのonStartGameServerSessionインターフェースを呼び出し、GameServerSessionのステータスを「アクティベート中」に変更します。
```
function OnStartGameServerSession(call, callback) {
		console.log("OnStartGameServerSession.request", call.request);
		gsesdkClient.OnStartGameServerSession(call.request);
		callback(null, {});
}
```
 4. Game Serverが onStartGameServerSessionを受信し、あなたが自らいくつかのロジックまたはリソースのアサインを処理して準備が完了すると、Game ServerがActivateGameServerSessionインターフェースを呼び出します。ゲームサーバーセッションがプロセスにすでにアサインされ、現在、プレイヤーのリクエストを受け入れる準備ができていることをGSEに通知し、サーバーのステータスを「アクティブ」に変更します。
```
function ActivateGameServerSession(param, w, callback) {
		console.log("ActivateGameServerSession.request", param);
		getGseGrpcSdkServiceClient().ActivateGameServerSession({
				gameServerSessionId: gameServerSession.gameServerSessionId,
				maxPlayers: param.maxPlayers
		}, getMetadata(), function (err, response) {
				console.log('ActivateGameServerSession.response:', err, response);
				if (callback != null) {
						callback(w, response);
				}
		});
}
```
 5. Clientが[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130)インターフェースを呼び出してプレイヤーが参加すると、Game ServerがAcceptPlayerSessionインターフェースを呼び出してプレイヤーの合法性を検証します。接続が受け入れられた場合は、PlayerSessionのステータスを「アクティブ」に変更します。ClientがJoinGameServerSessionインターフェースを呼び出して60秒以内に応答がない場合は、PlayerSessionのステータスを「タイムアウト」に変更し、その後再び JoinGameServerSessionを呼び出します。
```
function AcceptPlayerSession(param, w, callback) {
		console.log("AcceptPlayerSession.request", param);
		getGseGrpcSdkServiceClient().AcceptPlayerSession({
				gameServerSessionId: gameServerSession.gameServerSessionId,
				playerSessionId: param.playerSessionId
		}, getMetadata(), function (err, response) {
				console.log('AcceptPlayerSession.response:', err, response);
				if (callback != null) {
						callback(w, response);
				}
		});
}
```
 6. ゲーム終了またはプレイヤーの退出後、Game ServerがRemovePlayerSessionインターフェースを呼び出してプレイヤーを削除します。playersessionのステータスを「完了」 に変更し、ゲームサーバーセッションの中のプレイヤーの位置をリザーブします。
```
function RemovePlayerSession(param, w, callback) {
		console.log("RemovePlayerSession.request", param);
		getGseGrpcSdkServiceClient().RemovePlayerSession({
				gameServerSessionId: gameServerSession.gameServerSessionId,
				playerSessionId: param.playerSessionId
		}, getMetadata(), function (err, response) {
				console.log('RemovePlayerSession.response:', err, response);
				if (callback != null) {
						callback(w, response);
				}
		});
}
```
 7. 1つのゲームサーバーセッション（1組のゲームの対戦または1つのサービス）が終了すると、Game ServerがTerminateGameServerSessionインターフェースを呼び出してGameServerSessionを終了し、GameServerSessionのステータスを「終了」に変更します。
```
function TerminateGameServerSession(param, w, callback) {
		console.log("TerminateGameServerSession.request", param);
		getGseGrpcSdkServiceClient().TerminateGameServerSession({
				gameServerSessionId: gameServerSession.gameServerSessionId
		}, getMetadata(), function (err, response) {
				console.log('TerminateGameServerSession.response:', response);
				if (callback != null) {
						callback(w, response);
				}
		});
}
```
 8. ヘルスチェックに失敗したかまたは容量縮小の時は、GSEがOnProcessTerminateインターフェースを呼び出してゲームプロセスを終了します。容量縮小時は、GSEコンソールで設定した[保護ポリシー]((https://intl.cloud.tencent.com/document/product/1055/36675)を根拠とします。
```
function OnProcessTerminate(call, callback) {
		console.log("OnProcessTerminate.request", call.request);
		callback(null, {});
}
```
 9. Game ServerがProcessEndingインターフェースを呼び出してプロセスを直ちに終了させ、サーバープロセスのステータスを「終了」に変更してリソースを回収します。
```
//自動呼び出し：ゲーム1局につき1つのプロセスが対応し、1局のゲームが終了すると自動でProcessEndingインターフェースを呼び出します
//手動呼び出し：容量縮小またはプロセスの異常によりヘルスチェックに失敗した時は、保護ポリシーにもとづき受動的にProcessEndingインターフェースが呼び出されます。完全保護および時間制限保護ポリシーを設定している時は、先にゲームサーバーセッション上のプレイヤーの有無を判断してから、手動で呼び出しを行う必要があります
function ProcessEnding(param, callback) {
		console.log("ProcessEnding.request", param);
		getGseGrpcSdkServiceClient().ProcessEnding({}, getMetadata(), function (err, response) {
				console.log('ProcessEnding.response:', response);
				if (callback != null) {
						callback(response);
				}
		});
}
```
 10. Game ServerがDescribePlayerSessionsインターフェースを呼び出してゲームサーバーセッション下のプレイヤー情報を取得します（業務に応じて任意選択）。
```
function DescribePlayerSessions(param, w, callback) {
		console.log("DescribePlayerSessions.request", param);
		getGseGrpcSdkServiceClient().DescribePlayerSessions({
				gameServerSessionId: gameServerSession.gameServerSessionId,
				playerSessionId: param.playerSessionId,
				playerId: param.playerId,
				playerSessionStatusFilter: param.playerSessionStatusFilter,
				nextToken: param.nextToken,
				limit: param.limit
		}, getMetadata(), function (err, response) {
				console.log('DescribePlayerSessions.response:', err, response);
				if (callback != null) {
						callback(w, response);
				}
		});
}
```
 11. Game ServerがUpdatePlayerSessionCreationPolicyインターフェースを呼び出してプレイヤーセッションの作成ポリシーを更新し、新規プレイヤーの受け入れの是非、つまりゲームセッションにプレイヤーの参加を許可するかを設定します（業務に応じて任意選択）。
```
function UpdatePlayerSessionCreationPolicy(param, w, callback) {
		console.log("UpdatePlayerSessionCreationPolicy.request", param);
		getGseGrpcSdkServiceClient().UpdatePlayerSessionCreationPolicy({
				gameServerSessionId: gameServerSession.gameServerSessionId,
				newPlayerSessionCreationPolicy: param.newPlayerSessionCreationPolicy
		}, getMetadata(), function (err, response) {
				console.log('UpdatePlayerSessionCreationPolicy.response:', err, response);
				if (callback != null) {
						callback(w, response);
				}
		});
}
```
 12. Game ServerがReportCustomDataインターフェースを呼び出し、GSEにカスタムデータを通知します（業務に応じて任意選択）。
```
function ReportCustomData(param, w, callback) {
		console.log("ReportCustomData.request", param);
		getGseGrpcSdkServiceClient().ReportCustomData({
				currentCustomCount: Number(param.currentCustomCount),
				maxCustomCount: Number(param.maxCustomCount)
		}, getMetadata(), function (err, response) {
				console.log('ReportCustomData.response:', response);
				if (callback != null) {
						callback(w, response);
				}
		});
}
```

## GSEをコールするためにサーバーを起動します。

サーバーの実行：GrpcServerを起動します。
```
function startGameServer() {
  var server = new grpc.Server();
  server.addService(GameServerGrpcSdkServiceProto.GameServerGrpcSdkService.service, {
       OnHealthCheck: OnHealthCheck,
       OnProcessTerminate: OnProcessTerminate,
       OnStartGameServerSession: OnStartGameServerSession
      });
  server.bind('0.0.0.0:7000', grpc.ServerCredentials.createInsecure());
  server.start();
  gsesdkClient.ProcessReady({
    logPathsToUpload: [
      "./log/path/1",
      "./log/path/2"
    ],
    clientPort: 2000,
    grpcPort: 7000
  });
}
```

## クライアントをGSEのgRPCサーバーに接続
サーバーに接続：gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使ってスタブインスタンスを作成します。
```
function getGseGrpcSdkServiceClient() {
  if (gseGrpcClient == null) {
    gseGrpcClient = new GseGrpcSdkServiceProto.GseGrpcSdkService('127.0.0.1:5758', grpc.credentials.createInsecure());
  }
  return gseGrpcClient;
}
```

## Nodejs DEMO
 1. [ここをクリック](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/nodejs-demo.zip)して、Nodejs DEMO コードをダウンロードします。
 2. gRPCコードを生成します。
Nodejsバージョンは、grpc/proto-loaderを使用して直接pbファイルをローディングします。gRPC-nodejsコードを生成する必要はありません。
 3. GSEをコールするためにサーバーを起動します。
  - サーバーの実装。
nodejs-demo/dynamic_code ディレクトリの下の game_server.jsに、サーバーの3つのインターフェースを実装しています。
  - サーバーの実行。
nodejs-demo/dynamic_codeディレクトリ下のgame_server.jsで、GrpcServerを起動します。
 4. クライアントをGSEのgRPCサーバーに接続します。
  - クライアントの実装。
nodejs-demo/dynamic_codeディレクトリ下のgsesdk_client.jsに、クライアントの9つのインターフェースを実装しています。
  - サーバーに接続。
gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使用してスタブインスタンスを作成します。
 5. コンパイルして実行
  1. nodejsをインストールします。バージョンはv12.16.0以上です。
  - grpcパッケージをインストールします。
 ```
cnpm install --save grpc-tools
cnpm install --save google-protobuf 
cnpm install --save grpc
cnpm install --save @grpc/proto-loader
cnpm install --save @grpc/grpc-js
 ```
 海外のサーバーノードで依存パッケージをダウンロードできない場合は、国内のnpmサイトを設定する必要があります。
  - コードをダウンロードし、nodejs-demoディレクトリ下で、次のコマンドを実行してテストを起動します。
	```
	cd dynamic_code
	node game_server.js  
 ```
  - 実行可能ファイルgame_server.jsをパッケージングして [アセット](https://intl.cloud.tencent.com/document/product/1055/36674)を作成します。起動パスの設定はnode、起動パラメータの設定はgame_server.jsです。
  - その後、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)でサーバーフリートを作成し、アセットをサーバーフリートにデプロイします。この後引き続き、[スケーリング](https://intl.cloud.tencent.com/document/product/1055/37445) などの一連の操作を行うことができます。
