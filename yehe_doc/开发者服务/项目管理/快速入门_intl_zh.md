本文档主要介绍如何快速使用 CODING 项目管理中的经典模式。

## 前提条件
使用 CODING 项目管理的前提是，您的腾讯云账号需要开通 CODING DevOps 服务。

## 初始化教学项目

1. 进入 CODING 页面，单击页面左边的<img src ="https://main.qcloudimg.com/raw/7531b01c25014beb2754277107fc4ab1.png" style ="margin:0">项目按钮，单击项目列表内右上角的创建项目按钮。
2. 选择从教学项目开始。
3. 单击经典项目管理教学项目。
4. 填写项目名称与标识，完成创建。

下文将以一个虚拟商城——飞鸟市集作为举例场景，说明团队如何使用经典项目管理模式进行协作。

## 创建需求

要想在竞争红海的电商领域立足，离不开详尽的潜在用户群体调研。通常情况下，产品经理会根据市场痛点或用户反馈形成产品的需求文档。此时，在**需求**功能页就可以进行需求创建，支持上传附件或引入外部资源（墨刀原型），任何时候的灵感闪现都可以方便地融入团队协同中。需求详情页右侧菜单还支持调整需求优先级、需求类型与截止日期。若对该需求的工作时间有所要求，还可以填写预估工时与项目进度。
![](https://qcloudimg.tencent-cloud.cn/raw/062d694a977e77fca3616bd9f2d062c7.png)

##  协调开发计划

需求调研结束后通常是需求池评审会，在对收集的需求进行统一讨论与评审后，项目 Leader 批准开发计划，自此衍生出的开发排期计划都可以使用**迭代**作为承载单元。
![](https://qcloudimg.tencent-cloud.cn/raw/abad38e9eeed7832a8435c829554fb18.png)

该功能可以将较为大型的计划（包括但不限于开发计划）拆分成具体的事项（如需求、任务）并落实至具体的责任人，产品经理前期编写的各项需求也可以无缝融入迭代计划中。
![](https://qcloudimg.tencent-cloud.cn/raw/1da18253b4a1aa21eeac998e7633d9fa.png)

需求可以分解为子需求或子任务，还支持关联缺陷和测试用例、设置执行本需求所需要的其他资源为前置事项、查看是否受其他事项进度影响造成阻塞关系、将其他需求或任务引用为本事项的资源，或查看本事项已被其他哪些资源引用。
![](https://qcloudimg.tencent-cloud.cn/raw/2a957ffef62115a1c4c8e7c08303f575.png)

##  分配开发任务
![](https://qcloudimg.tencent-cloud.cn/raw/bcc04eff059fb53133f10bb851888ee3.png)

在一个迭代计划中，通过创建事项或接受他人的事项指派进行协作，团队成员能够各司其职。譬如**客服入口**的上线需求，就可以分解为开发任务和测试任务，待开发完成后，还能够继续分解为推广任务并交由运营部门开展功能点营销活动。
![](https://qcloudimg.tencent-cloud.cn/raw/542aa1b6f31dad66b83fe50428a2d1dc.png)

##  执行计划

待各项计划制订完成并分发至具体的执行人后，团队内成员都可以在团队首页的**工作台** > **我的事项**中清晰看到待完成的事项、由本人发起的合并请求或待检视的合并请求、持续集成中的构建任务、待确认的持续部署发布单。
![](https://qcloudimg.tencent-cloud.cn/raw/9b704822cc2a36319ee3cb5b9b2f4cad.png)

开发任务还支持直接引用代码仓库中的合并请求记录，详情请参见 [引用资源和上传附件](https://intl.cloud.tencent.com/document/product/1133/44770)。关联完成后在开发任务中，就可以看到代码的提交记录与编写情况。
![](https://qcloudimg.tencent-cloud.cn/raw/b573b8d04198ede076b6d87c53846c18.png)

在事项详情页右侧菜单中，可以登记工时，通过填写事项预估工时和使用工时（已经工作的时间），能够自动形成完整的工时记录，有助于迭代完成后的复盘与效率分析。
![](https://qcloudimg.tencent-cloud.cn/raw/c71d0c3a21eb3a7b5a3b76d3845286f5.png)

在完成每天的开发后，除了将状态变更为**已完成**，还可以填写开发进度百分比，整体迭代的进度将会随着各个事项的进度推进情况而增长。
![](https://qcloudimg.tencent-cloud.cn/raw/5feaca843d458dcc0a7007a737508492.png)

##  测试环节

开发任务的闭环关键离不开全面的测试环节。虽然开发人员的自测通常可以解决大部分常见问题，但仅仅依靠个人自觉是不够的。测试有助于尽早暴露开发过程中的基础执行逻辑问题与可能的缺失项。CODING 内置的代码扫描、制品扫描等自动化测试工具，可以帮助测试人员发现 Bug 后，快速在迭代中新建缺陷并与需求或任务相关联。
![](https://qcloudimg.tencent-cloud.cn/raw/bdf75c06002a626a80cb7597d2161f7b.png)

修复缺陷的过程中同样支持登记工时与填写进度百分比。除了在事项中进行测试任务的分配与填写，测试人员还可以前往**测试管理** > **用例管理**编写测试用例。
![](https://qcloudimg.tencent-cloud.cn/raw/a043615a2fbfb19e4034f0fee5ce13ab.png)

在**测试管理** > **测试计划**的**编辑**选项中，能够设置测试所属迭代。


##  项目上线

基础开发任务完成后，通过 CODING 的持续集成/持续部署等服务，能让代码的有效性快速被验证。
<dx-alert infotype="explain" title="扩展阅读">
<ul style = "margin-bottom: 0px;">
<li><a href = "https://help.coding.net/docs/ci/start.html">持续集成——快速开始</a></li>
<li><a href = "https://help.coding.net/docs/cd/start.html">持续部署——示例项目实践</a></li>
</ul>
</dx-alert>

各项迭代计划结束后，进入任意迭代，在**概览与统计**中可以查看该迭代周期的状态趋势与工时燃尽图，管理者能够随时掌握团队在该计划下的工作进度。
![](https://qcloudimg.tencent-cloud.cn/raw/2f69e2cbcb88e52454ea10d1cd7a556b.png)

##  自定义团队工作流

事项的完成状态与流程状态并非仅有默认选项，可在**项目设置** > **项目协同** > **事项类型**中，各事项末端的**工作流**内自定义各事项的工作流，详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。
