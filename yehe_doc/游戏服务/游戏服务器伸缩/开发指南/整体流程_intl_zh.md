## 整体流程图
![](https://main.qcloudimg.com/raw/70af47a2520180f93b202547acaadac8.png)
## 接入步骤
### 步骤1：服务器集成 gRPC 框架
游戏服务器和 GSE 通过 gRPC 通信，游戏服务器程序集成 gRPC 框架，实现多语言接入，生成游戏服务器可执行文件。各语言服务端接入 GSE 的具体教程请您参考腾讯云 [gRPC-C++ 教程](https://intl.cloud.tencent.com/document/product/1055/37408)、[gRPC-C# 教程](https://intl.cloud.tencent.com/document/product/1055/37409)、[gRPC-Go 教程](https://intl.cloud.tencent.com/document/product/1055/37410)、[gRPC-Java 教程](https://intl.cloud.tencent.com/document/product/1055/37411)、[gRPC-Lua 教程](https://intl.cloud.tencent.com/document/product/1055/37412)、[gRPC-Nodejs 教程](https://intl.cloud.tencent.com/document/product/1055/37413) 文档。其他语言请您参考 [gRPC 官方文档](http://doc.oschina.net/grpc)。

### 步骤2：发布程序

1. 上传生成包 
生成包包括游戏服务器可执行文件、依赖包、安装脚本，将其打包成 zip 包后上传。详情请参见 [创建生成包](https://intl.cloud.tencent.com/document/product/1055/36674)。
2. 创建服务器舰队 
将上传的生成包部署在新建的服务器舰队上，并完成进程管理、部署配置、扩缩容配置等。 详情请参见 [创建服务器舰队](https://intl.cloud.tencent.com/document/product/1055/36675)。   

### 步骤3：调用云 API ，获取服务器地址（IP:port）

通过创建游戏服务器会话或放置游戏服务器会话，即可获取服务器地址（IP:port）。

#### 方式一：创建游戏服务器会话
调用云 API：
根据不同的游戏服务器会话支持方式，有不同的客户端云 API 调用流程。
-  当一个游戏服务器会话仅支持一局游戏时 ：
   - 创建游戏服务器会话（[CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)）；
   - 加入游戏服务器会话（[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)）。
-  当一个游戏服务器会话支持多局游戏或一个服务（如登录服）时：
   - 查询游戏服务器会话列表（[DescribeGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37136)）或搜索游戏服务器会话列表（[SearchGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37131)）；
   - 当已有游戏服务器会话时，则加入游戏服务器会话（[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)）；
   - 当没有游戏服务器会话时，则先创建游戏服务器会话（[CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)），再加入游戏服务器会话（[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)）。

调用云 API 的具体操作请参见 [创建游戏服务器会话](https://intl.cloud.tencent.com/document/product/1055/37416) 文档。

#### 方式二：放置游戏服务器会话
调用云 API：
 - 开始放置游戏服务器会话（[StartGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37130)）；
 - 查询游戏服务器会话的放置（[DescribeGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37137)）；
 - 停止放置游戏服务器会话（[StopGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37129)）。

调用云 API 的具体操作请参见 [放置游戏服务器会话](https://intl.cloud.tencent.com/document/product/1055/37417) 文档。

### 步骤4：客户端通过 IP:port访问服务器
步骤3已返回服务端 IP:port，客户端可通过该 IP:port连接至目标服务器。

## 工作流程图
![](https://main.qcloudimg.com/raw/02ec2067c8e06f5e1d1f3130aee7b81d.png)
