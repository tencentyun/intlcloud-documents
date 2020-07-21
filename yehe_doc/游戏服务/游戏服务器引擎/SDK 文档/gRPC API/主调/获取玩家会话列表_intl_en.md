## API Name
DescribePlayerSessions 
<span id="DescribePlayerSessions"></span>


## API Description

This API is used for the game process to get a list of player sessions that are currently in the `GameServerSession`.

## Request Message

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

## Response Message

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

## Field Description

**DescribePlayerSessionsRequest**

For field definitions, see [Input Parameters](https://intl.cloud.tencent.com/document/product/1055/37135#2.-input-parameters).

**DescribePlayerSessionsResponse**

For field definitions, see [PlayerSession](https://intl.cloud.tencent.com/document/product/1055/37140#playersession).

## Sample

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
