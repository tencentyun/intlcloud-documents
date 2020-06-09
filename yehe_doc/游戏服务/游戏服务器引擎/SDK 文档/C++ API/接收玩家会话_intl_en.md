

### API Description
This API is used to verify the validity of `PlayerSession`. If the `GameServerSession` status is `Active` and the player has called `JoinGameServerSession` or `JoinGameServerSessionBatch`, a success will be returned, and the `PlayerSession` status will be set to "ACTIVE".

If no response is received in 60 seconds after `JoinGameServerSession` or `JoinGameServerSessionBatch` is called, please change the `PlayerSession` status to "TIMEOUT" and reserve a place for the player in the game session again.

### Parameter Description

| Parameter Name | Type/Value | Description |
|:---|---|---|
|playerSessionId|String| Player session ID |


### Returned Value Description

- True: success.
- False: failure.

A generic result in [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type containing an error message will be returned.


### Use Cases
```
TencentCloud::Gse::GenericOutcome outcome = 
   	TencentCloud::Gse::Server::AcceptPlayerSession(playerSessionId);
if(outcome .IsSuccess())
{
        // Accept connection
}
else 
{
        // Reject connection
} 
```
