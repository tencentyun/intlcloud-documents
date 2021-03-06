

#### 接口描述
本接口（ProcessReady）用于告知服务准备就绪，同步方法。它可注册回调函数、端口、和日志目录。 
GSE 服务器接收后，将服务器实例状态改为 ACTIVE， 如果已注册回调函数，每1分钟调用1次 onHealthCheck，onHealthCheck 在1分钟内返回有效。

#### 参数描述

|参数名|类型/值|描述|
|:---|---|---|
|onStartGameServerSession|[std::function <void(TencentCloud::Gse::Model::GameServerSession) > onStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/36689#onstartgameserversession)|创建游戏会话后的回调函数|
|onProcessTerminate|[std::function<void()>onProcessTerminate](https://intl.cloud.tencent.com/document/product/1055/36689#onhealthcheck)|通知请结束进程|
|onHealthCheck |[std::function<bool()> onHealthCheck](https://intl.cloud.tencent.com/document/product/1055/36689#onprocessterminate)|定时健康检查函数|
|port|int 类型|游戏进程监听的端口号|
|logParameters|[TencentCloud::Gse::Server::LogParameters](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx)|要上传的日志路径|

#### 返回值说明  
- True：成功。
- False：失败。

包含错误消息的一般结果，具体类型为 [GenericOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx)。

#### 使用示例
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
#### 接口描述
回调函数：通知分配了一个游戏会话。 	

#### 参数描述

|参数名|类型/值|描述|
|:---|---|---|
|自定义|TencentCloud::Gse::Model::GameServerSession|游戏会话信息|

#### 返回值说明
无参数。


#### 使用示例
```
void GseManager::OnStartGameServerSession(TencentCloud::Gse::Server::Model::GameServerSession myGameServerSession)
{
    TencentCloud::Gse::GenericOutcome outcome = 
    	TencentCloud::Gse::Server::ActivateGameServerSession();
}
```

### onHealthcheck
#### 接口描述
回调函数：健康检查，1分钟检查1次，1分钟内需要答复健康状态。 

#### 参数描述

无参数。


#### 返回值说明
- True：成功。
- False：失败。




#### 使用示例
```
void GseManager::OnHealthCheck()
{
    //根据进程实际健康情况，返回true or false
    return true;
}
```

### onProcessTerminate

#### 接口描述
回调函数：结束进程。

#### 参数描述
无参数。

#### 返回值说明
- True：成功。
- False：失败。




#### 使用示例
```
void GseManager::onProcessTerminate()
{
	TencentCloud::Gse::GenericOutcome outcome = 
		TencentCloud::Gse::Server::TerminateGameServerSession();
}   
```
