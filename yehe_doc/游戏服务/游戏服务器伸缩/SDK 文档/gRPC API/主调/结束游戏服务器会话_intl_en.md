## API Name
TerminateGameServerSession 
<span id="TerminateGameServerSession"></span>


## API Description	

This API is used for the game process to notify GSE that a `GameServerSession` sustained by it has ended, and GSE can subsequently reassign another `GameServerSession` to the process.

## Request Message

```
message TerminateGameServerSessionRequest {
    string gameServerSessionId = 1;
}
```

## Response Message

```
message GseResponse 
```

## Field Description

**TerminateGameServerSessionRequest**

| Field Name | Type | Description |
| ------------------- | ------ | ------------------------------------------------------------ |
| gameServerSessionId | string | `GameServerSessionId` which uniquely identifies a `GameServerSession` |

## Sample

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
