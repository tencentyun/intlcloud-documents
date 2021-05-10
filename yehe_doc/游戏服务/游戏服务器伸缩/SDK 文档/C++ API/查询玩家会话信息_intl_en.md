### API Description
This API is used to get the player information under a game session.

### Parameter Description

| Parameter Name | Type/Value | Description |
|:---|---|---|
|Custom|[TencentCloud::Gse::Server::Model::DescribePlayerSessionsRequest](#DescribePlayerSessionsRequest)| Parameter for requesting player information |

### Returned Value Description
If the information is successfully obtained, the [DescribePlayerSessionsOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) object will be returned, which contains a set of player session objects matching the request parameter.

### Use Cases
```
TencentCloud::Gse::Server::Model::DescribePlayerSessionsRequest request;
auto gameSessionIdOutcome = TencentCloud::Gse::Server::GetGameServerSessionId();
request.SetGameServerSessionId(gameSessionId);    

TencentCloud::Gse::DescribePlayerSessionsOutcome playerSessionsOutcome =
	TencentCloud::Gse::Server::DescribePlayerSessions(request);

if (!playerSessionsOutcome.IsSuccess())
{
// Request error fixing logic
}
```



<span id="DescribePlayerSessionsRequest">

#### DescribePlayerSessionsRequest type

| Member Variable                  | Type   | Required | Description                                                         |
| ------------------------- | ------ | -------- | ------------------------------------------------------------ |
| GameServerSessionId       | string | Yes       | Game session ID                                                  |
| PlaySessionId             | string | No       | Player session ID                                                   |
| PlayId                    | string | No       | Player ID                                                      |
| PlayerSessionStatusFilter | string | No       | Player status filter. Valid values: <li>RESERVED: reserved <li>ACTIVE: active<li>COMPLETED: ended <li>TIMEDOUT: timed-out |
| NextToken                 | string | No       | It is required for pagination and does not need to be passed in for the first request                                   |
| Limit                     | int    | No       | Number of entries to be returned per page                                               |
