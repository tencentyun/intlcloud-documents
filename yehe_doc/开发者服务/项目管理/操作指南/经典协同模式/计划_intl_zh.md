本文为您介绍经典项目管理模式下的计划功能。


## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏中的**项目协同**功能页。

## 功能介绍

**计划**功能按迭代分组显示事项的进度和时间视图，可通过**计划**规划迭代、分解需求、分配任务、设置任务周期等，便于安排较大项目的交付计划。
![](https://qcloudimg.tencent-cloud.cn/raw/032bf0b90a7ba9a1bcae08e7eea61300.png)

### 根据迭代进行规划[](#plan)

根据经典项目管理模式的工作流，团队在完成需求评审，项目 Leader 批准开发计划后，将以**迭代**作为承载单元，衍生出一系列开发排期计划。可以通过**计划**页右上角创建迭代，填写标题、负责人、开始和结束时间、迭代目标后，单击**创建**即可完成创建。
![](https://qcloudimg.tencent-cloud.cn/raw/20990a7732ebcd39d3ada36d5a5d073a.png)
单击**创建并规划**则可将已创建但未规划的事项拖拽或勾选至当前迭代中。
![](https://qcloudimg.tencent-cloud.cn/raw/8d2ff0d446608f49182b35959bde3740.png)
创建迭代后，**计划**内将显示该迭代，可在该迭代下通过**+**创建事项（需求、任务、缺陷）完善计划安排。具体操作请参见 [规划迭代](https://intl.cloud.tencent.com/document/product/1133/44746)。
![](https://qcloudimg.tencent-cloud.cn/raw/8fa6e36dc012542fc4b756ba4c4912db.png)

### 查看计划[](#check)

#### 按筛选条件查看[](#filter-criteria)

在**计划**内，通过上方筛选器**更多筛选**设置条件快速定位特定事项，系统将自动保存单次筛选设置的条件，方便再次查询。
![](https://qcloudimg.tencent-cloud.cn/raw/e74480385bcfe93a2109a837f0ab3d35.png)

#### 按时间周期查看[](#time-period)

在**计划**内通过右上方筛选器设置时间周期，支持按日、按周、按月显示，系统将自动保存设置的周期，方便再次查询。
![](https://qcloudimg.tencent-cloud.cn/raw/1f8795c3a4a8ea49f2346ea7ef51a38a.png)

### 跟踪计划[](#track)

#### 甘特图[](#gantt-chart)

**计划**内右侧展示甘特图，直观表明在整个计划中各事项的完成情况，帮助管理者评估并把控工作进度，协调滞后事项，确保计划顺利推动。
![](https://qcloudimg.tencent-cloud.cn/raw/a95b731e17136e72996935fe4788d49a.png)
<dx-alert infotype="explain" title="颜色说明">

<ul style = "margin-bottom: 0px;">
<li>完成状态：绿色</li>
<li>未完成无进度：灰色</li>
<li>未完成有进度：蓝色</li>
<li>事项未完成且开始和截止时间超出父级事项：橙色</li>
<li>截止到期但未完成：橙色</li>
</ul>
</dx-alert>
可以根据使用习惯，收起或展开事项属性。

![](https://qcloudimg.tencent-cloud.cn/raw/ff9edb5b366a4a0977c7a350036e829b.png)

#### 查看阻塞关系[](#blocking)

在**计划**内指定事项后方的甘特图中，会展示该事项的阻塞关系与数量，包含阻塞关系中的前置与后置事项。
![](https://qcloudimg.tencent-cloud.cn/raw/fb19013da50b3b77ca0035ce4f842658.png)

可通过阻塞事项右方**`···`** > **解除阻塞关系**移除该事项，或选择**关联前置/后置事项**新增阻塞事项。
![](https://qcloudimg.tencent-cloud.cn/raw/4806a6c387af3ae9b994f8b390b0825a.png)

#### 展示阻塞关系[](#display)

在**计划**上方开启**阻塞关系**显示模式时，筛选条件将会被自动清空，方便展示当前事项的前后阻塞关系。若开启**显示依赖链**，则将递归展示与当前事项依赖关系相关的所有事项的依赖。
![](https://qcloudimg.tencent-cloud.cn/raw/b363d93e91fc594ddbd3ad73f340df4b.png)

### 控制风险[](#risk-control)

#### 逾期警告[](#delay-warning)

当事项开始时间早于父级事项开始时间、截止时间超过父级事项截止时间、开始时间早于前置事项结束时间，或事项已逾期 N 天，**计划**内将会使用黄色感叹号**！**，在该事项前方提示风险及时间，帮助团队及时调整计划。
![](https://qcloudimg.tencent-cloud.cn/raw/e857a679141f7c83d4fe6dc278f7a963.png)

### 视图设置[](#view)

**计划**内**视图设置**用于调整显示的迭代数量，支持按开始时间正序或倒序排序。默认关闭**显示近期完成的迭代**，简化界面显示，便于团队聚焦当前进行的迭代，可根据需求开启。
![](https://qcloudimg.tencent-cloud.cn/raw/681aa9245878f8e0c6c31f7e5da0eaf5.png)
