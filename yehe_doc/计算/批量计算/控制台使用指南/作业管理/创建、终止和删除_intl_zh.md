## 操作场景
本文介绍如何通过批量计算控制台，创建、终止及删除作业。作业相关说明，请参见 [名词解释](https://intl.cloud.tencent.com/document/product/599/10396) 中“作业”。


## 操作步骤
### 创建作业
1. 登录 [批量计算控制台](https://console.cloud.tencent.com/batch/job)。如果您尚未开通批量计算服务，请参照批量计算控制台主页相关提示开通。
2. 选择左侧导航栏中的**作业**，并在页面上方选择目标地域。
3. 在“作业”列表页面，单击**新建**。
4. 进入“新建作业”页面，配置作业基本信息。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/aef77141251c4b605449439ea215859d.png)
5. 选中“任务流”左侧任务模板，移动鼠标将任务放置到右侧画布中，拖拽锚点建立连接。如下图所示：
 ![](https://main.qcloudimg.com/raw/1436b756d73f6fffa68eff65741922ee.png)
6. 打开“任务流”右侧“任务详情”，进行配置确认。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a96a06571e4849b8e655cd4d672f1de2.png)
 + 在作业任务流中，每个任务均基于任务模板定制生成。
 + 打开右侧“任务信息”选项，选中某一个任务，可以编辑该任务部分配置。编辑操作对任务模板没有影响。
7. 确认无误后，单击**完成**即可完成创建。   
	
### 终止作业
您可以在特定条件下终止作业的运行。终止相关说明，请参见 API 文档 [终止任务实例](https://intl.cloud.tencent.com/document/product/599/30489)。控制台操作步骤如下：
1. 登录批量计算控制台，选择左侧导航栏中的 **[作业](https://console.cloud.tencent.com/batch/job)**。
2. 选择需终止作业所在行右侧的**终止**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/71601c4651392824992868b8be1c0fd9.png)
3. 在弹出的确认窗口中，单击**确定**即可。

### 删除作业
当作业处于完结状态，即“成功”或“运行失败”状态时，即可在“作业列表”中删除作业。控制台操作步骤如下：
1. 登录批量计算控制台，选择左侧导航栏中的 **[作业](https://console.cloud.tencent.com/batch/job)**。
2. 选择需终止作业所在行右侧的**删除**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/844978fd665933043d1acce1c7a9f961.png)
3. 在弹出的确认窗口中，单击**确定**即可。



