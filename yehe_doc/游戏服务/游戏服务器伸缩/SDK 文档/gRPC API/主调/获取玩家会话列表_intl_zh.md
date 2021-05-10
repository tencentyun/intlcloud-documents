## 接口名称
DescribePlayerSessions 
<span id="DescribePlayerSessions"></span>


## 接口说明

游戏进程可以通过该接口，获取当前已经加入 GameServerSession 的玩家信息列表。

## 请求消息体

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

## 返回消息体

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

## 字段说明

**DescribePlayerSessionsRequest**

相关字段含义请参见 [输入参数](https://intl.cloud.tencent.com/document/product/1055/37135#2.-input-parameters)。

**DescribePlayerSessionsResponse**

相关字段含义参见 [PlayerSession](https://intl.cloud.tencent.com/document/product/1055/37140#playersession)。

## 使用示例

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
