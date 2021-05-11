



### API Description
This API is used to activate a game server session.
- Calling `CreateGameServerSession` or `startGameServerSessionPlacement` will trigger the `onStartGameServerSession` callback and set the session status to `ACTIVATING`.
- After a process receives the `onStartGameServerSession` callback, it can call this API to indicate that it is ready to accept player access, and server status will be changed to `ACTIVE`.

### Parameter Description
No parameters.

### Returned Value Description
- True: success.
- False: failure.

A generic result in [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type containing an error message will be returned.

### Use Cases
```
 // This function is generally used as a part of the `onStartGameServerSession` callback function and will be called when a session is ready to accept player connections. For more information, please see the description of the `ProcessReady` function  
 TencentCloud::Gse::GenericOutcome outcome = 
 	TencentCloud::Gse::Server::ActivateGameSession();
 if (!outcome .IsSuccess())
 {
	return false;
 }
```
