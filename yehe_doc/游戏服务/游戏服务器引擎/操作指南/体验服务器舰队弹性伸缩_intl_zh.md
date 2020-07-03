## 操作场景
本文档主要指导您如何在服务器舰队进行弹性伸缩操作。



## 准备工作 
- 已集成 [ServerSDK 的代码包](https://intl.cloud.tencent.com/document/product/1055/36674)，您也可以 [使用示范包](https://intl.cloud.tencent.com/document/product/1055/36678)。
- 已完成 [新建服务器舰队](https://intl.cloud.tencent.com/document/product/1055/36675)。



## 操作步骤
### 修改扩缩容配置和进程数 
1. 登录 [游戏服务器引擎控制台](https://console.cloud.tencent.com/gse/asset)，单击左侧菜单【服务器舰队】。
2. 单击刚创建的服务器舰队的 ID，进入服务器舰队详情页。
3. 单击【扩缩容】，进入扩缩容详情页，单击右上角【修改】，修改扩缩容配置：
 - 游戏服务会话缓冲配置成50%，当服务器承载的游戏对局超过50%时，即会扩容。
 - 实例范围调整到0 - 3，让其有扩的空间。  
 ![](https://main.qcloudimg.com/raw/8c5756b270c965498e19a5954ce53905.png)  

### 创建游戏服务器会话，观察扩容情况
除了代码里集成 SDK 调用云 API，还可以通过 [云 API 调试](https://console.cloud.tencent.com/api/explorer?Product=gse) 快捷创建。
 ![](https://main.qcloudimg.com/raw/7a51ee63925890bd0ff336b0d684214b.png)  

通过云 API 调试创建成功一个游戏服务器会话，即可看到服务器舰队产生一个游戏服务器会话。
 ![](https://main.qcloudimg.com/raw/9eaf67be7b686426f0d026d5afb7aa69.png)

此步骤中一个 CVM 配置的默认是1个进程，创建一个游戏服务器会话将占用100%，上文游戏服务器会话配置为50%的缓冲，此时将自动扩容成2个服务器实例。  



### 结束游戏服务器会话，观察缩容情况
结束1个游戏服务器会话，自动缩容为1个实例。








