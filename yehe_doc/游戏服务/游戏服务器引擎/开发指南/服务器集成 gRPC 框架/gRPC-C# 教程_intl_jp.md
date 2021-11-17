
## gRPCのインストール
1. gRPC C#を使用する場合には、先に.Net Core 3.1 SDKをインストールする必要があります。CentOSを例にとると、バージョンはCentOS 7またはCentOS 8以上にする必要があります。
  - 署名キーを追加する
```
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm```
 - .NET Core SDKをインストールする
```
 sudo yum install dotnet-sdk-3.1```
2. その上、次の実行環境 /IDEで gRPC C#を使用することもできます。
 - Windows：.NET Framework 4.5以上のバージョン、Visual Studio 2013以上のバージョン、Visual Studio Code。
 - Linux：Mono 4以上のバージョン、Visual Studio Code。
 - Mac OS X：Mono 4以上のバージョン、Visual Studio Code、Visual Studio for Mac。


<dx-alert infotype="explain" title="">
 インストール手順の詳細については、[gRPC C#のインストール](https://github.com/grpc/grpc/blob/v1.30.0/src/csharp/README.md#prerequisites)をご参照ください。
</dx-alert>




## サービスの定義
 プロトコル バッファを使用してRPCサービスを定義し、gRPCクライアントインターフェースを生成します。RPCサービスは、パラメータとリターンタイプを使用してリモートで呼び出すことができるメソッドを指定します。

>?サービス定義用の.protoファイルを提供します。[protoファイル](https://intl.cloud.tencent.com/document/product/1055/37419) からダウンロードしてご利用ください。

## gRPCコードの生成 
1. サービスを定義した後、protoc（プロトコルバッファコンパイラ）を使用してクライアントとサーバーのコードを生成します（gRPCがサポートする任意の言語）。 
2. 生成されたコードには、クライアントのstubとサーバーによって実装される抽象インターフェースが含まれています。
3. gRPCコード生成の手順：
     - コードをダウンロードします。csharp-demoディレクトリで、次のコマンドを実行します。
       ```
       dotnet run
       ```
         自動的にコンパイルされ、サービスを実行します。
     - プログラムがコンパイルされて正しく実行されると、プロジェクトが依存するライブラリとバイナリファイル、およびprotoファイルのコンパイルによって作成された.csファイルがcsharp-demo/obj/Debug/netcoreapp3.1フォルダーに生成されます。
     - protoファイルは csharp-demo/csharpdemo.csproj の中にインポートされます。
       ```
       <Protobuf Include="..\proto\csharp-demo\GameServerGrpcSdkService.proto" Link="GameServerGrpcSdkService.proto"/>
       <Protobuf Include="..\proto\csharp-demo\GseGrpcSdkService.proto" Link="GseGrpcSdkService.proto" />
       ```
       プロジェクトはproto/csharp-demoフォルダの中の GameServerGrpcSdkService.protoと GseGrpcSdkService.protoの2つのprotoファイルに依存します。

## ゲームプロセス統合の流れ
![](https://main.qcloudimg.com/raw/96018551bc88c71a02333b1f197b3111.png)

####  Game Serverコールバックインターフェイスリスト

| インターフェース名 | インターフェース機能|
|-----|----|
|[OnHealthCheck](https://intl.cloud.tencent.com/document/product/1055/37422)| ヘルスチェック|
|[OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423)|ゲームサーバーセッションの受信|
|[OnProcessTerminate](https://intl.cloud.tencent.com/document/product/1055/37424)|ゲームプロセスの終了|

#### Game Server 呼び出しインターフェイスリスト

| インターフェース名 | インターフェース機能 |
|-----|----|
|[ProcessReady](https://intl.cloud.tencent.com/document/product/1055/37426)|プロセス準備完了|
|[ActivateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37427)|ゲームサーバーセッションのアクティブ化|
|[AcceptPlayerSession](https://intl.cloud.tencent.com/document/product/1055/37428)|プレイヤーセッションの受信|
|[RemovePlayerSession](https://intl.cloud.tencent.com/document/product/1055/37429)|プレイヤーセッションの削除|
|[DescribePlayerSessions](https://intl.cloud.tencent.com/document/product/1055/37430)|プレイヤーセッションリストの取得|
|[UpdatePlayerSessionCreationPolicy](https://intl.cloud.tencent.com/document/product/1055/37431)|プレイヤーセッション作成ポリシーの更新|
|[TerminateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37432)|ゲームサーバーセッションの終了|
|[ProcessEnding](https://intl.cloud.tencent.com/document/product/1055/37434)|プロセスの終了|
|[ReportCustomData](https://intl.cloud.tencent.com/document/product/1055/37435)|カスタムデータ報告|

#### その他

 ゲームプロセスがgRPCを介してゲームサーバーのインターフェースを呼び出す場合、gRPCリクエストのメタに2つのフィールドを追加する必要があります。

| フィールド      | 意味                                      | タイプ   |
| --------- | ----------------------------------------- | ------ |
| pid       | 現在のゲームプロセスのpid                         | string |
| requestId | 現在のリクエストのrequestId。リクエストを一意に識別するために使用されます | string |

1. 通常、サーバーの初期化後、プロセスはサービスを提供できるかどうかを確認するために自身をチェックし、ゲームサーバーはProcessReadyインターフェースを呼び出して、プロセスの準備が完了し、ゲームサーバーセッションのホスティングの準備ができたことをGSEに通知します。GSEはこれを受信した後、サーバーインスタンスのステータスを「アクティブ」に変更します。
```
public static GseResponse ProcessReady(string[] logPath, int clientPort, int grpcPort)
{
	logger.Println($"Getting process ready, LogPath: {logPath}, ClientPort: {clientPort}, GrpcPort: {grpcPort}");
	//ポートを設定
	var req = new ProcessReadyRequest{
		ClientPort = clientPort,
		GrpcPort = grpcPort,
	};
	//ログパス
	req.LogPathsToUpload.Add(logPath);         //repeatedタイプは、pb解析後、読み取り専用タイプとなり、Add追加が必要           
	//準備完了。対外的にサービス提供可能
	return GrpcClient.GseClient.ProcessReady(req, meta);
}
```
2. プロセスの準備ができたら、GSEはOnHealthCheckインターフェースを呼び出し、ゲームサーバーに対してヘルスチェックを実行します。1分ごとに1回チェックし、3回連続で失敗するとプロセスが異常であると判定し、ゲームサーバーセッションをこのプロセスに割り当てられません。
```
public override Task<HealthCheckResponse> OnHealthCheck(HealthCheckRequest request, ServerCallContext context)
{
	logger.Println($"OnHealthCheck, HealthStatus: {GseManager.HealthStatus}");
	return Task.FromResult(new HealthCheckResponse{
			HealthStatus = GseManager.HealthStatus
	});
}
```
3.クライアントが [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)インターフェースを呼び出して、ゲームサーバーセッションを作成し、このゲームサーバーセッションをプロセスに割り当てるため、GSEがトリガーされて当該プロセスのonStartGameServerSessionインターフェースを呼び出し、GameServerSessionのステータスを「アクティベート中」に変更します。
```java
public override Task<GseResponse> OnStartGameServerSession(StartGameServerSessionRequest request, ServerCallContext context)
{
	logger.Println($"OnStartGameServerSession, request: {request}");
	GseManager.SetGameServerSession(request.GameServerSession);
	var resp = GseManager.ActivateGameServerSession(request.GameServerSession.GameServerSessionId, request.GameServerSession.MaxPlayers);
	return Task.FromResult(resp);
}
```
4. ゲームサーバーが onStartGameServerSessionを受信した後、ロジックまたはリソースの割り当てを自分で処理する必要があります。全ての準備が完了すると、ゲームサーバーがActivateGameServerSessionインターフェースを呼び出します。ゲームサーバーセッションがプロセスにすでにアサインされ、現在、プレイヤーのリクエストを受け入れる準備ができていることをGSEに通知し、サーバーのステータスを「アクティブ」に変更します。
<dx-codeblock>
::: java
public static GseResponse ActivateGameServerSession(string gameServerSessionId, int maxPlayers)
{
	logger.Println($"Activating game server session, GameServerSessionId: {gameServerSessionId}, MaxPlayers: {maxPlayers}");
	var req = new ActivateGameServerSessionRequest{
			GameServerSessionId = gameServerSessionId,
			MaxPlayers = maxPlayers,
	};  
	return GrpcClient.GseClient.ActivateGameServerSession(req, meta);
}
:::
</dx-codeblock>
5. Clientが[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130)インターフェースを呼び出してプレイヤーが参加すると、Game ServerがAcceptPlayerSessionインターフェースを呼び出してプレイヤーの合法性を検証します。接続が受け入れられた場合は、PlayerSessionのステータスを「アクティブ」に変更します。ClientがJoinGameServerSessionインターフェースを呼び出して60秒以内に応答がない場合は、PlayerSessionのステータスを「タイムアウト」に変更し、その後再び JoinGameServerSessionを呼び出します。
<dx-codeblock>
::: java
public static GseResponse AcceptPlayerSession(string playerSessionId)
{
	logger.Println($"Accepting player session, PlayerSessionId: {playerSessionId}");
	var req = new AcceptPlayerSessionRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId,
			PlayerSessionId = playerSessionId,
	};            
	return GrpcClient.GseClient.AcceptPlayerSession(req, meta);
}
:::
</dx-codeblock>
6. ゲーム終了またはプレイヤーの退出後、Game ServerがRemovePlayerSessionインターフェースを呼び出してプレイヤーを削除します。playersessionのステータスを「完了」 に変更し、ゲームサーバーセッションの中のプレイヤーの位置をリザーブします。
<dx-codeblock>
::: java 
public static GseResponse RemovePlayerSession(string playerSessionId)
{
	logger.Println($"Removing player session, PlayerSessionId: {playerSessionId}");
	var req = new RemovePlayerSessionRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId,
			PlayerSessionId = playerSessionId,
	};            
	return GrpcClient.GseClient.RemovePlayerSession(req, meta);
}
:::
</dx-codeblock>
7. 1つのゲームサーバーセッション（1組のゲームの対戦または1つのサービス）が終了すると、Game ServerがTerminateGameServerSessionインターフェースを呼び出してGameServerSessionを終了し、GameServerSessionのステータスを「終了」に変更します。
<dx-codeblock>
::: java 
public static GseResponse TerminateGameServerSession()
{
	logger.Println($"Terminating game server session, GameServerSessionId: {gameServerSession.GameServerSessionId}");
	var req = new TerminateGameServerSessionRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId
	};            
	return GrpcClient.GseClient.TerminateGameServerSession(req, meta);
}
:::
</dx-codeblock>
8. ヘルスチェックに失敗したかまたは容量縮小の時は、GSEがOnProcessTerminateインターフェースを呼び出してゲームプロセスを終了します。容量縮小時の根拠は、GSEコンソールで設定した[保護ポリシー](https://intl.cloud.tencent.com/document/product/1055/36675#test12)です。
<dx-codeblock>
::: java 
 public override Task<GseResponse> OnProcessTerminate(ProcessTerminateRequest request, ServerCallContext context)
{
		logger.Println($"OnProcessTerminate, request: {request}");
		// プロセス終了時間の設定
		GseManager.SetTerminationTime(request.TerminationTime);
		//次の2つのインターフェースを呼び出すと、ゲームサーバーセッションが直ちに終了します。プレイヤーがいなくなったか、またはゲームサーバーセッションがなくなってから、ProcessEndingを呼び出してプロセスを終了することをお勧めします
		//次の2つのインターフェースを呼び出さない場合は、保護ポリシーに基づきProcessEndingを呼び出してプロセスを終了します。時間制限を設定して保護することをお勧めします

		// ゲームサーバーセッションの終了
		GseManager.TerminateGameServerSession();
		// プロセスの終了
		GseManager.ProcessEnding();
		return Task.FromResult(new GseResponse{
				Status = GseResponse.Types.Status.Ok,
				ResponseData = "SUCCESS",
		});
}
:::
</dx-codeblock>
9. Game ServerがProcessEndingインターフェースを呼び出してプロセスを直ちに終了させ、サーバープロセスのステータスを「終了」に変更してリソースを回収します。
<dx-codeblock>
::: java 
//自動呼び出し：ゲーム1局につき1つのプロセスが対応し、1局のゲームが終了すると自動でProcessEndingインターフェースを呼び出します
//手動呼び出し：容量縮小またはプロセスの異常によりヘルスチェックに失敗した時は、保護ポリシーにもとづき受動的にProcessEndingインターフェースが呼び出されます。完全保護および時間制限保護ポリシーを設定している時は、先にゲームサーバーセッション上のプレイヤーの有無を判断してから、手動で呼び出しを行う必要があります
public static GseResponse ProcessEnding()
{
	logger.Println($"Process ending, pid: {pid}");
	var req = new ProcessEndingRequest();            
	return GrpcClient.GseClient.ProcessEnding(req, meta);
}
:::
</dx-codeblock>
10. Game ServerがDescribePlayerSessionsインターフェースを呼び出してゲームサーバーセッション下のプレイヤー情報を取得します（業務に応じて任意選択）。
<dx-codeblock>
::: java 
public static DescribePlayerSessionsResponse DescribePlayerSessions(string gameServerSessionId, string playerId, string playerSessionId, string playerSessionStatusFilter, string nextToken, int limit)
{
	logger.Println($"Describing player session, GameServerSessionId: {gameServerSessionId}, PlayerId: {playerId}, PlayerSessionId: {playerSessionId}, PlayerSessionStatusFilter: {playerSessionStatusFilter}, NextToken: {nextToken}, Limit: {limit}");
	var req = new DescribePlayerSessionsRequest{
			GameServerSessionId = gameServerSessionId,
			PlayerId = playerId,
			PlayerSessionId = playerSessionId,
			PlayerSessionStatusFilter = playerSessionStatusFilter,
			NextToken = nextToken,
			Limit = limit,
	};            
	return GrpcClient.GseClient.DescribePlayerSessions(req, meta);
}
:::
</dx-codeblock>
11. Game ServerがUpdatePlayerSessionCreationPolicyインターフェースを呼び出してプレイヤーセッションの作成ポリシーを更新し、新規プレイヤーの受け入れの是非、つまりゲームセッションにプレイヤーの参加を許可するかを設定します（業務に応じて任意選択）。
<dx-codeblock>
::: java
public static GseResponse UpdatePlayerSessionCreationPolicy(string newPolicy)
{
	logger.Println($"Updating player session creation policy, newPolicy: {newPolicy}");
	var req = new UpdatePlayerSessionCreationPolicyRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId,
			NewPlayerSessionCreationPolicy = newPolicy,
	};            
	return GrpcClient.GseClient.UpdatePlayerSessionCreationPolicy(req, meta);
}
:::
</dx-codeblock>
12. Game ServerがReportCustomDataインターフェースを呼び出し、GSEにカスタムデータを通知します（業務に応じて任意選択）。
<dx-codeblock>
::: java
public static GseResponse ReportCustomData(int currentCustomCount, int maxCustomCount)
{
	logger.Println($"Reporting custom data, CurrentCustomCount: {currentCustomCount}, MaxCustomCount: {maxCustomCount}");
	var req = new ReportCustomDataRequest{
			CurrentCustomCount = currentCustomCount,
			MaxCustomCount = maxCustomCount,
	};            
	return GrpcClient.GseClient.ReportCustomData(req, meta);
}
:::
</dx-codeblock>

## GSEをコールするためにサーバーを起動します。

サーバーの実行：GrpcServerを起動します。
<dx-codeblock>
::: java
public class Program
{
public static int ClientPort = PortServer.GenerateRandomPort(2000, 6000);
public static int GrpcPort = PortServer.GenerateRandomPort(6001, 10000);

public static void Main(string[] args)
{
	CreateHostBuilder(args).Build().Run();
}
public static IHostBuilder CreateHostBuilder(string[] args) =>
Host.CreateDefaultBuilder(args)
	.ConfigureWebHostDefaults(webBuilder =>
	{
		webBuilder.ConfigureKestrel(options =>
		{
			 // gRPCポート（TLS証明書なしでHTTP/2エンドポイントを設定）
			options.ListenAnyIP(GrpcPort, o => o.Protocols = 
					HttpProtocols.Http2);

			// HTTPポート
			options.ListenAnyIP(ClientPort);
		});
	
		webBuilder.UseStartup<Startup>();
	});
}
:::
</dx-codeblock>

## クライアントをGSEのgRPCサーバーに接続
サーバーに接続：gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使ってスタブインスタンスを作成します。
<dx-codeblock>
::: java
public class GrpcClient
{
	private static string agentAdress = "127.0.0.1:5758";
	public static GameServerGrpcSdkService.GameServerGrpcSdkServiceClient GameServerClient
	{
		get
		{
			Channel channel = new Channel(agentAdress, ChannelCredentials.Insecure);
			return new GameServerGrpcSdkService.GameServerGrpcSdkServiceClient(channel);
		}
	 }
	public static GseGrpcSdkService.GseGrpcSdkServiceClient GseClient
	{
		get
		{
			Channel channel = new Channel(agentAdress, ChannelCredentials.Insecure);
			return new GseGrpcSdkService.GseGrpcSdkServiceClient(channel);
		}
	}
}
:::
</dx-codeblock>


## C# DEMO
1. [ここをクリック](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/csharp-demo.zip)して、C# DEMOコードをダウンロードします。
2. gRPCコードを生成します。
C# DEMOコードのサンプルの中にgRPCコードがすでに生成されています。proto/csharp-demoディレクトリ下にありますので、別途生成する必要はありません。
3. GSEをコールするためにサーバーを起動します。
 - サーバーの実装。
csharp-demo/apiディレクトリ下のgameserversdk.csに、サーバーの3つのインターフェースを実装しています。
 - サーバーの実行。
csharp-demoディレクトリ下のProgram.csで、GrpcServerを起動します。
4. クライアントをGSEのgRPCサーバーに接続します。
 - クライアントの実装。
csharp-demo/Modelsディレクトリ下のGseManager.csに、クライアントの9つのインターフェースを実装しています。
 - サーバーに接続。
gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使用してスタブインスタンスを作成します。
5. コンパイルして実行。
 1. 実行可能ファイルおよび依存を生成します
  ```
  dotnet publish -c Release -r linux-x64 --self-contained true 
  ```
 以上によって、csharp-demo/bin/Release/netcoreapp3.1/linux-x64ディレクトリ下に、アセットに必要なすべての依存ファイルが生成され、パッケージングされます。これにはこのサービスを稼働させる実行可能ファイルcsharpdemoが含まれています。
 - Pre-request Script install.shをコピーします
 ```
 chmod u+x install.sh
cp install.sh bin/Release/netcoreapp3.1/linux-x64
 ```
 - GSEアセットをパッケージングします
 ```
 cd csharp-demo/bin/Release/netcoreapp3.1/linux-x64
zip -r csharpdemo.zip * 
 ```
パッケージングしたcsharpdemo.zip、すなわちGSEに必要な  [アセット](https://intl.cloud.tencent.com/document/product/1055/36674)です。起動パスはcsharpdemoを入力し、起動パラメータはありません。
 - その後、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)でサーバーフリートを作成し、アセットをサーバーフリートにデプロイします。この後引き続き、[スケーリング](https://intl.cloud.tencent.com/document/product/1055/37445) などの一連の操作を行うことができます。

 
