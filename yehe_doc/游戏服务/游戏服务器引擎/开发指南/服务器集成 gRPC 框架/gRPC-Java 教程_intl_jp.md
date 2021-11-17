
## gRPCのインストール
1. Java gRPCは、JDK以外の他のツールは必要ありません。
2. ローカルにgRPC JavaライブラリSNAPSHOTをインストールします。これにはコード生成のPlug-inが含まれます。
>?具体的なインストール手順については、[gRPC Javaインストールの説明](https://github.com/grpc/grpc-java/blob/master/COMPILING.md)をご参照ください。
## サービスの定義
gRPCは、protocol buffersを利用してサービスの定義を実現します。1つのRPCのサービスに､パラメータとリターンタイプによってリモートの呼び出しが可能なメソッドが指定されます。

<dx-alert infotype="explain" title="">
>?サービスを定義したprotoファイルを提供していますので、[protoファイル](https://intl.cloud.tencent.com/document/product/1055/37419) からダウンロードしてご利用ください。ご自身で生成する必要はありません。

</dx-alert>



## gRPCコードの生成 
1. サービスを定義した後、 protocol bufferコンパイラprotocを利用して、クライアントとサーバーのコードを生成します（gRPCがサポートする任意の言語）。 
2. 生成するコードには、クライアントのstubとサーバーに実装したい抽象インターフェースが含まれています。
3. gRPCコード生成の手順：
 - 方法一：java-demo/src/main/protoでスクリプトを実行します。gprc公式サイトからprotocとprotoc-gen-grpc-java生成ツールをダウンロードする必要があります。
```
sh gen_pb.sh
```
```
protoc --java_out=../java --proto_path=. GameServerGrpcSdkService.proto
protoc --plugin=protoc-gen-grpc-java=`which protoc-gen-grpc-java` --grpc-java_out=../java --proto_path=. GameServerGrpcSdkService.proto
protoc --java_out=../java --proto_path=. GseGrpcSdkService.proto
protoc --plugin=protoc-gen-grpc-java=`which protoc-gen-grpc-java` --grpc-java_out=../java --proto_path=. GseGrpcSdkService.proto
```
 - 方法二：mavenツールを使用してgRPCコードを生成します。mavenの中にgrpcコードをコンパイルするmaven Plug-inを追加します。詳細については、[gRPC-Java-RPCライブラリおよびフレームワーク](https://github.com/grpc/grpc-java)をご参照ください。
<dx-codeblock>
::: java
<build>
	 <extensions>
	 <extension>
		<groupId>kr.motd.maven</groupId>
		<artifactId>os-maven-plugin</artifactId>
		<version>1.6.2</version>
	 </extension>
	 </extensions>
	 <plugins>
	 <plugin>
		<groupId>org.xolstice.maven.plugins</groupId>
		<artifactId>protobuf-maven-plugin</artifactId>
		<version>0.6.1</version>
		<configuration>
			<protocArtifact>com.google.protobuf:protoc:3.12.0:exe:${os.detected.classifier}</protocArtifact>
			<pluginId>grpc-java</pluginId>
			<pluginArtifact>io.grpc:protoc-gen-grpc-java:1.30.2:exe:${os.detected.classifier}</pluginArtifact>
		</configuration>
		<executions>
			<execution>
			<goals>
				<goal>compile</goal>
				<goal>compile-custom</goal>
			</goals>
		 </execution>
		 </executions>
	 </plugin>
	</plugins>
</build>
:::
</dx-codeblock>


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
```java
public GseResponseBo processReady(ProcessReadyRequestBo request) {
	logger.info("processReady request=" + new Gson().toJson(request));
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.ProcessReadyRequest rpcRequest = GseGrpcSdkServiceOuterClass.ProcessReadyRequest
					//ポート設定。
					.newBuilder().setClientPort(request.getClientPort())
					.setGrpcPort(request.getGrpcPort())
					//ログパス。
					.addAllLogPathsToUpload(request.getLogPathsToUploadList()).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().processReady(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	//準備完了。対外的にサービス提供可能。
	logger.info("processReady response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 2. プロセス準備完了後、GSEがOnHealthCheckインターフェースを呼び出し、Game Serverに対してヘルスチェックを実施します。1分ごとに1回検査し、連続3回失敗するとそのプロセスを異常と判定し、ゲームサーバーセッションをこのプロセスにアサインしません。
```java
public boolean onHealthCheck() {
	//ヘルスチェックのためにゲームサーバーのロジックを追加します。
	boolean res = getGrpcServiceConfig().getGseGrpcSdkServiceClient().isProcessHealth();
	logger.info("onHealthCheck status=" + res);
	return res;
}
```
 3. Clientが [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)インターフェースを呼び出して、ゲームサーバーセッションを作成し、このゲームサーバーセッションを1つのプロセスにアサインしたため、GSEがトリガーされて当該プロセスのonStartGameServerSessionインターフェースを呼び出し、GameServerSessionのステータスを「アクティベート中」に変更します。
```java
public GseResponseBo onStartGameServerSession(GameServerSessionBo gameServerSessionBo) {
	logger.info("onStartGameServerSession gameServerSession=" + new Gson().toJson(gameServerSessionBo));
	//ゲームサーバーセッションの起動に使用するゲームサーバーのロジックを追加します。

	//ゲームサーバーセッションを保存します。
	getGrpcServiceConfig().getGseGrpcSdkServiceClient().onStartGameServerSession(gameServerSessionBo);
	//ゲームサーバーセッションをアクティベートします。
	ActivateGameServerSessionRequestBo activateRequest = new ActivateGameServerSessionRequestBo();
	activateRequest.setGameServerSessionId(gameServerSessionBo.getGameServerSessionId());
	activateRequest.setMaxPlayers(gameServerSessionBo.getMaxPlayers());
	getGrpcServiceConfig().getGseGrpcSdkServiceClient().activateGameServerSession(activateRequest);

	//ここに最終的なロジックを追加します。
	return createResponseBo(0, "SUCCESS");
}
```
 4. Game Serverが onStartGameServerSessionを受信し、あなたが自らいくつかのロジックまたはリソースのアサインを処理して準備が完了すると、Game ServerがActivateGameServerSessionインターフェースを呼び出します。ゲームサーバーセッションがプロセスにすでにアサインされ、現在、プレイヤーのリクエストを受け入れる準備ができていることをGSEに通知し、サーバーのステータスを「アクティブ」に変更します。
```java
public GseResponseBo activateGameServerSession(ActivateGameServerSessionRequestBo request) {
	logger.info("activateGameServerSession request=" + new Gson().toJson(request));
	if (gameServerSessionBo == null) {
			return createResponseBo(Constants.gameServerSessionExpectCode, "no game server session found.");
	}
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.ActivateGameServerSessionRequest rpcRequest = GseGrpcSdkServiceOuterClass.ActivateGameServerSessionRequest
					.newBuilder().setMaxPlayers(request.getMaxPlayers())
					.setGameServerSessionId(gameServerSessionBo.getGameServerSessionId()).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().activateGameServerSession(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	logger.info("activateGameServerSession response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 5. Clientが[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130)インターフェースを呼び出してプレイヤーが参加すると、Game ServerがAcceptPlayerSessionインターフェースを呼び出してプレイヤーの合法性を検証します。接続が受け入れられた場合は、PlayerSessionのステータスを「アクティブ」に変更します。ClientがJoinGameServerSessionインターフェースを呼び出して60秒以内に応答がない場合は、PlayerSessionのステータスを「タイムアウト」に変更し、その後再び JoinGameServerSessionを呼び出します。
```java
public GseResponseBo acceptPlayerSession(PlayerSessionRequestBo request) {
	logger.info("acceptPlayerSession request=" + new Gson().toJson(request));
	if (gameServerSessionBo == null) {
			return createResponseBo(Constants.gameServerSessionExpectCode, "no game server session found.");
	}
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.AcceptPlayerSessionRequest rpcRequest = GseGrpcSdkServiceOuterClass.AcceptPlayerSessionRequest
					.newBuilder().setGameServerSessionId(gameServerSessionBo.getGameServerSessionId())
					.setPlayerSessionId(request.getPlayerSessionId()).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().acceptPlayerSession(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	logger.info("acceptPlayerSession response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 6. ゲーム終了またはプレイヤーの退出後、Game ServerがRemovePlayerSessionインターフェースを呼び出してプレイヤーを削除します。playersessionのステータスを「完了」 に変更し、ゲームサーバーセッションの中のプレイヤーの位置をリザーブします。
```java
public GseResponseBo removePlayerSession(PlayerSessionRequestBo request) {
	logger.info("removePlayerSession request=" + new Gson().toJson(request));
	if (gameServerSessionBo == null) {
			return createResponseBo(Constants.gameServerSessionExpectCode, "no game server session found.");
	}
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.RemovePlayerSessionRequest rpcRequest = GseGrpcSdkServiceOuterClass.RemovePlayerSessionRequest
					.newBuilder().setGameServerSessionId(gameServerSessionBo.getGameServerSessionId())
					.setPlayerSessionId(request.getPlayerSessionId()).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().removePlayerSession(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	logger.info("removePlayerSession response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 7. 1つのゲームサーバーセッション（1組のゲームの対戦または1つのサービス）が終了すると、Game ServerがTerminateGameServerSessionインターフェースを呼び出してGameServerSessionを終了し、GameServerSessionのステータスを「終了」に変更します。
```java
public GseResponseBo terminateGameServerSession(String gameServerSessionId) {
	logger.info("terminateGameServerSession request=" + gameServerSessionId);
	if (StringUtils.isEmpty(gameServerSessionId) && gameServerSessionBo != null
					&& !StringUtils.isEmpty(gameServerSessionBo.getGameServerSessionId())) {
			gameServerSessionId = gameServerSessionBo.getGameServerSessionId();
	}
	if (StringUtils.isEmpty(gameServerSessionId)) {
			return createResponseBo(Constants.gameServerSessionExpectCode, "no game server session found.");
	}
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.TerminateGameServerSessionRequest rpcRequest = GseGrpcSdkServiceOuterClass.TerminateGameServerSessionRequest
					.newBuilder().setGameServerSessionId(gameServerSessionId).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().terminateGameServerSession(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	logger.info("terminateGameServerSession response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 8. ヘルスチェックに失敗したかまたは容量縮小の時は、GSEがOnProcessTerminateインターフェースを呼び出してゲームプロセスを終了します。容量縮小時の根拠は、GSEコンソールで設定した[保護ポリシー](https://intl.cloud.tencent.com/document/product/1055/36675#test12)です。
```java
public GseResponseBo onProcessTerminate(long terminationTime) {
	logger.info("onProcessTerminate terminationTime=" + terminationTime);
	//現在ゲームサーバーを終了できます。

	return createResponseBo(0, "SUCCESS");
}
```
 9. Game ServerがProcessEndingインターフェースを呼び出してプロセスを直ちに終了させ、サーバープロセスのステータスを「終了」に変更してリソースを回収します。
```java
//自動呼び出し：ゲーム1局につき1つのプロセスが対応し、1局のゲームが終了すると自動でProcessEndingインターフェースを呼び出します
//手動呼び出し：容量縮小またはプロセスの異常によりヘルスチェックに失敗した時は、保護ポリシーにもとづき受動的にProcessEndingインターフェースが呼び出されます。完全保護および時間制限保護ポリシーを設定している時は、先にゲームサーバーセッション上のプレイヤーの有無を判断してから、手動で呼び出しを行う必要があります
public GseResponseBo processEnding() {
	logger.info("processEnding begin");
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.ProcessEndingRequest rpcRequest = GseGrpcSdkServiceOuterClass.ProcessEndingRequest
					.newBuilder().build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().processEnding(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	logger.info("processEnding response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 10. Game ServerがDescribePlayerSessionsインターフェースを呼び出してゲームサーバーセッション下のプレイヤー情報を取得します（業務に応じて任意選択）。
```java
public DescribePlayerSessionsResponseBo describePlayerSessions(DescribePlayerSessionsRequestBo request) {
	logger.info("describePlayerSessions request=" + new Gson().toJson(request));
	if (StringUtils.isEmpty(request.getGameServerSessionId()) &&
					gameServerSessionBo != null && !StringUtils.isEmpty(gameServerSessionBo.getGameServerSessionId())) {
			request.setGameServerSessionId(gameServerSessionBo.getGameServerSessionId());
	}
	GseGrpcSdkServiceOuterClass.DescribePlayerSessionsRequest rpcRequest = GseGrpcSdkServiceOuterClass.DescribePlayerSessionsRequest
					.newBuilder().setGameServerSessionId(request.getGameServerSessionId())
					.setLimit(request.getLimit())
					.setNextToken(request.getNextToken())
					.setPlayerId(request.getPlayerId())
					.setPlayerSessionId(request.getPlayerSessionId())
					.setPlayerSessionStatusFilter(request.getPlayerSessionStatusFilter()).build();

	GseGrpcSdkServiceOuterClass.DescribePlayerSessionsResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().describePlayerSessions(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return null;
	}
	logger.info("describePlayerSessions response=" + rpcResponse.toString());
	return toPlayerSessionsResponseBo(rpcResponse);
}
```
 11. Game ServerがUpdatePlayerSessionCreationPolicyインターフェースを呼び出してプレイヤーセッションの作成ポリシーを更新し、新規プレイヤーの受け入れの是非、つまりゲームセッションにプレイヤーの参加を許可するかを設定します（業務に応じて任意選択）。
```java
public GseResponseBo updatePlayerSessionCreationPolicy(UpdatePlayerSessionCreationPolicyRequestBo request) {
	logger.info("updatePlayerSessionCreationPolicy request=" + new Gson().toJson(request));
	if (gameServerSessionBo == null) {
			return createResponseBo(Constants.gameServerSessionExpectCode, "no game server session found.");
	}
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.UpdatePlayerSessionCreationPolicyRequest rpcRequest = GseGrpcSdkServiceOuterClass.UpdatePlayerSessionCreationPolicyRequest
					.newBuilder().setGameServerSessionId(gameServerSessionBo.getGameServerSessionId())
					.setNewPlayerSessionCreationPolicy(request.getNewPlayerSessionCreationPolicy()).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().updatePlayerSessionCreationPolicy(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	logger.info("updatePlayerSessionCreationPolicy response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 12. Game ServerがReportCustomDataインターフェースを呼び出し、GSEにカスタムデータを通知します（業務に応じて任意選択）。
```java
public GseResponseBo reportCustomData(ReportCustomDataRequestBo request) {
	logger.info("reportCustomData request=" + new Gson().toJson(request));
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.ReportCustomDataRequest rpcRequest = GseGrpcSdkServiceOuterClass.ReportCustomDataRequest
					.newBuilder()
					.setCurrentCustomCount(request.getCurrentCustomCount())
					.setMaxCustomCount(request.getMaxCustomCount()).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().reportCustomData(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	logger.info("reportCustomData response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```

## GSEをコールするためにサーバーを起動します。
サーバーの実行：GrpcServerを起動します。
 ```java
@Bean(name = "grpcService", initMethod = "startup", destroyMethod = "shutdown")
	public GrpcService getGrpcService() {
		GrpcServiceConfig grpcServiceConfig = new GrpcServiceConfig();
		grpcServiceConfig.setGseGrpcSdkServiceClient(gseGrpcSdkServiceClient);
		grpcServiceConfig.setGameServerGrpcPort(gameServerGrpcPort);
		grpcServiceConfig.setGameServerToClientPort(gameServerToClientPort);
		grpcServiceConfig.setTargetAddress(targetAddress);
		grpcServiceConfig.setGameServerUploadLogPath(gameServerUploadLogPath);
		GrpcService grpcService = new GrpcService(grpcServiceConfig);
		return grpcService;
}
 ```

## クライアントをGSEのgRPCサーバーに接続
サーバーに接続：gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使ってスタブインスタンスを作成します。
```java
public GseGrpcSdkServiceGrpc.GseGrpcSdkServiceBlockingStub getGseGrpcSdkServiceClient() {     
	// ここの「channel」は1つのチャネルであり、ManagedChannelではないため、このコードのタスクはそれを無効にすることではありません。
	//チャネルをコードに転送し、コードがテストとチャネルをより再利用しやすくなるようにします。
	if (blockingStub == null) {
			managedChannel = getGrpcChannel(targetAddress);
			blockingStub = GseGrpcSdkServiceGrpc.newBlockingStub(managedChannel);
	}
	if (managedChannel.isShutdown() || managedChannel.isTerminated()) {
			managedChannel.shutdownNow();
			managedChannel = getGrpcChannel(targetAddress);
			blockingStub = GseGrpcSdkServiceGrpc.newBlockingStub(managedChannel);
	}
	return blockingStub;
}
```
## Java DEMO
 1. [ここをクリック](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/java-demo.zip)して、Java DEMOコードをダウンロードします。
 2. gRPCコードを生成します。
Java DEMOコードのサンプルの中にgRPCコードがすでに生成されています。java-demo/src/main/java/tencentcloudディレクトリ下にありますので、別途生成する必要はありません。
 3. GSEをコールするためにサーバーを起動します。
  - サーバーの実装。
java-demo/src/main/java/com/tencentcloud/gse/gameserver/service/gamelogic/implディレクトリ下の GameServerGrpcCallbackImpl.javaに、サーバーの3つのインターフェースを実装しています。
  - サーバーの実行。
java-demo/src/main/java/com/tencentcloud/gse/gameserver/config ディレクトリ下のGameServerConfig.javaで、GrpcServerを起動します。
 4. クライアントをGSEのgRPCサーバーに接続します。
  - クライアントの実装。
java-demo/src/main/java/com/tencentcloud/gse/gameserver/service/gsegrpc/impl ディレクトリ下の GseGrpcSdkServiceClientImpl.javaに、クライアントの9つのインターフェースを実装しています。
  - サーバーに接続。
gRPCのチャネルを作成して、接続したいホスト名とサーバーポートを指定し、その後このチャネルを使用してスタブインスタンスを作成します。
 5. コンパイルして実行。
  1. インストールするjavaの バージョンは1.8以上が必要です。linuxではyumを使用してopenjdkをインストールできます。
```
yum install -y java-1.8.0-openjdk
```
- コードをダウンロードし、java-demoディレクトリ下で、mavenを利用してビルドし、gse-gameserver-demo.jarを生成します。次のコマンドを使用して起動します。
   ```
   java -jar gse-gameserver-demo.jar
   ```
- 実行可能ファイルgse-gameserver-demo.jar をパッケージングして [アセット](https://intl.cloud.tencent.com/document/product/1055/36674)を作成します。起動パスの設定は java、起動パラメータの設定はjar gse-gameserver-demo.jarとします。
- その後、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)でサーバーフリートを作成し、アセットをサーバーフリートにデプロイします。この後引き続き、[スケーリング](https://intl.cloud.tencent.com/document/product/1055/37445) などの一連の操作を行うことができます。

