本文为您介绍 Scrum 敏捷管理模式中的 Backlog 功能。

## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏中的**项目协同**功能页。 

## 功能介绍

进入**项目协同**模块后，**待规划**中的**Backlog**版块展示了所有未规划进迭代并且未完成的事项，可以在此处维护 Backlog，支持创建事项，还可以通过拖拽事项上下进行优先级排序。

在敏捷研发流程中，CODING 建议首先由 Product Owner（产品负责人）在 Backlog 中录入并调整事项优先级，然后在迭代开始前由团队评估 Backlog 中排序靠前的事项。在创建迭代后，将事项纳入迭代中，即可开始迭代。

![](https://qcloudimg.tencent-cloud.cn/raw/658046fb7393f0698e0e393a9c5faea2.png)

### 快速创建事项[](#create)

1. 通过**Backlog**下方的**创建事项**，可以快速创建事项（用户故事、需求、任务、缺陷）。
![](https://qcloudimg.tencent-cloud.cn/raw/4cc781afa049a3a3041a8f833912fbde.png)
<dx-alert infotype="explain" title="">
**需求**事项默认关闭，可参见 [自定义事项类型](https://intl.cloud.tencent.com/document/product/1133/44766) 进行开启。
</dx-alert>
2. 可以在下拉菜单中选择事项类型，通过**标题**+**回车**快捷创建事项，也可使用**Shift**+**回车**完整创建事项。
![](https://qcloudimg.tencent-cloud.cn/raw/b8e8955722b023e9bb2b1a72a26c222c.png)
3. 在**Backlog**事项列表中点击任意事项，即可在右侧查看指定事项详情页，对事项进行快速编辑。
![](https://qcloudimg.tencent-cloud.cn/raw/0f73ea638ac9910f47afd3c733b14d7c.png)

### 调整事项优先级[](#priority)

**Backlog**事项列表支持拖拽排序，选择事项行即可上下拖拽该事项调整优先级。新创建的事项默认排在列表最后。
![](https://qcloudimg.tencent-cloud.cn/raw/b8fa5bff04e29625fa08bb72bacf138c.png)

### 待评估事项[](#be-assessed)

**Backlog**的待评估区域主要用于放置等待评估的事项，评估完成后即可放入已评估区域中进行排序和规划迭代，通常适用于需要维护大规模需求池的项目。
1. 需要前往**项目设置** > **项目协同** > **敏捷特性**页面，单击**Backlog 待评估区域**开关开启。
![](https://qcloudimg.tencent-cloud.cn/raw/7150faeb9698179a4cb7cdc8b495d35a.png)
2. 开启后将会出现分隔线，将**Backlog**分为**已评估**和**待评估**区域，事项可以在两个区域间互相拖拽，表示事项已完成评估或待评估；也可以将分隔线上下拖动，快速批量评估事项。
![](https://qcloudimg.tencent-cloud.cn/raw/670ca7ff14b5478ff01ee0cf064f0761.png)
<dx-alert infotype="notice" title="">
若在功能开关中关闭该功能，所有待评估的事项将自动转为已评估状态。
</dx-alert>

