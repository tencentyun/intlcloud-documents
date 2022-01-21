### 接口描述
本接口（GetGameServerSessionId）用于获取游戏服务器会话 ID。		

### 参数描述
无参数。



### 返回值说明
游戏服务器会话 ID，具体类型为 [StringOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx)。

### 使用示例
```
TencentCloud::Gse::StringOutcome sessionIdOutcome = 
	TencentCloud::Gse::Server::GetGameServerSessionId();
```

