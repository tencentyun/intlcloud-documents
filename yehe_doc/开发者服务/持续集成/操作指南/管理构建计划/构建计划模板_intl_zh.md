---
title: 构建计划模板 - CODING 帮助中心
pageTitle: 构建计划模板
pagePrevTitle: 分组管理
pagePrev: ci/manage/group.html
pageNextTitle: 上传 Generic 制品
pageNext: ci/plugins/generic.html
alias: 
-   ci/node/overview.html
-   ci/team-template.html
---

### [功能介绍](#intro)

CODING 持续集成支持编制统一的**构建计划模板**。一次配置，就能在团队内的跨项目协作中复用统一而规范的构建计划模板，优化团队成员配置构建流程的效率，集中管理团队中通用的构建计划。

### [新建构建计划模板](#new)

点击团队首页右上角的齿轮图标 <img src ="https://help-assets.codehub.cn/enterprise/20210928153255.png" style ="margin:0"> 进入团队设置中心，你可以在「功能设置」→「构建计划模板」中新建团队构建模板。

![](https://qcloudimg.tencent-cloud.cn/raw/cdb2aa9960ca23fd3be79a16805c8157.png)

### [编辑构建计划模板](#edit)

在模板内能够编辑流程配置、基础配置、触发规则以及变量与缓存。

#### [流程配置](#process)

您可以使用「图形化编辑器」或「文本编辑器」编写该构建模板的执行流程。图形化编辑器的优势在于能够获得边看边写的可视化体验，在图形化编辑器中增删的所有步骤都可以转换成文本，但反之则不一定能够兼容。

![](https://qcloudimg.tencent-cloud.cn/raw/0c3bb006a4c2a797d1f3bcb8274c5c2a.png)

#### [基础配置](#basic)

在基础配置页能够更改模板名称、图标。点击右侧的操作下拉菜单能够执行删除模板或[同步模板](#sync)。

![](https://qcloudimg.tencent-cloud.cn/raw/bd43b35f8a4c44e89038fee4327fe14d.png)

当模板有更新时，模板作者可以通过[「同步模板」](#sync)操作将更新同步至所有使用该模板创建的构建计划。该操作将覆盖对应构建计划的配置，点击查看[场景举例](#sync)。

#### [触发规则](#trigger)

支持代码源触发、定时触发及手动触发。与普通构建计划下的触发规则设置方式一致，具体说明请参考[《触发规则》](https://intl.cloud.tencent.com/document/product/1135/45430)。

#### [变量与缓存](#variable)

您可以在此处添加构建计划的环境变量。在手动启动构建任务时，环境变量也将作为启动参数的默认值，具体配置说明请参考[《环境变量》](/docs/ci/env.html)。

### [使用构建计划模板](#using)

模板作者完成团队构建模板的编写后，其他团队成员就可以在任一项目中使用该构建计划模板。

![](https://qcloudimg.tencent-cloud.cn/raw/f80296b00fccf0f0b7c1dc947158fbf3.png)

构建计划左上角处会标注为构建计划模板，使用者可以按照项目需求选择不同的代码源。

![](https://qcloudimg.tencent-cloud.cn/raw/ad7c4bfb3e4cd2d142d9c1f3f0d6e429.png)

创建成功后，构建计划流程、触发配置、环境变量及默认值与模版保持一致，使用者可以按照项目的实际情况进行修改。基于模板做出的不会影响模板内容，如需修改模板请前往设置中心的【功能设置】>【构建计划模板】处进行更新。

### [同步构建计划模板](#sync)

当团队内部使用了某项构建计划模板作为其他构建计划的基石时，修改构建计划模板后使用同步功能，就能够让其他构建计划向构建计划模板对齐。

**使用场景举例**：A 团队已在内部全面推行持续集成构建规范，大部分构建计划皆是基于某一规范性构建计划模板进行编写。随着项目推进，旧有规范亟待更新，此时模板作者仅需完成构建计划模板的更新并使用同步功能，就能让其他构建计划与模板进行对齐。

![](https://qcloudimg.tencent-cloud.cn/raw/bb3f08a7ac75fb25946485fd4b455176.png)

同步功能并不会覆盖其他构建计划中的所有内容，下图为同步所导致的「变更」效果图：

![](https://qcloudimg.tencent-cloud.cn/raw/8f044ebaf0f69fceca8a410bbfed01d2.png)

> ⚠️ 使用同步功能前请确保已知晓该操作可能会造成的影响。

==== 2020/11/27 ====
