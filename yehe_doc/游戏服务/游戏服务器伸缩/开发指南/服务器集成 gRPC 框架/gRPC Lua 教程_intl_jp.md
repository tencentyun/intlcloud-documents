
## gRPCのインストール
1. gRPCをインストール します。インストールが完了するとgrpc_cpp_pluginの実行可能プログラムが生成されます。このプログラムが、gRPC コード生成時に必要となります。
2. protocol buffersをインストールします。

<dx-alert infotype="explain" title="">
>?具体的なインストール手順については、[gRPC Luaインストールの説明](https://github.com/grpc/grpc/blob/master/BUILDING.md)、[protocol buffersインストールの説明](https://github.com/protocolbuffers/protobuf/blob/master/src/README.md)をご参照ください。
</dx-alert>




## サービスの定義
 gRPCは、protocol buffersを利用してサービスの定義を実現します。1つのRPCのサービスに､パラメータとリターンタイプによってリモートの呼び出しが可能なメソッドが指定されます。


<dx-alert infotype="explain" title="">
>?サービスを定義したprotoファイルを提供していますので、[protoファイル](https://intl.cloud.tencent.com/document/product/1055/37419)からダウンロードしてご利用ください。ご自身で生成する必要はありません。
</dx-alert>




## gRPCコードの生成 
1. サービスを定義した後、 protocol bufferコンパイラprotocを利用して、クライアントとサーバーのコードを生成します（gRPCがサポートする任意の言語）。 
2. 生成するコードには、クライアントのstubとサーバーに実装したい抽象インターフェースが含まれています。
3. gRPCコード生成の手順：
    Lua DEMOは、C++フレームワークに依存し、手順は C++ DEMOと同じです。protoディレクトリ下で次のように実行します。
 ```
 protoc --cpp_out=. *.proto``` 
 pb.ccとpb.hファイルを生成します。
 ```
protoc --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` *.proto```
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
```Lua
static bool luaProcessReady(std::vector <std::string> &logPath, int clientPort, int grpcPort) {
	GseResponse reply;
	//ログパス、ポート設定
	Status status = GGseManager->ProcessReady(logPath, clientPort, grpcPort, reply);
	//準備完了。対外的にサービス提供可能
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
		return false;
	}
	return true;
}
```
 2. プロセス準備完了後、GSEがOnHealthCheckインターフェースを呼び出し、Game Serverに対してヘルスチェックを実施します。1分ごとに1回検査し、連続3回失敗するとそのプロセスを異常と判定し、ゲームサーバーセッションをこのプロセスにアサインしません。
```Lua
Status GameServerGrpcSdkServiceImpl::OnHealthCheck(ServerContext* context, const HealthCheckRequest* request,  HealthCheckResponse* reply)
{
	healthStatus = GSESDK()->exec("return OnHealthCheck()");
	std::cout << "healthStatus=" << healthStatus << std::endl;
	reply->set_healthstatus(healthStatus);
	return Status::OK;
}
```
 3. Clientが [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)インターフェースを呼び出して、ゲームサーバーセッションを作成し、このゲームサーバーセッションを1つのプロセスにアサインしたため、GSEがトリガーされて当該プロセスのonStartGameServerSessionインターフェースを呼び出し、GameServerSessionのステータスを「アクティベート中」に変更します。
```Lua
Status GameServerGrpcSdkServiceImpl::OnStartGameServerSession(ServerContext* context, const StartGameServerSessionRequest* request,  GseResponse* reply)
{
	auto gameServerSession = request->gameserversession();
	GGseManager->SetGameServerSession(gameServerSession);

	std::ostringstream o;
	o << "return OnStartGameServerSession('" << gameServerSession.gameserversessionid() << "'," << gameServerSession.maxplayers() << ")";
	std::string luaCmd = o.str();

	bool res = GSESDK()->exec(luaCmd);

	return Status::OK;
}
```
 4. Game Serverが onStartGameServerSessionを受信し、あなたが自ら幾つかのロジックまたはリソースのアサインを処理して、準備が完了すると、Game Server が ActivateGameServerSession インターフェースを呼び出して、GSEに、ゲームサーバーセッションがプロセスに既にアサインされ、現在プレイヤーのリクエストを受け入れる準備ができていることを通知し、サーバーのステータスを「アクティブ」に変更します。
```Lua
static bool luaActivateGameServerSession(const std::string &gameServerSessionId, int maxPlayers) {
	GseResponse reply;
	Status status = GGseManager->ActivateGameServerSession(gameServerSessionId, maxPlayers, reply);
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
			return false;
	}
	return true;
}
```
 5. Clientが [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130)インターフェースを呼び出してプレイヤーが参加すると、Game ServerがAcceptPlayerSessionインターフェースを呼び出してプレイヤーの合法性を検証します。接続が受け入れられた場合は、PlayerSessionのステータスを「アクティブ」に変更します。ClientがJoinGameServerSessionインターフェースを呼び出して60秒以内に応答がない場合は、PlayerSessionのステータスを「タイムアウト」に変更し、その後再び JoinGameServerSessionを呼び出します。
```Lua
static bool luaAcceptPlayerSession(const std::string &gameServerSessionId, const std::string &playerSessionId) {
	GseResponse reply;
	Status status = GGseManager->AcceptPlayerSession(gameServerSessionId, playerSessionId, reply);
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
			return false;
	}
	return true;
}
```
 6. ゲーム終了またはプレイヤーの退出後、Game ServerがRemovePlayerSessionインターフェースを呼び出してプレイヤーを削除します。playersessionのステータスを「完了」 に変更し、ゲームサーバーセッションの中のプレイヤーの位置をリザーブします。
```Lua
static bool luaRemovePlayerSession(const std::string &gameServerSessionId, const std::string &playerSessionId) {
	GseResponse reply;
	Status status = GGseManager->RemovePlayerSession(gameServerSessionId, playerSessionId, reply);
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
			return false;
	}
	return true;
}
```
 7. 1つのゲームサーバーセッション（1組のゲームの対戦または1つのサービス）が終了すると、Game ServerがTerminateGameServerSessionインターフェースを呼び出してGameServerSessionを終了し、GameServerSessionのステータスを「終了」に変更します。
```Lua
static bool luaTerminateGameServerSession(const std::string &gameServerSessionId) {
	GseResponse reply;
	Status status = GGseManager->TerminateGameServerSession(gameServerSessionId, reply);
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
			return false;
	}
	return true;
}
```
 8. ヘルスチェックに失敗したかまたは容量縮小の時は、GSEがOnProcessTerminateインターフェースを呼び出してゲームプロセスを終了します。容量縮小時の根拠は、GSEコンソールで設定した[保護ポリシー](https://intl.cloud.tencent.com/document/product/1055/36675#test12)です。
```Lua
Status GameServerGrpcSdkServiceImpl::OnProcessTerminate(ServerContext* context, const ProcessTerminateRequest* request,  GseResponse* reply)
{
	auto terminationTime = request->terminationtime();
	std::to_string(terminationTime));
	std::ostringstream o;
	o << "OnProcessTerminate(" << terminationTime << ")";
	std::string luaCmd = o.str();

	GSESDK()->execWithNilResult(luaCmd);

	return Status::OK;
}
```
 9. Game ServerがProcessEndingインターフェースを呼び出してプロセスを直ちに終了させ、サーバープロセスのステータスを「終了」に変更してリソースを回収します。
```Lua
//自動呼び出し：ゲーム1局につき1つのプロセスが対応し、1局のゲームが終了すると自動でProcessEndingインターフェースを呼び出します
//手動呼び出し：容量縮小またはプロセスの異常によりヘルスチェックに失敗した時は、保護ポリシーにもとづき受動的にProcessEndingインターフェースが呼び出されます。完全保護および時間制限保護ポリシーを設定している時は、先にゲームサーバーセッション上のプレイヤーの有無を判断してから、手動で呼び出しを行う必要があります
static bool luaProcessEnding() {
	GseResponse reply;
	Status status = GGseManager->ProcessEnding(reply);
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
			return false;
	}
	return true;
}
```
 10. Game ServerがDescribePlayerSessionsインターフェースを呼び出してゲームサーバーセッション下のプレイヤー情報を取得します（業務に応じて任意選択）。
```Lua
static bool luaDescribePlayerSessions(const std::string &gameServerSessionId, 
									  const std::string &playerId,
								  	const std::string &playerSessionId,
									  const std::string &playerSessionStatusFilter, const std::string &nextToken,
																				int limit) {
	DescribePlayerSessionsResponse reply;
	Status status = GGseManager->DescribePlayerSessions(gameServerSessionId,playerId, playerSessionId, playerSessionStatusFilter, nextToken, limit, reply);

	GSESDK()->setDescribePlayerSessionsResponse(reply);
	if (!status.ok()) {
		return false;
	}
	return true;
}
```
 11. Game ServerがUpdatePlayerSessionCreationPolicyインターフェースを呼び出してプレイヤーセッションの作成ポリシーを更新し、新規プレイヤーの受け入れの是非、つまりゲームセッションにプレイヤーの参加を許可するかを設定します（業務に応じて任意選択）。
```Lua
static bool luaUpdatePlayerSessionCreationPolicy(const std::string &newpolicy) {
	GseResponse reply;
	Status status = GGseManager->UpdatePlayerSessionCreationPolicy(newpolicy, reply);
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
			return false;
	}
	return true;
}
```
 12. Game ServerがReportCustomDataインターフェースを呼び出し、GSEにカスタムデータを通知します（業務に応じて任意選択）。
```Lua
static bool luaReportCustomData(int currentCustomCount, int maxCustomCount) {
	GseResponse reply;
	Status status = GGseManager->ReportCustomData(currentCustomCount, maxCustomCount, reply);
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
			return false;
	}
	return true;
}
```

## GSEをコールするためにサーバーを起動します。

サーバーの実行：GrpcServerを起動します。
```
// grpc serverの起動
std::thread tGrpc(&GameServerGrpcSdkServiceImpl::StartGrpcServer, GGameServerGrpcSdkService);
sem_wait(&(GGameServerGrpcSdkService->sem));
auto grpcPort = GGameServerGrpcSdkService->GetGrpcPort();
```

## クライアントをGSEのgRPCサーバーに接続
サーバーに接続：gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使ってスタブインスタンスを作成します。
```
void GseManager::InitStub() {
	auto channel = grpc::CreateChannel("127.0.0.1:5758", grpc::InsecureChannelCredentials());
	stub_ = GseGrpcSdkService::NewStub(channel);
}
```

## Lua DEMO
 1. [ここをクリック](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/lua-demo.zip)して、Lua DEMOコードをダウンロードします。
 2. gRPCコードを生成します。
Lua DEMOは、C++フレームワークに依存します。生成済みの gRPCコードが cpp-demo/source/grpcsdkディレクトリ下にありますので、別途生成する必要はありません。
 3. GSEをコールするためにサーバーを起動します。
  - サーバーの実装。
lua-demo/source/apiディレクトリ下のgrpcserver.cppに、サーバーの3つのインターフェースを実装しています。
  - サーバーの実行。
lua-demoディレクトリ下のmain.cppで、GrpcServerを起動します。
 4. クライアントをGSEのgRPCサーバーに接続します。
  - クライアントの実装。
lua-demo/source/luaディレクトリ下の GSESdkHandleWrapper.cppに、クライアントの9つのインターフェースを実装しています。
  - サーバーに接続。
gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使用してスタブインスタンスを作成します。
 5. コンパイルして実行。
  1. cmakeをインストールします。
  -  gccをインストールします、バージョン要件は4.9以上です。
  -  luajit開発パッケージとboost開発パッケージをインストールします。
 ```
yum install -y luajit-devel
yum install -y boost-devel
yum install -y cmake
 ```
  - コードをダウンロードし、lua-demoディレクトリ下で、次のコマンドを実行します。
 ```
 mkdir build
 cd build
 cmake ..
 make
 cp ../source/lua/gse.lua .
 ```
  対応するlua-demoの実行可能ファイルが生成されます。./lua-demoを実行して起動します。
  - 実行可能ファイルlua-demo.cppをパッケージングして[アセット](https://intl.cloud.tencent.com/document/product/1055/36674)を作成します。起動パスの設定はlua-demo、起動パラメータはありません。
  - その後、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)でサーバーフリートを作成し、アセットをサーバーフリートにデプロイします。この後引き続き、[スケーリング](https://intl.cloud.tencent.com/document/product/1055/37445) などの一連の操作を行うことができます。
