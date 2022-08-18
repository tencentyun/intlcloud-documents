## 操作场景
批量发送适用于大规模发送场景，支持多个变量并且每个变量支持对不同收件人替换为不同的变量值，在邮件的"收件人"一栏中只显示收件人自己。通过邮件推送控制台，您可以配置邮件批量发送的操作，本文将为您介绍如何进行邮件批量发送。

## 操作步骤
1. 登录 [邮件推送控制台](https://console.cloud.tencent.com/ses/send)，进入**邮件发送** > **批量发送**页面，您可以看到发送任务列表。发送任务列表展示每个发送任务的详细信息，包括发送进度、任务类型、任务状态以及请求数量。
![](https://qcloudimg.tencent-cloud.cn/raw/03e8a8f74f5d0ab785bb016427712502.png)
2. 单击**新建发送任务**，在任务类型中选择**批量发送**，并填写完整发送任务中的必填项，即可实现批量发送邮件。
![](https://qcloudimg.tencent-cloud.cn/raw/bd85315b7f512173a687f6c0ea4f706c.png)
>?发送任务界面中所选择的收件人列表中的变量，需要与所选择的模板中的变量数量与命名一致。

### 定时发送
1. 在 [邮件推送控制台](https://console.cloud.tencent.com/ses/send) 中进入**邮件发送** > **批量发送**页面，**新建发送任务**，选择**定时发送**。
![](https://qcloudimg.tencent-cloud.cn/raw/7e4f2dcdca1e2f11ba55e7d03861489e.png)
2. 所有的邮件都可以按照您的计划定时发送，选择**任务开始时间**，即可在特定某个时间自动有序发出邮件。
![](https://qcloudimg.tencent-cloud.cn/raw/55482b11771bbe336023ca840d346234.png)

### 频率发送
1. 在 [邮件推送控制台](https://console.cloud.tencent.com/ses/send) 中进入**邮件发送 **> **批量发送**页面，**新建发送任务**，选择**频率发送**。
![](https://qcloudimg.tencent-cloud.cn/raw/972566ee846e6629d9518f67686cec99.png)
2. 在控制台设置邮件频率发送，选择**任务开始时间**和**任务周期**等。控制台将自动完成邮件的频率发送。
![](https://qcloudimg.tencent-cloud.cn/raw/e5ca62b26bbbfc467855d04d4e9c088e.png)

>?
>
>- 控制台批量发送功能适用于营销类、通知类邮件的批量发送，触发类邮件（身份验证、交易相关等）建议通过 API- SendEmail 接口发送。
>- 批量发送内置自动 Warm Up 功能，关于 Warm Up 功能详情参见 [入门相关问题 > 什么是 Warm Up](https://intl.cloud.tencent.com/document/product/1084/42368)。
>- 同一域名可执行多个发送任务，当总发信量超过当日最大发信量时，超额未发邮件进行队列缓存次日发送，以此类推。
>- 任务进入队列缓存时，状态为暂停，发送进度条保持静止状态。次日重启发送任务后，状态为发送中，发送进度条会更新。
