
## Installing gRPC
1. Prerequisites: install Node.js v12.16.0 or above.
2. Install gRPC.
<dx-alert infotype="explain" title="">
For more information, please see [Installing gRPC Node.js](https://github.com/grpc/grpc/tree/master/examples/node).
</dx-alert>


## Defining Service

gRPC uses Protocol Buffers to define a service: an RPC service specifies methods that can be called remotely by using parameters and return types.
<dx-alert infotype="explain" title="">
We provide the .proto files for service definition. You can [click here](https://intl.cloud.tencent.com/document/product/1055/37419) to directly download them with no need to generate them by yourself.
</dx-alert>



## Generating gRPC Code
1. After defining the service, you can use protoc (protocol buffer compiler) to generate the client and server code (in any language supported by gRPC). 
2. The generated code includes the client stub and the abstract APIs to be implemented by the server.
3. Generate the gRPC code.
    Node.js uses `grpc/proto-loader` to load `pb` files directly, so there is no need to generate `gRPC-nodejs` code.

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
```
function ProcessReady(param) {
		console.log("ProcessReady.request", param);
		getGseGrpcSdkServiceClient().ProcessReady({
				// Log path
				logPathsToUpload: param.logPathsToUpload,
				// Set the ports
				clientPort: param.clientPort,
				grpcPort: param.grpcPort
		}, getMetadata(), function (err, response) {
				// Ready to provide services
				console.log('ProcessReady.response:', err, response);
		});
}
```
 2. After the process is ready, GSE will call the `OnHealthCheck` API to perform a health check on the game server every minute. If the health check fails three consecutive times, the process will be considered to be unhealthy, and no game server sessions will be assigned to it.
```
function OnHealthCheck(call, callback) {
		console.log("OnHealthCheck.request", call.request);

		callback(null, {healthStatus: gsesdkClient.IsProcessHealth() });
}
```
 3. Because the client calls the [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) API to create a game server session and assigns it to a process, GSE will be triggered to call the `onStartGameServerSession` API for the process and change the status of `GameServerSession` to "Activating".
```
function OnStartGameServerSession(call, callback) {
		console.log("OnStartGameServerSession.request", call.request);
		gsesdkClient.OnStartGameServerSession(call.request);
		callback(null, {});
}
```
 4. After the game server receives `onStartGameServerSession`, you need to handle the logic or resource allocation by yourself. After everything is ready, the game server will call the `ActivateGameServerSession` API to notify GSE that the game server session has been assigned to a process and is ready to receive player requests and will change the server status to "Active".
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
 5. After the client calls the [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130) API for the player to join, the game server will call the `AcceptPlayerSession` API to verify the validity of the player. If the connection is accepted, the status of `PlayerSession` will be set to "Active". If the client receives no response within 60 seconds after calling the `JoinGameServerSession` API, it will change the status of `PlayerSession` to "Timeout" and then call `JoinGameServerSession` again.
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
 6. After the game ends or the player exits, the game server will call the `RemovePlayerSession` API to remove the player, change the status of `playersession` to "Completed", and reserve the player slot in the game server session.
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
 7. After a game server session (a game battle or a service) ends, the game server will call the `TerminateGameServerSession` API to end the `GameServerSession` and change its status to `Terminated`.
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
 8. In case of health check failure or reduction, GSE will call the `OnProcessTerminate` API to end the game process. The reduction will be triggered according to the [protection policy](https://intl.cloud.tencent.com/document/product/1055/36675) configured in the GSE console.
```
function OnProcessTerminate(call, callback) {
		console.log("OnProcessTerminate.request", call.request);
		callback(null, {});
}
```
 9. The game server calls the `ProcessEnding` API to end the process immediately, change the server process status to "Terminated", and repossess the resources.
```
// Active call: a game battle corresponds to a process. The `ProcessEnding` API will be actively called after the game battle ends
// Passive call: in case of reduction, process exception, or health check failure, the `ProcessEnding` API will be called passively according to the protection policy. If a full protection or time-period protection policy is configured, it is required to determine whether there are any players in the game server session before the passive call can be made
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
 10. The game server calls the `DescribePlayerSessions` API to get the information of the player in the game server session (which is optional based on your actual business needs).
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
 11. The game server calls the `UpdatePlayerSessionCreationPolicy` API to update the player session creation policy and set whether to accept new players, i.e., whether to allow new players to join a game session (which is optional based on your actual business needs).
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
 12. The game server calls the `ReportCustomData` API to notify GSE of the custom data (which is optional based on your actual business needs).
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

## Launching Server for GSE to Call

Server running: launch `GrpcServer`.
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

## Connecting Client to gRPC Server of GSE
Server connecting: create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
```
function getGseGrpcSdkServiceClient() {
  if (gseGrpcClient == null) {
    gseGrpcClient = new GseGrpcSdkServiceProto.GseGrpcSdkService('127.0.0.1:5758', grpc.credentials.createInsecure());
  }
  return gseGrpcClient;
}
```

## Nodejs DEMO
 1. [Click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/nodejs-demo.zip) to download the code of the Demo for Node.js.
 2. Generate the gRPC code.
Node.js uses `grpc/proto-loader` to load `pb` files directly, so there is no need to generate `gRPC-nodejs` code.
 3. Launch the server for GSE to call.
  - Implement the server.
`game_server.js` in the `nodejs-demo/dynamic_code` directory implements three server APIs.
  - Run the server.
`game_server.js` in the `nodejs-demo/dynamic_code` directory launches `GrpcServer`.
 4. Connect the client to the gRPC server of GSE.
  - Implement the client.
`gsesdk_client.js` in the `nodejs-demo/dynamic_code` directory implements nine client APIs.
  - Connect to the server.
Create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
 5. Compile and run the project.
  1. Install Node.js v12.16.0 or above.
  - Install the gRPC package.
 ```
cnpm install --save grpc-tools
cnpm install --save google-protobuf 
cnpm install --save grpc
cnpm install --save @grpc/proto-loader
cnpm install --save @grpc/grpc-js
 ```
 If you cannot download dependencies outside Mainland China, you need to configure an npm site in Mainland China.
  - Download the code and run the following command in the `nodejs-demo` directory to launch the test:
	```
	cd dynamic_code
	node game_server.js  
 ```
  - Package the executable file `game_server.js` as an [asset package](https://intl.cloud.tencent.com/document/product/1055/36674) and configure the launch path as `node` and the launch parameter as `game_server.js`.
  - [Create a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675) and deploy the asset package on it. After that, you can perform various operations such as [scaling](https://intl.cloud.tencent.com/document/product/1055/37445).
