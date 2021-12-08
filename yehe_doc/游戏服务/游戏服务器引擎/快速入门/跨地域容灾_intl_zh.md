## 操作场景

本文档主要指导您通过游戏服务器队列实现跨地域容灾的功能。


## 前提条件 

- 创建两个上海和硅谷的服务器舰队。操作步骤为：
  - 完成 [入门示例](https://intl.cloud.tencent.com/document/product/1055/37401) 操作步骤的前三步：单击**一键上传示范包**、**一键创建服务器舰队**、**创建游戏服务器会话**，最后单击**完成**。
- 已创建服务器舰队1（上海地区）。
![](https://main.qcloudimg.com/raw/7726bf7876142b7b1e7ed626e2cd2f46.png)
- 已创建服务器舰队2（美国地区）。
![](https://main.qcloudimg.com/raw/5881c69ab304675cf86c741364a5502b.png)

## 操作步骤

### 创建游戏服务器队列

1. 登录 [游戏服务器伸缩控制台](https://console.cloud.tencent.com/gse)，单击左侧菜单**游戏服务器队列**，进入游戏服务器队列页面。
2. 选择左上侧服务地域，然后单击**新建**。
3. 进入新建游戏服务器队列页面，填写基本信息：
   - 标识符：输入合法的标识符，仅限英文字符，此示例填 “disasterrecovery”。
   - 分配超时时间：输入游戏服务器会话请求可在多区域等待的最长时间，最大值为600秒，此处示例配置30秒。
4. 填写延迟策略： 
  - 剩余超时时间（30s）查找所有玩家延时在150ms内的服务器舰队。
5. 目标选择已创建好的服务器舰队1（上海地区）和服务器舰队2（美国地区）。
6. 单击**确定**即可创建完成游戏服务器队列。
![](https://main.qcloudimg.com/raw/5499f546232f016127e201c6ce40f871.png)


### 无故障时，请求服务端地址

通过“开始放置游戏服务器会话”云API，将游戏服务器会话放置在服务器舰队中的进程里。在代码里调用云 API，此示例通过 [云 API 调试](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=StartGameServerSessionPlacement&SignVersion=) 快捷创建。
>?输入参数说明：
>- Region 区域，此示例选择“华东地区（上海）”；
>- PlacementId 开始部署游戏服务器会话的唯一标识符，此示例填1；
>- GameServerSessionQueueName 游戏服务器会话队列名称，此示例填 “disasterrecovery”；
>- MaximumPlayerSessionCount 游戏服务器允许同时连接到游戏会话的最大玩家数量，此示例填2；
>- DesiredPlayerSessions.N 玩家游戏会话信息，其中 PlayerId 是与玩家会话关联的唯一玩家标识，此示例添加两组，分别填1和2；
>- PlayerLatencies.N 玩家延迟，其中PlayerId是玩家 Id，RegionIdentifier是延迟对应的区域名称，LatencyInMilliseconds 是毫秒级延迟。此示例添加四组，分别填[1，ap-shanghai，100]、[1，na-siliconvalley，50]、[2，ap-shanghai，60]、[2，na-siliconvalley，80]。

![](https://main.qcloudimg.com/raw/bf528fd7700938e035cbe7ccd201954c.png)
![](https://main.qcloudimg.com/raw/29baaa97fb0e6a3e20a2f9b53f0a5bdd.png)
![](https://main.qcloudimg.com/raw/0327f3c13ce77d07af24e6fc5a417f59.png)
**延迟策略调度结果评估：**
两个玩家到目标地址的延迟情况：

- player1 至上海的延时100ms，至硅谷的延时50ms。
- player2 至上海的延时60ms，至硅谷的延时80ms。
因为延迟策略配置查找所有玩家延时在150ms内的服务器，硅谷和上海都满足要求，所以，游戏服务器会话自动创建于优先级高的服务器舰队1（上海地区）上。
![](https://main.qcloudimg.com/raw/7a1a2d5bbb156d6dd99e29abd3cb8821.png)

### 有故障时，自动容灾

假设现在上海出现了故障，上海的速度将无法测出。
>?输入参数说明： 
  - PlayerLatencies.N 玩家延迟，其中 PlayerId 玩家 Id，RegionIdentifier 延迟对应的区域名称，LatencyInMilliseconds 毫秒级延迟。此示例添加四组，分别填[1，ap-shanghai，0]、[1，na-siliconvalley，50]、[2，ap-shanghai，0]、[2，na-siliconvalley，80]。设置无法测出速度的条件时，将延时输入为0或者无穷大，或者不输入，此示例到上海的延迟输入为0。
  - 其他参数输入与上文保持一致。

![](https://main.qcloudimg.com/raw/bf528fd7700938e035cbe7ccd201954c.png)
![](https://main.qcloudimg.com/raw/e6b46c5b84adb4dea5e8da0613eb8bc2.png)
![](https://main.qcloudimg.com/raw/482798618d6366bd186a726364d7a831.png)


**延迟策略调度结果评估：**
两个玩家到目标地址的延迟情况：
- player1 至上海的延时0ms，至硅谷的延时50ms。
- player2 至上海的延时0ms，至硅谷的延时80ms。

上海的延迟为0ms表示因为上海出现故障，无法测出延迟，因此游戏服务器会话自动创建于美国区的服务器舰队2上。
![](https://main.qcloudimg.com/raw/eccba22674c685285bb94220bd9b407c.png)

### 有故障时，手动容灾

如果某一地域出现故障，您需要从游戏服务器会话队列的目标列表中，手动删除该故障地域的服务器舰队，GSE 会将游戏服务器会话调度到目标列表中剩余的服务器舰队上。
![](https://main.qcloudimg.com/raw/94c558e6fa2df116135e8d0017bb19b2.png)

