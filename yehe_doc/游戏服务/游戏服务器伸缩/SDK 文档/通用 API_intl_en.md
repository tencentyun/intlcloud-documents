
## Overview
The game process communicates with GSE through gRPC. For gRPC protocol files, please see `GameServerGrpcSdkService.proto` and `GseGrpcSdkService.proto`.

`GameServerGrpcSdkService.proto` defines three service APIs, which should be called by GSE in the game process.
The service APIs defined by `GseGrpcSdkService.proto` should be called by the game server, and the corresponding APIs should be called in the game process at the right timing. GSE APIs listen on the gRPC port 5758. You can generate protocol files in different programming languages as needed.

>?
>- The [Chinese edition](http://doc.oschina.net/grpc) and [English edition](https://www.grpc.io/) of the GProxy user guide are for your reference.
>- The sample codes are in the Go programming language, and the protocol package is named as `grpcsdk`. For the common function `getContext`, constant `LOCAL_ADDRESS`, and message structure `GseResponse`, please see [Others](#others).



## Game Process Integration Process
After the game process is started, the gRPC server and the three APIs defined by `GameServerGrpcSdkService.proto` should be implemented.

<span id="OnHealthCheck"></span>
### OnHealthCheck

#### API description
This API is used for GSE to get the health status of the current game process every minute, and for the current game process to return its health status.

#### Request message

```
message HealthCheckRequest {
}
```

#### Response message

```
message HealthCheckResponse {
    bool healthStatus = 1;
}
```

#### Field description

**HealthCheckResponse**

| Field Name | Type | Description |
| ------------ | ---- | --------------------------------- |
| healthStatus | Bool | `true` will be returned if the process is healthy; otherwise, `false` will be returned. |


#### Sample code

```
func (s *rpcService) OnHealthCheck(ctx context.Context, req *grpcsdk.HealthCheckRequest) (*grpcsdk.HealthCheckResponse, error) {
	resp := &grpcsdk.HealthCheckResponse{
		HealthStatus: s.healthStatus,  // Identify the health status of the current process
	}

	return resp, nil
}
```

<span id="OnStartGameServerSession"></span>
### OnStartGameServerSession

#### API description

This API is used for GSE to return the `GameServerSession` information to the game process after you called Tencent Cloud APIs such as `CreateGameServerSession` to generate a `GameServerSession`. After receiving the request, the game process should retain the `GameServerSession` information and call the GSE API [ActivateGameServerSession](#ActivateGameServerSession) in its implementation.

#### Request message

```
// game server session
message GameServerSession {
    string gameServerSessionId = 1;
    string fleetId = 2;
    string name = 3;
    int32 maxPlayers = 4;
    bool joinable = 5;
    repeated GameProperty gameProperties = 6;
    int32 port = 7;
    string ipAddress = 8;
    string gameServerSessionData = 9;
    string matchmakerData = 10;
    string dnsName = 11;
}

// Assign `gameserversession` to the game process
message StartGameServerSessionRequest {
    GameServerSession gameServerSession = 1;
}
```

#### Response message

```
message GseResponse {
   enum Status {
      OK = 0;
      ERROR_400 = 1;
      ERROR_500 = 2;
   }
   Status status = 1;
   string responseData = 2;
   string errorMessage = 3;
}
```

#### Field description

**GameServerSession**
For more information on game session, please see [GameServerSession](https://intl.cloud.tencent.com/zh/document/product/1055/37140#GameServerSession).


**GseResponse**

| Field Name | Type | Description |
| ------------ | ------ | ---------------------------------------- |
| status | Enumeration | Return code. 0: success; 400: request error; 500: internal error |
| responseData | String | Returned data |
| errorMessage | String | Message indicating success or failure |

#### Sample code

```
func (s *rpcService) OnStartGameServerSession(ctx context.Context, req *grpcsdk.StartGameServerSessionRequest) (*grpcsdk.GseResponse, error) {
	s.GameServerSession = req.GameServerSession  // Save `GameServerSession`
	conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
	defer conn.Close()
	cli := grpcsdk.NewGseGrpcSdkServiceClient(conn)

	request := &grpcsdk.ActivateGameServerSessionRequest{  //Call this API to activate the game session
		GameServerSessionId:  req.GameServerSession.GameServerSessionId,
		MaxPlayers:           req.GameServerSession.MaxPlayers,
	}

	return cli.ActivateGameServerSession(getContext(), request)
}
```

<span id="OnProcessTerminate"></span>
### OnProcessTerminate

#### API description

This API is used for GSE to tell the game process to end itself during reduction or if health check keeps failing. After the game process receives the request, it needs to end the game session which it sustains on [OnStartGameServerSession](#OnStartGameServerSession), and call the two GSE APIs [TerminateGameServerSession](#TerminateGameServerSession) and [ProcessEnding](#ProcessEnding) to tell GSE to end the game session and the process.

#### Request message

```
// End the game process
message ProcessTerminateRequest {
    int64 terminationTime = 1;
}
```

#### Response message

```
message GseResponse
```

#### Field description

##### ProcessTerminateRequest

| Field Name | Type | Description |
| --------------- | ----- | ------------------------------------------------------------ |
| terminationTime | Int64 | Time (timestamp) after which GSE will end the process.<li>If the server fleet is under full protection, the time will be ignored.<li>If the server fleet is under time-period protection, the time will be the protection period.<li>If the server fleet is under no protection, the time will be 5 minutes by default. |


#### Sample code

```
func (s *rpcService) OnProcessTerminates(ctx context.Context, req *grpcsdk.ProcessTerminateRequest) (*grpcsdk.GseResponse, error) {
   s.TerminationTime = req.TerminationTime  
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   cli := grpcsdk.NewGseGrpcSdkServiceClient(conn)

   request := &grpcsdk.ProcessEndingRequest{  // Inform GSE that the process is being ended
   }

   return cli.ProcessEnding(getContext(), request)
}
```

<span id="GSE"></span>
## GSE APIs

<span id="ProcessReady"></span>
### ProcessReady

#### API description

This API is used to notify GSE that a game process is started and ready to sustain a game session. Then, GSE can call the [OnStartGameServerSession](#OnStartGameServerSession) API to assign the game session to the process.

#### Request message

```
message ProcessReadyRequest {
    repeated string logPathsToUpload = 1;
    int32 clientPort = 2;
    int32 grpcPort = 3;
}
```

#### Response message

```
message GseResponse 
```

#### Field description

**ProcessReadyRequest**

| Field Name | Type | Description |
| ---------------- | ----------- | ------------------------------------------------------------ |
| logPathsToUpload | String array | Path of the game process logs to be uploaded to Tencent Cloud. GSE will upload logs in the specified paths to Tencent Cloud for you to download. |
| clientPort       | Int32       | Port to be connected to by the game client.                           |
| grpcPort         | Int32       | Port used by GSE to call the service APIs defined by `GameServerGrpcSdkService.proto` in the game process. |

#### Sample request

```
func (r *rpcClient) ProcessReady(logPath []string, clientPort int32, grpcPort int32) (*grpcsdk.GseResponse, error) {
	conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
	defer conn.Close()
	req := &grpcsdk.ProcessReadyRequest{
		LogPathsToUpload: logPath,
		ClientPort:       clientPort,
		GrpcPort:         grpcPort,
	}

	client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
	return client.ProcessReady(getContext(), req)
}
```

<span id="ActivateGameServerSession"></span>
### ActivateGameServerSession

#### API description

This API is used for a game process to tell GSE to activate the corresponding `GameServerSession` after receiving the callback from GSE through the [OnStartGameServerSession](#OnStartGameServerSession) API.

#### Request message

```
message ActivateGameServerSessionRequest{
    string gameServerSessionId = 1;
    int32 maxPlayers = 2;
}
```

#### Response message

```
message GseResponse 
```

#### Field description

##### ActivateGameServerSessionRequest

| Field Name | Type | Description |
| ------------------- | ------ | ------------------------------------------------------------ |
| gameServerSessionId | String | `GameServerSessionId` which uniquely identifies a `GameServerSession`. |
| maxPlayers          | Int32  | Maximum number of players allowed by a game session.                                |

#### Sample code

For the sample code, please see the [OnStartGameServerSession](#OnStartGameServerSession) API.


<span id="AcceptPlayerSession"></span>
### AcceptPlayerSession 

#### API description

This API is used for the game process to notify GSE that a new player has joined. GSE will then authenticate the player using the `gameServerSessionId` and `playerSessionId` parameters passed in through this API.

#### Request structure

```
message AcceptPlayerSessionRequest {
    string gameServerSessionId = 1;
    string playerSessionId = 2;
}
```

#### Response structure

```
message GseResponse
```

#### Field description

**AcceptPlayerSessionRequest**

| Field Name | Type | Description |
| ------------------- | ------ | ------------------------------------------------------------ |
| gameServerSessionId | String | `GameServerSessionId` which uniquely identifies a `GameServerSession`. |
| playerSessionId     | String | Unique ID of a player in the game session returned through the API call of `JoinGameServerSession`. |

#### Sample code

```
func (r *rpcClient) AcceptPlayerSession(gameServerSessionId, playerSessionId string) (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()

   req := &grpcsdk.AcceptPlayerSessionRequest{
      GameServerSessionId:  gameServerSessionId,
      PlayerSessionId:      playerSessionId,
   }

   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.AcceptPlayerSession(getContext(), req)
}
```

<span id="RemovePlayerSession"></span>
### RemovePlayerSession 

#### API description
This API is used for a game process to notify GSE that a player has quit. After GSE receives the request, it will update the current number of players in the corresponding game session to allow other players to join.

#### Request message

```
message RemovePlayerSessionRequest {
    string gameServerSessionId = 1;
    string playerSessionId = 2;
}
```

#### Response message

```
message GseResponse 
```

#### Field description

For the sample code, please see the [AcceptPlayerSession](#AcceptPlayerSession) API.

#### Sample code

```
func (r *rpcClient) RemovePlayerSession(gameServerSessionId, playerSessionId string) (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   req := &grpcsdk.RemovePlayerSessionRequest{
      GameServerSessionId:  gameServerSessionId,
      PlayerSessionId:      playerSessionId,
   }

   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.RemovePlayerSession(getContext(), req)
}
```

<span id="DescribePlayerSessions"></span>
### DescribePlayerSessions 

#### API description

This API is used for a game process to obtain the information list of the current players in its game session.

#### Request message

```
message DescribePlayerSessionsRequest {
   string gameServerSessionId = 1;
   string playerId = 2;
   string playerSessionId = 3;
   string playerSessionStatusFilter = 4;
   string nextToken = 5;
   int32 limit = 6 ;
}
```

#### Response message

```
message PlayerSession {
   string playerSessionId = 1;
   string playerId = 2;
   string gameServerSessionId = 3;
   string fleetId = 4;
   string ipAddress = 5;
   string status = 6;
   int64 creationTime = 7;
   int64 terminationTime = 8;
   int32 port = 9;
   string playerData = 10;
   string dnsName = 11;
}

message DescribePlayerSessionsResponse {
   string nextToken = 1;
   repeated PlayerSession playerSessions = 2;
}
```

#### Field description

**DescribePlayerSessionsRequest**

For field definitions, please see the **Input Parameters** paragraph in [DescribePlayerSessions](https://intl.cloud.tencent.com/document/product/1055/37135).

**DescribePlayerSessionsResponse**

For field definitions, please see [PlayerSession](https://intl.cloud.tencent.com/zh/document/product/1055/37140#PlayerSession).

#### Sample code

```
func (r *rpcClient) DescribePlayerSessions(gameServerSessionId, playerId, playerSessionId, playerSessionStatusFilter, nextToken string,limit int32) (*grpcsdk.DescribePlayerSessionsResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()

   req := &grpcsdk.DescribePlayerSessionsRequest{
      GameServerSessionId:       gameServerSessionId,
      PlayerId:                  playerId,
      PlayerSessionId:           playerSessionId,
      PlayerSessionStatusFilter: playerSessionStatusFilter,
      NextToken:                 nextToken,
      Limit:                     limit,
   }

   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.DescribePlayerSessions(getContext(), req)
}
```
<span id="UpdatePlayerSessionCreationPolicy"></span>
### UpdatePlayerSessionCreationPolicy 

#### API description

This API is used for a game process to update the policy for players to join the current game session.

#### Request message

```
message UpdatePlayerSessionCreationPolicyRequest {
   string gameServerSessionId = 1;
   string newPlayerSessionCreationPolicy = 2;
}
```

#### Response message

```
message GseResponse 
```

#### Field description

**UpdatePlayerSessionCreationPolicyRequest**

| Field Name | Type | Description |
| ------------------------------ | ------ | ------------------------------------------------------------ |
| gameServerSessionId | String | `GameServerSessionId` which uniquely identifies a `GameServerSession`. |
| newPlayerSessionCreationPolicy | String | Updated policy. Valid values:<li>**ACCEPT_ALL** (accepts all new player sessions)<li>**DENY_ALL** (denies all new player sessions) |

#### Sample code

```
func (r *rpcClient) UpdatePlayerSessionCreationPolicy(gameServerSessionId, newpolicy string) (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()

   req := &grpcsdk.UpdatePlayerSessionCreationPolicyRequest{
      GameServerSessionId:            gameServerSessionId,
      NewPlayerSessionCreationPolicy: newpolicy,
   }

   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.UpdatePlayerSessionCreationPolicy(getContext(), req)
}
```

<span id="TerminateGameServerSession"></span>
### TerminateGameServerSession 

#### API description	

This API is used for a game process to notify GSE that the game session sustained on the game process has ended. GSE can then assign other game sessions to this process.

#### Request message

```
message TerminateGameServerSessionRequest {
    string gameServerSessionId = 1;
}
```

#### Response message

```
message GseResponse 
```

#### Field description

**TerminateGameServerSessionRequest**

| Field Name | Type | Description |
| ------------------- | ------ | ------------------------------------------------------------ |
| gameServerSessionId | String | `GameServerSessionId` which uniquely identifies a `GameServerSession`. |

#### Sample code

```
func (r *rpcClient) TerminateGameServerSession(gameServerSessionId string) (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   req := &grpcsdk.TerminateGameServerSessionRequest{
      GameServerSessionId: gameServerSessionId,
   }

   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.TerminateGameServerSession(g.getContext(), req)
}
```

<span id="ProcessEnding"></span>
### ProcessEnding 

#### API description

This API is used for a game process to notify GSE that the game process is closing.

#### Request structure

```
message ProcessEndingRequest {
}
```

#### Response message

```
message GseResponse
```

#### Field description

N/A

#### Sample code

```
func (r *rpcClient) ProcessEnding() (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   req := &grpcsdk.ProcessEndingRequest{
   }
   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.ProcessEnding(g.getContext(), req)
}
```

<span id="ReportCustomData"></span>
### ReportCustomData 

#### API description

This API is used for a game process to inform GSE of custom data.

#### Request message

```
message ReportCustomDataRequest {
    int32 currentCustomCount = 1 ;
    int32 maxCustomCount = 2;
}
```

#### Response message

```
message GseResponse
```

#### Field description

##### ReportCustomDataRequest

| Field Name | Type | Description |
| ------------------ | ----- | ------------ |
| currentCustomCount | Int32 | Current custom value |
| maxCustomCount     | Int32 | Maximum custom value |

#### Sample code

```
func (r *rpcClient) ReportCustomData(currentCustomCount, maxCustomCount int32) (*grpcsdk.GseResponse, error) {
   conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
   defer conn.Close()
   req := &grpcsdk.ReportCustomDataRequest{
      CurrentCustomCount:   currentCustomCount,
      MaxCustomCount:       maxCustomCount,
   }

   client := grpcsdk.NewGseGrpcSdkServiceClient(conn)
   return client.ReportCustomData(getContext(), req)
}
```


<span id="other"></span>
## Others

### Request `meta`

When the game process uses gRPC to call [GSE APIs](#GSE), you need to add two fields to `meta` of the gRPC request.

| Field      | Description                                      | Type   |
| --------- | ----------------------------------------- | ------ |
| pid       | `pid` of the current game process                         | String |
| requestId | `requestId` of the current request, which is used to uniquely identify a request. | String |

### Sample common code

```
const (
	LOCAL_ADDRESS = "127.0.0.1:5758"
)

var (
   pid = strconv.Itoa(os.Getpid())
)

func getContext() context.Context {
   requestId := uuid.NewV4().String()   //The process generates its own `requestId`.
   ctx := metadata.AppendToOutgoingContext(context.Background(), "pid", pid)
   return metadata.AppendToOutgoingContext(ctx, "requestId", requestId)
}

message GseResponse {
   enum Status {
      OK = 0;
      ERROR_400 = 1;
      ERROR_500 = 2;
   }
   Status status = 1;
   string responseData = 2;
   string errorMessage = 3;
}
```

