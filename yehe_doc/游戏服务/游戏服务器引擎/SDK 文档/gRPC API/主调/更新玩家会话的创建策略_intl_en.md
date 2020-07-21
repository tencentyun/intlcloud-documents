## API Name
 UpdatePlayerSessionCreationPolicy 
<span id="UpdatePlayerSessionCreationPolicy"></span>


## API Description

This API is used for the game process to update the policy of creating player sessions in the current game server session.

## Request Message

```
message UpdatePlayerSessionCreationPolicyRequest {
   string gameServerSessionId = 1;
   string newPlayerSessionCreationPolicy = 2;
}
```

## Response Message

```
message GseResponse 
```

## Field Description

**UpdatePlayerSessionCreationPolicyRequest**

| Field Name | Type | Description |
| ------------------------------ | ------ | ------------------------------------------------------------ |
| gameServerSessionId            | string | `GameServerSessionId` which uniquely identifies a `GameServerSession` |
| newPlayerSessionCreationPolicy | string | Updated policy. Valid values:<li>**ACCEPT_ALL** (accepts all new player sessions)<li>**DENY_ALL** (denies all new player sessions) |

## Sample

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
