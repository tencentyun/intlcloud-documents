## 操作场景


## 准备工作 
- 已集成 [ServerSDK 的代码包](https://intl.cloud.tencent.com/document/product/1055/36674)，您也可以 [使用示范包](https://intl.cloud.tencent.com/document/product/1055/36678)。  
- 已创建服务器舰队1（上海地区）。
- 已创建服务器舰队2（美国地区）。
![](https://main.qcloudimg.com/raw/e9240bad9dc778191158a37dba941908.png)
![](https://main.qcloudimg.com/raw/a22c7cb934124b91728523e56d42f3fc.png)


## 操作步骤
### 创建游戏服务器队列
1. 登录 [游戏服务器引擎控制台](https://console.cloud.tencent.com/gse)，单击左侧菜单【游戏服务器队列】。
2. 选择刚创建的服务器舰队，并将上海-服务器舰队1和美国-服务器舰队2加入至队列。
3. 进入服务器舰队详情页，修改延迟策略： 
 - 前10s优先查找所有玩家延时在80ms内的区域的服务器。  
 - 再花10s（前20s）优先查找所有玩家延时在100ms内的区域的服务器。
 - 剩下其余时间查找所有玩家延时在150ms内的区域的服务器。 
![](https://main.qcloudimg.com/raw/8cbb559b51629ba60935de0c8b5fd735.png)


### 使用队列创建游戏服务器会话

使用开始放置游戏服务器会话，除了在代码里集成 SDK 调用云 API，您还可以通过 [云 API 调试](https://console.cloud.tencent.com/api/explorer?Product=gse) 快捷创建。

**输入参数**：  
- player1 至上海的延时100ms，至硅谷的延时50ms。
- player2 至上海的延时60ms，至硅谷的延时80ms。
![](https://main.qcloudimg.com/raw/17f2f5c2259cbb8259aaa518c6483195.png)
![](https://main.qcloudimg.com/raw/e22e0c148d52885be3ceea010c13ce19.png)
![](https://main.qcloudimg.com/raw/6d3d71aa4c6173ae78112727ac12abec.png)



因为延迟策略配置为前10s优先查找所有玩家延时在80ms内的区域的服务器，所以，游戏服务器会话会调度至硅谷。  



**调用 API 后测试结果：游戏服务器会话将调度至硅谷-服务器舰队2**
![](https://main.qcloudimg.com/raw/65d66c009ed756257c91772cc249f4c1.png)




