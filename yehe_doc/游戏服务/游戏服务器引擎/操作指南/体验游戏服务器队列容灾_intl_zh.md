## 操作场景
本文档主要指导您在游戏服务器队列进行容灾操作。


## 准备工作 
- 已集成 [ServerSDK 的代码包](https://intl.cloud.tencent.com/document/product/1055/36674)，您也可以 [使用示范包](https://intl.cloud.tencent.com/document/product/1055/36678)。
- 已创建服务器舰队1（上海地区）。
- 已创建服务器舰队2（美国地区）。
![](https://main.qcloudimg.com/raw/7726bf7876142b7b1e7ed626e2cd2f46.png)
![](https://main.qcloudimg.com/raw/5881c69ab304675cf86c741364a5502b.png)


## 操作步骤
### 创建游戏服务器队列
1. 登录 [游戏服务器引擎控制台](https://console.cloud.tencent.com/gse)，单击左侧菜单【游戏服务器队列】。
2. 选择刚创建的服务器舰队，并将上海-服务器舰队1和美国-服务器舰队2加入至队列。
3. 进入服务器舰队详情页，修改延迟策略：延时设置在150ms内：
![](https://main.qcloudimg.com/raw/1bbaed4ecdf6946d4b8d89490a18e5fb.png)


### 请求服务端地址
使用开始放置游戏服务器会话，除了在代码里集成 SDK 调用云 API，您还可以通过 [云 API 调试](https://console.cloud.tencent.com/api/explorer?Product=gse) 快捷创建。

**输入参数**：
- player1 至上海的延时100ms，至硅谷的延时50ms。
- player2 至上海的延时60ms，至硅谷的延时80ms。
![](https://main.qcloudimg.com/raw/fa0aa1e00bab6cfa89c1cd211b1af562.png)
![](https://main.qcloudimg.com/raw/29baaa97fb0e6a3e20a2f9b53f0a5bdd.png)
![](https://main.qcloudimg.com/raw/0327f3c13ce77d07af24e6fc5a417f59.png)



因为延迟策略配置查找所有玩家延时在150ms内的区域的服务器，硅谷和上海都满足要求，所以，游戏服务器会话自动创建于优先级高的上海-服务器舰队1上。
![](https://main.qcloudimg.com/raw/7a1a2d5bbb156d6dd99e29abd3cb8821.png)

### 自动容灾

假设现在上海出现了故障，上海的速度将无法测出。

**输入参数**：  
![](https://main.qcloudimg.com/raw/a143ffef65105d4a785e11803946ac3d.png)
![](https://main.qcloudimg.com/raw/e6b46c5b84adb4dea5e8da0613eb8bc2.png)
![](https://main.qcloudimg.com/raw/482798618d6366bd186a726364d7a831.png)


游戏服务器会话自动创建于优先级高的硅谷-服务器舰队2上。
![](https://main.qcloudimg.com/raw/d10d4b8c38a10b8a8bfb89ca9b292406.png)


### 手动容灾
如果某一区域出现故障，从游戏服务器会话队列中的目标列表，踢出该故障区域的 fleet。
![](https://main.qcloudimg.com/raw/94c558e6fa2df116135e8d0017bb19b2.png)
