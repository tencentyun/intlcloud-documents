## 排队功能
本节主要介绍如何引入用户排队系统。当用户在线数大于资源并发数量时，建议业务引入用户排队系统，提升用户体验。
### 时序图
![](https://qcloudimg.tencent-cloud.cn/raw/ef3d594d9fe81d0f98e856cbc289491c.jpg)

### 步骤说明
1. 业务客户端调用 [TCGSDK.init()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.init(params)) 接口完成初始化构建。初始化完成后，再调用 [TCGSDK.getClientSession()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.getClientSession()) 获取 Client 端的 ClientSession。
2. [](id:step2)业务客户端通过传入 UserId 和 ClientSession 等参数向业务后台请求启动应用，其中 UserId 是由业务方自定义的唯一用户标识，在用户排队和重连应用时应保持不变。业务后台需要根据当前排队状况进行如下处理： 
	- 队列不为空时，则将用户加入队列并返回当前队列排名信息。业务客户端收到排队信息后定时发起请求，重复 [步骤2](#step2) 直到启动应用成功。
	- 如果队列为空或者用户排在第一位跳转到 [步骤3](#step3)。
3. [](id:step3)业务后台通过云渲染 API 调用 [ApplyConcurrent()](https://intl.cloud.tencent.com/document/product/1158/49969) 申请锁定云渲染并发，根据返回结果进行如下处理：
	- 没有空闲并发或者其他错误时，则将用户加入队列并返回当前队列排名信息，跳转回 [步骤2](#step2) 重新请求。
	- 申请并发成功则跳转到 [步骤4](#step4)。
4. [](id:step4)业务后台通过云渲染 API 调用 [CreateSession()](https://intl.cloud.tencent.com/document/product/1158/49968)  创建会话，将返回的服务端 ServerSession 回传给业务客户端。

5. 业务客户端调用 [TCGSDK.start()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.start(serverSession)) 接口启动云渲染应用，SDK 完成应用连接后会触发回调 onConnectSuccess()，建议包括数据通道等其他功能都在这之后调用创建。