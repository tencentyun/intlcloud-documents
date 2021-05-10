

#### API Description
This API is used to synchronously notify the server that the service is ready. It can register the callback function, port, and log directory. 
After the GSE server receives the request, it will change the instance status to `ACTIVE`. If a callback function has been registered, `onHealthCheck` will be called once per minute, and its result will be valid if returned in 1 minute.

#### Parameter Description

| Parameter Name | Type/Value | Description |
|:---|---|---|
|onStartGameServerSession|[std::function <void(TencentCloud::Gse::Model::GameServerSession) > onStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/36689#onstartgameserversession)| Callback function for game session creation |
|onProcessTerminate|[std::function<void()>onProcessTerminate](https://intl.cloud.tencent.com/document/product/1055/36689#onhealthcheck)| Notification of process end |
|onHealthCheck |[std::function<bool()> onHealthCheck](https://intl.cloud.tencent.com/document/product/1055/36689#onprocessterminate)| Regular health check function |
|port|int| Port number listened on by game process |
|logParameters|[TencentCloud::Gse::Server::LogParameters](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx)| Path of logs to be uploaded |

#### Returned Value Description  
- True: success.
- False: failure.

A generic result in [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx) type containing an error message will be returned.

#### Use Cases
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




### onStartGameServerSession
#### API Description
Callback function: this API is used to notify the server that a game session is assigned. 	

#### Parameter Description

| Parameter Name | Type/Value | Description |
|:---|---|---|
|Custom|TencentCloud::Gse::Model::GameServerSession| Game session information|

#### Returned Value Description
No parameters.


#### Use Cases
```
void GseManager::OnStartGameServerSession(TencentCloud::Gse::Server::Model::GameServerSession myGameServerSession)
{
    TencentCloud::Gse::GenericOutcome outcome = 
    	TencentCloud::Gse::Server::ActivateGameServerSession();
}
```

### onHealthcheck
#### API Description
Callback function: this API is used to perform health check once per minute, and the health status needs to be returned within 1 minute. 

#### Parameter Description

No parameters.


#### Returned Value Description
- True: success.
- False: failure.




#### Use Cases
```
void GseManager::OnHealthCheck()
{
    // `true` or `false` will be returned based on the actual process health status
    return true;
}
```

### onProcessTerminate

#### API Description
Callback function: this API is used to end a process.

#### Parameter Description
No parameters.

#### Returned Value Description
- True: success.
- False: failure.




#### Use Cases
```
void GseManager::onProcessTerminate()
{
	TencentCloud::Gse::GenericOutcome outcome = 
		TencentCloud::Gse::Server::TerminateGameServerSession();
}   
```
