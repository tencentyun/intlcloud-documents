

### API Description
This API is used to verify whether the PlayerSession is acceptable. If the status of `GameServerSession` is `Active`, and the player has invoked `JoinGameServerSession` or `JoinGameServerSessionBatch`, the session is acceptable. and the `PlayerSession` status is set to `ACTIVE`.

If the request to invoke `JoinGameServerSession` or `JoinGameServerSessionBatch` is not responsed in 60 seconds, the `PlayerSession` status will be `TIMEOUT` and the player place in the game session is reserved again.

### Parameters

|Parameter|Type/value|Description|
|:---|---|---|
|playerSessionId|String|PlayerSession ID|


### Returned value description

- `True`: success.
- `False`: failure.

A result containing the error message. Type: GenericOutcome


### Examples
```
TencentCloud::Gse::GenericOutcome outcome = 
   	TencentCloud::Gse::Server::AcceptPlayerSession(playerSessionId);
if(outcome .IsSuccess())
{
        // Accept the connection
}
else 
{
        // Reject the connection
} 
```

