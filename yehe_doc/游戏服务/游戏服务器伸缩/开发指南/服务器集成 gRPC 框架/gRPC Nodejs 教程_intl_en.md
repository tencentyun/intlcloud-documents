
## Installing gRPC
1. Install gRPC. The installation will generate an executable program `grpc_cpp_plugin`, which will be needed for generating gRPC code.
2. Install protocol buffers.

<dx-alert infotype="explain" title="">
For more information on the installation process, see [Installing gRPC Lua](https://github.com/grpc/grpc/blob/master/BUILDING.md) and [Installing Protocol Buffers](https://github.com/protocolbuffers/protobuf/blob/master/src/README.md).
</dx-alert>




## Defining Service
 gRPC uses Protocol Buffers to define a service: an RPC service specifies methods that can be called remotely by using parameters and return types.


<dx-alert infotype="explain" title="">
We provide the .proto files for service definition. You can [click here](https://intl.cloud.tencent.com/document/product/1055/37419) to directly download them with no need to generate them by yourself.
</dx-alert>



## Generating gRPC Code
1. After defining the service, you can use protoc (protocol buffer compiler) to generate the client and server code (in any language supported by gRPC). 
2. The generated code includes the client stub and the abstract APIs to be implemented by the server.
3. Steps for generating gRPC code:
   1. The Demo for Lua relies on the C++ framework. Just like with the Demo for C++, in the `proto` directory, run:
		 ```plaintext
		 protoc --cpp_out=. *.proto
		```
  2. Generate the `pb.cc` and `pb.h` files.
		```plaintext
		protoc --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` *.proto
	```
 3. Generate the corresponding gRPC code.
 4. Move the eight generated files to an appropriate location in the project.    

## Game Process Integration Process
![](https://main.qcloudimg.com/raw/96018551bc88c71a02333b1f197b3111.png)


#### Game server callback API list

| API Name | API Description |
|-----|----|
|[OnHealthCheck](https://intl.cloud.tencent.com/document/product/1055/37422)| Runs health check|
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
```JavaScript
static bool luaProcessReady(std::vector <std::string> &logPath, int clientPort, int grpcPort) {
	GseResponse reply;
	// Log path. Set the ports.
	Status status = GGseManager->ProcessReady(logPath, clientPort, grpcPort, reply);
	// Ready to provide services
	GSESDK()->setReplyStatus(status);
	if (!status.ok()) {
		return false;
	}
	return true;
}
```
 2. After the process is ready, GSE will call the `OnHealthCheck` API to perform a health check on the game server every minute. If the health check fails three consecutive times, the process will be considered to be unhealthy, and no game server sessions will be assigned to it.
```JavaScript
Status GameServerGrpcSdkServiceImpl::OnHealthCheck(ServerContext* context, const HealthCheckRequest* request,  HealthCheckResponse* reply)
{
	healthStatus = GSESDK()->exec("return OnHealthCheck()");
	std::cout << "healthStatus=" << healthStatus << std::endl;
	reply->set_healthstatus(healthStatus);
	return Status::OK;
}
```
 3. Because the client calls the [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) API to create a game server session and assigns it to a process, GSE will be triggered to call the `onStartGameServerSession` API for the process and change the status of `GameServerSession` to "Activating".
```JavaScript
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
 4. After the game server receives `onStartGameServerSession`, you need to handle the logic or resource allocation by yourself. After everything is ready, the game server will call the `ActivateGameServerSession` API to notify GSE that the game server session has been assigned to a process and is ready to receive player requests and will change the server status to "Active".
```JavaScript
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
 5. After the client calls the [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130) API for the player to join, the game server will call the `AcceptPlayerSession` API to verify the validity of the player. If the connection is accepted, the status of `PlayerSession` will be set to "Active". If the client receives no response within 60 seconds after calling the `JoinGameServerSession` API, it will change the status of `PlayerSession` to "Timeout" and then call `JoinGameServerSession` again.
```JavaScript
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
 6. After the game ends or the player exits, the game server will call the `RemovePlayerSession` API to remove the player, change the status of `playersession` to "Completed", and reserve the player slot in the game server session.
```JavaScript
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
 7. After a game server session (a game battle or a service) ends, the game server will call the `TerminateGameServerSession` API to end the `GameServerSession` and change its status to `Terminated`.
```JavaScript
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
 8. In case of health check failure or reduction, GSE will call the `OnProcessTerminate` API to end the game process. The reduction will be triggered according to the [protection policy](https://intl.cloud.tencent.com/document/product/1055/36675) configured in the GSE console.
```JavaScript
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
 9. The game server calls the `ProcessEnding` API to end the process immediately, change the server process status to "Terminated", and repossess the resources.
```JavaScript
// Active call: a game battle corresponds to a process. The `ProcessEnding` API will be actively called after the game battle ends
// Passive call: in case of reduction, process exception, or health check failure, the `ProcessEnding` API will be called passively according to the protection policy. If a full protection or time-period protection policy is configured, it is required to determine whether there are any players in the game server session before the passive call can be made
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
 10. The game server calls the `DescribePlayerSessions` API to get the information of the player in the game server session (which is optional based on your actual business needs).
```JavaScript
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
 11. The game server calls the `UpdatePlayerSessionCreationPolicy` API to update the player session creation policy and set whether to accept new players, i.e., whether to allow new players to join a game session (which is optional based on your actual business needs).
```JavaScript
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
 12. The game server calls the `ReportCustomData` API to notify GSE of the custom data (which is optional based on your actual business needs).
```JavaScript
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

## Launching Server for GSE to Call

Server running: launch `GrpcServer`.
```JavaScript
// Launch the gRPC server
std::thread tGrpc(&GameServerGrpcSdkServiceImpl::StartGrpcServer, GGameServerGrpcSdkService);
sem_wait(&(GGameServerGrpcSdkService->sem));
auto grpcPort = GGameServerGrpcSdkService->GetGrpcPort();
```

## Connecting Client to gRPC Server of GSE
Server connecting: create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
```JavaScript
void GseManager::InitStub() {
	auto channel = grpc::CreateChannel("127.0.0.1:5758", grpc::InsecureChannelCredentials());
	stub_ = GseGrpcSdkService::NewStub(channel);
}
```

## Demo for Lua
 1. [Click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/lua-demo.zip) to download the code of the Demo for Lua.
 2. Generate the gRPC code.
The Demo for Lua relies on the C++ framework, with gRPC code generated in the `cpp-demo/source/grpcsdk` directory, so there is no need to generate it again.
 3. Launch the server for GSE to call.
  - Implement the server.
`grpcserver.cpp` in the `lua-demo/source/api` directory implements three server APIs.
  - Run the server.
`main.cpp` in the `lua-demo` directory launches `GrpcServer`.
 4. Connect the client to the gRPC server of GSE.
  - Implement the client.
`GSESdkHandleWrapper.cpp` in the `lua-demo/source/lua` directory implements nine client APIs.
  - Connect to the server.
Create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
 5. Compile and run the project.
  1. Install CMake.
  - Install GCC v4.9 or above.
  - Install the LuaJIT and Boost development kits:
 ```
yum install -y luajit-devel
yum install -y boost-devel
yum install -y cmake
 ```
  - Download the code and run the following command in the `lua-demo` directory:
 ```
 mkdir build
 cd build
 cmake ..
 make
 cp ../source/lua/gse.lua .
 ```
  The corresponding `lua-demo` executable file will be generated. Run `./lua-demo` to launch it.
  - Package the executable file `lua-demo.cpp` as an [asset package](https://intl.cloud.tencent.com/document/product/1055/36674) and configure the launch path as `lua-demo` with no launch parameter needed.
  - [Create a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675) and deploy the asset package on it. After that, you can perform various operations such as [scaling](https://intl.cloud.tencent.com/document/product/1055/37445).
