

## gRPCのインストール
1. 前提条件--CMakeをインストールしてあること。
  - Linux
	<dx-codeblock>
	::: Linux
		$ sudo apt install -y cmake
	:::
	</dx-codeblock>
  - MAC OS
    <dx-codeblock>
	**iOS**
		$ brew install cmake
	:::
	</dx-codeblock>
2. ローカルにgRPCとprotocol buffersをインストールします。
<dx-alert infotype="explain" title="">
>?具体的なインストール手順は、[CMakeのインストール](https://cmake.org/install)、[gRPC C ++インストールの説明](https://github.com/grpc/grpc/blob/master/BUILDING.md)、[protocol buffersインストールの説明](https://github.com/protocolbuffers/protobuf/blob/master/src/README.md)をご参照ください。
</dx-alert>




## サービスの定義
gRPCは、protocol buffersを利用してサービスの定義を実現します。1つのRPCのサービスに､パラメータとリターンタイプによってリモートの呼び出しが可能なメソッドが指定されます。

<dx-alert infotype="explain" title="">
>?サービスを定義したprotoファイルを提供していますので、[protoファイル](https://intl.cloud.tencent.com/document/product/1055/37419) からダウンロードしてご利用ください。ご自身で生成する必要はありません。
</dx-alert>


## gRPCコードの生成 
1. サービスを定義した後、 protocol bufferコンパイラprotocを利用して、クライアントとサーバーのコードを生成します（gRPCがサポートする任意の言語）。 
2. 生成するコードには、クライアントのstubとサーバーに実装したい抽象インターフェースが含まれています。
3. gRPCコード生成の手順：
    protoディレクトリ下で次を実行します。
 ```
 protoc --cpp_out=. *.proto
 ```
pb.ccとpb.hファイルを生成します。

```
protoc --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` *.proto```
```

対応するgRPCコードを生成します。
生成した8つのファイルをプロジェクトの適切な位置に移動します。

## ゲームプロセス統合の流れ
![アラームポリシーリスト](https://main.qcloudimg.com/raw/3b2af877848e11c337901172055ba466.png)

#### Game Server 回调接口列表

| インターフェース名 | インターフェース機能|
|-----|----|
|[OnHealthCheck](https://intl.cloud.tencent.com/document/product/1055/37422)| ヘルスチェック|
|[OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423)|ゲームサーバーセッションの受け入れ|
|[OnProcessTerminate](https://intl.cloud.tencent.com/document/product/1055/37424)|ゲームプロセスの終了|

#### Game Server 主调接口列表

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

 metaのリクエスト：ゲームプロセスがgRPCを介してクライアントインターフェースを呼び出す時に、gRPCがリクエストするmetaの中に2つのフィールドを追加する必要があります。

| フィールド      | 意味                                      | タイプ   |
| --------- | ----------------------------------------- | ------ |
| pid       | 現在のゲームプロセスのpid                         | string |
| requestId | 現在のリクエストのrequestId。一意のタグを使いリクエスト | string |

1. 通常は、サーバーの初期化後、プロセスが対外的にサービス提供可能かセルフチェックします。Game ServerがProcessReadyインターフェースを呼び出して、プロセスの準備が完了し、ゲームサーバーセッションのホスティングの準備ができたことをGSEに通知します。GSEはこれを受信した後、サーバーインスタンスのステータスを「アクティブ」に変更します。
<dx-codeblock>
::: java
Status GseManager::ProcessReady(std::vector<std::string> &logPath, int clientPort, int grpcPort, GseResponse& reply)
{
	ProcessReadyRequest request;
	//ログパス
	for (auto iter = logPath.begin(); iter != logPath.end(); iter++)
	{
		request.add_logpathstoupload(*iter);
	}

	GConsoleLog->PrintOut(true, "ProcessReady clientPort is %d\n", clientPort);
	GConsoleLog->PrintOut(true, "ProcessReady grpcPort is %d\n", grpcPort);

	//ポート設定
	request.set_clientport(clientPort);
	request.set_grpcport(grpcPort);

	ClientContext context;
	AddMetadata(context);

	//準備完了。対外的にサービス提供可能
	return stub_->ProcessReady(&context, request, &reply);
}
:::
</dx-codeblock>

2. プロセス準備完了後、GSEがOnHealthCheckインターフェースを呼び出し、Game Serverに対してヘルスチェックを実施します。1分ごとに1回検査し、連続3回失敗するとそのプロセスを異常と判定し、ゲームサーバーセッションをこのプロセスにアサインしません。
```
Status GameServerGrpcSdkServiceImpl::OnHealthCheck(ServerContext* context, const HealthCheckRequest* request,  HealthCheckResponse* reply)
{
	reply->set_healthstatus(healthStatus);
	return Status::OK;
}
```
3. Clientが [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)インターフェースを呼び出して、ゲームサーバーセッションを作成し、このゲームサーバーセッションを1つのプロセスにアサインしたため、GSEがトリガーされて当該プロセスのonStartGameServerSessionインターフェースを呼び出し、GameServerSessionのステータスを「アクティベート中」に変更します。
```
Status GameServerGrpcSdkServiceImpl::OnStartGameServerSession(ServerContext* context, const StartGameServerSessionRequest* request,  GseResponse* reply)
{
	auto gameServerSession = request->gameserversession();
	GGseManager->SetGameServerSession(gameServerSession);

	GseResponse processReadyReply;
	Status status = GGseManager->ActivateGameServerSession(gameServerSession.gameserversessionid(), gameServerSession.maxplayers(), processReadyReply);
	// statusとreplayに対して、アクティベートが成功したか判断します
	
	return Status::OK;
}
```
4. Game Serverが onStartGameServerSessionを受信し、あなたが自らいくつかのロジックまたはリソースのアサインを処理して準備が完了すると、Game ServerがActivateGameServerSessionインターフェースを呼び出します。ゲームサーバーセッションがプロセスにすでにアサインされ、現在、プレイヤーのリクエストを受け入れる準備ができていることをGSEに通知し、サーバーのステータスを「アクティブ」に変更します。
```
Status GseManager::ActivateGameServerSession(std::string gameServerSessionId, int maxPlayers, GseResponse& reply)
{
	GConsoleLog->PrintOut(true, "ActivateGameServerSession gameServerSessionId is %s\n", gameServerSessionId.c_str());
	GConsoleLog->PrintOut(true, "ActivateGameServerSession maxPlayers is %d\n", maxPlayers);

	ActivateGameServerSessionRequest request; 
	request.set_gameserversessionid(gameServerSessionId);
	request.set_maxplayers(maxPlayers);
	
	ClientContext context;
	AddMetadata(context);
	
	return stub_->ActivateGameServerSession(&context, request, &reply);
}
```
5. Clientが[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130)インターフェースを呼び出してプレイヤーが参加すると、Game ServerがAcceptPlayerSessionインターフェースを呼び出してプレイヤーの合法性を検証します。接続が受け入れられた場合は、PlayerSessionのステータスを「アクティブ」に変更します。ClientがJoinGameServerSessionインターフェースを呼び出して60秒以内に応答がない場合は、PlayerSessionのステータスを「タイムアウト」に変更し、その後再び JoinGameServerSessionを呼び出します。
```
Status GseManager::AcceptPlayerSession(std::string playerSessionId, GseResponse& reply)
{
	AcceptPlayerSessionRequest request;
	request.set_gameserversessionid(gameServerSession.gameserversessionid());
	request.set_playersessionid(playerSessionId);

	ClientContext context;
	AddMetadata(context);
	
	return stub_->AcceptPlayerSession(&context, request, &reply);
}
```
6. ゲーム終了またはプレイヤーの退出後、Game ServerがRemovePlayerSessionインターフェースを呼び出してプレイヤーを削除します。playersessionのステータスを「完了」 に変更し、ゲームサーバーセッションの中のプレイヤーの位置をリザーブします。
```
Status GseManager::RemovePlayerSession(std::string playerSessionId, GseResponse& reply)
{
	GConsoleLog->PrintOut(true, "RemovePlayerSession playerSessionId is %s\n", playerSessionId.c_str());
	RemovePlayerSessionRequest request;
	request.set_gameserversessionid(gameServerSession.gameserversessionid());
	request.set_playersessionid(playerSessionId);

	ClientContext context;
	AddMetadata(context);
	
	return stub_->RemovePlayerSession(&context, request, &reply);
}
```
7. 1つのゲームサーバーセッション（1組のゲームの対戦または1つのサービス）が終了すると、Game ServerがTerminateGameServerSessionインターフェースを呼び出してGameServerSessionを終了し、GameServerSessionのステータスを「終了」に変更します。
```
Status GseManager::TerminateGameServerSession(GseResponse& reply)
{
	GConsoleLog->PrintOut(true, "start to TerminateGameServerSession\n");
	TerminateGameServerSessionRequest request;
	request.set_gameserversessionid(gameServerSession.gameserversessionid());

	ClientContext context;
	AddMetadata(context);
	
	return stub_->TerminateGameServerSession(&context, request, &reply);
}
```

8. ヘルスチェックに失敗したかまたは容量縮小の時は、GSEがOnProcessTerminateインターフェースを呼び出してゲームプロセスを終了します。容量縮小時の根拠は、GSEコンソールで設定した[保護ポリシー](https://intl.cloud.tencent.com/document/product/1055/36675#test12)です。
```
Status GameServerGrpcSdkServiceImpl::OnProcessTerminate(ServerContext* context, const ProcessTerminateRequest* request,  GseResponse* reply)
{
	auto terminationTime = request->terminationtime();
	GGseManager->SetTerminationTime(terminationTime);

	//次の2つのインターフェースを呼び出すと、ゲームサーバーセッションが直ちに終了します。プレイヤーがいなくなったか、またはゲームサーバーセッションがなくなってから、ProcessEndingを呼び出してプロセスを終了することをお勧めします
	//次の2つのインターフェースを呼び出さない場合は、保護ポリシーに基づきProcessEndingを呼び出してプロセスを終了します。時間制限を設定して保護することをお勧めします
	
	//ゲームサーバーセッションの終了
	GseResponse terminateGameServerSessionReply;
	GGseManager->TerminateGameServerSession(terminateGameServerSessionReply);
	
	// プロセスの終了
	GseResponse processEndingReply;
	GGseManager->ProcessEnding(processEndingReply);
	
	return Status::OK;
}
```

9. Game ServerがProcessEndingインターフェースを呼び出してプロセスを直ちに終了させ、サーバープロセスのステータスを「終了」に変更してリソースを回収します。
```
//自動呼び出し：ゲーム1局につき1つのプロセスが対応し、1局のゲームが終了すると自動でProcessEndingインターフェースを呼び出します
//手動呼び出し：容量縮小またはプロセスの異常によりヘルスチェックに失敗した時は、保護ポリシーにもとづき受動的にProcessEndingインターフェースが呼び出されます。完全保護および時間制限保護ポリシーを設定している時は、先にゲームサーバーセッション上のプレイヤーの有無を判断してから、手動で呼び出しを行う必要があります
Status GseManager::ProcessEnding(GseResponse& reply)
{
	GConsoleLog->PrintOut(true, "start to ProcessEnding\n");
	ProcessEndingRequest request;

	ClientContext context;
	AddMetadata(context);
	
	return stub_->ProcessEnding(&context, request, &reply);
}
```
10. Game ServerがDescribePlayerSessionsインターフェースを呼び出してゲームサーバーセッション下のプレイヤー情報を取得します（業務に応じて任意選択）。
```
Status GseManager::DescribePlayerSessions(std::string gameServerSessionId, std::string  playerId, std::string  playerSessionId,std::string playerSessionStatusFilter, std::string nextToken, int limit, DescribePlayerSessionsResponse& reply)
{
	GConsoleLog->PrintOut(true, "start to DescribePlayerSessions\n");
	DescribePlayerSessionsRequest request;
	request.set_gameserversessionid(gameServerSessionId);
	request.set_playerid(playerId);
	request.set_playersessionid(playerSessionId);
	request.set_playersessionstatusfilter(playerSessionStatusFilter);
	request.set_nexttoken(nextToken);
	request.set_limit(limit);

	ClientContext context;
	AddMetadata(context);
	
	return stub_->DescribePlayerSessions(&context, request, &reply);
}
```
11. Game ServerがUpdatePlayerSessionCreationPolicyインターフェースを呼び出してプレイヤーセッションの作成ポリシーを更新し、新規プレイヤーの受け入れの是非、つまりゲームセッションにプレイヤーの参加を許可するかを設定します（業務に応じて任意選択）。
```
Status GseManager::UpdatePlayerSessionCreationPolicy(std::string newpolicy, GseResponse& reply)
{
	GConsoleLog->PrintOut(true, "UpdatePlayerSessionCreationPolicy, newpolicy is %s\n", newpolicy.c_str());
	UpdatePlayerSessionCreationPolicyRequest request;
	request.set_gameserversessionid(gameServerSession.gameserversessionid());
	request.set_newplayersessioncreationpolicy(newpolicy);

	ClientContext context;
	AddMetadata(context);
	
	return stub_->UpdatePlayerSessionCreationPolicy(&context, request, &reply);
}
```
12. Game ServerがReportCustomDataインターフェースを呼び出してGSEにカスタムデータを通知します。ゲームサーバーセッションのクエリー時に確認することができます（業務に応じて任意選択）。
```
Status GseManager::ReportCustomData(int currentCustomCount, int maxCustomCount, GseResponse& reply)
{
	GConsoleLog->PrintOut(true, "ReportCustomData, currentCustomCount is %d\n", currentCustomCount);
	GConsoleLog->PrintOut(true, "ReportCustomData, maxCustomCount is %d\n", maxCustomCount);

	ReportCustomDataRequest request;
	request.set_currentcustomcount(currentCustomCount);
	request.set_maxcustomcount(maxCustomCount);
	
	ClientContext context;
	AddMetadata(context);
	
	return stub_->ReportCustomData(&context, request, &reply);
}
```

## GSEをコールするためにサーバーを起動します。

サーバーの実行：GrpcServerを起動します。

```
GameServerGrpcSdkServiceImpl::GameServerGrpcSdkServiceImpl() : serverAddress("127.0.0.1:0"), healthStatus(true)
{
	sem_init(&sem, 0, 0);
}

void GameServerGrpcSdkServiceImpl::StartGrpcServer()
{
	ServerBuilder builder;
	builder.AddListeningPort(serverAddress, grpc::InsecureServerCredentials(), &grpcPort);
	builder.RegisterService(this);
	std::unique_ptr<Server> server(builder.BuildAndStart());
	sem_post(&sem);
	server->Wait();
}
```


## クライアントをGSEのgRPCサーバーに接続

サーバーに接続：gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使ってスタブインスタンスを作成します。

```
void GseManager::InitStub()
{
	auto channel = grpc::CreateChannel("127.0.0.1:5758", grpc::InsecureChannelCredentials());
	stub_ = GseGrpcSdkService::NewStub(channel);
}
```

## C++ DEMO
1. [ここをクリック](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/cpp-demo.zip)して、C# DEMOコードをダウンロードします。
2. gRPCコードを生成します。
C# DEMOコードサンプルの中にgRPCコードがすでに生成されています。cpp-demo/source/grpcsdkディレクトリ下にありますので、別途生成する必要はありません。
3. GSEをコールするためにサーバーを起動します。
  - サーバーの実装。
cpp-demo/source/apiディレクトリ下のgrpcserver.cppに、サーバーの3つのインターフェースを実装しています。
  - サーバーの実行。
cpp-demo/source/apiディレクトリ下のgrpcserver.cppで、 GrpcServerを起動します。
4. クライアントをGSEのgRPCサーバーに接続します。
  - クライアントの実装。
cpp-demo/source/gsemanagerディレクトリ下のgsemanager.cppに、クライアントの9つのインターフェースを実装しています。
  - サーバーに接続。
gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使用してスタブインスタンスを作成します。
5. コンパイルして実行。
 1. cmakeをインストールします。
 2.  gccをインストールします。バージョン要件：4.9以上。
 3. コードをダウンロードし、cpp-demoディレクトリ下で、次のコマンドを実行します。
```
  mkdir build
  cmake ..
  make
```
 対応するcpp-demo実行可能ファイルが生成されます。
 4. cpp-demo実行可能ファイルをパッケージングして [アセット](https://intl.cloud.tencent.com/document/product/1055/36674)を作成します。起動パスの設定はcpp-demo、起動パラメータはありません。
 5. その後、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)でサーバーフリートを作成し、アセットをサーバーフリートにデプロイします。この後引き続き、[スケーリング](https://intl.cloud.tencent.com/document/product/1055/37445) などの一連の操作を行うことができます。


