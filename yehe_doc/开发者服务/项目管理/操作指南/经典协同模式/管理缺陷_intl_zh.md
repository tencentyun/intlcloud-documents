本文为您介绍经典项目管理模式下的缺陷功能。


## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏中的**项目协同**功能页。

## 功能介绍

CODING 项目协同的**缺陷**功能可以帮助团队清晰了解缺陷（Bug）的具体信息，提高缺陷流转及处理效率，极大提升企业用户进行大规模缺陷管理的效率。

## 创建缺陷[](#create)

1.  进入任意项目后，在**项目协同** > **缺陷**页面，单击模块右上方**创建缺陷**，填写缺陷标题、缺陷描述等基本信息后即可完成创建。
![](https://qcloudimg.tencent-cloud.cn/raw/2ced008b1111ffbd1e53927f935ee780.png)
2.  创建完成后，缺陷状态默认为**待处理**，可以在缺陷详情页切换状态，并进行设置处理人、关联所属需求、规划所属迭代、调整优先级、设置起始日期、预估/记录工时、添加标签等详细操作。
![](https://qcloudimg.tencent-cloud.cn/raw/4a30426a2e4b7c974fb2c5fd9677413d.jpeg)

## 关联阻塞关系[](#blocking)

缺陷内可以设置已有事项为前置/后置阻塞事项。在缺陷详情页内，通过上方**阻塞关系**选项，输入事项 ID 或标题，即可查找并完成关联。可在**前置/后置事项**中切换。关于阻塞关系的详细讲解，请参见 [阻塞关系](https://intl.cloud.tencent.com/document/product/1133/44750)。
![](https://qcloudimg.tencent-cloud.cn/raw/38e95fb7cd4c3263871a8857d06f2fb3.jpeg)

## 引用资源[](#references)

在缺陷详情页的描述或评论中，可通过 `# + 引用 ID/标题` 形式选择资源，引用的资源将会在引用列表中展示；如果当前缺陷被其他资源引用，那么其他资源将会显示在该缺陷的被引用列表中。
![](https://qcloudimg.tencent-cloud.cn/raw/09d7d476bb4267eeafd0c23fdd7026a9.jpeg)

还支持将**代码提交**与事项进行关联，可以在代码执行提交时，在提交信息中插入关联事项 `# + 引用 ID/标题` 信息（例如：这是一次提交 #3）。详情请参见 [引用资源和上传附件](https://intl.cloud.tencent.com/document/product/1133/44770)。


## 缺陷状态流转[](#status)

缺陷状态是指缺陷在生命周期中所处的阶段，用于组织和跟踪缺陷，是实现缺陷处理工作流的核心手段，默认包含 6 个状态：待处理、处理中、待验证、已拒绝、重新打开、已关闭。

1.  在缺陷列表页**创建缺陷**后，进入该缺陷详情页，缺陷状态默认为**待处理**，可在右侧下拉菜单中手动切换状态。
![](https://qcloudimg.tencent-cloud.cn/raw/c171d366e19dd6f3a77e0a5fce1af6af.jpeg)
2.  在缺陷列表页，可以在**状态**栏中，根据缺陷进行的阶段切换缺陷状态。
![](https://qcloudimg.tencent-cloud.cn/raw/5bf56200f55ddb3dd99f273c839d065b.png)
3.  在**项目设置** > **项目协同** > **事项类型** > **缺陷**末端的**工作流**中，可自定义缺陷工作流，详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。


## 缺陷视图[](#view)

在缺陷列表页，可以根据使用习惯，在右上角**平铺视图**、**看板视图**中切换视图模式，系统将默认记住上次使用的视图模式，下次使用时将应用相同的视图模式。可以配合使用搜索框与筛选器，快速筛选出需要的内容。详细操作及管理请参见 [事项视图管理](https://intl.cloud.tencent.com/document/product/1133/44773)。
![](https://qcloudimg.tencent-cloud.cn/raw/fdefd232885fc415bf8ca094bfb734c9.png)

## 版本回溯[](#backdate)

缺陷的变更与修改都会记录在活动日志中，可以通过**查看该版本**按时间查看所有历史版本。支持版本回溯，可以选择任意历史版本进行恢复，详情请参见 [版本管理](https://intl.cloud.tencent.com/document/product/1133/44771)。
![](https://qcloudimg.tencent-cloud.cn/raw/5341a44ac5ca9416cd65ce50f458756f.jpeg)

## 缺陷类型与缺陷模块[](#type&module)

### 管理缺陷类型[](#type)

在创建缺陷以及进行缺陷管理操作时，可以设置缺陷的所属类型。
>?CODING 缺陷管理默认提供了五种缺陷类型：
-   功能缺陷
-   UI 界面问题
-   易用性问题
-   安全问题
-   性能问题


也可以根据团队需求自定义缺陷类型，仅**团队所有者**及**管理员**可创建缺陷类型。缺陷类型添加成功后，团队内所有项目均可选用该缺陷类型。

#### 创建/使用缺陷类型[](#type-create)

1.  在任一项目内，在左侧菜单**项目设置** > **项目协同** > **事项类型**中，选择**缺陷**末端的**属性**菜单。
![](https://qcloudimg.tencent-cloud.cn/raw/ca5f4ecacc56884277f67cc62908ec80.jpeg)
2.  进入**事项类型/缺陷**后，选择**缺陷类型**末端的**配置菜单选项**。
![](https://qcloudimg.tencent-cloud.cn/raw/2564d169c5be55908ede95f9d309420b.png)
3.  输入新增缺陷类型名称，可上下拖拽调整各缺陷类型优先级，**添加**并**确定**.
![](https://qcloudimg.tencent-cloud.cn/raw/cea65867443d3d5258e16dd1633278ac.jpeg)
然后在**事项类型/缺陷**中选择**应用配置**，即可完成缺陷类型的添加并生效。
![](https://qcloudimg.tencent-cloud.cn/raw/2564d169c5be55908ede95f9d309420b.png)
4.  创建缺陷时或在缺陷详情页，通过右侧**缺陷类型**菜单即可选择新增缺陷类型。
![](https://qcloudimg.tencent-cloud.cn/raw/264e8e580e7f5ed68bb474afd61d9810.png)

### 管理缺陷模块[](#module)

该功能主要用于配置缺陷所属模块，创建不同的模块可便于管理和定位缺陷位置，满足专业化场景需要，且模块数据在项目内共享，协作更为高效。

#### 创建或使用缺陷模块[](#module-create)

1.  在任一项目内，在左侧菜单**项目设置** > **项目协同** > **模块设置**页面中，单击**创建模块**。
![](https://qcloudimg.tencent-cloud.cn/raw/68e3cbfd7b91caf525b7837f9a64b886.jpeg)
2.  输入模块名称，选择**保存**即可完成缺陷模块添加。
![](https://qcloudimg.tencent-cloud.cn/raw/2db501d7dbd9a57557226dd6ca8aafbe.jpeg)
可在**模块设置**中的各模块末端，通过**↑****↓**调整多个模块的显示优先级，并进行模块重命名、删除操作。
![](https://qcloudimg.tencent-cloud.cn/raw/66cbebccefabeeec09630409c58f1e3b.jpeg)
3.  创建缺陷时或在缺陷详情页，通过右侧**模块**菜单即可将缺陷规划入。
![](https://qcloudimg.tencent-cloud.cn/raw/afdf44ab4f2380d661846881778f2adc.jpeg)

## 删除缺陷[](#delete)

在缺陷详情页内，通过右上方**`···`**内的**删除**，即可删除缺陷。
![](https://qcloudimg.tencent-cloud.cn/raw/4ddb8960be8d0ca1a83e63d2b8572a9d.jpeg)
