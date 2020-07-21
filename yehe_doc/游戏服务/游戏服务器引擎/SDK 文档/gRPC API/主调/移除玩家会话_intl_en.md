## API Name
RemovePlayerSession 
<span id="RemovePlayerSession"></span>


## API Description
This API is used for the game process to notify GSE that a player has quit. After GSE receives the request, it will update the current number of players in the corresponding game server session to allow other players to join.

## Request Message

```
message RemovePlayerSessionRequest {
    string gameServerSessionId = 1;
    string playerSessionId = 2;
}
```

## Response Message

```
message GseResponse 
```

## Field Description

For field definitions, see [AcceptPlayerSession](https://intl.cloud.tencent.com/document/product/1055/37428).

## Sample

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
