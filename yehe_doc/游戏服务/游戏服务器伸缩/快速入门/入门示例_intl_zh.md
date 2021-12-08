
## 操作场景

本文档主要指导您如何通过“入门示例”，体验 GSE 主流程，入门游戏服务器托管服务。

## 操作步骤

### 步骤1：上传示范包
 1. 登录 [游戏服务器伸缩控制台](https://console.cloud.tencent.com/gse)，单击左侧菜单**入门示例**。
 2. 选择左上侧服务区域，单击**一键上传示范包**，上传示范包，提示创建成功后，单击**下一步**。
    ![](https://main.qcloudimg.com/raw/aba9f81e1e145dd9233c962a71f9938e.png)
 >?
    - GSE 为您提供的示范包已经集成了 gRPC 框架，游戏进程和 GSE 通过 gRPC 通信。
    - 如果是您自行创建，请您参考 [创建生成包](https://intl.cloud.tencent.com/document/product/1055/36674) 操作指南。

### 步骤2：创建服务器舰队
单击**一键创建服务器舰队**，依次会提示“新建（进行中）”、“下载中（进行中）”、直至提示“创建服务器舰队成功”后，单击**下一步**。
 - 创建服务器舰队需要6个步骤：新建（已完成）、下载中（已完成）、验证中（已完成）、生成中（已完成）、激活中（已完成）、活跃（已完成）。
 - 当前状态：创建中、创建服务器舰队成功。
![](https://main.qcloudimg.com/raw/8854d79ca8ce4f1edbb4f93529766bdb.png)
![](https://main.qcloudimg.com/raw/013f88008a3833369c8ab2ca1ae8a0a9.png)
![](https://main.qcloudimg.com/raw/d395303b0afa601cd1e7bd29713816e2.png)
 >?
   - 创建服务器舰队，将示范包部署在服务器舰队上。
   - 服务器舰队为一组服务器，具有弹性伸缩的能力，示范包可轻松部署到全球。
   - 如果是您自行创建，请您参考 [创建服务器舰队](https://intl.cloud.tencent.com/document/product/1055/36675) 操作指南。

### 步骤3：创建游戏服务器会话和玩家会话
- 单击**创建游戏服务器会话**，提示创建游戏服务器会话成功。 
![](https://main.qcloudimg.com/raw/00e1ad7d8190f60cf021f5a1ec82d437.png)
 >?
    - 该操作调用“创建游戏服务器会话”云 API，GSE 创建一个游戏服务器会话，为其分配一个服务进程。
    - 如果是您自行创建，请您参考 [创建游戏服务器会话](https://intl.cloud.tencent.com/zh/document/product/1055/37139) API 文档。 
- 单击**创建玩家会话**，提示创建玩家会话成功。
![](https://main.qcloudimg.com/raw/3ac88d02e60888dafce042625927cba4.png)
>?
    - 该操作调用“加入游戏服务器会话”云 API，GSE 创建一个玩家会话，将玩家加入到游戏服务器会话中。
    - 如果是您自行创建，请您参考 [加入游戏服务器会话](https://intl.cloud.tencent.com/zh/document/product/1055/39130) API 文档。

### 步骤4：客户端连接游戏服务器
   单击**跳转至客户端网页**，进入客户端连接游戏服务器页面，单击**连接**，提示服务器：连接成功。 
   ![](https://main.qcloudimg.com/raw/c4975e69e97cfb875b72af739c290888.png)

>?
>
>- 在完成创建玩家会话后，玩家（客户端）需要在1分钟内连接服务端，否则将失效。
>- 此示范包是一个聊天服务。当多个玩家连接到该服务器时，可进行聊天。

 以上四个步骤模拟了 GSE 整个接入过程，更多详细信息请您参考 [开发指南](https://intl.cloud.tencent.com/zh/document/product/1055/36683) 文档。
