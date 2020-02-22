## 快速开始
本文介绍如何使用批量计算控制台提交一个作业，具体操作步骤如下。
### 准备
准备好 [对象存储](https://intl.cloud.tencent.com/document/product/436) 存储桶。如果您尚未创建存储桶，请参照 [创建存储桶](https://cloud.tencent.com/document/product/436/13309) 完成创建。

### 登录 [控制台](https://console.cloud.tencent.com/batch/task)
如果您尚未开通批量计算服务，请参照批量计算控制台主页相关提示开通。

### 创建任务模板

1. 单击左侧导航栏“任务模板”选项，选择目标地域，例如“广州”。单击【新建】按钮。

2. 配置基本信息。
  * 名称：如 hello
  * 描述：如 hello demo
  * 资源配置：默认值
  * 资源数量：如1台
  * 超时时间：默认值
  * 重试次数：默认值
  * 镜像：img-m4q71qnf
![](https://main.qcloudimg.com/raw/5eaf007532cdb04dc9f359e24a2f6922.png)

3. 配置程序信息。
  * 执行方式：Local
  * Stdout 日志：格式参考 [COS、CFS路径填写](https://cloud.tencent.com/document/product/599/13996)
  * Stderr 日志：同 Stdout 日志
  * 命令行：echo 'hello, world'
![](https://main.qcloudimg.com/raw/df04fd8aa361eff74796d40bb7d85171.png)

4. 配置存储映射，完成后单击【下一步】按钮。
   ![](https://main.qcloudimg.com/raw/a9f02dff4b5f84a7253a5b940c5f6e2d.png)

5. 预览任务 JSON 文件，确认无误后，单击【保存】按钮。
  ![](https://main.qcloudimg.com/raw/fe380f3cb4e60cd405f623ab70677461.png)

6. 查看任务模板。
  ![](https://main.qcloudimg.com/raw/56ba751132050eefd71a451cd24aca00.png)

### 提交作业
1. 单击左侧导航栏“作业”选项，选择目标地域，例如“广州”。点【新建】按钮。

2. 配置作业基本信息。
  * 作业名称：如 hello
  * 优先级：默认值
  * 描述：如 hello job
  ![](https://main.qcloudimg.com/raw/7aac41e3f597d348daf9aadb2d4f0dd2.png)

3. 选中“任务流”左侧 “hello” 任务，移动鼠标将任务放置到右侧画布中。
  ![](https://main.qcloudimg.com/raw/023f92bcda936696fd0434eeac1c0765.png)

4. 打开“任务流”右侧“任务详情”，确认配置无误后，单击“完成”按钮。
![](https://main.qcloudimg.com/raw/b592938fa04583d04943db6f3047e93d.png)

5. 查询结果。您可以在作业列表页查看作业的运行状态。
  ![](https://main.qcloudimg.com/raw/018544b3a1f84fd3e32c141c880b007f.png)
 - 单击作业ID，在“任务运行情况”下可以看到各个任务实例的运行状态
 - 单击“查询日志”按钮，可以查看任务实例的标准输出和标准错误。

  ![](https://main.qcloudimg.com/raw/3f0f2dab7b34e29cb92a2498911f03eb.png)

## 下一步可以干什么？

这个是一个最简单的例子，它是一个单任务的作业，也没有使用到远程存储映射能力，仅仅是向用户展示最基本的能力，您可以根据控制台使用指南继续测试 Batch 更高阶的能力。
- **丰富的云服务器配置**：Batch 提供了丰富的云服务器 CVM 配置项，您可以根据业务场景自定义 CVM 配置。
- **执行远程代码包**：Batch 提供 **自定义镜像 + 远程代码包 + 命令行** 的方式，在技术上全方位的覆盖您的业务需要。
- **远程存储映射**：Batch 在存储访问上进行优化，将对远程存储服务的访问简化为对本地文件系统操作。
