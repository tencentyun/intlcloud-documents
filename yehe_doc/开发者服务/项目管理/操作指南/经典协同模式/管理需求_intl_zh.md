本文为您介绍经典项目管理模式下的需求功能。

## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏中的**项目协同**功能页。

需求是指用户解决某一问题或达到某一目标所需的软件功能，决定了软件研发的方向与结果。团队可以通过 CODING 经典项目管理中的**需求**模块，创建并将较大粒度的需求分解为较小的子需求，并在需求下新建或关联任务、缺陷，实现开发任务的快速分解和分配。

## 创建需求[](#create)

1.  进入任一项目后，在**项目协同** > **需求**页面，单击模块右上方**创建需求**，填写需求标题、需求描述等基本信息后即可完成创建。
![](https://qcloudimg.tencent-cloud.cn/raw/37d35d77d24623c1dcd580a25768c81b.png)
2.  创建完成后，可以进行设置处理人、规划所属迭代、调整优先级、设置起始日期等详细操作，支持团队根据管理习惯，对需求的属性维度自定义，具体设置请参见 [自定义事项属性](https://intl.cloud.tencent.com/document/product/1133/447671)。
![](https://qcloudimg.tencent-cloud.cn/raw/15cbb620735f11cb21fd104f6674804c.png)

## 需求分解[](#decompose)

子工作项（子需求、子任务）是为实现需求所进行的具体活动，通过在需求下创建子工作项可实现对需求的分解和分配。

### 分解子需求[](#sub-requirement)

需求可分解子需求，子需求内又可继续分解，最多支持 5 层子需求。请注意，一个需求同时只能属于一个父需求。

1.  在需求详情页选择**分解需求**。
![](https://qcloudimg.tencent-cloud.cn/raw/30ec16abb81505d53132062a38582bdb.png)
2.  可以仅输入子需求标题快速创建，也可以在**创建**下拉菜单中选择**完整创建**（快捷键：shift + 回车），填写子需求详情后完成创建。
![](https://qcloudimg.tencent-cloud.cn/raw/ac8d584e2e37f91af514508d5dfd048b.jpeg)
也可以关联已有需求，输入事项 ID 或标题即可快速查找。
![](https://qcloudimg.tencent-cloud.cn/raw/28f7055407322085129da278b59723ec.png)
3.  子需求项创建成功后，可以在父需求详情页中查看，也可以在需求列表页查看该子需求。
![](https://qcloudimg.tencent-cloud.cn/raw/8edc5948c5a740f80c2b828cc50cb36a.png)
4.  在需求详情页内，通过指定子需求后方**`···`**菜单内**创建子需求**。
![](https://qcloudimg.tencent-cloud.cn/raw/193b925134dafa101e32b7625e4e097d.png)
或在子需求详情页内，通过上方的**分解需求**，均可创建该子需求的子需求。
![](https://qcloudimg.tencent-cloud.cn/raw/f4c8bd51ebaa380b6ddf7340cab9592c.png)
5.  在需求详情页内，通过指定子需求后方**`···`**菜单内的选项，可以更改关联的父需求。也可以与当前父需求解除关联。


### 分解子任务[](#sub-tasks)

需求可分解子任务，一个任务只能同时关联一个父需求。

1.  在需求详情页选择**分解任务**。
![](https://qcloudimg.tencent-cloud.cn/raw/db06d35ef28709b21c062247e7ee6e18.png)
2.  可以仅输入子任务标题快速创建，也可以在**创建**下拉菜单中选择**完整创建**（快捷键：shift + 回车），填写子任务详情后完成创建；也可以关联已有任务，输入事项 ID 或标题即可快速查找。
![](https://qcloudimg.tencent-cloud.cn/raw/ddf61566e193f1149bc6f95f84606489.png)
3.  子任务项创建成功后，可以在父需求详情页中查看，也可以在任务列表页查看该子任务。
![](https://qcloudimg.tencent-cloud.cn/raw/05f105c097bd5f6cae2cb19e7988095c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/68ed0cd14f7c96a080934d7e51c03c1d.png)
4.  在需求详情页内，通过指定子任务后方**`···`**菜单内的选项，可以更改关联的父需求，也可以与当前父需求解除关联。


## 关联资源[](#resource)

### 关联缺陷[](#bugs)

需求可以关联相同项目内的多个缺陷，但一个缺陷只能关联一个需求。

1.  在需求列表页，通过上方**关联缺陷**选项，可以关联已有缺陷，或者快速创建新的缺陷与之关联。
![](https://qcloudimg.tencent-cloud.cn/raw/663efe34a0cb5bcd981b9d2c13ca4461.png)
2.  在需求详情页，可以通过关联缺陷右侧**`···`**菜单**取消关联**；同时在缺陷详情页右侧菜单内。
![](https://qcloudimg.tencent-cloud.cn/raw/5f24f2285b544f8e5653356602a4ef7a.png)
也可以查看当前关联的需求，并解除或切换关联。
![](https://qcloudimg.tencent-cloud.cn/raw/6026ca6ffb9a73d4d6e61c3d6ab47caf.png)
3.  在缺陷详情页内，通过右上方**`···`**，可将该缺陷转为新需求。
![](https://qcloudimg.tencent-cloud.cn/raw/a18e1cdf218fed6698752e0600cf25f2.png)

### 关联测试用例[](#cases)

需求可以关联已有测试用例。在需求详情页内，通过上方**`···`**菜单内的**关联测试用例**，输入测试用例 ID 或标题，即可查找并完成关联。关于测试用例的创建与管理，请参见 [测试用例](https://help.coding.net/docs/test-management/cases/create.html)。
![](https://qcloudimg.tencent-cloud.cn/raw/89a3caf9ab5c34da739bd45f5abf5bc7.png)

### 关联阻塞关系[](#blocking)

需求内可以设置已有事项为前置/后置阻塞事项。在需求详情页内，通过上方**`···`**菜单内的**阻塞关系**，输入事项 ID 或标题，即可查找并完成关联。可在**前置/后置事项**中切换。关于阻塞关系的详细讲解，请参见 [阻塞关系](https://intl.cloud.tencent.com/document/product/1133/44750)。
![](https://qcloudimg.tencent-cloud.cn/raw/08b9f74bfa111fa46807b99054376352.png)

### 引用资源[](#references)

在需求详情页的描述或评论中，可通过 `# + 引用 ID/标题` 形式选择资源，引用的资源将会在引用列表中展示；如果当前需求被其他资源引用，那么其他资源将会显示在该需求的被引用列表中。
![](https://qcloudimg.tencent-cloud.cn/raw/ffefaa4fb1a94dfcd4e0720907e7d0bd.png)

还支持将**代码提交**与事项进行关联，可以在代码执行提交时，在提交信息中插入关联事项 `# + 引用 ID/标题` 信息（例如：这是一次提交 #3）。详情请参见 [引用资源和上传附件](https://intl.cloud.tencent.com/document/product/1133/44770)。


## 需求状态流转[](#status)

需求状态是指需求在生命周期中所处的阶段，用于组织和跟踪需求，默认包含 4 个状态：未开始、开发中、测试中、已完成。

1.  在需求列表页**创建需求**后，进入该需求详情页，需求状态默认为**未开始**，可在右侧下拉菜单中手动切换状态。
![](https://qcloudimg.tencent-cloud.cn/raw/9b8342732e5a86a9eacff10bea25c4dc.png)
2.  在需求列表页，可以在**状态**栏中，根据需求进行的阶段切换需求状态。
![](https://qcloudimg.tencent-cloud.cn/raw/c420d169cdf3e3e7151258bc70b7f09e.png)
3.  在**项目设置** > **项目协同** > **事项类型** > **需求**末端的**工作流**页面中，可自定义需求工作流，详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。
![](https://qcloudimg.tencent-cloud.cn/raw/cae1423bed3f408d893cbfac1720e474.png)

## 需求视图[](#view)

在需求列表页，可以根据使用习惯，在**树状视图**、**平铺视图**、**看板视图**中无缝切换视图模式，这是产品相关人员的主要工作界面，可以帮助您对目前项目内的所有需求建立全局概念。系统将默认记住上次使用的视图模式，下次使用时将应用相同的视图模式。

当存在大量需求时，配合使用搜索框与筛选器，便可以在繁杂的信息中快速筛选出需要的内容。具体操作及管理请参见 [事项视图管理](https://intl.cloud.tencent.com/document/product/1133/44773)。
![](https://qcloudimg.tencent-cloud.cn/raw/84ba59211d8d9f0ce3a6097cd2416bf9.png)

## 版本回溯[](#backdate)

需求内所有变更都会记录在活动日志中，可以通过详情页内右上方**`···`**菜单内的**历史版本**按时间顺序查看所有版本。支持版本回溯，可以选择任意历史版本进行恢复，详情请参见 [版本管理](https://intl.cloud.tencent.com/document/product/1133/44771)。
![](https://qcloudimg.tencent-cloud.cn/raw/e6f5e508b06419a412b22594c5fff570.png)

## 导入和导出需求[](#import)

需求支持批量导入和导出，可在需求列表页右上角**`···`**菜单中导入/导出需求，具体操作请参见 [导入和导出事项](https://intl.cloud.tencent.com/document/product/1133/44765)。
![](https://qcloudimg.tencent-cloud.cn/raw/d3929d1e93afe61e75bfccb664b4e048.png)

## 删除需求[](#delete)

在需求详情页内，可以通过右上方**`···`**菜单进行**删除**操作。如果含有子工作项（子需求、子任务），将全部删除，但不会影响所关联缺陷的状态，请谨慎操作。
![](https://qcloudimg.tencent-cloud.cn/raw/8ddb79041b3322602ddbe3e752506ec1.png)
如仅需删除子需求/子任务/缺陷，可在需求详情页或子需求/子任务/缺陷详情页内，通过**`···`**菜单进行**删除**操作。
