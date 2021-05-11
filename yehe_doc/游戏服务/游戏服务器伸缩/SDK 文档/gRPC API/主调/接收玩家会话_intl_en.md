## API Name
AcceptPlayerSession 

<span id="AcceptPlayerSession"></span>

## API Description

This API is used for the game process to notify GSE that a new player has joined. GSE will then authenticate the player using the `gameServerSessionId` and `playerSessionId` parameters passed in through this API.

## Request Structure

```
message AcceptPlayerSessionRequest {
    string gameServerSessionId = 1;
    string playerSessionId = 2;
}
```

## Response Structure

```
message GseResponse
```

## Field Description

**AcceptPlayerSessionRequest**

| Field Name | Type | Description |
| ------------------- | ------ | ------------------------------------------------------------ |
| gameServerSessionId | string | `GameServerSessionId` which uniquely identifies a `GameServerSession` |
| playerSessionId     | string | Unique ID of a player in the corresponding `GameServerSession` returned by the game developer by calling `JoinGameServerSession` |

## Sample

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
