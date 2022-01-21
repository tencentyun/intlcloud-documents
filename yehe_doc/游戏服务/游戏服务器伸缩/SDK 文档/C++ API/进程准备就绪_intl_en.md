

## API Description
This API is used to notify the server that that service is ready. It can register the callback function, port and log directory.  
When the GSE service receive the notification, it changes the server status to ACTIVE, and, if the callback function is registered, it calls onHealthCheck once per minute. It’s considered valid if the result is returned in one minute.

### Parameters

<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th>Type/value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">onStartGameServerSession</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/1055/37426">std::function &lt;void(tencentcloud::gse::model::gameserversession)&gt; onStartGameServerSession</a></td>
<td>The callback function after creation of the game session</td>
</tr>
<tr>
<td align="left">onProcessTerminate</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/1055/37426">std::function&lt;void()&gt;onProcessTerminate</a></td>
<td>Notify the server to end the process</td>
</tr>
<tr>
<td align="left">onHealthCheck</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/1055/37426">std::function&lt;bool()&gt; onHealthCheck</a></td>
<td>Scheduled health check function</td>
</tr>
<tr>
<td align="left">port</td>
<td>int type</td>
<td>The port listened by the game process</td>
</tr>
<tr>
<td align="left">logParameters</td>
<td>TencentCloud::Gse::Server::LogParameters</a></td>
<td>The log directory to upload</td>
</tr>
</tbody></table>

#### Return value description  
- true: success.
- `False`: failure.

A result containing the error message. Type: GenericOutcome

#### Example
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
## API Description
Callback function: notify that a game session is assigned 	

### Parameters

|Parameter|Type/value|Description|
|:---|---|---|
|Custom|TencentCloud::Gse::Model::GameServerSession|Game session information|

#### Returned value description
No parameters


#### Example
```
void GseManager::OnStartGameServerSession(TencentCloud::Gse::Server::Model::GameServerSession myGameServerSession)
{
    TencentCloud::Gse::GenericOutcome outcome = 
    	TencentCloud::Gse::Server::ActivateGameServerSession();
}
```

### onHealthcheck
## API Description
Callback function: health check, once per minute. It’s considered healthy if the response is returned in one minute. 

### Parameters

No parameters


#### Returned value description
- `True`: success.
- `False`: failure.




#### Example
```
void GseManager::OnHealthCheck()
{
    // Return `true` or `false` according to the health status of the process
    return true;
}
```

### onProcessTerminate

## API Description
Callback function: end the process

### Parameters
No parameters

#### Returned value description
- `True`: success.
- `False`: failure.



#### Example
```
void GseManager::onProcessTerminate()
{
	TencentCloud::Gse::GenericOutcome outcome = 
		TencentCloud::Gse::Server::TerminateGameServerSession();
}   
```
