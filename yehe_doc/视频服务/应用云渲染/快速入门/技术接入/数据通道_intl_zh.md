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