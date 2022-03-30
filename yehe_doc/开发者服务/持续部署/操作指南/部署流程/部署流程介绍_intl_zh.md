本文为您详细介绍 CODING 持续部署中的部署流程。

## 前提条件

使用 CODING 项目管理的前提是，您的腾讯云账号需要开通 CODING DevOps 服务。 

## 进入项目

1. 登录 CODING 控制台，单击**立即使用**进入 CODING 使用页面。
2. 单击工作台首页左侧的 <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" style ="margin:0" data-nonescope="true">，进入持续部署控制台。

## 功能介绍

部署流程是实现持续部署最核心的模块。其强大之处在于支持阶段以任意的顺序组合，这样的能力让部署流程具备出色的灵活性、一致性和可重复性。

- 灵活性：支持串行、并行控制
- 一致性：支持多种部署策略，回滚能力，确保发布结果符合预期
- 可重复性：部署流程可重复执行，阶段可被其他部署流程复制使用

您可以配置完全自动化的部署流程，也可以在某些阶段加入手工判断条件。此外部署流程支持多种事件的自动化触发，如 Webhook 触发、由其他部署流程触发等。

## 新建部署流程

前往部署控制台，单击应用卡片右下方的部署流程按钮。

![](https://qcloudimg.tencent-cloud.cn/raw/4ddc682c3bcebda9daf23b87b057476e.png)

1. 单击右上角的**创建流程**按钮。
![](https://qcloudimg.tencent-cloud.cn/raw/dc51fd45991ee1a255dcb4017a91b373.png)
2. 您可以复制在其他应用中创建的流程，或通过空白流程自行创建。CODING 亦提供了 Kubernetes 与腾讯云弹性伸缩参考流程模板。
![](https://qcloudimg.tencent-cloud.cn/raw/7aa628a2fa00ed118aae1b2de5ed4588.png)

## 基础配置

应用的基础配置可以理解为构建整体的初始环节，既可以设置触发条件，也可以配置部署流程的通知方式等。

![](https://qcloudimg.tencent-cloud.cn/raw/43536778c6cd104bfaacd1f8115c368c.png)

### 自动触发器

自动触发器支持 CODING Docker 制品仓库、TCR 个人版仓库触发器、Git 仓库触发器等触发条件。

![](https://qcloudimg.tencent-cloud.cn/raw/f2e5d1bbde7eb62274cf92ec8e23c4cc.png)

### 添加部署流程参数

在部署流程配置页面，单击**添加启动参数**，即可开始填写参数。

![](https://qcloudimg.tencent-cloud.cn/raw/dccb548c5afdac2960d010b9c1b21e73.png)

### 添加阶段

在部署流程配置页面单击**+**即可添加新的阶段，右侧列表中支持选择阶段类型。
![](https://qcloudimg.tencent-cloud.cn/raw/e6a1bf1defe6883427188d19368c53e5.png)

## 执行部署流程

部署流程配置完成后，您可以通过设置好的触发器以提交自动执行，或在持续部署中提交发布单手动触发部署流程。

![](https://qcloudimg.tencent-cloud.cn/raw/b4de188f629b5e3438454fc3ea2a3470.png)

## 部署流程配置

部署流程支持删除、禁用、锁定、查看历史版本与编辑 JSON 配置。

![](https://qcloudimg.tencent-cloud.cn/raw/d08efa52feae739abd7ba8269bcb6acd.png)

### 删除部署流程

设置后，将删除此部署流程。

### 禁用部署流程

设置后，将禁止任意触发器启动部署流程，包括手动触发。可以选择在团队内整体禁用或仅在项目内禁用。

![](https://qcloudimg.tencent-cloud.cn/raw/7e33280a84311cf5ce2ec0fe020edcdd.png)

### 锁定部署流程

锁定部署流程后，将不能通过部署控制台编辑部署流程。可以选择是否允许通过 API 接口对部署流程进行更新。

![](https://qcloudimg.tencent-cloud.cn/raw/d3fb49d5bd092eaaebf83996c82516ce.png)

### 查看修订历史

保存新的部署流程配置后，旧版本将会添加到修订历史。您可以在修订历史页对比各版本信息，选择并还原到任意历史版本。
![](https://qcloudimg.tencent-cloud.cn/raw/a7912b8d24d038cf4e109ddcd5dadb84.png)

### 编辑 JSON 配置

在部署控制台中所做的任何更改最终都会以 JSON 格式文件保存，直接编辑部署流程的 JSON 内容可以为部署流程添加新属性或自定义 UI 界面尚未显示的配置项。

>! 此种方式允许用户将在文本框内自由编辑部署流程，但有可能会破坏部署流程的可用性，我们提供了从修订历史中恢复到任意指定版本的能力。

![](https://qcloudimg.tencent-cloud.cn/raw/b67161f563142b0efb95153ee2d9feb3.png)
