
## gRPCのインストール
1. gRPC Goを使用する場合、先に最新のGoのメジャーバージョンをインストールする必要があります。
2. Protocol bufferコンパイラをインストールします。バージョンは protoc3です。
3. Protocol buffer コンパイラの中にGoのPlug-inをインストールします。
  - 次のコマンドを使用してGo（protoc-gen-go）のためにProtocol bufferコンパイラのPlug-inをインストールします。
  ```
  $ export GO111MODULE=on  # Enable module mode
  $ go get github.com/golang/protobuf/protoc-gen-go
  ```
  - Protocol bufferコンパイラがGo Plug-inを見つけられるようにパスを更新します。
```
$ export PATH="$PATH:$(go env GOPATH)/bin"
```

 

<dx-alert infotype="explain" title="">
>?具体的な手順は、[Goのインストール説明](https://github.com/grpc/grpc-go/tree/master/examples)、[Protocol bufferコンパイラのインストール説明](https://www.grpc.io/docs/protoc-installation/)をご参照ください。
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
protoc --go_out=plugins=grpc:. *.proto```
	protoを含むgo_packageパスが自動生成されますので、必要に応じて自分に合うようにgo_packageパスを修正することができます。ただしpackageの修正はできません。
	  ```

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
```go
func (g *gsemanager) ProcessReady(logPath []string, clientPort int32, grpcPort int32) error {
	logger.Info("start to processready", zap.Any("logPath", logPath), zap.Int32("clientPort", clientPort),
		zap.Int32("grpcPort", grpcPort))
	req := &grpcsdk.ProcessReadyRequest{
		//ログパス
		LogPathsToUpload: logPath,
		//ポート設定
		ClientPort:       clientPort,
		GrpcPort:         grpcPort,
	}

	_, err := g.rpcClient.ProcessReady(g.getContext(), req)
	if err != nil {
		logger.Info("ProcessReady fail", zap.Error(err))
		return err
	}

	//準備完了。対外的にサービス提供可能
	logger.Info("ProcessReady success")
	return nil
}
```
 2. プロセス準備完了後、GSEがOnHealthCheckインターフェースを呼び出し、Game Serverに対してヘルスチェックを実施します。1分ごとに1回検査し、連続3回失敗するとそのプロセスを異常と判定し、ゲームサーバーセッションをこのプロセスにアサインしません。
```go
func _GameServerGrpcSdkService_OnHealthCheck_Handler(srv interface{}, ctx context.Context, dec func(interface{}) error, interceptor grpc.UnaryServerInterceptor) (interface{}, error) {
	in := new(HealthCheckRequest)
	if err := dec(in); err != nil {
		return nil, err
	}
	if interceptor == nil {
		return srv.(GameServerGrpcSdkServiceServer).OnHealthCheck(ctx, in)
	}
	info := &grpc.UnaryServerInfo{
		Server:     srv,
		FullMethod: "/tencentcloud.gse.grpcsdk.GameServerGrpcSdkService/OnHealthCheck",
	}
	handler := func(ctx context.Context, req interface{}) (interface{}, error) {
		return srv.(GameServerGrpcSdkServiceServer).OnHealthCheck(ctx, req.(*HealthCheckRequest))
	}
	return interceptor(ctx, in, info, handler)
}
```
 3. Clientが [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)インターフェースを呼び出して、ゲームサーバーセッションを作成し、このゲームサーバーセッションを1つのプロセスにアサインしたため、GSEがトリガーされて当該プロセスのonStartGameServerSessionインターフェースを呼び出し、GameServerSessionのステータスを「アクティベート中」に変更します。
```go
func _GameServerGrpcSdkService_OnStartGameServerSession_Handler(srv interface{}, ctx context.Context, dec func(interface{}) error, interceptor grpc.UnaryServerInterceptor) (interface{}, error) {
	in := new(StartGameServerSessionRequest)
	if err := dec(in); err != nil {
		return nil, err
	}
	if interceptor == nil {
		return srv.(GameServerGrpcSdkServiceServer).OnStartGameServerSession(ctx, in)
	}
	info := &grpc.UnaryServerInfo{
		Server:     srv,
		FullMethod: "/tencentcloud.gse.grpcsdk.GameServerGrpcSdkService/OnStartGameServerSession",
	}
	handler := func(ctx context.Context, req interface{}) (interface{}, error) {
		return srv.(GameServerGrpcSdkServiceServer).OnStartGameServerSession(ctx, req.(*StartGameServerSessionRequest))
	}
	return interceptor(ctx, in, info, handler)
}
```
 4. Game Serverが onStartGameServerSessionを受信し、あなたが自らいくつかのロジックまたはリソースのアサインを処理して準備が完了すると、Game ServerがActivateGameServerSessionインターフェースを呼び出します。ゲームサーバーセッションがプロセスにすでにアサインされ、現在、プレイヤーのリクエストを受け入れる準備ができていることをGSEに通知し、サーバーのステータスを「アクティブ」に変更します。
```go
func (g *gsemanager) ActivateGameServerSession(gameServerSessionId string, maxPlayers int32) error {
	logger.Info("start to ActivateGameServerSession", zap.String("gameServerSessionId", gameServerSessionId),
		zap.Int32("maxPlayers", maxPlayers))
	req := &grpcsdk.ActivateGameServerSessionRequest{
		GameServerSessionId:  gameServerSessionId,
		MaxPlayers:           maxPlayers,
	}

	_, err := g.rpcClient.ActivateGameServerSession(g.getContext(), req)
	if err != nil {
		logger.Error("ActivateGameServerSession fail", zap.Error(err))
		return err
	}

	logger.Info("ActivateGameServerSession success")
	return nil
}
```
 5. Clientが[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130)インターフェースを呼び出してプレイヤーが参加すると、Game ServerがAcceptPlayerSessionインターフェースを呼び出してプレイヤーの合法性を検証します。接続が受け入れられた場合は、PlayerSessionのステータスを「アクティブ」に変更します。ClientがJoinGameServerSessionインターフェースを呼び出して60秒以内に応答がない場合は、PlayerSessionのステータスを「タイムアウト」に変更し、その後再び JoinGameServerSessionを呼び出します。
```
func (g *gsemanager) AcceptPlayerSession(playerSessionId string) (*grpcsdk.GseResponse, error) {
	logger.Info("start to AcceptPlayerSession", zap.String("playerSessionId", playerSessionId))
	req := &grpcsdk.AcceptPlayerSessionRequest{
		GameServerSessionId:  g.gameServerSession.GameServerSessionId,
		PlayerSessionId:      playerSessionId,
	}

	return g.rpcClient.AcceptPlayerSession(g.getContext(), req)
}
```
 6. ゲーム終了またはプレイヤーの退出後、Game ServerがRemovePlayerSessionインターフェースを呼び出してプレイヤーを削除します。playersessionのステータスを「完了」 に変更し、ゲームサーバーセッションの中のプレイヤーの位置をリザーブします。
```go
func (g *gsemanager) RemovePlayerSession(playerSessionId string) (*grpcsdk.GseResponse, error) {
	logger.Info("start to RemovePlayerSession", zap.String("playerSessionId", playerSessionId))
	req := &grpcsdk.RemovePlayerSessionRequest{
		GameServerSessionId:  g.gameServerSession.GameServerSessionId,
		PlayerSessionId:      playerSessionId,
	}

	return g.rpcClient.RemovePlayerSession(g.getContext(), req)
}
```
 7. 1つのゲームサーバーセッション（1組のゲームの対戦または1つのサービス）が終了すると、Game ServerがTerminateGameServerSessionインターフェースを呼び出してGameServerSessionを終了し、GameServerSessionのステータスを「終了」に変更します。
```go
func (g *gsemanager) TerminateGameServerSession() (*grpcsdk.GseResponse, error) {
	logger.Info("start to TerminateGameServerSession")
	req := &grpcsdk.TerminateGameServerSessionRequest{
		GameServerSessionId:  g.gameServerSession.GameServerSessionId,
	}

	return g.rpcClient.TerminateGameServerSession(g.getContext(), req)
}
```
 8. ヘルスチェックに失敗したかまたは容量縮小の時は、GSEがOnProcessTerminateインターフェースを呼び出してゲームプロセスを終了します。容量縮小時の根拠は、GSEコンソールで設定した[保護ポリシー](https://intl.cloud.tencent.com/document/product/1055/36675#test12)です。
```go
func _GameServerGrpcSdkService_OnProcessTerminate_Handler(srv interface{}, ctx context.Context, dec func(interface{}) error, interceptor grpc.UnaryServerInterceptor) (interface{}, error) {
	in := new(ProcessTerminateRequest)
	if err := dec(in); err != nil {
		return nil, err
	}
	if interceptor == nil {
		return srv.(GameServerGrpcSdkServiceServer).OnProcessTerminate(ctx, in)
	}
	info := &grpc.UnaryServerInfo{
		Server:     srv,
		FullMethod: "/tencentcloud.gse.grpcsdk.GameServerGrpcSdkService/OnProcessTerminate",
	}
	handler := func(ctx context.Context, req interface{}) (interface{}, error) {
		return srv.(GameServerGrpcSdkServiceServer).OnProcessTerminate(ctx, req.(*ProcessTerminateRequest))
	}
	return interceptor(ctx, in, info, handler)
} 
```
 9. Game ServerがProcessEndingインターフェースを呼び出してプロセスを直ちに終了させ、サーバープロセスのステータスを「終了」に変更してリソースを回収します。
```go
//自動呼び出し：ゲーム1局につき1つのプロセスが対応し、1局のゲームが終了すると自動でProcessEndingインターフェースを呼び出します
//手動呼び出し：容量縮小またはプロセスの異常によりヘルスチェックに失敗した時は、保護ポリシーにもとづき受動的にProcessEndingインターフェースが呼び出されます。完全保護および時間制限保護ポリシーを設定している時は、先にゲームサーバーセッション上のプレイヤーの有無を判断してから、手動で呼び出しを行う必要があります
func (g *gsemanager) ProcessEnding() (*grpcsdk.GseResponse, error) {
	logger.Info("start to ProcessEnding")
	req := &grpcsdk.ProcessEndingRequest{
	}

	return g.rpcClient.ProcessEnding(g.getContext(), req)
}
```
 10. Game ServerがDescribePlayerSessionsインターフェースを呼び出してゲームサーバーセッション下のプレイヤー情報を取得します（業務に応じて任意選択）。
```go
func (g *gsemanager) DescribePlayerSessions(gameServerSessionId, playerId, playerSessionId, playerSessionStatusFilter, nextToken string,limit int32) (*grpcsdk.DescribePlayerSessionsResponse, error) {
	logger.Info("start to DescribePlayerSessions", zap.String("gameServerSessionId", gameServerSessionId),
		zap.String("playerId", playerId), zap.String("playerSessionId", playerSessionId),
		zap.String("playerSessionStatusFilter", playerSessionStatusFilter), zap.String("nextToken", nextToken),
		zap.Int32("limit", limit))

	req := &grpcsdk.DescribePlayerSessionsRequest{
		GameServerSessionId:       gameServerSessionId,
		PlayerId:                  playerId,
		PlayerSessionId:           playerSessionId,
		PlayerSessionStatusFilter: playerSessionStatusFilter,
		NextToken:                 nextToken,
		Limit:                     limit,
	}

	return g.rpcClient.DescribePlayerSessions(g.getContext(), req)
}
```
 11. Game ServerがUpdatePlayerSessionCreationPolicyインターフェースを呼び出してプレイヤーセッションの作成ポリシーを更新し、新規プレイヤーの受け入れの是非、つまりゲームセッションにプレイヤーの参加を許可するかを設定します（業務に応じて任意選択）。
```go
func (g *gsemanager) UpdatePlayerSessionCreationPolicy(newPolicy string) (*grpcsdk.GseResponse, error) {
	logger.Info("start to UpdatePlayerSessionCreationPolicy", zap.String("newPolicy", newPolicy))
	req := &grpcsdk.UpdatePlayerSessionCreationPolicyRequest{
		GameServerSessionId:            g.gameServerSession.GameServerSessionId,
		NewPlayerSessionCreationPolicy: newPolicy,
	}

	return g.rpcClient.UpdatePlayerSessionCreationPolicy(g.getContext(), req)
}
```
 12. Game ServerがReportCustomDataインターフェースを呼び出し、GSEにカスタムデータを通知します（業務に応じて任意選択）。
```go
func (g *gsemanager) ReportCustomData(currentCustomCount, maxCustomCount int32) (*grpcsdk.GseResponse, error) {
	logger.Info("start to UpdatePlayerSessionCreationPolicy", zap.Int32("currentCustomCount", currentCustomCount),
		zap.Int32("maxCustomCount", maxCustomCount))
	req := &grpcsdk.ReportCustomDataRequest{
		CurrentCustomCount:   currentCustomCount,
		MaxCustomCount:       maxCustomCount,
	}

	return g.rpcClient.ReportCustomData(g.getContext(), req)
}
```

## GSEをコールするためにサーバーを起動します。
サーバーの実行：GrpcServerを起動します。
```go
func (s *rpcService) StartGrpcServer() {
	listen, err := net.Listen("tcp", "127.0.0.1:")
	if err != nil {
			logger.Fatal("grpc fail to listen", zap.Error(err))
	}

	addr := listen.Addr().String()
	portStr := strings.Split(addr, ":")[1]
	s.grpcPort, err = strconv.Atoi(portStr)
	if err != nil {
			logger.Fatal("grpc fail to get port",zap.Error(err))
	}

	logger.Info("grpc listen port is", zap.Int("port", s.grpcPort))

	grpcServer := grpc.NewServer()
	grpcsdk.RegisterGameServerGrpcSdkServiceServer(grpcServer, s)
	logger.Info("start grpc server success")
	go grpcServer.Serve(listen)
}
```

## クライアントをGSEのgRPCサーバーに接続
サーバーに接続：gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使ってスタブインスタンスを作成します。
```go
const (
		localhost = "127.0.0.1"
		agentPort = 5758
)
type gsemanager struct {
        pid    string
        gameServerSession *grpcsdk.GameServerSession
        terminationTime int64
        rpcClient grpcsdk.GseGrpcSdkServiceClient
}
```

## Go DEMO
 1. [ここをクリック](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/go-demo.zip)して、Go DEMOコードをダウンロードします。
 2. gRPCコードを生成します。
Go DEMOコードのサンプルの中にgRPCコードがすでに生成されています。go-demo/grpcsdkディレクトリ下にありますので、別途生成する必要はありません。
 3. GSEをコールするためにサーバーを起動します。
  - サーバーの実装。
go-demo/apiディレクトリ下のgrpcserver.goに、サーバーの3つのインターフェースを実装しています。
  - サーバーの実行。
go-demo/api ディレクトリ下のgrpcserver.goで、 GrpcServerを起動します。
 4. クライアントをGSEのgRPC サーバーに接続します。
  - クライアントの実装。
go-demo/gsemanagerディレクトリ下のgsemanager.goに、クライアントの9つのインターフェースを実装しています。
  - サーバーに接続。
gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使用してスタブインスタンスを作成します。
 5. コンパイルして実行。
  1. go-demoディレクトリ下で次を実行します
  ```
	go mod vendor```
	vendorディレクトリを生成します。
  - コマンドの編集：
  ```
	go build -mod=vendor main.go```
	対応するgo-demoの実行可能ファイルmain.goが生成されます。
  - 実行可能ファイルmain.goをパッケージングして [アセット](https://intl.cloud.tencent.com/document/product/1055/36674)を作成します。起動パスの設定はmain、起動パラメータはありません。
  - その後、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)でサーバーフリートを作成し、アセットをサーバーフリートにデプロイします。この後引き続き、[スケーリング](https://intl.cloud.tencent.com/document/product/1055/37445) などの一連の操作を行うことができます。

 
