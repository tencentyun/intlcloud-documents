

## Installing gRPC
1. Prerequisites: install CMake.
  - Linux
	<dx-codeblock>
	:::  linux
		$ sudo apt install -y cmake
	:::
	</dx-codeblock>
  - MAC OS
    <dx-codeblock>
	:::  iOS
		$ brew install cmake
	:::
	</dx-codeblock>
2. Install gRPC and Protocol Buffers locally.
<dx-alert infotype="explain" title="">
For more information on the installation process, see [Installing CMake](https://cmake.org/install), [Installing gRPC C++](https://github.com/grpc/grpc/blob/master/BUILDING.md), and [Installing Protocol Buffers](https://github.com/protocolbuffers/protobuf/blob/master/src/README.md).
</dx-alert>




## Defining Service
gRPC uses Protocol Buffers to define a service: an RPC service specifies methods that can be called remotely by using parameters and return types.

<dx-alert infotype="explain" title="">
We provide the [.proto files](https://intl.cloud.tencent.com/document/product/1055/37419) for service definition. You can directly download them with no need to generate them by yourself.
</dx-alert>


## Generating gRPC Code
1. After defining the service, you can use protoc (protocol buffer compiler) to generate the client and server code (in any language supported by gRPC). 
2. The generated code includes the client stub and the abstract APIs to be implemented by the server.
3. Steps for generating gRPC code:
    In the `proto` directory, run:
 ```
 protoc --cpp_out=. *.proto
 ```
to generate the `pb.cc` and `pb.h` files.

```
protoc --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` *.proto
```

to generate the corresponding gRPC code.
Move the eight generated files to an appropriate location in the project.

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
<dx-codeblock>
:::  Java
Status GseManager::ProcessReady(std::vector<std::string> &logPath, int clientPort, int grpcPort, GseResponse& reply)
{
	ProcessReadyRequest request;
	// Log path
	for (auto iter = logPath.begin(); iter != logPath.end(); iter++)
	{
		request.add_logpathstoupload(*iter);
	}

	GConsoleLog->PrintOut(true, "ProcessReady clientPort is %d\n", clientPort);
	GConsoleLog->PrintOut(true, "ProcessReady grpcPort is %d\n", grpcPort);

	// Set the ports
	request.set_clientport(clientPort);
	request.set_grpcport(grpcPort);

	ClientContext context;
	AddMetadata(context);

	// Ready to provide services
	return stub_->ProcessReady(&context, request, &reply);
}
:::
</dx-codeblock>

2. After the process is ready, GSE will call the `OnHealthCheck` API to perform a health check on the game server every minute. If the health check fails three consecutive times, the process will be considered to be unhealthy, and no game server sessions will be assigned to it.
```
Status GameServerGrpcSdkServiceImpl::OnHealthCheck(ServerContext* context, const HealthCheckRequest* request,  HealthCheckResponse* reply)
{
	reply->set_healthstatus(healthStatus);
	return Status::OK;
}
```
3. Because the client calls the [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) API to create a game server session and assigns it to a process, GSE will be triggered to call the `onStartGameServerSession` API for the process and change the status of `GameServerSession` to "Activating".
```
Status GameServerGrpcSdkServiceImpl::OnStartGameServerSession(ServerContext* context, const StartGameServerSessionRequest* request,  GseResponse* reply)
{
	auto gameServerSession = request->gameserversession();
	GGseManager->SetGameServerSession(gameServerSession);

	GseResponse processReadyReply;
	Status status = GGseManager->ActivateGameServerSession(gameServerSession.gameserversessionid(), gameServerSession.maxplayers(), processReadyReply);
	// Determine whether the activation has succeeded based on `status` and `replay`
	
	return Status::OK;
}
```
4. After the game server receives `onStartGameServerSession`, you need to handle the logic or resource allocation by yourself. After everything is ready, the game server will call the `ActivateGameServerSession` API to notify GSE that the game server session has been assigned to a process and is ready to receive player requests and will change the server status to "Active".
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
5. After the client calls the [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130) API for the player to join, the game server will call the `AcceptPlayerSession` API to verify the validity of the player. If the connection is accepted, the status of `PlayerSession` will be set to "Active". If the client receives no response within 60 seconds after calling the `JoinGameServerSession` API, it will change the status of `PlayerSession` to "Timeout" and then call `JoinGameServerSession` again.
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
6. After the game ends or the player exits, the game server will call the `RemovePlayerSession` API to remove the player, change the status of `playersession` to "Completed", and reserve the player slot in the game server session.
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
7. After a game server session (a game battle or a service) ends, the game server will call the `TerminateGameServerSession` API to end the `GameServerSession` and change its status to `Terminated`.
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

8. In case of health check failure or reduction, GSE will call the `OnProcessTerminate` API to end the game process. The reduction will be triggered according to the [protection policy](https://intl.cloud.tencent.com/document/product/1055/36675) configured in the GSE console.
```
Status GameServerGrpcSdkServiceImpl::OnProcessTerminate(ServerContext* context, const ProcessTerminateRequest* request,  GseResponse* reply)
{
	auto terminationTime = request->terminationtime();
	GGseManager->SetTerminationTime(terminationTime);

	// If the following two APIs are called, the game server session will be ended immediately. We recommend you call `ProcessEnding` to end the process only when there are no players or game server sessions
	// If the following two APIs are not called, `ProcessEnding` will be called to end the process according to the protection policy. We recommend you configure time-period protection
	
	//End the game server sessions
	GseResponse terminateGameServerSessionReply;
	GGseManager->TerminateGameServerSession(terminateGameServerSessionReply);
	
	// End the processes
	GseResponse processEndingReply;
	GGseManager->ProcessEnding(processEndingReply);
	
	return Status::OK;
}
```

9. The game server calls the `ProcessEnding` API to end the process immediately, change the server process status to "Terminated", and repossess the resources.
```
// Active call: a game battle corresponds to a process. The `ProcessEnding` API will be actively called after the game battle ends
// Passive call: in case of reduction, process exception, or health check failure, the `ProcessEnding` API will be called passively according to the protection policy. If a full protection or time-period protection policy is configured, it is required to determine whether there are any players in the game server session before the passive call can be made
Status GseManager::ProcessEnding(GseResponse& reply)
{
	GConsoleLog->PrintOut(true, "start to ProcessEnding\n");
	ProcessEndingRequest request;

	ClientContext context;
	AddMetadata(context);
	
	return stub_->ProcessEnding(&context, request, &reply);
}
```
10. The game server calls the `DescribePlayerSessions` API to get the information of the player in the game server session (which is optional based on your actual business needs).
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
11. The game server calls the `UpdatePlayerSessionCreationPolicy` API to update the player session creation policy and set whether to accept new players, i.e., whether to allow new players to join a game session (which is optional based on your actual business needs).
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
12. The game server calls the `ReportCustomData` API to notify GSE of the custom data that can be viewed during game server session query (which is optional based on your actual business needs).
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

## Launching Server for GSE to Call

Server running: launch `GrpcServer`.

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


## Connecting Client to gRPC Server of GSE

Server connecting: create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.

```
void GseManager::InitStub()
{
	auto channel = grpc::CreateChannel("127.0.0.1:5758", grpc::InsecureChannelCredentials());
	stub_ = GseGrpcSdkService::NewStub(channel);
}
```

## Demo for C++
1. [Click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/cpp-demo.zip) to download the code of the Demo for C++.
2. Generate the gRPC code.
As the gRPC code has already been generated in the `cpp-demo/source/grpcsdk` directory of the Demo for C++, you do not need to generate it again.
3. Launch the server for GSE to call.
  - Implement the server.
`grpcserver.cpp` in the `cpp-demo/source/api` directory implements three server APIs.
  - Run the server.
`grpcserver.cpp` in the `cpp-demo/source/api` directory launches `GrpcServer`.
4. Connect the client to the gRPC server of GSE.
  - Implement the client.
`gsemanager.cpp` in the `cpp-demo/source/gsemanager` directory implements nine client APIs.
  - Connect to the server.
Create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
5. Compile and run the project.
 1. Install CMake.
 2. Install GCC v4.9 or above.
 3. Download the code and run the following command in the `cpp-demo` directory:
```
  mkdir build
  cmake ..
  make
```
 The corresponding `cpp-demo` executable file will be generated.
 4. Package the `cpp-demo` executable file as an [asset package](https://intl.cloud.tencent.com/document/product/1055/36674) and configure the launch path as `cpp-demo` with no launch parameter needed.
 5. [Create a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675) and deploy the asset package on it. After that, you can perform various operations such as [scaling](https://intl.cloud.tencent.com/document/product/1055/37445).


