


### API Description
This API is used to remove a player, change the `playersession` status to `COMPLETED`, and reserve a place in the game session.

### Parameter Description

| Parameter Name | Type/Value | Description |
|:---|---|---|
|playerSessionId|string| Player ID|


### Returned Value Description

- True: success.
- False: failure.

A generic result in [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type containing an error message will be returned.



### Use Cases
```
TencentCloud::Gse::GenericOutcome outcome = 	
	TencentCloud::Gse::Server::RemovePlayerSession(playerSessionId);

if (outcome.IsSuccess())
{
       // Subsequent processing
}
```

