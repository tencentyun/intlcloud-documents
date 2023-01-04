本文档介绍反弹 Shell 功能的事件列表。

## 筛选刷新事件列表
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**运行时安全** > **反弹 Shell** > **事件列表**，进入事件列表页面。
2. 在事件列表页面，单击搜索框，可通过“进程名称、父进程名称和父进程名称”等关键词对反弹 Shell 事件进行查询。
<img src="https://qcloudimg.tencent-cloud.cn/raw/d638226da41c8ab75f2c9b328e95e967.png" style="zoom:67%;" />
3. 在事件列表页面，单击操作栏右侧![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png)图标，即可刷新反弹 Shell 事件列表。

## 导出事件列表
在事件列表页面，单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的反弹 Shell 事件后，单击![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png)图标即可导出反弹 Shell 事件。
>? 可单击![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png)图标勾选多个镜像后，单击![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png)图标可进行批量导出。

![](https://qcloudimg.tencent-cloud.cn/raw/1e66b5e216c669017e0811c7bc91f04f.png)

## 事件状态处理[](id:SJZTCL)
在事件列表页面，可对反弹 Shell 事件列表进行标记已处理、忽略和删除处理。
 - 标记已处理：单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选反弹 Shell 事件后，单击**标记已处理** > **确定**，即可将选中事件标记已处理。
>? 建议您参照事件详情中的“解决方案”，人工对该事件风险进行处理，可将事件标记为已处理。

 - 忽略：单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的反弹 Shell 事件后，单击**忽略** > **确定**，即可将选中事件忽略。
>? 仅将已选事件进行忽略，若再有相同事件发生依然会进行告警。

 - 删除：单击![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png)图标勾选所需的反弹 Shell 事件后，单击**删除** > **确定**，即可将选中事件删除。
>! 删除已选事件记录，控制台将不再显示，无法恢复记录，请慎重操作。

## 查看列表详情
1. 在事件列表页面，单击事件类型左侧![](https://main.qcloudimg.com/raw/5b9eac8b014539648daf1ade48e3188a.png)	图标，可查看事件描述。
![](https://qcloudimg.tencent-cloud.cn/raw/fd5f572f826c9fddc790e279133dfdbf.png)
2. 在事件列表页面，单击“容器名称/ID ”或“镜像名称/ID”，可跳转至对应的资产管理列表。
![](https://qcloudimg.tencent-cloud.cn/raw/c22322d25976bdfd7df7a58b7e1ba3a1.png)
3. 在事件列表页面，单击**查看详情**，右侧抽屉展示事件详细信息，包括告警事件详情、进程信息、父进程信息和事件描述。
![](https://qcloudimg.tencent-cloud.cn/raw/d72ee15c6ff9aa0bf1afc4a1fd005073.png)
4. 在事件列表页面，事件状态包含已处理、已忽略、待处理。可对不同状态的事件进行以下操作：
 - 已处理/已加白：单击**删除**，并在弹窗中进行二次确认删除，可将事件删除。
>? 删除该事件记录，控制台将不再显示，无法恢复记录，请慎重操作。

 ![](https://qcloudimg.tencent-cloud.cn/raw/58f1b9063155c272c68dbe8e028e157e.png)
 - 待处理：单击**立即处理**，可将事件标记为已处理、忽略、删除和添加白名单，详情请参见 [事件状态处理](#SJZTCL)。
 - 已忽略：单击**取消忽略**或**删除**，可将事件变为待处理或删除。
![](https://qcloudimg.tencent-cloud.cn/raw/7576f77d59d6a9a109f079536985162a.png)

## 自定义列表管理
1. 在事件列表页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
2. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/c6d4593f5d192cc388d221ff5de1db61.png" style="zoom:67%;" />

### 列表重点字段说明
1. 首次生成时间：该 Shell 反向连接事件首次触发告警的时间。
>? 系统默认对未处理的相同告警事件进行聚合。

2. 最近生成时间：聚合的告警事件最近触发告警的时间。可单击右侧排序按钮对列表事件按时间正序和时间反序进行排列。
3. 事件数量：聚合时间范围内该 Shell 反向连接事件触发告警的总数量。
4.  状态：包括已处理、已忽略、未处理、已加白，支持按状态对列表事件进行快速筛选。