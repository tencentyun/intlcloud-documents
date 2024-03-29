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


## 应用心跳连接
本节主要介绍如何维持服务心跳连接。建议业务通过心跳来感知用户连接情况，可以收集管理用户连接时长等数据，当客户端异常退出之后业务后台可以快速回收资源，更合理利用并发资源。
### 时序图
![](https://qcloudimg.tencent-cloud.cn/raw/ff17676e26edbdda33036b615fe6d55a.jpg)

### 步骤说明
1. 业务客户端定时向业务后台发送心跳上报，业务后台根据心跳上报维护用户连接状态。
2. 业务后台定时检查用户连接状态，如果有用户心跳超时，业务后台通过云渲染 API 调用 [DestroySession()](https://intl.cloud.tencent.com/document/product/1158/49967) 销毁会话，业务云端应用将被主动关闭，业务客户端断开与云应用连接。

## 数据通道
本节主要介绍如何使用数据通道与云端运行的应用直接进行通信。当业务需要建立客户端与云端应用的通信时，可以使用数据通道能力。
### 时序图
![](https://qcloudimg.tencent-cloud.cn/raw/d30a87c7f0069f555992b253ecf190e2.jpg)

### 步骤说明
1. [](id:step4_1)业务云端应用创建 UDP 服务，监听一个本地 UDP 端口（`localhost 127.0.0.1` 端口范围建议为 10000 - 20000），并开始等待接收 UDP 包。
2. 业务客户端调用 [TCGSDK.start()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.start(serverSession)) 接口启动云渲染应用，SDK 完成应用连接后会触发回调 onConnectSuccess()，建议业务客户端在这之后创建数据通道。
3. 业务客户端调用[TCGSDK.createCustomDataChannel()](https://intl.cloud.tencent.com/document/product/1158/49627#tcgsdk.createcustomdatachannel(.7Bdestport.2Conmessage.7D)) 接口创建透传通道，接口里的目标端口参数应为 [步骤1](#step4_1) 中云端应用监听的端口，如果创建失败则重复本步骤直到创建成功。
4. [](id:step4_4)数据通道创建成功后，业务客户端可以调用 sendMessage()  发送业务自定义的数据包，云端应用 UDP 服务收到请求，解析出 UDP 来源地址。
5. 云端应用向 [步骤4](#step4_4) 拿到的 UDP 来源地址发送自定义数据包，数据包将通过创建好的数据通道回传，业务客户端可以在回调 onMessage()  接口中处理回传的数据包。

## 重连应用
本节主要介绍如何重连应用。当用户直接关闭客户端而未主动调用关闭应用功能时，业务可以通过再次调用申请并发和创建会话接口实现重连应用功能。
### 时序图
![](https://qcloudimg.tencent-cloud.cn/raw/01990988def83c87a9e35693ebcf857e.jpg)

### 步骤说明
1. 业务客户端关闭后会断开与业务云端应用的连接，若非主动调用接口关闭云端应用，则默认保持 90s 的重连时间等待重连。
2. 业务客户端重新打开后，通过传入相同的 UserId 向业务后台请求启动应用，若 UserId 不同则不能实现重连功能。
3. 业务后台通过云渲染 API 调用 [ApplyConcurrent()](https://intl.cloud.tencent.com/document/product/1158/49969) 申请锁定并发，根据并发状态进行如下处理：
	- 用户上次连接并发还未回收，返回上一次连接并发资源。
	- 用户上次连接并发已回收，返回新并发资源。
4. 业务后台通过云渲染 API 调用 [CreateSession()](https://intl.cloud.tencent.com/document/product/1158/49968)  创建会话，将返回的服务端 ServerSession 回传给业务客户端，重新启动应用。
