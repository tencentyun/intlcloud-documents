
## Installing gRPC
1. To use gRPC Go, you need to install the latest major release of Go first.
2. Install the protocol buffer compiler protoc3.
3. Install the Go plugin in the protocol buffer compiler.
  - Run the following command to install the protocol buffer compiler plugin for Go (protoc-gen-go):
  ```
  $ export GO111MODULE=on  # Enable module mode
  $ go get github.com/golang/protobuf/protoc-gen-go
  ```
  - Update the path so that the protocol buffer compiler can find the Go plugin:
```
$ export PATH="$PATH:$(go env GOPATH)/bin"
```

 

<dx-alert infotype="explain" title="">
For more information on the installation process, see [Installing Go](https://github.com/grpc/grpc-go/tree/master/examples) and [Installing Protocol Buffer Compiler](https://www.grpc.io/docs/protoc-installation/).
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
    In the `proto` directory, run:
      ```
protoc --go_out=plugins=grpc:. *.proto```
	to automatically generate the `go_package` path that contains proto. You can modify the `go_package` path as needed but not the package.
	  ```

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
```Go
func (g *gsemanager) ProcessReady(logPath []string, clientPort int32, grpcPort int32) error {
	logger.Info("start to processready", zap.Any("logPath", logPath), zap.Int32("clientPort", clientPort),
		zap.Int32("grpcPort", grpcPort))
	req := &grpcsdk.ProcessReadyRequest{
		// Log path
		LogPathsToUpload: logPath,
		// Set the ports
		ClientPort:       clientPort,
		GrpcPort:         grpcPort,
	}

	_, err := g.rpcClient.ProcessReady(g.getContext(), req)
	if err != nil {
		logger.Info("ProcessReady fail", zap.Error(err))
		return err
	}

	// Ready to provide services
	logger.Info("ProcessReady success")
	return nil
}
```
 2. After the process is ready, GSE will call the `OnHealthCheck` API to perform a health check on the game server every minute. If the health check fails three consecutive times, the process will be considered to be unhealthy, and no game server sessions will be assigned to it.
```Go
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
 3. Because the client calls the [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) API to create a game server session and assigns it to a process, GSE will be triggered to call the `onStartGameServerSession` API for the process and change the status of `GameServerSession` to "Activating".
```Go
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
 4. After the game server receives `onStartGameServerSession`, you need to handle the logic or resource allocation by yourself. After everything is ready, the game server will call the `ActivateGameServerSession` API to notify GSE that the game server session has been assigned to a process and is ready to receive player requests and will change the server status to "Active".
```Go
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
 5. After the client calls the [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130) API for the player to join, the game server will call the `AcceptPlayerSession` API to verify the validity of the player. If the connection is accepted, the status of `PlayerSession` will be set to "Active". If the client receives no response within 60 seconds after calling the `JoinGameServerSession` API, it will change the status of `PlayerSession` to "Timeout" and then call `JoinGameServerSession` again.
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
 6. After the game ends or the player exits, the game server will call the `RemovePlayerSession` API to remove the player, change the status of `playersession` to "Completed", and reserve the player slot in the game server session.
```Go
func (g *gsemanager) RemovePlayerSession(playerSessionId string) (*grpcsdk.GseResponse, error) {
	logger.Info("start to RemovePlayerSession", zap.String("playerSessionId", playerSessionId))
	req := &grpcsdk.RemovePlayerSessionRequest{
		GameServerSessionId:  g.gameServerSession.GameServerSessionId,
		PlayerSessionId:      playerSessionId,
	}

	return g.rpcClient.RemovePlayerSession(g.getContext(), req)
}
```
 7. After a game server session (a game battle or a service) ends, the game server will call the `TerminateGameServerSession` API to end the `GameServerSession` and change its status to `Terminated`.
```Go
func (g *gsemanager) TerminateGameServerSession() (*grpcsdk.GseResponse, error) {
	logger.Info("start to TerminateGameServerSession")
	req := &grpcsdk.TerminateGameServerSessionRequest{
		GameServerSessionId:  g.gameServerSession.GameServerSessionId,
	}

	return g.rpcClient.TerminateGameServerSession(g.getContext(), req)
}
```
 8. In case of health check failure or reduction, GSE will call the `OnProcessTerminate` API to end the game process. The reduction will be triggered according to the [protection policy](https://intl.cloud.tencent.com/document/product/1055/36675) configured in the GSE console.
```Go
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
 9. The game server calls the `ProcessEnding` API to end the process immediately, change the server process status to "Terminated", and repossess the resources.
```Go
// Active call: a game battle corresponds to a process. The `ProcessEnding` API will be actively called after the game battle ends
// Passive call: in case of reduction, process exception, or health check failure, the `ProcessEnding` API will be called passively according to the protection policy. If a full protection or time-period protection policy is configured, it is required to determine whether there are any players in the game server session before the passive call can be made
func (g *gsemanager) ProcessEnding() (*grpcsdk.GseResponse, error) {
	logger.Info("start to ProcessEnding")
	req := &grpcsdk.ProcessEndingRequest{
	}

	return g.rpcClient.ProcessEnding(g.getContext(), req)
}
```
 10. The game server calls the `DescribePlayerSessions` API to get the information of the player in the game server session (which is optional based on your actual business needs).
```Go
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
 11. The game server calls the `UpdatePlayerSessionCreationPolicy` API to update the player session creation policy and set whether to accept new players, i.e., whether to allow new players to join a game session (which is optional based on your actual business needs).
```Go
func (g *gsemanager) UpdatePlayerSessionCreationPolicy(newPolicy string) (*grpcsdk.GseResponse, error) {
	logger.Info("start to UpdatePlayerSessionCreationPolicy", zap.String("newPolicy", newPolicy))
	req := &grpcsdk.UpdatePlayerSessionCreationPolicyRequest{
		GameServerSessionId:            g.gameServerSession.GameServerSessionId,
		NewPlayerSessionCreationPolicy: newPolicy,
	}

	return g.rpcClient.UpdatePlayerSessionCreationPolicy(g.getContext(), req)
}
```
 12. The game server calls the `ReportCustomData` API to notify GSE of the custom data (which is optional based on your actual business needs).
```Go
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

## Launching Server for GSE to Call
Server running: launch `GrpcServer`.
```Go
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

## Connecting Client to gRPC Server of GSE
Server connecting: create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
```Go
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

## Demo for Go
 1. [Click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/go-demo.zip) to download the code of the Demo for Go.
 2. Generate the gRPC code.
As the gRPC code has already been generated in the `go-demo/grpcsdk` directory of the Demo for Go, you do not need to generate it again.
 3. Launch the server for GSE to call.
  - Implement the server.
`grpcserver.go` in the `go-demo/api` directory implements three server APIs.
  - Run the server.
`grpcserver.go` in the `go-demo/api` directory launches `GrpcServer`.
 4. Connect the client to the gRPC server of GSE.
  - Implement the client.
`gsemanager.go` in the `go-demo/gsemanager` directory implements nine client APIs.
  - Connect to the server.
Create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
 5. Compile and run the project.
  1. In the `go-demo` directory, run
  ```
	go mod vendor```
	to generate the `vendor` directory.
  - Run the compile command:
  ```
	go build -mod=vendor main.go```
	to generate the corresponding `go-demo` executable file `main.go`.
  - Package the executable file `main.go` as an [asset package](https://intl.cloud.tencent.com/document/product/1055/36674) and configure the launch path as `main` with no launch parameter needed.
  - [Create a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675) and deploy the asset package on it. After that, you can perform various operations such as [scaling](https://intl.cloud.tencent.com/document/product/1055/37445).

 
