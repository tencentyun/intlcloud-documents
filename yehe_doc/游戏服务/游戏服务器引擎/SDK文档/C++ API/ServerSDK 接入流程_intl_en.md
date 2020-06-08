

### Integrating ServerSDK
Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for the ServerSDK download link, which will be provided after your application is approved.

```
Import the header file
 #include <tencentcloud/gse/server/GseServerAPI.h>
```

### Calling API

1. Call `InitSDK` to perform initialization. For detailed directions, please see [Initializing SDK](https://intl.cloud.tencent.com/document/product/1055/36688).  

```
TencentCloud::Gse::Server::InitSDKOutcome initOutcome =               
                         TencentCloud::Gse::Server::InitSDK();
if (!initOutcome.IsSuccess())
{
	return false;
} 
```

2. Call `ProcessReady` to get the process ready. Be sure to implement three callback functions. For detailed directions, please see [Getting Process Ready](https://intl.cloud.tencent.com/document/product/1055/36689). 
 - onStartGameSession  
 - onProcessTerminate  
 - onHealthCheck  

```
    std::string serverOut("./logs/serverLog.txt");
    std::string serverErr("./logs/serverErr.txt");
    std::vector<std::string> logPaths;
    logPaths.push_back(serverOut);
    logPaths.push_back(serverErr);
    int listenPort = 9090;

    TencentCloud::Gse::Server::ProcessParameters processReadyParameter = TencentCloud::Gse::Server::ProcessParameters(
        std::bind(&GseManager::OnStartGameSession, this, std::placeholders::_1),
        std::bind(&GseManager::OnProcessTerminate, this),
        std::bind(&GseManager::OnHealthCheck, this),
        listenPort, TencentCloud::Gse::Server::LogParameters(logPaths)
        );

    TencentCloud::Gse::GenericOutcome readyOutcome = TencentCloud::Gse::Server::ProcessReady(processReadyParameter);

    if (!readyOutcome.IsSuccess())
    {
        return false;
    }  
```

```
void GseManager::OnStartGameServerSession(TencentCloud::Gse::Server::Model::GameServerSession myGameServerSession)
{
    TencentCloud::Gse::GenericOutcome outcome = 
    	TencentCloud::Gse::Server::ActivateGameServerSession();
}
```

```
void GseManager::OnHealthCheck()
{
    // `true` or `false` will be returned based on the actual process health status
    return true;
}
```

```
void GseManager::onProcessTerminate()
{   // Before calling the following API, determine whether the game server session on the process can be ended immediately based on the actual conditions. You can also set a flag first and then wait for the appropriate time to call the API
	TencentCloud::Gse::GenericOutcome outcome = 
		TencentCloud::Gse::Server::TerminateGameServerSession();
   TencentCloud::Gse::GenericOutcome outcome =
	TencentCloud::Gse::Server::ProcessEnding();
}   
```


3. Call `AcceptPlayerSession` to check whether the connection has a reserved place during client connection. For detailed directions, please see [Accepting Player Session](https://intl.cloud.tencent.com/document/product/1055/36691).  

```
// When the client is connected, call `AcceptPlayerSession` to check the validity of the connection
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
4. Call `RemovePlayerSession` to remove the player from the game server session. For detailed directions, please see [Removing Player Session](https://intl.cloud.tencent.com/document/product/1055/36692).

```
// The player exits the game server session call
TencentCloud::Gse::GenericOutcome outcome = 	
	TencentCloud::Gse::Server::RemovePlayerSession(playerSessionId);

if (outcome.IsSuccess())
{
       // Subsequent processing
}
```
5. Call `TerminateGameSession` to end the game server session. For detailed directions, please see [Ending Game Server Session](https://intl.cloud.tencent.com/document/product/1055/36695).  

```
// The game server session ends itself or is ended; for example, it can be ended when there are no players connected to it
TencentCloud::Gse::GenericOutcome outcome = 
	TencentCloud::Gse::Server::TerminateGameSession();

if (outcome.IsSuccess())
{
       // Subsequent processing
}
```
6. Call `ProcessEnding` to end the process. For detailed directions, please see [Ending Process](https://intl.cloud.tencent.com/document/product/1055/36696).   

```

// Reduction or process restart is notified
 TencentCloud::Gse::GenericOutcome outcome = TencentCloud::Gse::Server::ProcessEnding();   
```




