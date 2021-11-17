
## Installing gRPC
1. gRPC Java does not require other tools except JDK.
2. Install the gRPC Java SNAPSHOT library locally, including the code generation plugin.
>?For more information on the installation process, please see [Installing gRPC Java](https://github.com/grpc/grpc-java/blob/master/COMPILING.md).
## Defining Service
gRPC uses Protocol Buffers to define a service: an RPC service specifies methods that can be called remotely by using parameters and return types.

<dx-alert infotype="explain" title="">
We provide the .proto files for service definition. You can [click here](https://intl.cloud.tencent.com/document/product/1055/37419) to directly download them with no need to generate them by yourself.

</dx-alert>



## Generating gRPC Code
1. After defining the service, you can use protoc (protocol buffer compiler) to generate the client and server code (in any language supported by gRPC). 
2. The generated code includes the client stub and the abstract APIs to be implemented by the server.
3. Methods for generating gRPC code:
 - Method 1. Execute the script under `java-demo/src/main/proto`. You need to download `protoc` and `protoc-gen-grpc-java` generation tools from the gRPC website:
```
sh gen_pb.sh
```
```
protoc --java_out=../java --proto_path=. GameServerGrpcSdkService.proto
protoc --plugin=protoc-gen-grpc-java=`which protoc-gen-grpc-java` --grpc-java_out=../java --proto_path=. GameServerGrpcSdkService.proto
protoc --java_out=../java --proto_path=. GseGrpcSdkService.proto
protoc --plugin=protoc-gen-grpc-java=`which protoc-gen-grpc-java` --grpc-java_out=../java --proto_path=. GseGrpcSdkService.proto
```
 - Method 2. Use the Maven tool to generate gRPC code by adding a Maven plugin for compiling gRPC code to Maven. For more information, please see [here](https://github.com/grpc/grpc-java).
<dx-codeblock>
:::  Java
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


## Game Process Integration Process
![](https://main.qcloudimg.com/raw/96018551bc88c71a02333b1f197b3111.png)

#### Game server callback API list

| API Name | API Description |
|-----|----|
|[OnHealthCheck](https://intl.cloud.tencent.com/document/product/1055/37422)| Runs health check |
|[OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423)| Receives game server session |
|[OnProcessTerminate](https://intl.cloud.tencent.com/document/product/1055/37424)| Ends game process |

#### Game server active API list

| API Name | API Description |
|-----|----|
|[ProcessReady](https://intl.cloud.tencent.com/document/product/1055/37426)| Gets process ready |
|[ActivateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37427)| Activates game server session |
|[AcceptPlayerSession](https://intl.cloud.tencent.com/document/product/1055/37428)| Receives player session |
|[RemovePlayerSession](https://intl.cloud.tencent.com/document/product/1055/37429)| Removes player session |
|[DescribePlayerSessions](https://intl.cloud.tencent.com/document/product/1055/37430)| Gets player session list |
|[UpdatePlayerSessionCreationPolicy](https://intl.cloud.tencent.com/document/product/1055/37431)| Updates player session creation policy |
|[TerminateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37432)| Ends game server session |
|[ProcessEnding](https://intl.cloud.tencent.com/document/product/1055/37434)| Ends process |
|[ReportCustomData](https://intl.cloud.tencent.com/document/product/1055/37435)| Reports custom data |

#### Others
 When the game process uses gRPC to call a game server active API, you need to add two fields to `meta` of the gRPC request.

| Field      | Description                                      | Type   |
| --------- | ----------------------------------------- | ------ |
| pid       | `pid` of the current game process                         | string |
| requestId | `requestId` of the current request, which is used to uniquely identify a request | string |

 1. Generally, after the server is initialized, the process will check itself to see whether it can provide services, and the game server will call the `ProcessReady` API to notify GSE that the process is ready to host a game server session. After receiving the notification, GSE will change the status of the server instance to "Active".
```Java
public GseResponseBo processReady(ProcessReadyRequestBo request) {
	logger.info("processReady request=" + new Gson().toJson(request));
	GseResponseBo responseBo = new GseResponseBo();
	GseGrpcSdkServiceOuterClass.ProcessReadyRequest rpcRequest = GseGrpcSdkServiceOuterClass.ProcessReadyRequest
					// Set the ports.
					.newBuilder().setClientPort(request.getClientPort())
					.setGrpcPort(request.getGrpcPort())
					// Log path.
					.addAllLogPathsToUpload(request.getLogPathsToUploadList()).build();

	GseGrpcSdkServiceOuterClass.GseResponse rpcResponse;
	try {
			rpcResponse = getGseGrpcSdkServiceClient().processReady(rpcRequest);
	} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return createRpcFailedResponseBo(e.getStatus());
	}
	// Ready to provide services.
	logger.info("processReady response=" + rpcResponse.toString());
	return createResponseBoByRpcResponse(rpcResponse);
}
```
 2. After the process is ready, GSE will call the `OnHealthCheck` API to perform a health check on the game server every minute. If the health check fails three consecutive times, the process will be considered to be unhealthy, and no game server sessions will be assigned to it.
```Java
public boolean onHealthCheck() {
	// Add game server logic for health check.
	boolean res = getGrpcServiceConfig().getGseGrpcSdkServiceClient().isProcessHealth();
	logger.info("onHealthCheck status=" + res);
	return res;
}
```
 3. Because the client calls the [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) API to create a game server session and assigns it to a process, GSE will be triggered to call the `onStartGameServerSession` API for the process and change the status of `GameServerSession` to "Activating".
```Java
public GseResponseBo onStartGameServerSession(GameServerSessionBo gameServerSessionBo) {
	logger.info("onStartGameServerSession gameServerSession=" + new Gson().toJson(gameServerSessionBo));
	// Add the game server logic used to launch the game server session.

	// Save the game server sessions
	getGrpcServiceConfig().getGseGrpcSdkServiceClient().onStartGameServerSession(gameServerSessionBo);
	// Activate the game server sessions
	ActivateGameServerSessionRequestBo activateRequest = new ActivateGameServerSessionRequestBo();
	activateRequest.setGameServerSessionId(gameServerSessionBo.getGameServerSessionId());
	activateRequest.setMaxPlayers(gameServerSessionBo.getMaxPlayers());
	getGrpcServiceConfig().getGseGrpcSdkServiceClient().activateGameServerSession(activateRequest);

	// Add the final logic here.
	return createResponseBo(0, "SUCCESS");
}
```
 4. After the game server receives `onStartGameServerSession`, you need to handle the logic or resource allocation by yourself. After everything is ready, the game server will call the `ActivateGameServerSession` API to notify GSE that the game server session has been assigned to a process and is ready to receive player requests and will change the server status to "Active".
```Java
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
 5. After the client calls the [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130) API for the player to join, the game server will call the `AcceptPlayerSession` API to verify the validity of the player. If the connection is accepted, the status of `PlayerSession` will be set to "Active". If the client receives no response within 60 seconds after calling the `JoinGameServerSession` API, it will change the status of `PlayerSession` to "Timeout" and then call `JoinGameServerSession` again.
```Java
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
 6. After the game ends or the player exits, the game server will call the `RemovePlayerSession` API to remove the player, change the status of `playersession` to "Completed", and reserve the player slot in the game server session.
```Java
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
 7. After a game server session (a game battle or a service) ends, the game server will call the `TerminateGameServerSession` API to end the `GameServerSession` and change its status to `Terminated`.
```Java
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
 8. In case of health check failure or reduction, GSE will call the `OnProcessTerminate` API to end the game process. The reduction will be triggered according to the [protection policy](https://intl.cloud.tencent.com/document/product/1055/36675) configured in the GSE console.
```Java
public GseResponseBo onProcessTerminate(long terminationTime) {
	logger.info("onProcessTerminate terminationTime=" + terminationTime);
	// It is possible to end the game server now.

	return createResponseBo(0, "SUCCESS");
}
```
 9. The game server calls the `ProcessEnding` API to end the process immediately, change the server process status to "Terminated", and repossess the resources.
```Java
// Active call: a game battle corresponds to a process. The `ProcessEnding` API will be actively called after the game battle ends
// Passive call: in case of reduction, process exception, or health check failure, the `ProcessEnding` API will be called passively according to the protection policy. If a full protection or time-period protection policy is configured, it is required to determine whether there are any players in the game server session before the passive call can be made
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
 10. The game server calls the `DescribePlayerSessions` API to get the information of the player in the game server session (which is optional based on your actual business needs).
```Java
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
 11. The game server calls the `UpdatePlayerSessionCreationPolicy` API to update the player session creation policy and set whether to accept new players, i.e., whether to allow new players to join a game session (which is optional based on your actual business needs).
```Java
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
 12. The game server calls the `ReportCustomData` API to notify GSE of the custom data (which is optional based on your actual business needs).
```Java
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

## Launching Server for GSE to Call
Server running: launch `GrpcServer`.
 ```Java
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

## Connecting Client to gRPC Server of GSE
Server connecting: create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
```java
public GseGrpcSdkServiceGrpc.GseGrpcSdkServiceBlockingStub getGseGrpcSdkServiceClient() {     
	// The "channel" here is a channel instead of a `ManagedChannel`; therefore, it is not the responsibility of the code to shut it down.
	// Pass the channel to the code to make it easier for the code to test and reuse the channel.
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
## Demo for Java
 1. [Click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/java-demo.zip) to download the code of the Demo for Java.
 2. Generate the gRPC code.
As the gRPC code has already been generated in the `java-demo/src/main/java/tencentcloud` directory of the Demo for Java, you do not need to generate it again.
 3. Launch the server for GSE to call.
  - Implement the server.
`GameServerGrpcCallbackImpl.java` in the `java-demo/src/main/java/com/tencentcloud/gse/gameserver/service/gamelogic/impl` directory implements three server APIs.
  - Run the server.
`GameServerConfig.java` in the `java-demo/src/main/java/com/tencentcloud/gse/gameserver/config` directory launches `GrpcServer`.
 4. Connect the client to the gRPC server of GSE.
  - Implement the client.
`GseGrpcSdkServiceClientImpl.java` in the `java-demo/src/main/java/com/tencentcloud/gse/gameserver/service/gsegrpc/impl` directory implements nine client APIs.
  - Connect to the server.
Create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
 5. Compile and run the project.
  1. Java v1.8 or above is required. You can use `yum` to install `openjdk` on Linux:
```
yum install -y java-1.8.0-openjdk
```
- Download the code, use Maven to build and generate `gse-gameserver-demo.jar` in the `java-demo` directory, and run the following command to launch it:
   ```
   java -jar gse-gameserver-demo.jar
   ```
- Package the executable file `gse-gameserver-demo.jar` as an [asset package](https://intl.cloud.tencent.com/document/product/1055/36674) and configure the launch path as `java` and the launch parameter as `jar gse-gameserver-demo.jar`.
- [Create a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675) and deploy the asset package on it. After that, you can perform various operations such as [scaling](https://intl.cloud.tencent.com/document/product/1055/37445).

