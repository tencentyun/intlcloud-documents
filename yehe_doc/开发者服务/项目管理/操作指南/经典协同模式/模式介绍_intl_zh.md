本文为您介绍 CODING 项目协同中的经典项目管理模式。

## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏中的**项目协同**功能页。

## 功能介绍

经典项目管理是相对于 Scrum 敏捷项目管理而言的概念，主要适用于使用传统项目管理方式的团队。传统项目管理的特点是强计划驱动，围绕着需求、资源和时间展开，需求固定下来后才可分配人员和时间，并在项目推进过程中积极跟踪和控制风险。

CODING **经典项目管理**旨在解决传统项目管理的五大难题：

**统一协同**，不同阶段、职能信息在同一个平台汇总；
**全局视图**，计划页汇总项目进度，实时掌握多个迭代的进展与情况；
**项目进度**，计划、迭代概览等页面跟踪进度，过程透明、进度可控；
**资源管理**，计划页可随时查看成员任务、分配和协调人员；
**质量管控**，通过测试管理、缺陷管理等随时跟踪测试进度和缺陷修复进度。

![](https://qcloudimg.tencent-cloud.cn/raw/db202780d6325804c2dbc0b8271e10eb.png)

下文将以一个虚拟商城——飞鸟市集作为举例场景，说明团队如何使用经典项目管理模式进行协作。

### 开启经典项目管理模式[](#start)

在首次启用项目协同功能时，请选择**经典项目管理**模式。
![](https://qcloudimg.tencent-cloud.cn/raw/4ce14c1b568e9140e4c27cf0d7715f7f.jpeg)

### 创建需求[](#create)

要想在竞争红海的电商领域立足，离不开详尽的潜在用户群体调研。通常情况下，产品经理会根据市场痛点或用户反馈形成产品的需求文档。此时，在**需求**功能页就可以进行需求创建，支持上传附件或引入外部资源（墨刀原型），任何时候的灵感闪现都可以方便地融入团队协同中。需求详情页右侧菜单还支持调整需求优先级、需求类型与截止日期。若对该需求的工作时间有所要求，还可以填写预估工时与项目进度。
![](https://qcloudimg.tencent-cloud.cn/raw/9db3e2c62316527a0c6914261e83952e.png)

### 协调开发计划[](#coordinate)

需求调研结束后通常是需求池评审会，在对收集的需求进行统一讨论与评审后，项目 Leader 批准开发计划，自此衍生出的开发排期计划都可以使用**迭代**作为承载单元。
![](https://qcloudimg.tencent-cloud.cn/raw/25e49b3ec650ba29e33d137ba34e1842.png)

该功能可以将较为大型的计划（包括但不限于开发计划）拆分成具体的事项（如需求、任务）并落实至具体的责任人，产品经理前期编写的各项需求也可以无缝融入迭代计划中。
![](https://qcloudimg.tencent-cloud.cn/raw/fc1e72752621604f76037e375d187c75.png)

需求可以分解为子需求或子任务，还支持关联缺陷和测试用例、设置执行本需求所需要的其他资源为前置事项、查看是否受其他事项进度影响造成阻塞关系、将其他需求或任务引用为本事项的资源，或查看本事项已被其他哪些资源引用。
![](https://qcloudimg.tencent-cloud.cn/raw/8b6cfa6052f601540b9291d10d9fa442.png)

### 分配开发任务[](#allocate)
![](https://qcloudimg.tencent-cloud.cn/raw/262a26c0d7e68a094e1fece88dcff845.png)

在一个迭代计划中，通过创建事项或接受他人的事项指派进行协作，团队成员能够各司其职。譬如**客服入口**的上线需求，就可以分解为开发任务和测试任务，待开发完成后，还能够继续分解为推广任务并交由运营部门开展功能点营销活动。
![](https://qcloudimg.tencent-cloud.cn/raw/ac512ef190952d5d80cff65440d99ef3.png)

### 执行计划[](#execution)

待各项计划制订完成并分发至具体的执行人后，团队内成员都可以在团队首页的**工作台** > **我的事项**中清晰看到待完成的事项、由本人发起的合并请求或待检视的合并请求、持续集成中的构建任务、待确认的持续部署发布单。
![](https://qcloudimg.tencent-cloud.cn/raw/91f0bb56758bd47d112f10271d274ab9.png)

开发任务还支持直接引用代码仓库中的合并请求记录，详情请参见 [引用资源和上传附件](https://intl.cloud.tencent.com/document/product/1133/44770)。关联完成后在开发任务中，就可以看到代码的提交记录与编写情况。
![](https://qcloudimg.tencent-cloud.cn/raw/5867eb177e95944e3053c5d312d5fb82.png)

在事项详情页右侧菜单中，可以登记工时，通过填写事项预估工时和使用工时（已经工作的时间），能够自动形成完整的工时记录，有助于迭代完成后的复盘与效率分析。
![](https://qcloudimg.tencent-cloud.cn/raw/64cadcfc3d927cfb3c633fbed494093b.png)

在完成每天的开发后，除了将状态变更为**已完成**，还可以填写开发进度百分比，整体迭代的进度将会随着各个事项的进度推进情况而增长。
![](https://qcloudimg.tencent-cloud.cn/raw/3985e0590da44d207a274f611aa0c9e2.png)

### 测试环节[](#test)

开发任务的闭环关键离不开全面的测试环节。虽然开发人员的自测通常可以解决大部分常见问题，但仅仅依靠个人自觉是不够的。测试有助于尽早暴露开发过程中的基础执行逻辑问题与可能的缺失项。CODING 内置的代码扫描、制品扫描等自动化测试工具，可以帮助测试人员发现 Bug 后，快速在迭代中新建缺陷并与需求或任务相关联。
![](https://qcloudimg.tencent-cloud.cn/raw/e92fc22b75d4a369948f124303cfe420.png)

修复缺陷的过程中同样支持登记工时与填写进度百分比。除了在事项中进行测试任务的分配与填写，测试人员还可以前往[**测试管理**](https://help.coding.net/docs/test-management/start.html) > **用例管理**编写测试用例。
![](https://qcloudimg.tencent-cloud.cn/raw/ab767bad626a5d3855db81c8839f47c0.png)

在**测试管理** > **测试计划**的**编辑**选项中，能够设置测试所属迭代。


### 项目上线[](#launched)

基础开发任务完成后，通过 CODING 的持续集成/持续部署等服务，能让代码的有效性快速被验证。
<dx-alert infotype="explain" title="扩展阅读"><ul style = "margin-bottom: 0px;">
<li><a href = "https://help.coding.net/docs/ci/start.html">持续集成——快速开始</a></li>
<li><a href = "https://help.coding.net/docs/cd/start.html">持续部署——示例项目实践</a></li></ul>
</dx-alert>
各项迭代计划结束后，进入任意迭代，在**概览与统计**中可以查看该迭代周期的状态趋势与工时燃尽图，管理者能够随时掌握团队在该计划下的工作进度。
<img src = "https://qcloudimg.tencent-cloud.cn/raw/ed799f3ac918f09fdd263000ed53f6c9.png" style="width: 100%">


### 自定义团队工作流[](#customize-workflow)

事项的完成状态与流程状态并非仅有默认选项，可在**项目设置** > **项目协同** > **事项类型**中，各事项末端的**工作流**内自定义各事项的工作流，详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。
