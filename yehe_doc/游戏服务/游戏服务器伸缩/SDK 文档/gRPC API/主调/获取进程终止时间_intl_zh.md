
### 接口描述
本接口（GetTerminationTime）用于获取估计的进程终止时间，返回-1表示随时缩容。	

### 参数描述

无参数。

### 返回值说明

获得终止时间，具体类型为 [LongOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx)。



### 使用示例
```
TencentCloud::Gse::LongOutcome TermTimeOutcome = 
	TencentCloud::Gse::Server::GetTerminationTime();
```
