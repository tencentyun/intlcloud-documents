## API Name
OnStartGameServerSession
<span id="OnStartGameServerSession"></span>
## API Description

This API is used for GSE to return the `GameServerSession` information to the game process after you create a `GameServerSession` by calling CreateGameServerSession or another TencentCloud API. Then, the game process needs to retain this information and call the GSE [ActivateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37427) API in its implementation.

## Request Message

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

// Assign `GameServerSession` to the game process
message StartGameServerSessionRequest {
    GameServerSession gameServerSession = 1;
}
```

## Response Message

```
message GseResponse {
}
```

## Field Description

**GameServerSession**
For more information on game session, please see [GameServerSession](https://intl.cloud.tencent.com/document/product/1055/37140#GameServerSession).



## Sample

```
func (s *rpcService) OnStartGameServerSession(ctx context.Context, req *grpcsdk.StartGameServerSessionRequest) (*grpcsdk.GseResponse, error) {
	s.GameServerSession = req.GameServerSession  // Save `GameServerSession`
	conn, _ := grpc.DialContext(context.Background(), LOCAL_ADDRESS, grpc.WithInsecure())
	defer conn.Close()
	cli := grpcsdk.NewGseGrpcSdkServiceClient(conn)

	request := &grpcsdk.ActivateGameServerSessionRequest{  // Call this API to activate the game session
		GameServerSessionId:  req.GameServerSession.GameServerSessionId,
		MaxPlayers:           req.GameServerSession.MaxPlayers,
	}

	return cli.ActivateGameServerSession(getContext(), request)
}
```


